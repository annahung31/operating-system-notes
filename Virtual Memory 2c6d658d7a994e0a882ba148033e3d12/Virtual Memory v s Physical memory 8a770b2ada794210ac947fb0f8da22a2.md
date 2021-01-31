# Virtual Memory v.s Physical memory

![Virtual%20Memory%20v%20s%20Physical%20memory%208a770b2ada794210ac947fb0f8da22a2/_2020-05-25_11.07.44.png](Virtual%20Memory%20v%20s%20Physical%20memory%208a770b2ada794210ac947fb0f8da22a2/_2020-05-25_11.07.44.png)

memory map = page table

假如某些 page 一直沒被用到，可以先把他 swap 去 disk 暫存。等到virtual memory 發現要用到，就叫 physical memory 把 page swap 回來。

`KEY`：要把誰 swap?

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)