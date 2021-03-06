# Download App 
an uitlity app to download ayahs of quran as **mp3**.

# Screenshots 
<div> 
 <img src="https://user-images.githubusercontent.com/13488900/75140273-37205c80-56f7-11ea-942d-de99b6f8704a.png" width = 20%> <img src="https://user-images.githubusercontent.com/13488900/75140276-37205c80-56f7-11ea-9194-a38459573271.png" width = 20%> <img src="https://user-images.githubusercontent.com/13488900/75140262-32f43f00-56f7-11ea-9769-928b7332e95c.png" width = 20%>
 <img src="https://user-images.githubusercontent.com/13488900/75140269-35569900-56f7-11ea-8e54-9d1d1d28965a.png" width = 20%>
 <img src="https://user-images.githubusercontent.com/13488900/75140272-35ef2f80-56f7-11ea-9e3d-5a57d707c015.png" width = 20%>
 <img src = "https://user-images.githubusercontent.com/13488900/75148649-d6018480-5708-11ea-8f14-df0cf40fe74b.png" width= 20%>
  </div>


# General Structure 
![uml (1)](https://user-images.githubusercontent.com/13488900/75139409-38508a00-56f5-11ea-9c76-7f66a42cb973.png)


# Download Service 
It maintains a queue with indexes of ayahs to be downloaded.
There are states of file (`IDEL`,`DOWNLOADING`,`PAUSED`,`DONE`,`IN-QUEUE` )
- `IDEL` : means file not downloaded before (i.e initial state ).
- `DOWNLOADING` : file is currently downloading 
- `PAUSED` : file is paused 
- `DONE` : completly downloaded 
- `IN-QUEUE`: file in queue of downloading

**Note**: These states used to track file and used with updating ui and for listing files as category (`DOWNLOADING`,`PAUSED`,`DONE`).

## Process 
- when it start it accepts index of ayah to be downloaed 
  ``` koltin 
   super.onStartCommand(intent, flags, startId)
          // get index of ayah sent in intent
          val index = intent.getIntExtra(INDEX, -1)
          startDownloading(index)
  ```
- add this index to its queue
``` koltin 
            val newItem = repo.getAyahItemByNumber(index)
            // add to list
            list.add(newItem)
```
- if no currently downloading item it starts else do nothing (as it added to list).
```  koltin 
            if (!isDownloading && list.size > 0) {
                download()
            }
```
- when it starts it allocate a path to file, make a name, call **PR Downloader library** to downlaod.
  ```
  PRDownloader.download(link, path, name)
                  .build()
                  .setOnCancelListener(this)
                  .setOnPauseListener(this)
                  .setOnProgressListener(this)
                  .setOnStartOrResumeListener(this)
                  .start(this)
  ```
- change ayah item state from `IDEL` to `DOWNLOADING`
```
        item.downloadSate = Constants.DOWNLODING
        // add downID
        item.downID = downID
        // update in db
        repo.updateAyahItem(item)
```

- listen to updates of *downloading progress* and update progress in database for this item.
  ``` koltin 
          // handle size details
          item.size = progress.totalBytes.div(1024) // as KB
          item.downloadedBytes = progress.currentBytes // to resume
          item.perecentage = progress.getPerecentage()

          updateNotification(getTitle(), msg, progress.getPerecentage()) 

          // update in db
          repo.updateAyahItem(item)
  ```
- when file **paused** it update it in database to `PAUSED`
  ``` koltin 
          item.downloadSate = Constants.PAUSED
          repo.updateAyahItem(item)
  ```
- when file **canceled** it remove it from queue also update in database to `IDEL`.
  ``` koltin 
          item.downloadSate = Constants.IDLE
          repo.updateAyahItem(item)
          // make state to not downloading to enable continue downloading other files
          isDownloading = false
          // remove from list 
          val rem = list.removeAt(currentDownloadIndex)

  ```
- when file **completes** it update its state to `DONE` and look for queue if has elements start downloading them. 
  ``` koltin 
         // update state
          item.downloadSate = Constants.DONE
          // update percentage
          item.perecentage = 100
          // update in db
          repo.updateAyahItem(item)
  ```


# Model in Database 
This model used to store ayah text,index, sura, also downloading states and info 
``` kotlin 
@Entity(tableName = "ayahs")
data class AyahDownloadItem(
    @PrimaryKey
    val number: Int,
    val numberInSurah: Int,
    val surahIndex: Int,
    val text: String,
    var path: String = "",
    var downID: Int = -1,
    var downloadSate: String = Constants.IDLE,
    var downloadedBytes: Long = 0,
    var perecentage: Int = 0,
    var size: Long = 0
)
```
**downID**: used to control downloading of file (i.e used with library to `pause`,`resume`,`cancel`).


# UI 

## 1.DownloadHolder 
- Placeholder fragement that will be used with ViewPager to represent 3 Fragments (ALL,DOWNLOADING,DONE)
- It accepts **state** as paramter which is used to distinct each fragment and will be used with db to get items from database
- It use this **state** to make query to database to get list of downloades based on state 
- There are 3 fragments
  - `ALL fragment` will hold downloading and downloaded items this query do this Job 
    ``` kotlin 
     @Query("select * from ayahs where downloadSate != :state")
        fun getAyahsInNonIdleSate(state: String): androidx.paging.DataSource.Factory<Int, AyahDownloadItem>

    ```
    here it accepts `IDLE` as state so query will return all items that not in `IDLE` state (i.e  `DOWNLOADING`,`PAUSED`,`DONE`).

  - `DOWNLOADING fragment` will hold downloading items (i.e  `DOWNLOADING`,`PAUSED`)
  - `DONE fragment` will hold downloaded items(i.e `DONE`)

## Actions 
- At `DOWNLOADING fragment` it will shows actions to be perofrmed of file such as `pause`,`resume`,`cancel` 
- Actions is down by **PR Downloader library** just pass download it for file and use proper method for example to pause an item `PRDownloader.pause(downID)`

**NOTE** for **cancel action** there are **two cases**: 
  - if file in downloading state so it currently downloading item so cancel it directly through **PR Downloader library**`PRDownloader.cancel(downID)`
  - else just change its state to `IDEL` to be not downloaded by **Service**.

# 2.ListSurahFragment 
- This fragment list Surah's names and count of ayahs of each one.
- when user click on Sura it opens **ListAyahs** fragment and pass index of Sura.

# 3.ListAyahs 
- Accept `sura index` and **load** all ayahs from database. 
- make query to get ayahs 
``` kotlin 
 @Query("select * from ayahs where surahIndex = :index order by number")
    fun getAyahsOfSuraIndex(index: Int): androidx.paging.DataSource.Factory<Int, AyahDownloadItem>
```
- `btnAddALL` is button used to add all sura ayahs to queue of downloading, this down by 
  - first it filter items that can be downloaded(i.e in`IDLE` state)
  - then change state to `IN-QUEUE` 
  ``` koltin 
     list.filterNotNull()
              .filter { it.downloadSate.equals(Constants.IDLE) }
              .forEach {
                  it.downloadSate = Constants.IN_QUEUE
              }
          model.updateitems(list)
  ```

## Technologies
Technology | Version
---------- | -------
Kotlin | 1.3.61
lifecycle-viewmodel | 2.0.0
retrofit2 | 2.5.0
paging| 2.0.0
Room| 2.0.0
koin| 2.0.1
rxjava2| 2.0.1
gson | 2.8.5
prdownloader | 0.4.0
easypermissions|1.1.1


