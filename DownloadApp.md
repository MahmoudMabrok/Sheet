# Download App 
an uitlity app to download ayahs of quran as **mp3**.

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

