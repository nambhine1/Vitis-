
<b> This tutorial do multiplication vectorial of  c = a * b </b>

In this tutorial the 

host code: is written using C++ OpenCL API (host.cpp and host.hpp)

Kernel code : is written using C++ (vadd.cpp)

In this tutorial you can dowload my source code using git clone command 

 
 To start with make sure that you download in your computer the vitis-/
 
How to DO that ?


-------------> Open your terminal and type the command bellow to dowload the host code and kernel function (host.cpp , host.hpp,vadd.cpp) : 

> $ git clone https://github.com/nambhine1/vitis-/


In my case i download the vitis- in  >$ /home/semi/

so you can see the source code of c = a * b , 

>$ /home/semi/vitis-/


host.cpp: is the host code

host.hpp:is library used by host.cpp 

vadd.cpp :kernel function

When you have an access to my code you can used it as reference and you can change it whatever you want ..

In vitis to compile and link application project the host and the kernel should compile and linked seperatly 

so we are going to compile and link the host first and then the kernel second 

1)- to compile and link the host used this command bellow 

Before you type this command make sure that you are in the right path which you have host.cpp, host.hpp, vadd.cpp those code are located in  >$ vitis-/

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

7) after running the application program using hardware emulation you should see this in your terminal 


<img src="https://github.com/nambhine1/vitis-/blob/master/imageilaiko.png" alt="output we should get" width="500" height="100" class="center" >






*******thank you so much***********








