# [day4] Process
### Process Management 
在os系統中負責process管理，其包含create、schedule、terminae、dead lock

#### Process architecture
process架構圖如下所示
* Stack: 儲存function variable、local variable的位址，每次呼叫function都會在建立一個stack frame區塊用來儲存所有變數狀態
* Heap: allocate memory，是c++使用malloc、new時動態分配的位址
* Data: 初始化資料區段(initialized data segment)，c++的global varaiable和static variable都會儲存於此處，包含read-only area和read-write area
* Text: 文字區段(text segmentation)，這裡是用來儲存CPU執行指令，此處的文字區段都是read-only are，防止被改寫指定

![](https://i.imgur.com/ga7X6Lx.png)


#### PCB (Process Control Blocks)
在Process建立時會先建立起PCB，每個PCB都會由PID所標示，其包含數據結構、進程訊息，執行狀態等等

* Process state: process狀態new、ready、running、waiting
* Program counter: 讓process在執行的時知道記憶體指向的位址
* CPU registers: accumulator, Stack Top pointer, Index register,etc.
* CPU scheduling information: process的優先順序
* Accounting and business information: 包含CPU數量、pid進程等等訊息
* Memory-management information: 包含Base limit register和page Table和Segment Table, 主要用來管理operating system實體、虛擬記憶體的使用。
* I/O status information: 包含開啟中的檔案以及正在進行中的process資訊

![](https://i.imgur.com/SJlOgkD.png)


## 參考
* https://blog.gtwang.org/programming/memory-layout-of-c-program/

