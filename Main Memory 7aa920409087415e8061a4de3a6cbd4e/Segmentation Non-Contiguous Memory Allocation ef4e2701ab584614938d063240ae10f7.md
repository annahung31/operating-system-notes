# Segmentation: Non-Contiguous Memory Allocation

programmer 比較常接觸到 segmentation

# 什麼是 segmentation

REVIEW: memory 分成 fix-size 跟 variable size

fix-size  → paging

variable-szie → segmentation

用使用者的角度去想要怎麼切割memory。

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.51.40.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.51.40.png)

把一個 program 切成多塊，個別的空間個別處理 → segmentation

一個 program 包含一大堆的物件，每個size都不一樣:

- main program
- function, object
- variables
- arrays

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.52.41.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.52.41.png)

需要一個 table 紀錄哪個單位放在哪個位置。 → Segmentation Table

# Segmentation Table

包含兩個資訊： `seg#` , `offset` (是誰，在哪裡)

因為 segment 可以長到很大，所以 offset 可以跟整個實體 addr 一樣大。

每個entry  包含  `Base` + `Limit` 

Base: 位置, physical addr

limit: 因為segment 長度都不一樣，所以需要紀錄這個 segment的長度，來知道 offset 的位置是否有效。

（Q: offset不是紀錄這個 segment在哪嗎？怎麼是在 segment裡面？offset 的意義是什麼？）

需要有一個pointer: `Segment-Table Base Register (STBR)` ，存在 PCB裡面，告訴我們這個 table 存在哪。

還要有一個 `Segment-Table Length Register (STLR)` ：知道現在到哪，假設是6，就不用allocate 6以後的。

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.54.09.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-20_11.54.09.png)

不同 segment 一定不會 overlap。假設要share, 一定要先創立一個獨立的segment。不會有某個 physical addr 指向兩個不同的 segment。

# Segment 跟 paging 的比較

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_10.35.23.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_10.35.23.png)

L12B (21:55)

在 segmentation 做 sharing, 才是現在系統的作法。

電腦會先做 segment ，再做paging

porcess 先 map 到一個假的大空 `linear address` ，做 segment，在這個空間裡面切固定大小的size (page)

再用paging  mapping 到真實的位置上。

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_10.34.51.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_10.34.51.png)

目標：降低external / internal 浪費。 

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_9.54.29.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-25_9.54.29.png)

1. physical mem size = 512B → 512B = 2^9 → physical address bit數量 = 9
2. page size = 32B → 32 = 2^5 → page offset = 5 bit
3. 有 8 segments →  virtual address 的前 3 個 bit 就是 segment 的 num，剩下的都是 segment 的 offest

![Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-23_1.09.59.png](Segmentation%20Non-Contiguous%20Memory%20Allocation%20ef4e2701ab584614938d063240ae10f7/_2020-05-23_1.09.59.png)

註：為什麼是前3個bit?

我們要給每個segment一個代表號碼，用3個bits就可以完整代表8個segments (2^3 = 8)

所以前3個bits是代表第幾個segment。

 

4.  given  `hexadecimal`(16進制) 448 → 換成 二進制  010001001000

```jsx
轉換方法：
4 -> 0100

4 -> 0100

8 -> 1000

所以448(hex) = 010001001000(binary)
```

前三碼 010 是 segment# = 2 → 得到00111010

5. 把 segment offset 跟 segment table 得到的值相加

001001000 + 00111010 = 010111110

後5 個 bit 是 page offset, 所以 前面 4個 bit 是page # → 0101=5 → 得到 physical addr。

另一個方法是，將 physical addr 除以 page size 可以得到 page number → `512 / 32 = 16`,  16 = 2^4 → 需要 4 個bit 來描述 第幾個 page → 前 4 位是 page #。