# IO performance

# IO 的重要性

因為

1. 要一層一層 call 下去才能讓動作完成
2. 有很多次的 data copy
3. 有很多 context switches
4. 決定如何 handle interrupt，可能造成 overhead

所以通常是 system performance 的關鍵

# Improve IO performance

- Reduce number of context switches ⬇️
- Reduce data copying ⬇️
- Reduce interrupts by using large transfers, smart controllers, polling  ⬇️
- Use DMA
- Balance CPU, memory, bus, and I/O  performance for highest throughput