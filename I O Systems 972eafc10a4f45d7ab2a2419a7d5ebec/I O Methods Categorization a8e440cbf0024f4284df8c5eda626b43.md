# I/O Methods Categorization

各種分類方法：

# 根據如何 address 一個 device

## Port-mapped I/O

上述的方法，用 IO instruction ，port address 來做 IO 溝通。

Ex: keyboard

## Memory-mapped I/O

寫到 memory 裡面。沒有 port number

ex: memory-mapped file [Memory-Mapped File (mmap)](../Virtual%20Memory%202c6d658d7a994e0a882ba148033e3d12/Memory-Mapped%20File%20(mmap)%201908c2d6c9b84e03ada2ae1a9c68a8da.md) 

😃  適合做大量資料的傳輸。因為 CPU 處理最快，不需要考慮 IO。 ex: 顯示卡 graphic card

😢  不太 reliable，假如 crash掉，檔案就遺失了。 假如資料很小，光是 setup 的時間就浪費掉不少。

# 根據如何跟 device 互動

## Poll(busy waiting)

主動的。

一直丟東西給你

😃 適用於資料量小

## Interrupt

被動的。

完成的時候再通知我。

😃  適用於資料量大

# 根據誰來control transfer

## Programmed I/O

用 CPU 下指令搬移。

😟  CPU 會忙著做這些事

## Direct memory access (DMA) I/O

用 IO controller 工作，CPU 不用搬資料。

負責搬資料的人： `DMA controller` （不負責計算）

😃  資料量很大的時候

當資料量大時，

initial IO request → 用 interrupt 的方式被 notify → 對 CPU 而言，不需要知道搬移的過程，只要在搬好的時候在 memory 裡面有東西。 → 常和 `memory-mapped IO` 一起用。

常見組合：

DMA  + Interrupt + Memory-mapped 

Programmed I/O + Poll + Port-mapped

EX: 要讀 file 到 memory

1. CPU 下 IO request，叫 disk controller 讀寫
2. 寫到 memory buffer 
3. disk controller 指定 用 DMA 來溝通
4. IDE controller 會跟 DMA 講（setup IO initiate），請 DMA 做資料搬移。提供它：資料在哪，要寫到哪裡(buffer)。
5. 在中間會有很多的 request 來回，慢慢把東西搬完。
6. 寫完之後，產生 interrupt 告訴 CPU 說執行完了。

CPU 直接檢查 memory buffer 看看有沒有搬完。

[]()

假如是 programming 的方式，

就是要 CPU 持續下指令叫 controller 搬東西，來來回回，於是 CPU 就會被拖慢。