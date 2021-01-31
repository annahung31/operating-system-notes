# blocking and Nonblocking IO

# Blocking IO

直到完成才會 return

會產生 synchronous 同步溝通

我收到資訊了，就代表已經做完了

😃 coding 比較直覺

😟 效能差

# Non-blocking IO

會立刻 return，把資訊記下來，慢慢做。

不同步的

因為 return 不代表做完了。

大部分的 system call 都是這種

write：寫

write_all_back : 真的寫完