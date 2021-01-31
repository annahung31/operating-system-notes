# Indexed allocation

像查字典一樣，把全部的 index 存在某個 block 裡面。

![Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_10.11.24.png](Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_10.11.24.png)

### 優點

1. random access 變得很有效率
2. 沒有 external fragmentation
3. 很容易 create, extend file

### 缺點

1. 會浪費掉一些 block 來紀錄 index。浪費的情形會更嚴重，因為整個 block 都被用來儲存 index，即使要存的 index 很少。
2. 當 file 很大， pointer 數量很多，超過單一 block 可存容量：需要多個 index block。如何做 extend:
    1. `Linked Indexed Scheme`: 在第一個 index block 加一個 pointer，指向第二個 index block

        **缺點**： random access 很不平均。後端會很慢

        ![Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.20.47.png](Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.20.47.png)

    2.  `Multilevel Scheme` : 第一個 index block 內容是存 pointer，指向另外的 data block。

        優點：比較平均，檔案大時適用

        缺點：浪費更多空間

        ![Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.20.53.png](Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.20.53.png)

    3. `Combined Scheme` : default inode。檔案很大 → 多 level。檔案很小 → 單一 level。

        ![Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.21.01.png](Indexed%20allocation%20ccac9e63557a4b8e87c4f911ae180d0b/_2020-06-10_11.21.01.png)

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)