# Deadlocks

## Lecture C

## Avoidance Algorithms

考慮 worst case，讓 worst case 也不發生deadlock。

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.29.23.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.29.23.png)

在 RAG 圖形中，原本有：

request edge

assignment edge

現在加上一個 `claim edge`，表示某個process  P 未來有可能會對某個 resource R 發出 request。

claim edge 可能轉變為 request edge，當 process 真的發出 request的時候，但這還不會造成 deadlock。真正該擔心的是轉變成 assignment edge, 就是 resource 真的把資源給了 P，就有可能造成deadlock。

今天假設有個 claim edge 變成 request edge ，而資源又被release出來了，這時system 就要做一個決定，要不要把資源給他，把他變成綠線（assignment）。那因為我們把所有可能性（claim edge）都畫出來了，所以系統可以藉此考慮會不會發生deadlock circle 來做這個決定。

→  `runtime decision`

但這樣的 algo 一定複雜度不會太低，時間會花很多，所以不一定會願意花這個代價去檢查。

## Multiple instances: Banker's algorithm

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.30.09.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.30.09.png)

把系統狀態分成 safe 跟 unsafe， 

safe: 一定不會發生

unsafe: 有可能發生

deadlock: 真的發生

Avoidance: 保持在 safe 區，擋掉任何會讓系統從safe 掉到 unsafe 的動作

`safe sequence` 找到一個執行的順序，讓整個系統不會有deadlock, 在 safe 區裡面。

### Safe sequence

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.30.40.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.30.40.png)

`Max needs` ：同時間最多會需要多少。

例如下圖的例子中， P0 的 max needs 是 10，目前有 5個，代表有可能下一秒鐘他會再多 request 5 個。

在這個例子裡面，目前還剩下 12 - (5+2+2) = 3 個，

而 P0 還需要 5個， 

P1 還需要 2 個，

P3 還需要 7 個。

1. 先給 P1 用，用完之後，會把所有資源都 release 出來。 目前共有 12 - (5 + 0 + 2) = 5個。
2. 5個足夠給 P0用，因此執行 P0。同樣的執行完後會將所有資源都release出來。目前共有 12 - (0 +0 + 2) = 10 個。
3. 10 個足夠給 P2 用（還需要 7 個），因此執行 P2。

所以，當執行順序是 P1 → P0 → P2 時，就可以順利執行完畢，不會發生 deadlock 沒有資源的情況。

P1 → P0 → P2 就叫做 safe sequence。只要能夠找到 一個 sequence就可以了， 順序不重要。

當找不到 safe sequence → 進入 unsafe state，不一定會發生 deadlock，是worse case才會發生。

### Banker's algorithm(safety algo)

在更改 current holding時，事先偵測是否留在 safe state，假如沒有，就會擋掉。(多個 resource的情況，跟上面的找法一樣)

1. 找出 process 最多需要多少資源
2. 先去看目前是否safe state
3. 只要滿足要求，就可以做完然後release

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.31.43.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.31.43.png)

今天假設 P1 有一個 request 進來，要求多要資源：

1. 先假設要答應他（把 P1 的 allocation 加上新 request的）
2. 去跑 safe sequence 偵測 
3. 如果找得到 → 答應 P1 

    如果找不到 → 拒絕 P1

## Detection

如果知道怎麼做avoidance, 就拿相同的演算法做detection。差別在於不用管未來會怎麼樣，只要判斷現在有沒有問題。

### single instance

用圖判斷:

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.50.59.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.50.59.png)

只管現在系統狀態：不用 claim edge

找 circle →找到代表有 deadlock

### Multiple instances

只有check safe/unsafe ，不代表真的有deadlock

![Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.50.06.png](Deadlocks%209e88d8629c2d495fa6f6e7b01f76a9dc/_2020-05-17_11.50.06.png)

和 avoidance時的差別：不用管 max， given request，就是直接用 available instance 來確認是否找得到 safe sequence。

## Recovery

選項一：重新開機

選項二：把有在 deadlock circle 裡的 process都關掉重來

選項三：一次砍一個 process，看能否解套

Q: 誰先砍？

假如每次都先砍某一個人，那他有可能永遠跑不完（starvation）