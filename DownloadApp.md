# Download App 
an uitlity app to download ayahs of quran as **mp3**.

# Screenshots 
<div> 
 <img src="https://user-images.githubusercontent.com/13488900/75140273-37205c80-56f7-11ea-942d-de99b6f8704a.png" width = 20%> <img src="https://user-images.githubusercontent.com/13488900/75140276-37205c80-56f7-11ea-9194-a38459573271.png" width = 20%> <img src="https://user-images.githubusercontent.com/13488900/75140262-32f43f00-56f7-11ea-9769-928b7332e95c.png" width = 20%>
 <img src="https://user-images.githubusercontent.com/13488900/75140269-35569900-56f7-11ea-8e54-9d1d1d28965a.png" width = 20%>
 <img src="https://user-images.githubusercontent.com/13488900/75140272-35ef2f80-56f7-11ea-9e3d-5a57d707c015.png" width = 20%>
 
  </div>


# General Structure 
![uml (1)](https://user-images.githubusercontent.com/13488900/75139409-38508a00-56f5-11ea-9c76-7f66a42cb973.png)


# Download Service 
It maintains a queue with indexes of ayahs to be downloaded.
There are states of file (`IDEL`,`DOWNLOADING`,`PAUSED`,`DONE`)
- `IDEL` : means file not downloaded before (i.e initial state ).
- `DOWNLOADING` : file is currently downloading 
- `PAUSED` : file is paused 
- `DONE` : completly downloaded 

**Note**: These states used to track file and used with updating ui and for listing files as category (`DOWNLOADING`,`PAUSED`,`DONE`).

## Process 
- when it start it accepts index of ayah to be downloaed 
- add this index to its queue
- if no currently downloading item it starts else do nothing (as it added to list).
- when it starts it allocate a path to file, make a name, call **PR Downloader library** to downlaod.
- add change ayah item state from `IDEL` to `DOWNLOADING`
- listen to updates of *downloading progress* and update progress in database for this item.
- when file **paused** it update it in database to `PAUSED`
- when file **canceled** it remove it from queue also update in database to `IDEL`.
- when file **completes** it update its state to `DONE` and look for queue if has elements start downloading them. 

