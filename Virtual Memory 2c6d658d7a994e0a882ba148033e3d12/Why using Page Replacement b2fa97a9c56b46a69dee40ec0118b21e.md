# Why using Page Replacement?

Page replacement 發生點 → [No free frame](https://www.notion.so/What-is-Demand-Paging-fe6888df0eca401f81717f9b2194a1cd#afead2a34f3b4bb58a2a1bd47c975d4e)

### 當 page fault 發生，且沒有 free frame時，

也許可以直接 swap 整個 process 到

 disk，把所有的 frame 都空出來，(這叫做 midterm scheduler)，但這樣該程式就完全不能動了。為了更有彈性，我們使用 page replacement。

## Dirty Bit

> to reduce overhead of page transfers  — only modified pages are written to disk

所有的 memory content 一開始都在 disk，要使用時只是load 到 memory。當要把他 swap 回去 disk 時，也可以想成只是重新回去 call disk 上面原有的那份 copy。

但假如在 memory 上時有被修改，就跟原來 disk 上的 copy 不相同了。因此，引用 `dirty bit` 紀錄這份 content 在 memory 時有無被修改過，如果有，就要重新更新 disk 上的 copy;如果沒有，就直接呼叫 copy 就好了。

/painting

## Demand Paging需要解決的問題

1.  `frame-allocation algorithm` : 每個 process 要給他幾個 frames? 
2. `page-replacement algorithm` : 在給定的 frame 裡面，哪些 frame 要被 replaced?

Continue to [Page Replacement Algorithms](https://www.notion.so/Algorithms-9b9f035dd47742c38fce4ead39d48462)

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)