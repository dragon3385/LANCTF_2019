##### Virus-VM

一个简单的栈虚拟机，给的code为虚拟机指令，可以根据函数sub_400806分析指令长度和功能。

flag判断部分首先要求dword_6024B0为0，其余为针对输入某几个字节的判断，主要分析如何使dword_6024B0为0。需要分析虚拟机执行逻辑和影响，针对虚拟机的分析可以通过复现其switch-case逻辑，结合一些日志打印进行分析，虚拟机指令执行期间对dword_6024B0位置进行了三次或运算，要使其最终为零需要三次相或结果为0，分三块分析指令行为可以快速理清其逻辑，要求满足：

((input_1 >> 4) * 0x15) – input_3 – 0x2e08f7cf=0

(input_3 >> 8) * 0x3 + input_2 – 0x748b93b7=0

(input_1 >> 8) + input_2 – 0x73b9d8df=0

结合之前对某几个字节的限制条件计算出输入即可得到flag