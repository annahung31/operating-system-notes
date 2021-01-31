# Swap space

當作一個 file 來管理

雖然比較慢，但是大小調整比較有彈性

獨立一塊 raw partition 來使用

優點

- 比較快
- 比較好 implement，因為 size 固定

缺點

- 因為是獨立保留，假如一開始切太小，之後要調整比較困難。

實務上是兩者皆用：

一開始還是請你先切出一塊空間用，假如之後不夠了，再跟 FS 借空間用

## Allocation

什麼時候要放進 swap space?

要存進去的東西越少越好，因為當 swap space 滿了， system 可能會 crash

### 1st version

只要 memory 上有任何內容，就 copy 一份到 swap space 上。

會有空間浪費

### 2nd version

只有在 load 到memory 的內容需要被 swap 時，再 load 到 swap space。

比較節省空間

### 更進一步節省空間的方法

作法一

- code 本來就是 binary file，存在 FS 裡面，所以被 swap 時就直接丟掉，等到要從新用到時，再去 FS 抓回來。
- 動態產生的 memory ，在產生時放到 swap space

做法二

- 動態的 memory，而且被 page out 時，才放到 swap space 上。

[BACK](https://www.notion.so/Mass-Storage-System-b400d207bbdc4b83b0a71464b138854b)