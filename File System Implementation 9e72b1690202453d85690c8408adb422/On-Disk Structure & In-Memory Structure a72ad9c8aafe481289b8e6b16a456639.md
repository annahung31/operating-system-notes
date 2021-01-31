# On-Disk Structure & In-Memory Structure

# On-Disk Structure

這些 structure 會永久存在 disk 上面。

分成以下的blocks:

- Boot control block：開機用的。每個 partition 都會保留一部分給開機用的程式。

    (不一定會有，不是每個 partition 都是用來開機）

- Partition control block：用來管理、分配 partition。OS 透過這個 block，可以知道要如何 access partition 裡的 content。

    Ex: num of blocks, block size, free-block list, free FCB pointers

- Directory and File control block (FCB)：partition 經過 formatting 之後，變成一個 volume 之後，可以開始存放 file，就需要這個 block 來管理 file 跟 dir 的 metadata。

    Ex: permission, size, location of data blocks 

切完 partition 之後，就會生成 Partition control block。 formatting 之後，才會生成 Directory and File control block。

![On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-07_1.36.55.png](On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-07_1.36.55.png)

Data Blocks 是真正存資料的空間。

# In-Memory Structure

- in-memory partition table ：紀錄所 mount 的 partition 資訊。把 partition table load 到 memory 裡面。
- in-memory directory structure：把最近曾經 accessed 的 dir 資訊 load 進來。只會紀錄dir entry。
- system-wide open-file table：找到 file 要打開它或編輯時， 把 file 的 FCB load 進來放這裡。
- per-process open-file table：紀錄每個 process 的權限等資訊。 ex: pointer (file handle/ descriptor)

# 比較

## File Open

secondary storage 就是 On-Disk Structure。

1. open file
2. 在 directory structure 中搜尋 file。

    如果找不到，會去 on-disk 那邊 load 進來，再繼續查找。

3. 找到之後，directory 指到的其實是 secondary storage 上面的 FCB，並且 load 到 memory 的 open-file table 裡面。

 

![On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-08_11.09.10.png](On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-08_11.09.10.png)

## File Read

( open 之後）

1. 會有兩層：
    1. per-process open-file table 紀錄 process 的權限，假如 user 無權編輯，就會把 user access 擋掉。並且確保現在 file 的確 open 了。
    2. system-wide open-file table： 找 file 真正的位置。可以去 access FCB 的位置。

![On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-08_11.09.15.png](On-Disk%20Structure%20&%20In-Memory%20Structure%20a72ad9c8aafe481289b8e6b16a456639/_2020-06-08_11.09.15.png)

## File Create

1. OS allocate a new FCB (一開始內容是空的，但還是要先宣吿這個 file 的存在）
2. Update directory structure: 說明這個 file 在整個 dir 中的位置。確保 path 真的存在。把 file name 加進去。再寫回 disk。

跳電 data 不見：一開始修改只是寫進 in-memory 裡面，沒有存進 disk。所以關機之後 data 就消失了。

寫 log 來確保 data 遺失後可以重新復原。 

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)