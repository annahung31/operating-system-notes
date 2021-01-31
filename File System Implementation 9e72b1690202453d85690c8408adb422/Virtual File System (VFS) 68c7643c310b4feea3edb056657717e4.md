# Virtual File System (VFS)

## 優點

1. 提供一個 object-oriented 的方式來實作 FS。
2. 提供使用者在相同的 API，使用不同的 FS

## Linux VFS 提供的四種 object types

1. inode： (發音： I know) 對應到on-disk structure 的 FCB
2. file object：load 到 memory 開始操作時的 object，對應到 in-memory structure
3. superblock object：整個 FS。→ partition block
4. dentry object：dir 。 （dir entry）

這些 objects 的實作，最重要的兩個部分：

1. 如何 maintain directory structure，可以很快知道某個 path 是否存在 → [Directory Implementation](Directory%20Implementation%20be31ef9828234c4ba99df85c47c24af2.md) 
2. data block 怎麼擺

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)