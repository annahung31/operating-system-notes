# Contiguous allocation

找一塊足夠大的連續位置存放

![Contiguous%20allocation%2060ce5cb4e4dc49038311a801af4bfbaa/_2020-06-08_11.14.45.png](Contiguous%20allocation%2060ce5cb4e4dc49038311a801af4bfbaa/_2020-06-08_11.14.45.png)

### 如何搜尋

Ex: 要搜尋 tr 的第 1000 個 byte，而一個 block size = 200

$1000/200 = 5$ → 在第 5 個 block，

而 tr 的起始點是 14 → $14 + 5 = 19$，可知在 No. 19 block。

### 優點

可以有效率的實作。 搜尋的 effort 最小。

### 缺點

1. External fragmentation ：會有用不到的碎空間，例如上圖的編號 17, 18 格。 **SOLVE**: compaction
2. File 不能變大，不然就擠不進去了，必須全部搬到別的位置。例如上圖的 `mail` 檔案，假如 length 變大成 12 ，就沒位置放了。 **SOLVE**: [extent-based FS](https://www.notion.so/Contiguous-allocation-60ce5cb4e4dc49038311a801af4bfbaa#2383a33d58474dc29486bf03d90c5b86)

## Extent-Based FS

修改版本的 Contiguous allocation

跟 linked-list 結合

一次 allocate 多個連續 block，被用完了不夠，再給一組連續 block，但不一定要接在第一次的連續block 後面，只要用幾個 byte 紀錄下一個 extend 在哪就好。

### 缺點

random access 變得比較昂貴。假設要讀 7th block，我知道在第三個 extend 中，但是不知道第三extend在哪，就必須要 traverse 整個 linked list 才能知道。

有可能造成 internal 跟 external fragmentation

internal : 每次 extend 都是固定長度時。

[BACK](https://www.notion.so/File-System-Implementation-9e72b1690202453d85690c8408adb422)