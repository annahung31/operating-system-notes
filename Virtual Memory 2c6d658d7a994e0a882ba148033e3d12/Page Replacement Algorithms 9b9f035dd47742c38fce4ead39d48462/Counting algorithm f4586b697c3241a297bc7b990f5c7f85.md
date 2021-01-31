# Counting algorithm

根據 frequency 來決定誰被踢掉。

# LFU

Least Frequently Used：最不常用的，就把它踢掉。

假如知道整個程式的 behavior， 也跑過一遍，知道誰是比較常被用，就把他留下來。

但是很常用不一定代表他正在用。

access pattern 有時會是，連續頻繁地用某一塊 memory，但結束後就完全不用。假如在這個情況下使用 LRU，那在後面不用的情況就會排擠到其他要使用的 page，造成 page fault。→ [MFU](https://www.notion.so/MFU-6682590f1ffd43c8a4e7b6e0dcbc61c5) 

# MFU

Most Frequently Used：最常用的，把它踢掉。

精神：現在最常用，代表工作快結束，等一下就不會用了，所以可以把他踢掉。

Ex: 執行某個 for loop，等執行完，等一下就不會再去使用了。

# Counting algorithms 的缺點

算 frequency 是一件很浪費時間的事。每做一次 access ，就要把 counter +1

最大的問題是 counter 可能會 [overflow](https://www.notion.so/Counting-algorithm-f4586b697c3241a297bc7b990f5c7f85#1720c412d1e94d969fa044b7883c3276)。 

### Overflow

**算術溢位**（arithmetic overflow）或簡稱為**溢位**（overflow）指的是：

在[電腦](https://zh.wikipedia.org/wiki/%E9%9B%BB%E5%AD%90%E8%A8%88%E7%AE%97%E6%A9%9F)領域裡所發生的溢位條件是，執行單項數值計算時，當計算產生出來的結果是非常大的，大於[暫存器](https://zh.wikipedia.org/wiki/%E6%9A%AB%E5%AD%98%E5%99%A8)或[記憶體](https://zh.wikipedia.org/wiki/%E8%A8%98%E6%86%B6%E9%AB%94)所能儲存或表示的能力限制。

[Counting Algo 會有 Belady Anomaly 嗎？](Counting%20algorithm%20f4586b697c3241a297bc7b990f5c7f85/Counting%20Algo%20%E6%9C%83%E6%9C%89%20Belady%20Anomaly%20%E5%97%8E%EF%BC%9F%208914b5d1d8e14f649eab62ae7695d4ea.md)