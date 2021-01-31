# Paging: Non-contiguous memory allocation

單一個程式本身空間就不是連續。

L10D   [http://ocw.nthu.edu.tw/ocw/index.php?page=chapter&cid=141&chid=3009](http://ocw.nthu.edu.tw/ocw/index.php?page=chapter&cid=141&chid=3009) 

[http://ocw.nthu.edu.tw/ocw/upload/141/news/周志遠教授作業系統_chap０8＿Operating System Chap8 Memory Management＿.pdf](http://ocw.nthu.edu.tw/ocw/upload/141/news/%E5%91%A8%E5%BF%97%E9%81%A0%E6%95%99%E6%8E%88%E4%BD%9C%E6%A5%AD%E7%B3%BB%E7%B5%B1_chap%EF%BC%908%EF%BC%BFOperating%20System%20Chap8%20Memory%20Management%EF%BC%BF.pdf)

`frames`: physical hardware memory 的 block （真的）

`pages`: logical, programming, software 的 block（虛擬的）

但是兩者的size相同。 

OS 要做的事：

1. 要知道哪些 frame 是 free 的
2. 建 `page table`： frame 跟 page 的關聯性，紀錄轉換時需要的資訊。（由 OS mantain, user碰不到）

### 優點

1. 使用者看見的空間仍然是連續，但實際上因為是mapping到各個frame，可以是不連續的。實現了 Non-contiguous ，可以減少空間浪費、空洞的情況。

2. 因為 frame 是固定大小的，所以沒有 external fragmantation

3. 因為frame 可以切很小，可以降低 internal fragmantation

4. 可以在 page table動手腳，指到相同的 frame → Share memory

![Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_9.01.07.png](Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_9.01.07.png)

每一個 process 有自己的page table，只要 pointer 指到相同的 frame 就可以share。

程式之間不互相干擾， memory protection: page table中不要指到別人的 frame。

### Address Translation Scheme

每一次指到一個 byte 。

Logical address 可以分成兩部分：

1. page number(p): 在program裡的第幾個 page。

    假如 page number 有 `N` 個 bits，代表一個 process 最多可以使用 `2^N` 個 pages， 可以用 `2^N * page size` 的 memory。

2. page offset(d)：在這個 page 裡的哪個位置。若 page offset 有 N個 bits，代表 page size 是 `2^N` 。

而Physical address = page base address + page offset。

page base address = page size * 第幾個frame 

### 例子與練習

![Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.07.23.png](Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.07.23.png)

![Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.08.06.png](Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.08.06.png)

(Lecture 11A 18:00)

`Free frames`: 用一個簡單的 linked-list 儲存哪裡有空的 frame，當需要新的 frame 時，就從這個 list pop。

### page size 是決定電腦效能的關鍵點

原則：

1. power of 2
2. 從 512 bytes 到 16MB 都有
3. 常見 4kB 的 page size

假如把 size 調大 → internal fragmentation 會大，浪費空間

把 size 調小 →  現在的 memory 都很大， page number 大， 則 table 很大， OS 會浪費很多空間存這些 table。當程式大，會跳來跳去，就會發現跑一個程式需要 access 的 page 很多。但是每讀一個 page 都需要去找他，就會很浪費時間。

所以 4kb 是經驗法則，最好的 size。

`frame table`: 每個 frame 裡面存著哪個 process 的 page。（good to know, 平常沒用）

## Implementation of page table

是在 OS memory 裡面

但是做轉換的是 MMU, 是硬體，所以必須把memory 的 content load 到 register，才能讓 MMU 做轉換。 

→ 需要 `page-table base register(PTBR)`，存在 PCB（process control block）裡面，在 context-switch 的時候改這個值。

每次查找時都要花兩個memory read ：第一個 memory read 用來找 page table，第二個 memory read 才是讀真實資料。 → 讀資料的速度變慢一倍

解決辦法 → 之前讀過的先存起來，有讀過就直接查，沒讀過再去讀。→ `TLB`

## TLB(Translation Look-aside Buffers)

其實就是 MMU 的 cache。

是一個 `associative memory`，在 hardware 裡面。

一樣是個 table,裡面是 cache，查過記在裡面，

沒有 ordering。

假如要查某個 page，就要全部掃過一次。但是這個設計成可以同時查找，所以是O(1)

所以比較貴，size 沒辦法太大，大概 64~1024。

在 context switch 之後，因為page table已經換了，所以 TLB 要清空(flushed)，（常用方法）;也可以不清空，但是多加一個欄位 process id。

所以為什麼context switch會變很慢？ 因為 把 TLB清空之後，每一個 page 都要重新查找，都有兩個 memory read，花很多時間。

![Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.11.19.png](Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.11.19.png)

### 效能： memory-access time

![Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.11.37.png](Paging%20Non-contiguous%20memory%20allocation%202163e04aca324ad08713081020308a16/_2020-05-18_10.11.37.png)

有在 TLB裡→ 只要查一次+ 一次 memory read = 0.7 * (20 + 00)。

沒有在 TLB裡 → 走下面的舊路，要重找 → 兩次 memory read → (1-0.7)*(20+100+100)。

事實上 hit-ratio 很容易可以達到 98%以上的，因為讀資料的時候通常資料是有順序性的，都在附近，都在同一個 page 裡面。