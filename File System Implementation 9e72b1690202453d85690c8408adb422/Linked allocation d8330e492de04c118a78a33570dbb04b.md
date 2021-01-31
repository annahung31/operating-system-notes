# Linked allocation

每個block 都像 linked list 一樣串起來

![Linked%20allocation%20d8330e492de04c118a78a33570dbb04b/_2020-06-10_10.09.28.png](Linked%20allocation%20d8330e492de04c118a78a33570dbb04b/_2020-06-10_10.09.28.png)

### 優點

很容易 reuse 或者擴大縮小，資源使用很有效率。

sequential read：沒有額外的 effort，所以不錯。

### 缺點

- random read：一定要 traverse 才能找到位置，需要花很久
- 會浪費掉一些空間來存 pointer。

    SOLVE: 把一些 block group 在一起

- reliablity：只要有其中一個 block 壞掉，link 斷掉，那後面的都找不到了。

# 實際的 FS： FAT(File Allocation Table)

解決 random access 的問題。

把 pointer 全部搜集起來，另外存成一個 table。再被 cached in memory

### FAT32

32 bits per table entry

![Linked%20allocation%20d8330e492de04c118a78a33570dbb04b/_2020-06-10_10.09.54.png](Linked%20allocation%20d8330e492de04c118a78a33570dbb04b/_2020-06-10_10.09.54.png)

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)