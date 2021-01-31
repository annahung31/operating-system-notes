# Maintain file 最主要的兩個 data structure

### In Process level

開了 file之後，跟這個 proess 有關的資訊，存在 `open-file table` 

### In OS level

可以 share 給其他 process 的資訊，存在 `system-wide table`

## Open-file table

Per-process: 只跟單個 process 有關

一個 file 可以被多個 process 打開，每個 process 針對這個 file 都有一個 position。一但做了動作，position 會往後移。

或者 permission 不同，也會記錄在這個 table 裡。

## System-wide table

會跨整個 OS。

Process-independent：跟 process 無關

ex: file disk location, file size

## 常見 attribute 會存在哪？

[Untitled](Maintain%20file%20%E6%9C%80%E4%B8%BB%E8%A6%81%E7%9A%84%E5%85%A9%E5%80%8B%20data%20structure%2004640507f2ec47a0b2efb9a5808067e9/Untitled%20Database%20111af58ef5c04aabb7b3e103e333ec8b.csv)

[BACK](https://www.notion.so/File-System-Interface-ebda5196a44a46fe95f8c54ab7db9255)