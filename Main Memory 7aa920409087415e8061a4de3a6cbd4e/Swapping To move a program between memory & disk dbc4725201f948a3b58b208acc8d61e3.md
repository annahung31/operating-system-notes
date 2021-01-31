# Swapping: To move a program between memory & disk

Swapping: disk 跟 memory 的 content 之間的移動

放在 disk 指定的一塊空間，跟 file system 是切開的。

在灌OS的時候，會問你 swap space 要多少，其實蠻重要的，不夠的時候很快就會 OOM。

### 為何要 Swap

1. 當 memory 空間不夠了，就會做 `midterm scheduling`, 挑一些process swap 到 disk上，讓出一些空間讓別人先做。
2. 把 priority 比較低的process swap 到 disk, 讓比較優先的process先做。

### swap v.s binding

compile-time / load-time binding: swap 回來的時候位置必須要相同，萬一那個位置有人，就要等他。

Execution-time binding: 位置可以不一樣，才能有效使用memory空間。

### 狀況

一個 process 要能被 swap掉 →  不能在做 I/O（must be idle），不然會有memory寫錯的情況發生。

**解決辦法**：

1. 設一個 flag 告知正在做 I/O，不能 swap。
2. OS 有一個 buffer，把資料先搬到 OS memory，再swap process， I/O 則寫到 OS buffer 裡面。等到 process 再 swap 回來了，再把 I/o結果寫回 process。（比較常用） 

### 怎麽讓swapping 快一點？搬動的資料少一點？不要搬錯人？

→ Vitural memory

會有一個 algo 找到最少搬移次數，決定要搬誰。