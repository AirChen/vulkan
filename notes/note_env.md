好的，在 Ubuntu 上安装 C++ 开发工具链非常直接。这里为你提供从基础到完整的安装指南。

## 1. 基础编译工具链

### 安装 GCC/G++ 编译器
```bash
# 更新包列表
sudo apt update

# 安装 build-essential（包含 gcc, g++, make 等）
sudo apt install build-essential

# 验证安装
gcc --version
g++ --version
```

### 安装调试工具 GDB
```bash
sudo apt install gdb
gdb --version
```

## 2. 包管理器和构建工具

### 安装 CMake
```bash
sudo apt install cmake
cmake --version
```

### 安装 Ninja（可选，更快的构建系统）
```bash
sudo apt install ninja-build
```

### 安装 pkg-config
```bash
sudo apt install pkg-config
```

## 3. 常用开发库

### 安装基础开发库
```bash
# 安装常用库的开发文件
sudo apt install libboost-all-dev
sudo apt install libssl-dev
sudo apt install libsystemd-dev
sudo apt install libevent-dev
sudo apt install zlib1g-dev
sudo apt install libssl-dev
```

### 安装 GUI 开发库（可选）
```bash
# Qt 开发
sudo apt install qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools

# GTK 开发
sudo apt install libgtk-3-dev

# OpenGL 开发
sudo apt install libglu1-mesa-dev freeglut3-dev mesa-common-dev
```

## 4. 集成开发环境（IDE）

### 安装 Visual Studio Code
```bash
# 方法1：通过 Snap（推荐）
sudo snap install code --classic

# 方法2：通过官方仓库
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

### 安装 CLion（专业 C++ IDE）
```bash
# 通过 Snap
sudo snap install clion --classic

# 或从 JetBrains 官网下载 tar.gz 包解压使用
```

### 安装 Qt Creator
```bash
sudo apt install qtcreator
```

## 5. 代码分析工具

### 安装静态分析工具
```bash
# Clang 工具链
sudo apt install clang clang-tools clang-format clang-tidy

# Cppcheck
sudo apt install cppcheck

# Valgrind（内存检测）
sudo apt install valgrind

# GProf（性能分析）
sudo apt install gprof
```

### 安装代码覆盖率工具
```bash
sudo apt install gcov lcov
```

## 6. 版本控制工具

```bash
sudo apt install git
git --version
```

## 7. 一键安装脚本

创建一个安装所有常用工具的脚本：

```bash
#!/bin/bash
# install_cpp_dev.sh

echo "更新包列表..."
sudo apt update

echo "安装基础编译工具..."
sudo apt install -y build-essential

echo "安装调试和分析工具..."
sudo apt install -y gdb valgrind cppcheck

echo "安装构建工具..."
sudo apt install -y cmake ninja-build

echo "安装开发库..."
sudo apt install -y libboost-all-dev libssl-dev zlib1g-dev

echo "安装代码格式化工具..."
sudo apt install -y clang-format

echo "安装版本控制工具..."
sudo apt install -y git

echo "C++ 开发环境安装完成！"
```

保存为 `install_cpp_dev.sh`，然后运行：
```bash
chmod +x install_cpp_dev.sh
./install_cpp_dev.sh
```

## 8. 验证安装

创建一个简单的测试程序验证环境：

**test.cpp**
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers = {1, 2, 3, 4, 5};
    
    std::cout << "C++ 开发环境测试成功！" << std::endl;
    std::cout << "GCC 版本: " << __VERSION__ << std::endl;
    
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

编译和运行：
```bash
# 编译
g++ -g -o test test.cpp

# 运行
./test

# 调试
gdb ./test

# 静态分析
cppcheck test.cpp

# 内存检查
valgrind --leak-check=full ./test
```

## 9. VS Code 扩展推荐

安装 VS Code 后，推荐安装以下扩展：
```bash
# C/C++ 扩展
code --install-extension ms-vscode.cpptools

# CMake 工具
code --install-extension twxs.cmake
code --install-extension ms-vscode.cmake-tools

# 其他有用扩展
code --install-extension eamodio.gitlens
code --install-extension ms-vscode.makefile-tools
```

## 10. 配置开发环境

### 设置默认编译器（如果需要使用 Clang）
```bash
sudo update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100
sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang++ 100
```

### 创建开发目录结构
```bash
mkdir -p ~/dev/cpp/{projects,libraries,tests}
```

这样就完成了完整的 C++ 开发环境搭建。你可以根据具体项目需求选择安装相应的组件。


安装 vulkan https://vulkan-tutorial.com/Development_environment#page_Linux

基本图形管线 https://vulkan-tutorial.com/Drawing_a_triangle/Graphics_pipeline_basics/Introduction

固定设置结构 https://vulkan-tutorial.com/Drawing_a_triangle/Graphics_pipeline_basics/Fixed_functions
