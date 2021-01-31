# Layered File System

檔案系統最重要的角色是 `mapping` ，把 user 要求的 file ， map 到實際硬體 disk 位置上。

`fh` = file handler

`buf` = buffer

FS 接收到 fh, buf, size 這些參數，執行 read，mapping 到 實體記憶體位置。

途中，會經過不同 layer 的 mapping。

1. **logical FS**

    最接近使用者，呈現給 user 的。 EX:  [ACL](https://www.notion.so/Sharing-e1442570b57146b1bd6d3d8e58c45903#939cb2c7a1da4b02b7aa96b18e87c269) （不用重寫，因為都差不多）

2.  **file-organization module**

    logical ↔ physical mapping。切成幾個 block? 放在第幾個 block？

    （不同 FS 最大差異 ）

3. **basic file system** 

    block ↔ physical position mapping。 是哪一個 disk?  哪一個 track? (不用重寫，因為使用的硬體都差不多）

![Layered%20File%20System%20a191c9ea27694332a958b2c585aa11c3/_2020-06-07_1.34.48.png](Layered%20File%20System%20a191c9ea27694332a958b2c585aa11c3/_2020-06-07_1.34.48.png)

左邊是實例，右邊是概念

![Layered%20File%20System%20a191c9ea27694332a958b2c585aa11c3/_2020-06-07_1.35.28.png](Layered%20File%20System%20a191c9ea27694332a958b2c585aa11c3/_2020-06-07_1.35.28.png)

以 OS 的角度，應該要能夠 support 不同的 FS，甚至不同的 disk type。

但對 user 而言，只想要面對一個 FS manager。

ex: 對客戶而言，他只需要有一個對口，可能是業務。而業務對公司內部就可以面對不同的部門，執行不同的事。

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)