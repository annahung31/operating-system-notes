# Demand Paging Performance

## EAT(Effective Access Time)

(1-p) x ma + p x pft

`p`: 百分之多少的 access 會產生 page fault

`ma`: memory access time(不只找到的時間，還要包含搬回來的時間)。 計算方法:  [TLB](https://www.notion.so/Paging-Non-contiguous-memory-allocation-2163e04aca324ad08713081020308a16#691855a9b3714cf19e9c724f4c84c991)

`pft`: 從 disk 把 memory content 搬回到 memory。所以算是 disk read time。在所有系統裡都一定遠大於 ma。

### Example

ma = 200ns,  pft = 8 ms

EAT = (1-p) * 200 ns + p * 8 ms

= 200 ns + 7999800 ns * p

你可以看到後面那項很大，前面項幾乎可以忽略。

所以可以說 EAT 幾乎正比於 page fault rate。

假如 1000 個 access 裡面會有一個造成 page fault，則 p = 0.001, EAT = 8.2 microsec → 會慢 40 倍  。

註： 8.2 microsec = 8.2 *1000 ns

和原來的 ma 相比：8200/ 200 = 41 ，時間長了 41倍。

反過來說，假如希望效能只有很少的影響，那你的 page fault 要極低。

### 但為什麼我們的電腦有 virtual memory，卻沒有感覺變慢很多？

因為 `locality` 。

第一次讀的時候會發生 page fault，但是讀進來之後，在一次又一次 reuse 的時候都不會有 page fault。所以其實 hit rate 是非常高的，在正常運作下， virtual memory不會造成慢很多。

### 再回來看 pft = 8ms 時間花在哪？

1. 存 page fault interrupt
2. 從 disk 把 page 讀進 memory **（花最多時間）**
3. restart process

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)