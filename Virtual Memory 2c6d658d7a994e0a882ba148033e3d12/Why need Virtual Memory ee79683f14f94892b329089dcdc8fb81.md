# Why need Virtual Memory?

### 目的：更 aggresive 的去節省 memory 空間。

很多的 error 跟 func call 根本就用不到，不需要load進來佔空間。

有一些資料被load,卻沒用到 → solved by Virtual memory

把 logical memory 跟 physical memory 分開來的機制。

## 優點

1. 你可以不受實體記憶體的大小， 跑大型的 process
2. 可以增加 CPU 及各種資源的使用率
3. 可以簡化 programming (不用去管 memory 怎麼安排了)
4. 可以讓 program 跑得更快一點（不需要在一開始一次load很多東西）

## 怎麼做 Virtual Memory?

1. Demand Paging : 比較容易管理
2. Demand segmentation ：比較符合 user view