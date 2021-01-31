# What is thrashing?

thrashing ：系統花在 paging 的時間大過於 execution。

![What%20is%20thrashing%20c38c0cd65d0d4be5805b8e259c15df48/_2020-06-03_11.50.12.png](What%20is%20thrashing%20c38c0cd65d0d4be5805b8e259c15df48/_2020-06-03_11.50.12.png)

當 degree of multiprogramming 一直增加（process 越來越多），每個 program 能分到的 frame 數越來越少（僧多粥少），便開始會有 page fault 產生。而當 page fault 非常頻繁在發生，此時會有非常多的 IO，系統必須要先去讀取 disk 上的東西， swap 到 memory 裡，cpu 等 IO，進到 idle 模式，而造成 cpu 使用率急速下降。

14D  12:34 

## 為什麼 CPU 使用率急速下降？

關鍵點在於，當 OS 發現 CPU 使用率下降，會覺得是自己的錯，為了提升使用率，於是 OS 提升 degree of programming，也就是讓更多的 process 進入 ready queue 裡面。每個 process 都有frame 的最低需求，於是 frame 就更加供不應求，page fault rate 越升越高，CPU 使用率更下降，造成惡性循環。

/作圖 

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)