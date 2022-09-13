# [day5] Memory Management

### Memory Management 
memory management主要負責管理memory的內存，在低階語言如c和c++在宣告malloc、new時，需在結束時使用free釋放記憶體，否則當memory越來越肥時，會跑出memory leak的問題

#### Garbage Collection(GC)
在高階語言如python、javascript加入garbage Collection機制來回收沒在使用的內存，回收方式大致分為兩種

##### Mark & Sweep GC
Mark & Sweep算法主要分為兩個階段，mark和sweep，在初始化object時會給定其初始化狀態`mark=false`，在mark階段時會將使用到的object進行標記起來`mark=true`，在sweep階段中將`mark=false`的object進行release掉，並且設置`mark=false`後重複上述動作，藉由不斷掃描並釋放在heap區段中多餘的object。

缺點: 
* 在程式中memory使用越多，scan所花的時間就越多。

##### Reference counting GC
在此算法中基礎做法為在initial物件時給一個初始值`reference count=1`，使用該object則+1，如果沒有使用到則-1，當`reference count=0`時則release該物件

缺點: 
* 無法處理ring garbage，如A引用B然後B再引用A，但是A、B物件在程式都使用不到。


### Inter Process communication
在兩個process中要互相溝通有兩種方式，分別是Shared Memory和Message passing，python針對process傳遞可參考[https://docs.python.org/2/library/multiprocessing.html#exchanging-objects-between-processes](https://docs.python.org/2/library/multiprocessing.html#exchanging-objects-between-processes)

#### Shared Memory
在不同的process間使用同一個memory區段去共同控管，會需要考量的race condition(https://ithelp.ithome.com.tw/articles/10239243)的問題

![](https://i.imgur.com/uOVhgzK.png)

#### Memory Passing
先建立起溝通的pipe，然後將其分別丟入兩個不同的process，在不同的process中透過pipe溝通

![](https://i.imgur.com/ddC9EnN.png)

----
以下偏hardware以及系統底層有簡易觀念了解架構即可
### I/O management 以及 POSIX介紹
I/O management主要是I/O device在電腦設備中如何去運作可以參考[https://www.tutorialspoint.com/operating_system/os_io_hardware.htm](https://www.tutorialspoint.com/operating_system/os_io_hardware.htm)簡易看過即可，以及unix中所有操作都是由POSIX API所定義而成，詳細內容可看[https://unix.stackexchange.com/questions/11983/what-exactly-is-posix](https://unix.stackexchange.com/questions/11983/what-exactly-is-posix)

### 基礎網路知識
[https://aws.amazon.com/tw/what-is/computer-networking/](https://aws.amazon.com/tw/what-is/computer-networking/)

## 參考
* https://unix.stackexchange.com/questions/11983/what-exactly-is-posix
* https://www.tutorialspoint.com/operating_system/os_io_hardware.htm
* https://www.omscs-notes.com/operating-systems/io-management/#typical-device-access
* https://dev.to/deepu105/demystifying-memory-management-in-modern-programming-languages-ddd
* https://www.geeksforgeeks.org/memory-management-in-operating-system/
* https://www.geeksforgeeks.org/inter-process-communication-ipc/
* https://ithelp.ithome.com.tw/articles/10239243
* https://aws.amazon.com/tw/what-is/computer-networking/

