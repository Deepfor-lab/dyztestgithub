# 第二次作业提交概况
## 第一次作业-第一个任务提交概况（没参考给出的.txt和main.cpp所以写起来可能会比较奇怪，见谅。）
### 1.在MathFunctions模块中实现静态库和动态库的构建，即在Cmake..命令中可以自行制定将MathFunctions模块构建成静态库还是动态库
在这里我们展示出了一个截图（名字叫做1_1\_使用静态库和动态库的展示.png）用于证明我们在构建相关代码时提供了动态库和静态库的相关构建方式。
### 2.外部依赖管理（如OpenCV库），这部分在ImageProc块当中，如果必要的话，您需要自行安装OpenCV库
在这里我们分几个步骤来对这个外部依赖opencv库做一个提交说明，首先我们先展示一个截图表示opencv被正常安装（名字叫做1_2\_证明opencv库已经安装的截图.png),随后我们展示截图（名字叫做/home1_2\_证明opencv库已经链接的截图.png)证明opencv可以在imag_proc/CMakelists.txt中正常链接，随后我们展示截图（名字叫做1_2\_证明opencv库可以正常使用的截图.png)说明opencv的指令在imag_proc/ImageProcessor.cpp文件中可以被正常使用，意思就是说我们可以在这个文件当中使用opencv库的功能和函数来对我们的图像进行处理，把它当作一个库来引入。而最后我们将会在下一步来展示图像处理的结果，来证明整个opencv库是可以被正常使用的。
### 3.针对自定义数学库的power方法，在cmake中实现test功能，也就是可以在cmake..命令中添加-DBUILD_TESTS=ON选项来测试用例
在这里我们贴出了一个截图（名字叫做1_3\_证明可以ctest的截图.png)来证明在math/CMakeLists.txt将这个选项调整成了ON，随后BUILD_TESTS=ON时，实际编译出测试可执行文件也就说明test_power已经被编译并且正确运行，而且能够最终产生输出就说明其能被ctest指令发现到然后输出最终结果，重复了是因为我在两个地方都加入了同一段代码，在最后我已经删除掉了，最终产生了一个正确的输出结果。
### 4.CMAKE_BUILD_TYPE自行指定构建类型release/debug
可以看到放到仓库中的两个截图，（名字分别为1_4\_调试类型输出截图1.png还有2）第一个图片说明DEBUG对应的的实际编译状态是-g，然后CMake默认对GNU省略-O0，Release对应的编译状态是-O3-DNDEBUG也是已经生效。第二个图片进一步给出了说明的依据：Debug验证：CMAKE_CXX_FLAGS_DEBUG=-g且编译命令含-g 关于Release验证CMAKE_CXX_FLAGS_RELEASE=-O3 -DNDEBUG 且编译命令含 -O3 -DNDEBUG，说明这两个调试状态都是成功的。
### 5.进行CMake Debug，在提交的README.md中简要写明步骤，并且附上图片（如果是gdb等调试工具只能给1分，本质上是需要熟悉一下CMake Debug)
我们同样分步骤来解决这个问题：首先第一步，rm -rf build && mkdir build && cd build，确保文件从干净的环境下开始，避免旧文件的干扰，随后使用cmake --debug-output ..指令来查看 CMake 配置阶段的详细输出，包括变量展开、策略提示等，随后调用指令cmake --trace-expand .. 2>&1 | grep -E 'set\(|Variable:' | head -20查看 CMake 变量的实际值，帮助排查变量未按预期展开的问题。随后调用指令cmake --graphviz=dep.dot ..和dot -Tpng dep.dot -o cmake_dep.png生成项目依赖关系图，直观展示模块间的依赖关系。最终调用指令cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON ..和ls compile_commands.json生成 compile_commands.json 文件，供 IDE 和调试器使用，包含编译命令和参数。形成命令之后可以进行深度调试。（截图分别叫做1_5_CMake调试截图1～4.png）
#### 在上传的其他材料之中，还有数学库和图像的处理结果，以及CMakeists.txt们，总的，math和imag_proc目录下的，已经全部打包上传了。(调试时候的dep.dot文件和command.json我也提交了）
#### 在这里做一个更新，真正的CMake调试截图详见1_5_CMake调试的真正截图，那个是经老队员指导后所领悟的真正结果。

