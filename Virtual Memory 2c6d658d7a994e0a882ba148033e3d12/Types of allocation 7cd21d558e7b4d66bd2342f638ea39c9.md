# Types of allocation

跨 process的問題： 每個 process 應該拿到多少個 frame?

每個 process 都有最小 frames 需求值，假如沒有被滿足，根本跑不起來。 例如 IBM 370 需要 6 pages 來儲存 MOVE 這個動作。

# 以固定或變動分類

---

## Fixed allocation

根據 process 一開始的 information 來決定要給他多少 frames。

- Equal allocation：平分
- Proportional allocation：事先知道 program 的 size，正比其可能會需要的

## Priority allocation

在 runtime 時，根據每個 process  的 priority 決定，比較重要或比較急的 process 的給他比較大的 size。

# 以 local v.s global 分類

---

## Local allocation

當需要發生 page replacement 時，只能跟自己的 frames 換。

通常跟 fixed allocation 綁在一起，因為是固定大小的，所以只能跟自己的換。

## Global allocation

但是通常很難事先知道 process 的行為，所以 global 比較常用。

不限制一定只能跟自己的換。會考慮 priority 來做 replacement。

缺點： priority 最小的永遠搶不到。

`thrashing` 

[BACK](https://www.notion.so/Virtual-Memory-2c6d658d7a994e0a882ba148033e3d12)