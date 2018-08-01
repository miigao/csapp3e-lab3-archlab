### Archlab

#### Part A

	##### 1)

书上251页，有一个类似的，区别是lab中处理的是链表，而书上处理的是数组，需要稍加改动。

##### 2）

需要将当前结点的值保存到栈上，递归返回后与返回值相加，然后要还原栈指针。

##### 3）

分别使用%rdi, %rsi, %rdx传递三个参数。

#### Part B

共计有8处需要添加IIADDQ，分别是：instr_valid，need_regids，need_valC，srcB，dstE，aluA，aluB，set_cc。==容易遗漏的是set_cc==。各阶段实现的计算描述如下：

| 阶段   | iaddq V, rB            |
| ------ | ---------------------- |
| 取指   | icode: ifun ← M~1~[PC] |
|        | rA:rB ← M~1~[PC+1]     |
|        | valC ← M~8~[PC+2]      |
|        | valP ← PC+10           |
| 译码   | valB ← R[rB]           |
| 执行   | valE ← valB+valC       |
|        | ==Set CC==             |
| 访存   |                        |
| 写回   | R[rB] ← valE           |
| 更新PC | PC ← valP              |

#### Part C

使ncopy.ys执行更快的思路：减少指令数量，减少bubble，利用循环展开实现高效率流水线等。

不使用循环展开时，CPE无法降低到9以下，当$k∈[2, 10]$ ，CPE分别为

| k    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| CPE  | 8.93 | 8.53 | 8.68 | 8.24 | 8.21 | 8.22 | 8.25 | 8.29 | 8.33 |

![](https://github.com/miigao/misc/blob/master/archlabchart.png?raw=true)

