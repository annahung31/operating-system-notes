# allocation

## Contiguous allocation

給你一段連續空間。

用規劃停車場為例子

## fixed-partition

切成一樣大的停車格，一人一個位置

停車格數量= degree of multi-programming

問題：一台機車，停在停車格裡面，浪費空間。

→ 

## variable-size

你告訴我你需要多少空間，我切給你。

問題：如何有效運用空間，不要有洞？

假設一開始填滿了，當某個人離開了，要怎麼再去運用這些洞？

幾個做法：

`first-fit`: 第一個找到的就停

`Best-fit`：全部找過一次，找到最好的，可以剛好佔滿的再停。但是有可能留下更小的洞，讓別人沒辦法用。

`worst-fit`: 找到最大的洞去停，讓別人可以再用。

### 小整理

最多人用 first-fit (average time complexity 最好)

# Fragmentation

有零碎的空間浪費掉

## External fragmentation

程式外的浪費。有一個新的程式要執行，卻沒辦法再塞進空間。

只會發生在 variable-size。

解決：compaction 做壓縮，清理memory，把空間清出來。

### Internal fragmentation

只會發生在 fix-partition。

給定的空間太大浪費掉了。 一台機車停在停車格。

唯一解決：把停車格切更小。 → [Paging](https://www.notion.so/Paging-Non-contiguous-memory-allocation-2163e04aca324ad08713081020308a16)