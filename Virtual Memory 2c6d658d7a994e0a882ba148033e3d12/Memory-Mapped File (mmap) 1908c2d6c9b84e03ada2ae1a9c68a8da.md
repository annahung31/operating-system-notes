# Memory-Mapped File (mmap)

把 file map 到 memory

希望讓使用者透過memory access 來做 read/ write file

file 裡面是 byte stream    把 file map 到 byte  stream 裡面，那你要讀哪一個 bit 就自己去 operate 這些 byte 。用 array, pointer 的概念去使用 file       (????) 

和 virtual memory 一樣的概念,

 one-to-one 的 mapping

### 優點

1. 更快的 file access。因為不用再經過 file system
2. 更容易做到 sharing。假如是 file system, 當第一個人write, 第二個人就不能再write。memory-mapped 沒有這個問題。 (????)

### 缺點

1. 很容易弄壞，不容易管控
2. data lost: 把 data load 到 memory 裡面，假如斷電，資料就遺失了。假如是  file system, 會有還原點。
3. programming更辛苦，要做更多事情。

系統層的軟體 programmer才比較會使用 memory-mapped 。

### File system 做的事

buffering:  open 一個 file, file system 會先把 content copy 到 file system 的 memory裡面。

write: 會先寫到 buffer 裡面，等到 file close 的時候，才會做 `flush`   

（效率的考量）

### Memory Mapped File 做的事

open 

→ 跟OS 說要 map file的哪個區段，到 memory 的哪個位置 （map 什麼？到哪裡？）

→ return 一個 pointer，將 file 跟 memory 一對一的對應

→ 用 pointer 來做 memory access，做操作

→ munmap 整個再寫一遍回去 file 裡面。

![Memory-Mapped%20File%20(mmap)%201908c2d6c9b84e03ada2ae1a9c68a8da/_2020-05-27_10.35.09.png](Memory-Mapped%20File%20(mmap)%201908c2d6c9b84e03ada2ae1a9c68a8da/_2020-05-27_10.35.09.png)