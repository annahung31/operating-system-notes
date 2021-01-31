# 性質：Stack Algorithm

是一個 algorithm 的性質。設計 page replacement 的 algorithm 時，會希望設計出有這樣性質的 algorithm。

## 定義

如果原來有 n 個 frame, 在這 n 個 frames 裡面，設有一個 subset  `A` 是有存放 page 的。 假如在相同 input, 相同 algorithm 的情況下,  增加 frame 的數量，一定還是會 include `A` 這個 subset。

Stack: 就是會一直加。你要把某個東西從 stack 拿出來，你一定要先把前面的人拿出來。（前面的人就是 `A` subset)

## Stack Algorithm 這個性質為何重要？

因為他確保一件事，就是當 resource 增加 (frame 數量增加)時，一定還是會 include 原來的 pages，甚至更多，因此 page fault rate 只會變低不會變高。(gooood!) → 不會有 `[Belady's anomaly](https://www.notion.so/FIFO-algorithm-e09a0ee68722473c92508adefedba2e5#1e3449f77e824c0c896a7a790d9cd8c9)` 

Q: 要怎麼判斷？ (????)

## 例子

[LRU algorithm](LRU%20algorithm%20bac5b2bd0069491893aa65c3d0639211.md) , [Optimal(Belady) Algorithm](Optimal(Belady)%20Algorithm%20201cbd6fbb694b1086a6d477962ac88e.md)