# What is Demand Paging?

`Demand` : 你要我才做。

以 page 為單位，決定要把他放在 memory 或是先留在 disk。

## 優點

1. 比較快
2. 使用率提高

## 需要處理

由於 page 是要用到才會搬進 memory，因此當 access memory ，遇到沒有這個page時，要多做一層判斷屬於哪一種情形：

→ access 的 addr 是真的無效（invalid)，超過使用範圍。  `Invalid reference`

→ 不知道你要用，因此還沒把這個 page 搬進來。 `Not-in-memory`

解決辦法： 用 page table 中的 `valid-invalid bit` 

if 1 → page in memory

if 0 → page not in memory

初始狀態，所有 page 都為 0 

（REVIEW: read, write.. 是在 segmentation 中的 bit 標記）

`Pure demand paging`:

1. 一開始什麼 page 都沒有
2. 開始 run :  開始把 page 放到 memory 裡面。

但是一般系統不會做到這麼極端，還是會先放部分的東西。

## Swapper v.s Pager

Swapper: 以 process 為單位移動到 disk

Pager: 以 page 為單位移動到 disk

在系統裡面，兩者是同時存在的，是不同程度的管理。

## Example

![What%20is%20Demand%20Paging%20fe6888df0eca401f81717f9b2194a1cd/Webp.net-gifmaker.gif](What%20is%20Demand%20Paging%20fe6888df0eca401f81717f9b2194a1cd/Webp.net-gifmaker.gif)

### STEP 1

指向 0 ，發現 invalid, 丟出 `page-fault` ，是一個 interrupt, 因為是軟體的，所以叫 trap  （?????)

→ OS 去看 internal table (在 PCB裡面) 檢查確認是否有效

if 有效但不在 → 做 paging，接到 step 2

if 無效 → abort （?????)

### STEP 2

1. 找到一個空的 frame

如果有空的→ 把 page 從 disk swap 進 memory

如果沒有空的 →做 [replacement](https://www.notion.so/What-is-Demand-Paging-fe6888df0eca401f81717f9b2194a1cd#afead2a34f3b4bb58a2a1bd47c975d4e)

2.  reset page table, 把 valid-invalid bit 改成 1

3.  (program counter 減 4（?????) ) restart instruction 再指一次

→ 有了！

→ 往下一行執行，重複上述步驟

Q: 怎麼知道 addr 到底是不是 v/i 還是只是還沒被 paging

A: 每個 segment 有 segment length, 就已經知道。到了 paging 這邊，已經經過很多長度的檢查，已經知道它是有效的。（L13B, 10:21） （?????)

## Page replacement

如果找不到空的 frame → 強迫把某個 page swap 去 disk，空出空間來。

用 replacement algorithms 決定要把誰swap出去。效能取決於這個 algo。

詳細介紹 → [Page replacement](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12#ce22a536c804415b9aab30a5ed7db8ac)

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)