## Win7 x64 + VS 环境下的cuda-convnet 编译配置指南 ##

### About **cuda-convnet**###

High-performance C++/CUDA implementation of convolutional neural networks

### Get **cuda-convnet** ###

- 源地址：https://code.google.com/p/cuda-convnet/
- 原作者：Alex Krizhevsky
- Paper：ImageNet Classification with Deep Convolutional Neural Networks， NIPS'2012

Google Code上面的原版本没有Dropout，我们从Github上下载一个带Dropout的可以用CMake编译的版本，如下：

```
git clone https://github.com/bitxiong/cuda-convnet
```

假定安装在`E:/Projects/cuda-convnet`。

PS：没有CMake工具的，请去[CMake](http://www.cmake.org "CMake")官网下载安装，Windows版本2.8及以上。

CMake 下载地址：[cmake-3.0.0-win32-x86.exe](http://www.cmake.org/files/v3.0/cmake-3.0.0-win32-x86.exe "CMake")或者[cmake-2.8.12.2-win32-x86.exe](http://www.cmake.org/files/v2.8/cmake-2.8.12.2-win32-x86.exe)

### Dependency###
**cuda-convnet** 依赖以下工具：

- Intel MKL
- Pthread
- CUDA

#####1. Intel MKL的安装#####
去Intel的网站下载试用版或者学生版即可。

比如：`c_studio_xe_2013_sp1_update1_setup.exe`，假定安装在`D:\Intel`文件夹

下载地址：[https://software.intel.com/en-us/intel-mkl](https://software.intel.com/en-us/intel-mkl)

#####2. Pthread#####
去网上下载预编译好的PTHREADS-WIN32，64位版本，比如：`pthreads-w32-2-9-1-release.zip`

假设放在`D:\Pthreads`文件夹

下载地址：[http://sourceforge.net/projects/pthreads4w/](http://sourceforge.net/projects/pthreads4w/)



#####3. CUDA#####
下载CUDA 6.0，直接安装，假设SDK安装在`D:\CUDA`文件夹，Samples安装在`D:\CUDA\Samples`文件夹

一般安装过程中，会自动在环境变量中添加`CUDA_PATH=D:\CUDA`，没有的话，就手动添加

下载地址：[https://developer.nvidia.com/cuda-toolkit](https://developer.nvidia.com/cuda-toolkit)

### CMake 配置 ###

打开`CMake/bin`中的`cmake-gui.exe`开始配置

先设置source的文件夹，然后设置binary的文件夹，点击Config，选择一个编译器，比如VS 2008 Win64，或者更高级的VS Win64版本。 如图：

![cmake](image1.jpg)

如果出现找不到MKL或Pthreads的错误，那么在CMake手动设置路径，如图：

 ![mkl & pthreads](image2.jpg)

然后继续，点击Config，Config完成之后，点击Generate。

这样就会在`E:/Projects/cuda-convnet/binary`自动生成VS2008的项目文件。
打开其中的`cuda-convnet.sln`，在VS环境中，Build All，会自动在Release目录下生成`convnet_.pyd`文件，即为编译好的python动态库文件。
