# Introduction

# What is RAID

是一種 storage system

# Why need RAID

硬體價格（每單位儲存空間的價格）越來越便宜

是否有可能組合很多個較便宜（易壞或效能較差）的硬碟，變成跟效能較好的硬碟效能相同甚至更好？

讓他變得比較 reliable → 因為有很多顆，可以備份

增加效果 → 可以平行運算 parallelism

# 三個原則

1.  striping: 把資料做切割，放在多顆硬碟
2. Mirror: 複製多份
3. Error-correcting code (ECC) & Parity bit：有多餘的空間可以存 debug 的 code。