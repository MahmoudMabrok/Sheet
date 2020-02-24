# Download App 
an uitlity app to download ayahs of quran as **mp3**.

# Download Service 
It maintains a queue with indexes of ayahs to be downloaded.
There are states of file (`IDEL`,`DOWNLOADING`,`PAUSED`,`DONE`)
- `IDEL` : means file not downloaded before (i.e initial state ).
- `DOWNLOADING` : file is currently downloading 
- `PAUSED` : file is paused 
- `DONE` : completly downloaded 
**Note**: These states used to track file and used with updating ui and for listing files as category (`DOWNLOADING`,`PAUSED`,`DONE`).

It start downloading first item at list, while it downloading it stores progress update of file in Room database. 
when it completes it update state of file to `DONE` 
