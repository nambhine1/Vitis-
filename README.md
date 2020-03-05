
<b>  <font size="24"> This tutorial show eatch and every step to run an application program in vitis xilinx software using C++ for host and kernel This application program perform c[i] = a[i] * b[i] </font> </b>

<b>  <font size="16"> Introduction: </font> </b>

Vitis is a new tool of xilinx, in vitis the application program is split into host and kernel function.The host and kernel are interconnected using PCIe, the host is written in C++ OpenCL API and the kernel (FPGA) is written using C++/C or RTL or OpenCL C, the figure bellow show the general architecture of host and kernel.


   <img src="https://github.com/nambhine1/vitis-/blob/master/host-kernel.png" alt="output we should get" width="600" height="300" class= "center" >

<b>  <font size="16"> Motivation: </font> </b>

 THis tutorial help us to understand the flow to build an application program so it will help us to create our own program and run it into an emulation hardware or software or hardware itself 
 
<b>  <font size="16"> Techical details: </font> </b>

In this tutorial the 

host code: is written using C++ OpenCL API (host.cpp and host.hpp)

Kernel code : is written using C++ (vadd.cpp)

In this tutorial you can dowload my source code using git clone command 

How to DO that ?


-------------> Open your terminal and type the command bellow to dowload the host code and kernel function (host.cpp , host.hpp,vadd.cpp) : 

> $ git clone https://github.com/nambhine1/vitis-/

After you download it you can go to vitis- using the command bellow :

>$ cd vitis-/

when you open this directory you can see :

host.cpp: is the host code

host.hpp:is library used by host.cpp 

vadd.cpp :kernel function

you only need this 3 source code to build and run our application program...

In vitis to compile and link an application program the host and the kernel should compile and linked seperatly 

so we are going to compile and link the host first and then the kernel second 

<b> 1)- to compile and link the host used this command bellow </b>

Before you type this command make sure that you are in the right path which you have host.cpp, host.hpp, vadd.cpp those code are located in  >$ vitis-/

input : host.cpp

output : host

> $ g++ -I$XILINX_XRT/include/ -I$XILINX_VIVADO/include/ -Wall -O0 -g -std=c++11 ./host.cpp  -o 'host'  -L$XILINX_XRT/lib/ -lOpenCL -lpthread -lrt -lstdc++


after you build it you can see that it create an output file name : host (this file is the executable file)


<b> 2)- second set upt the environment of vitis and xrt using the command bellow before you compile and link kernel otherwise it will show error </b>

> $ source /tools/Xilinx/Vitis/2019.2/settings64.sh

> $ source /opt/xilinx/xrt/setup.sh


<b> 3) after that compile the kernel function using the command bellow : </b>

input file :vadd.cpp
output file : vadd.hw_emu.xo

> $ v++ -t hw_emu --platform xilinx_u200_xdma_201830_2 -c -k vadd -I'./src' -o 'vadd.hw_emu.xo' ./vadd.cpp



<b> 4) after we compile the source code of kernel we can link with platform </b>

input file : vadd.hw_emu.xo
output file : krnl_vadd.hw_emu.xclbin
platform: xilinx_u200_xdma_201830_2

> $ v++ -t hw_emu --platform xilinx_u200_xdma_201830_2 --link vadd.hw_emu.xo \ -o 'krnl_vadd.hw_emu.xclbin' --config ./connectivity.cfg


after linking the xilinx object file vadd.hw_emu.xo with the platform xilinx_u200_xdma_201830_2 we get an xclbin file so we can run it now 



<b> 5) Before running set the command bellow : </b>

> $ emconfigutil --platform xilinx_u200_xdma_201830_2

> $ export XCL_EMULATION_MODE=hw_emu 


<b> 6) run the program last step  </b>

> $ ./host krnl_vadd.hw_emu.xclbin


<b> 7) after running the application program using hardware emulation you should see this in your terminal </b>


<img src="https://github.com/nambhine1/vitis-/blob/master/imageilaiko.png" alt="output we should get" width="500" height="100" class= "center" >






*******thank you so much***********
any query email me : nambhine1@gmail.com







