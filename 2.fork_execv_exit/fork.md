# fork——状态机的创建

* 前提背景：操作系统中的第一个程序就是 "/bin/init"，init进程，参考kernel的启动
* 操作系统为所有的程序提供API，其中fork就是程序`状态机的创建`
* fork的本意是叉子：实际上fork就是做一次状态机完整的复制（内存、寄存器等）
* 通过 **pstree** 命令，也能看出来，实际上都是由init进程fork而来的

![pstree](.\pic\pstree.jpg)

# fork API

```bash
man 3 fork
```

1. 立即复制状态机
2. 新创建的子进程返回0
3. 执行fork的父进程，返回的是子进程的进程号

# code

```cpp
#include <unistd.h>
#include <stdio.h>

int main() {
    pid_t pid1 = fork();
    printf("Hello World from (%d)\n", pid1);
}
```

输出结果：

```bash
./a.out 
Hello World from (8829)
Hello World from (0)
```

能看出两点：

1. 8829是子进程的进程号
2. 执行到fork之后，分出了父子进程，并且子进程完全继承了父进程的内容，接着打印



