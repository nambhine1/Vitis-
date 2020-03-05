
<b> This tutorial is for the beginner who wouldlike to start with vitis doing c = a * b </b>

In this tutorial we used the reference file provides by xilinx to do an vectorial additioning c = a + b 


so we try to change it with c = a * b 
 means we modify a little bit the host code and the kernel function using c++
 
 
 To start with make sure that you download in your computer the vitis-reference file ...
 
How to DO that ?


-------------> Open terminal and tape : 

> $ git clone https://github.com/Xilinx/Vitis-Tutorials/


In my case i download the Vitis-Tutorial in >$ /home/semi/

so you can see the source code of c = a + b , 

>$ /home/semi/Vitis-Tutorials/docs/my-first-program/reference-files/src


host.cpp host code

host.hpp host code 

vadd.cpp kernel function


you can reffered with the code i change to do c = a * b , I modify the host.cpp and vadd.cpp


you can used my code import it in vitis after you import the host.cpp, host.hpp,vadd.cpp


you can build and run it 



First of all in vitis the host and the kernel are build seperatly 


so i compile and link the host first and then the kernel second 




1)- to compile and link the host used this command bellow 

> $ g++ -I$XILINX_XRT/include/ -I$XILINX_VIVADO/include/ -Wall -O0 -g -std=c++11 ./host.cpp  -o 'host'  -L$XILINX_XRT/lib/ -lOpenCL -lpthread -lrt -lstdc++


after you build it you can see that it create an output file name : host (this file is the executable file)


2)- second set upt the environment of vitis and xrt using the command bellow before you compile and link kernel otherwise it will show error

> $ source /tools/Xilinx/Vitis/2019.2/settings64.sh
> $ source /opt/xilinx/xrt/setup.sh

3) after that compile the kernel function using the command bellow :

input file :vadd.cpp
output file : vadd.hw_emu.xo

> $ v++ -t hw_emu --platform xilinx_u200_xdma_201830_2 -c -k vadd -I'./src' -o 'vadd.hw_emu.xo' ./vadd.cpp


4) after we compile the source code of kernel we can link with platform

input file : vadd.hw_emu.xo
output file : krnl_vadd.hw_emu.xclbin
platform: xilinx_u200_xdma_201830_2

> $ v++ -t hw_emu --platform xilinx_u200_xdma_201830_2 --link vadd.hw_emu.xo \ -o 'krnl_vadd.hw_emu.xclbin' --config ./connectivity.cfg


after linking the xilinx object file vadd.hw_emu.xo with the platform xilinx_u200_xdma_201830_2 we get an xclbin file so we can run it now 


5) Before running set the command bellow :

> $ emconfigutil --platform xilinx_u200_xdma_201830_2

> $ export XCL_EMULATION_MODE=hw_emu 

6) run the program last step 

> $ ./host krnl_vadd.hw_emu.xclbin




thank you so much 