## 第二次作业-第二个任务提交概况
首先我们先来根据实验要求来提交对应的内容，这里我们会基本串联实验的心路历程来对每个提交的文件和对应内容做一个说明。
### 1.使用CMake来管理任务
在仓库中我们提交了一个截图（名字叫做2_1_CMake管理截图.png），里面包含了我们下载了原仓库中提供的所有材料，和我们后期加上的main.cpp和CMakelist.txt文件，其在同级目录之下（请注意必须在同级目录之下，要不然你会吃很大亏，笔者在后面会提及。）
### 2.用Eigen完成向量计算和矩阵求逆
在仓库中我们同样上传了一个截图（名字叫做2_2\_使用Eigen库的截图.png），包含在main.cpp中使用Eigen库中的函数来进行矩阵求逆矩阵的相关过程，当然在使用Eigen之前我们需要在txt和cpp中先把材料中给的Eigen当个库给引进来，然后再直接使用就可以了。
### 3.用spdlog输出日志到终端和optimizer.log中，以debug级别记录每一步迭代的结果（从x0到x·),以info级别记录得到的最小值，所有的数值和向量直接输出，不加任何描述
这个也有终端截图（名字叫做2_3\_使用实验指导书中给出的数据输出的正确日志结果.png)，然后我也把log的文件传送上去了(名字叫做2_3_optimizer.log），作为一种验证，证明算法正确的是，实验指导书给出的初值一样的时候我们的算法输出和指导书上的完全一致，输出形式也是完全一致的。
### 4.不允许引入其他的库
在编写代码的过程当中没有使用其他的库，代码可以证明只使用了材料给的Eigen，spdlog和fmt三个可以使用的库。
#### 这个实验不涉及步骤之外的提供的附加内容所以没有附加内容需要提交来额外提示了。

-------(分割线）

## 分割线之外和大家聊一些本实验的心路历程（比较痛苦的一些点 希望别中招）
## 第一个任务
### 1.关于main.cpp中定义MathFunctions类的问题
```
/home/dyz/下载/Cmakeproject/main.cpp: In function ‘int main(int, char**)’:
/home/dyz/下载/Cmakeproject/main.cpp:7:5: error: ‘MathFunctions’ was not declared in this scope
    7 |     MathFunctions math;
      |     ^~~~~~~~~~~~~
/home/dyz/下载/Cmakeproject/main.cpp:8:38: error: ‘math’ was not declared in this scope
    8 |     std::cout << "[Math] 2^10 = " << math.power(2, 10) << std::endl;
      |                                      ^~~~
gmake[2]: *** [CMakeFiles/CMakeHW.dir/build.make:76：CMakeFiles/CMakeHW.dir/main.cpp.o] 错误 1
gmake[1]: *** [CMakeFiles/Makefile2:123：CMakeFiles/CMakeHW.dir/all] 错误 2
``` 
这个的原因其实是因为你的main.cpp协同性做的不够好，也就是说你的main.cpp中没有定义属于其MathFunctions的类所以你的系统才会在你执行Math库相关指令的时候报这个错误，应该对你的主函数做一个修改。
### 2.关于主函数与分部分的内容不匹配的问题
```
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Cmakeproject/build$ ar t math/libMathFunctions.a
MathFunctions.cpp.o
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Cmakeproject/build$ nm -C math/libMathFunctions.a | grep power
0000000000000000 T power(double, int)
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Cmakeproject/build$ nm -C math/libMathFunctions.a | grep power
0000000000000000 T power(double, int)
```
这个其实有一点节外生枝的意思，就是说我在检查主函数和分部分内容的时候发现如果定义参数问题不匹配的话（也就是定义参数内容并不完全对应的时候也是会报错的，也就是一个提示，无关宏旨，但是是一个最基本的问题，希望引起自己的关注；
### 3.还是关于类的实现和cpp配合的问题
```
[ 10%] Building CXX object image_proc/CMakeFiles/ImageProcessor.dir/ImageProcessor.cpp.o
/home/dyz/下载/Cmakeproject/image_proc/ImageProcessor.cpp:43:6: error: no declaration matches ‘void ImageProcessor::brighten(const string&, const string&, double)’
   43 | void ImageProcessor::brighten(const std::string& in, const std::string& out, double alpha) {
      |      ^~~~~~~~~~~~~~
/home/dyz/下载/Cmakeproject/image_proc/ImageProcessor.cpp:43:6: note: no functions named ‘void ImageProcessor::brighten(const string&, const string&, double)’
In file included from /home/dyz/下载/Cmakeproject/image_proc/ImageProcessor.cpp:1:
/home/dyz/下载/Cmakeproject/image_proc/ImageProcessor.h:15:7: note: ‘class ImageProcessor’ defined here
   15 | class ImageProcessor {
      |       ^~~~~~~~~~~~~~
gmake[2]: *** [image_proc/CMakeFiles/ImageProcessor.dir/build.make:76：image_proc/CMakeFiles/ImageProcessor.dir/ImageProcessor.cpp.o] 错误 1
gmake[1]: *** [CMakeFiles/Makefile2:227：image_proc/CMakeFiles/ImageProcessor.dir/all] 错误 2
gmake: *** [Makefile:101：all] 错误 2
```
这个其实也是在自己的.h类中没有定义出这个东西，但是在同名的.cpp文件中却实现了这个东西，说明没有配合上，需要在.h文件中加入这个类的使用方式然后再在cpp中进行实现。
### 4.CMake调试的真正步骤（在已有项目的基础之上）
#### 4.1 修改launch.json文件
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "CMake: Debug",
            "type": "cppdbg",
            "request": "launch",
            // 核心：让 CMake Tools 扩展自动找到并设置可执行文件路径
            "program": "${command:cmake.launchTargetPath}",
            "args": [],
            "stopAtEntry": false, // 如果设为 true，程序会在 main 函数开头自动暂停
            // 核心：将工作目录设置为 CMake 的构建目录
            "cwd": "${command:cmake.getLaunchTargetDirectory}",
            "environment": [
                // 可选：在 Windows 上运行 MinGW 编译的程序可能需要
                {
                    "name": "PATH",
                    "value": "${env:PATH}:${command:cmake.getLaunchTargetDirectory}"
                }
            ],
            "externalConsole": false, // 使用 VS Code 内置终端
            "MIMode": "gdb", // 根据你的调试器选择 gdb 或 lldb
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            // 核心：自动执行 CMake 的构建任务，确保总是运行最新代码
            "preLaunchTask": "CMake: build",
            "logging": {
                "moduleLoad": false,
                "trace": true
            }
        }
    ]
}

