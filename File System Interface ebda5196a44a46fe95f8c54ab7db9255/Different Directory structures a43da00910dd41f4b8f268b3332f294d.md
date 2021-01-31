# Different Directory structures

## Directory v.s File

一開始建立 directory 的目的只是要能夠對應到每個 file 的 unique ID

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.15.32.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.15.32.png)

## Directory Operations

- Search for a file
- Create a file
- Delete a file
- List a directory: 常常是系統的 bottle neck，因為資料夾很多很多，要全部練出來很耗時。不要隨便執行 `ls` 啊哈哈。
- Rename a file
- Traverse the file system

## Single-Level Directory

沒有 folder，一個 dir 對應 一個 file。

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.09.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.09.png)

### 缺點

1. filename 一定要 unique
2. 檔案越來越多就會變得耗時。

## Two-Level Directory

兩層

就有 path 的概念 

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.14.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.14.png)

## Tree-structured Directory

目前使用的

會有絕對路徑 vs 相對路徑

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.21.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.21.png)

## Acyclic-Graph Directory

不同檔案名字，對應到相同的檔案內容

可以加 edge，但是不能出現 cycle。

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.27.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_10.17.27.png)

```bash
//linux 中加 edge 的方法：
ln -s /spell/count /dict/count
```

如此一來，一個 file 就可能有多個不一樣的絕對路徑。

### 優點

不需要同一份檔案 copy 多份

### 要處理的問題

萬一有一方把 file 刪除了呢？

→ 是只要刪除 link

→ 還是要真的把 file content 刪掉？

**SOLVE:** 加一個 `reference counter` ，有一個 edge 指向這個 file， counter == 1，兩個 edge 的話 counter == 2，假如 counter == 0， file content 才會被刪掉。

## General-Graph Directory

任何情況都被允許發生，所以有可能產生 cycle。

### 要處理的問題

Q: 有 cycle 時怎麼辦？

![Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_11.23.28.png](Different%20Directory%20structures%20a43da00910dd41f4b8f268b3332f294d/_2020-06-05_11.23.28.png)

`Garbage collection` : 從 root 開始 label 下來，看看是不是 reachable，假如不行，就代表他是 cycle，要被 delete 掉。

例如圖中， g2 跟 t1 是沒辦法被 reach 的，就要被 delete 掉。

但是當檔案數量超大時，performance 會變很差。

**SOLVE**: 每當要產生一個 link 時，先做 cycle-detection。

[BACK](https://www.notion.so/File-System-Interface-ebda5196a44a46fe95f8c54ab7db9255)