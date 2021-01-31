# General Idea

FS = File System

IO 在 memory 跟 disk 轉換過程中的最小單位： `block`

physical 硬體上的最小單位： `sectors`

1 sector = 512 bytes

1 block = 1 or more sectors

一個 OS 可以有多個 File System。

## FS中，兩個需要設計的問題

1. interface to `user programs` (可以一樣)
2. interface to `physical storages` (不會一樣)

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)