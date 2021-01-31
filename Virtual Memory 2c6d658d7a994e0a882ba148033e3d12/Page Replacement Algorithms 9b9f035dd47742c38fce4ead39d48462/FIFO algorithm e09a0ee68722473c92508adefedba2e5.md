# FIFO algorithm

First-In-First-Out

設要使用的 page ID 序列(reference string): 

1,2,3,4,1,2,5,1,2,3,4,5

空的 frame 數： 3

設一個空的 queue 當作 allocate page 的位置，當位置不夠的時候，先進來的會先被擠出去。

（圖中數字的位置不代表 page 在 實體記憶體中的位置，只代表該 page 在 algorithm 中相對順序）

紅色數字代表出現 page-fault，黑色數字則無。

![FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/Webp.net-gifmaker_(1).gif](FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/Webp.net-gifmaker_(1).gif)

→ 共有 9 個 page-fault 。

### FIFO illustrating `Belady's Anomaly`

![FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/_2020-05-28_11.12.39.png](FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/_2020-05-28_11.12.39.png)

當增加 frame 的數量時，page-fault 有可能不減反增。

例如，增加為 4 個 frame， page fault 變成 10個！

![FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/_2020-05-28_11.12.32.png](FIFO%20algorithm%20e09a0ee68722473c92508adefedba2e5/_2020-05-28_11.12.32.png)

對於設計電腦系統的人是很討厭的，不好 tune 參數。

因為花更多錢，建更多 memory，有可能跑越慢。

## FIFO 問題

根據 Belady's Anomaly， page-fault 不一定會減少。

改進： → 最好的: [Optimal Algorithm](https://www.notion.so/Optimal-algorithm-201cbd6fbb694b1086a6d477962ac88e)

[Other Algorithms](https://www.notion.so/Algorithms-9b9f035dd47742c38fce4ead39d48462)