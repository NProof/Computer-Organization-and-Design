[Expections]

* Exception vs. interrupt
  * Exception. 
  Any unexpected change in control flow without distinguishing whether
  
  內部，外部
  兩個主要的
  造成影響的指令的PC存起來，存在EPC
  控制權交給OS
    終止程式，或繼續
    
  兩種方法知道發生什麼例外
  1. Cause register ，跳到特定位址，再看cause .
  2. Vectored interrupts
    If 不知道原因，問作業系統
    32 bytes or 8 instructions

EPC register 發生的指令程式位址
Cause r 
A 32-bit
跳到80000180hex

加入例外處理，要五個
1. 控制權轉給flush.
無效:  
Main control has IF.flush
ID.flush,控制訊號線歸零
EX.flush

跳到80000180
2. PC-4
