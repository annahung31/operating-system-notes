# Free space

把 free space 當成是一個 file，做法類似 file allocation

因為沒有內容差異，只需要 support sequential access 就好。

# 四種 Scheme：

# 1. Bit vector

每個 block 都用一個 bit 紀錄他是空還是非空，建立一個 vector。

![Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.13.png](Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.13.png)

### 優點

簡單，有效率。

### 缺點

當 disk 很大， bitmap 也會變得很大，甚至大到沒辦法 cached 到 memory，就沒辦法發揮效用。

## Why 需要一次把所有 0 的位置都標出來？

ex: sequential allocation 需要找一塊連續的 free space，就需要用 bitmap 去找出連續為 0 的區塊。

linked-list 雖然不受連續的限制，但假如可以擺在較近的地方，那 disk 磁頭的移動距離也可以變短，都是比較好的。

實務上 allocation 時，FS 會要求，給定一個位置，return 離它最近且大小超過某個 size 的連續 0 在哪。此時 bitmap 就會發生效用。

# 2. Linked-list

同 file 的 allocate method

![Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.20.png](Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.20.png)

# 3. Grouping & 4. Counting

同 file 的 allocate method

![Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.33.png](Free%20space%20f088030bcab24fd7bf9ca863bdfc6819/_2020-06-10_11.21.33.png)