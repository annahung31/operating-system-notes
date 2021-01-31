# Optimal(Belady) Algorithm

最晚會再被使用的，先被踢出去

但是這是建立在知道未來所有的 access 序列的前提下，所以實作上是做不到的。

但可以當作是一個“上限”，表示最好的情況。

![Optimal(Belady)%20Algorithm%20201cbd6fbb694b1086a6d477962ac88e/_2020-06-03_9.13.04.png](Optimal(Belady)%20Algorithm%20201cbd6fbb694b1086a6d477962ac88e/_2020-06-03_9.13.04.png)

### 衍生的研究問題

可以如何觀察程式執行過程，預測出下一次被 reuse 的時間點，這樣就可以逼近 optimal。

實作上，最常用的：[LRU algorithm](LRU%20algorithm%20bac5b2bd0069491893aa65c3d0639211.md) 

[Other Algorithms](https://www.notion.so/Algorithms-9b9f035dd47742c38fce4ead39d48462)