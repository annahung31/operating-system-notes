# Counting Algo 會有 Belady Anomaly 嗎？

課堂中老師只提到， [LRU algorithm](../LRU%20algorithm%20bac5b2bd0069491893aa65c3d0639211.md) 跟 [Optimal(Belady) Algorithm](../Optimal(Belady)%20Algorithm%20201cbd6fbb694b1086a6d477962ac88e.md)  不會有 Belady anomaly，但是沒有說明 counting Algo 會不會，網路上也查不到這個資訊，因此決定自己試試看。

遇到的疑問：

把最不常遇到的 page 刪掉，那他的次數要歸零嗎？

→ 暫用策略：歸零

當page freq 一樣大時，如何決定刪哪個 page?

→ 暫用策略： page string 小的