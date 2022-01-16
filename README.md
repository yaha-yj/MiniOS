# MiniOS操作系统小型实例

## 0. 项目文件结构

## 1. 操作系统复现

### 1. mbr.S实现主引****导

- 初始化段寄存器为0, 初始化程序运行虚拟地址`0x7c00`
- 通过`int 0x10`中断清空屏幕
- 通过硬盘控制器接口写入`第2扇区长度4扇区的加载器`

### 2. loader.S实现加载器

- 初始化程序运行虚拟地址`0x900`
- 定义4个基本GDT段描述符: `空白描述符`, `代码段描述符`, `数据段/栈段描述符`, `显存段描述符`
- 通过`int 0x15`中断3种基本内存检测方式检测内存大小
- 开启保护模式

  - 打开A20地址线
  - 加载GDT全局描述符表
  - cr0寄存器的pe位置1
- 根据GDT描述符表初始化段寄存器
- 将内核移动至内存中
- 建立页表, 采用普通二级页表

### 3. print.S实现内核打印函数

- 打印单个字符
- 打印字符串
- 打印十六进制整型

### 4. kernel.S实现内核
- 实现中断处理程序
