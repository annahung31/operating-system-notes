# Basic IO method

# Port-mapped IO

- 每個 IO port(device) 都有一個 unique 的 port address。
- 每個 IO port 都有四個 registers (1 ~ 4 bytes)
    1. Data-in register：由 host 讀取 input
    2. Data-out register：由 host 寫入 output
    3. Status register：由 host 讀取目前 device 狀態
    4. Control register：由 host 寫入控制 device
- Program 會經由 `special IO instructions` 跟 IO port 互動