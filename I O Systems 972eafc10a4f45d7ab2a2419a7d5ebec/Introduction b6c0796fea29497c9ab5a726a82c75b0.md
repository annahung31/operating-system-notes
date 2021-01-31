# Introduction

## 從 computer 角度出發

主要的兩個工作就是

1. IO
2. Computation

## IO devices 有哪些？

tape, HD, mouse, joystick, network card, screen, flash disks

## IO Subsystem

用來控制所有 IO  devices 的方法

## Conflicting trends

1. Standardization of HW/SW interfaces：才能用同樣的方式，控制所有的 device。
2. Board variety of I/O devices：非常多樣化。

## Device drivers

OS 最下層

能夠 access IO subsystem 的 interface。 

跟 system call 的功能類似，連接 apps 跟 OS。

## Device categories

行為相同的分一類：

- Storage devices: disks, tapes
- Transmission devices: network cards, modems
- Human-interface devices: keyboard, screen,
mouse
- Specialized devices: joystick, touchpad