# Partition, Volume & Directory

`Volume` : C槽, D槽

`partition`: 磁碟上切割出來的區塊

Volume是切割區塊格式化，有檔案系統之後的 partition。

partition → formatting(建立檔案系統) → volume 

partition 可以跨硬碟 → distributed file system

並不是所有儲存裝置都可以被切割成 partition。

有些 database 會直接用 raw partition，而不用file system。

`directory`: 讓使用者簡單的找到 file 的 logical position

[BACK](https://www.notion.so/File-System-Interface-ebda5196a44a46fe95f8c54ab7db9255)