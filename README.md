# Implement-UART-based-on-FPGA
该工程为2020新工科联盟赛琳思暑期学校所含工程，通过使用verilog hdl语言在FPGA上实现了UART通信过程<br><br>
Vivado 版本为2018.3 <br><br>
串口调试工具为 stc-isp-15xx-v6.85F <br><br>
开发板为ALINX-ZYNQ 7020, 芯片型号为XC7Z020-2CLG400II
## Description
该工程测试使用的开发板为ZYNQ-7020开发板，经上板验证，可以实现与上位机的简单通信。其整体设计方案如下：<br><br>
  1.物理设备采用一路UART物理接口进行上位机与FPGA的通信<br><br>
  2.FPGA模拟三个数据处理模块PROCESS0~3,来模拟不同外设需要进行的数据处理工作<br><br>
  3.该设计采用发送模块、接受模块、用户数据处理模块相互独立的设计；模块直接通过忙碌标识信号进行数据传输判断<br><br>
  4.数据接收过程，通过上位机发送的通道切换指令来进行切换数据输出进入的模块，例如SCH0，标识数据传输指模块0，该过程由PC2DEVICE_CT模块进行判决控制<br><br>
  5.数据发送模块，采用总线轮询的设计方式，对各用户数据模块进行轮询，当某个模块有数据发送需求时，则进入等待阶段，当该模块完成1个字节的信息传输后，继续轮询<br><br>
  6.用户定义模块中包含三个PROCESS模块，分别模拟三个不同的数据处理工作。PROCESS0不对数据进行处理，直接返回；PROCESS1对数据进行+1操作后返回；PROCESS2对数据+2操作后返回<br>
## Sourcecode
uart_loop 文件夹包含了完整的工程<br>
## ExecutableFiles
该文件夹中的UART_TOP.bit文件为针对黑金ZYNQ7020开发板生成的比特流文件
