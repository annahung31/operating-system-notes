# Virtual Memory 如何幫助 process?

1. Demand Paging: 每次只要讀一個 page，比較快。
2. [Copy-on-write](https://www.notion.so/Copy-on-Write-717b49f907aa460ab0c6e68e66054c74): 當 process 在 fork 時，如何讓 fork 變快。 
3. [Memory-Mapped File](https://www.notion.so/Memory-Mapped-File-1908c2d6c9b84e03ada2ae1a9c68a8da): I/O 讀取file時。一般來說透過 file system 來讀取file，但是畢竟是一個 system，需要很多步驟才能去碰觸到file，花比較多時間。用這樣的方式操作file，可以跳過 file system。