```
#### 4.2 生成tasks.json文件
```
快捷键ctrl+shift+P打开管理，然后输入Tasks: Configure Default Build Task，有build直接选Cmake：build，如果没有的话就选是cmake生成，然后千万注意检查文件中的中文是否会混淆视听。在label出看看一定确保是：Cmake: build这种描述；
```
#### 4.3 运行和调试
```
按正常的步骤走，生成，点开运行与调试的界面，在main.cpp处打一个断点，然后开始用调试工具进行调试，确保图形化界面有显示就行，能够确保你用的是cmake tools而不是gdb等调试工具。
```
有输出就保证你成功了。

### 所以感觉自己第一个任务中不协调性比较明显，希望自己注意罢！
## 第二个任务
### 1.关于CMake管理项目的路径问题
```
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Second_assignments-master/second_assignments/secondCMake/deps/build$ make
[ 50%] Building CXX object CMakeFiles/optimizer.dir/main.cpp.o
/home/dyz/下载/Second_assignments-master/second_assignments/secondCMake/deps/main.cpp:13:10: fatal error: Eigen/Dense: 没有那个文件或目录
   13 | #include <Eigen/Dense>
      |          ^~~~~~~~~~~~~
compilation terminated.
make[2]: *** [CMakeFiles/optimizer.dir/build.make:76：CMakeFiles/optimizer.dir/main.cpp.o] 错误 1
make[1]: *** [CMakeFiles/Makefile2:83：CMakeFiles/optimizer.dir/all] 错误 2
make: *** [Makefile:91：all] 错误 2
```
这个是我做第二个实验遇到的最常见的问题，感谢pyh学长和强大的工具最终让我明白了这个路径问题：
#### 加粗给个提示：CMakelists.txt和main.cpp作为管理项目的工具，其必须和提供的材料库在同级目录之下！！！
#### 再次看到没有文件和目录就看看自己是不是路径弄错了，相对路径和绝对路径都检查一下，大概率是这个问题。
#### 再强调一下，路径！！！！！

### 2.一个非常愚蠢的问题：路径打开文件的问题
```
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Second_assignments-master/second_assignments$ cd /secondCmake
bash: cd: /secondCmake: 没有那个文件或目录
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Second_assignments-master/second_assignments$ cd ~/下载/Second_assignments-master/second_assignments/secondCMake/dep
bash: cd: /home/dyz/下载/Second_assignments-master/second_assignments/secondCMake/dep: 没有那个文件或目录
```
打开本级目录用cd .然后上级目录打开用的是cd ..下级就直接输入该打开的目录就可以了。别胡乱打开这样就会乱。
### 3.关于算法自查的问题
```
dyz@dyz-OMEN-by-HP-Gaming-Laptop-16-wf0xxx:~/下载/Second_assignments-master/second_assignments/secondCMake/build$ ./optimizer
[optimizer] [debug] (-548, -871)
[optimizer] [debug] (-274, -435.5)
[optimizer] [debug] (-137, -217.75)
[optimizer] [debug] (-68.5, -108.875)
[optimizer] [debug] (-34.25, -54.4375)
[optimizer] [debug] (-17.125, -27.21875)
[optimizer] [debug] (-8.5625, -13.609375)
[optimizer] [debug] (-4.28125, -6.8046875)
[optimizer] [debug] (-2.140625, -3.40234375)
[optimizer] [debug] (-1.0703125, -1.701171875)
[optimizer] [debug] (-0.53515625, -0.8505859375)
[optimizer] [debug] (-0.267578125, -0.42529296875)
[optimizer] [debug] (-0.1337890625, -0.212646484375)
[optimizer] [debug] (-0.06689453125, -0.1063232421875)
[optimizer] [debug] (-0.033447265625, -0.05316162109375)
[optimizer] [debug] (-0.0167236328125, -0.026580810546875)
[optimizer] [debug] (-0.00836181640625, -0.0132904052734375)
[optimizer] [info] Min value at x: 0.015702065021647536
```
#### 其实没啥可说的，就是看看第一个点自己代入的对不对，这里面第一个出问题了后面肯定对不了了
### 最后一些想说的话：感觉脚手架搭建比较跳跃，希望多一些细节步骤来辅助完成任务罢，但已经很完善。
