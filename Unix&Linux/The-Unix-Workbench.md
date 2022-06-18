# The Unix Workbench

一本入门书，内容很简单。点[这里](https://seankross.com/the-unix-workbench/)看原文。

## 第一章 What is Unix？

1. Unix = OS + tools
2. shell：一种命令解释程序，提供命令行接口 (command line interface) 。本书以 Bash 为例。

## 第二章 Getting Unix

1. Mac & Unbantu 使用系统自带的终端 (Terminal) 程序。
2. Windows 10 可用 WSL 或者安装虚拟机。

## 第三章 Command Line Basics

### 3.1 Hello Terminal

1. 提示符 (prompt)。
2. 方向键上、下可在历史输入中切换。
3. `clear` 命令可用于清屏。
4. `echo` 命令可用于打印字符串。

```sh
echo 'Hello World'
```

4. 命令结构

```sh
[command] [options] [arguments]
```

### 3.2 Navigating the Command Line

1. 绝对路径 (absolute path) ：从根目录 `/` 开始。
2. 相对路径 (relative path) ：从当前目录开始。
3. `~` 表示当前用户的家目录，打开终端自动处于家目录。
4. `pwd` 命令可用于打印当前所处绝对路径，也称为工作目录 (print word directory) 。
5. `cd` 命令用于切换目录 (change directory) 。
6. `ls` 命令 (list) 用于列出目录下的文件（目录也是一种文件）。
7. `Tab` 键可用于补全命令。

### 3.3 Creation and Inspection

1. `mkdir` 命令 （make directory） 可用于创建目录，`-p` 选项可用于创建多级目录。
2. `touch` 命令可用于创建文件，也可用于更新已有文件的修改时间。
3. `ls` 命令的 `-l` 选项将输出转为长格式 (long format) 。
    1. 第一列为文件模式 (mode) 。第一个字符代表文件类型，如 `d` 表示目录文件，`-` 表示普通文件，`l` 表示链接文件等。之后的 9 个字符，每 3 个一组，依次为所有者权限 (u)、所有组权限 (g) 和其他权限 (o)，`r` 表示可读，`w` 表示可写，`x` 表示可执行。
    2. 硬链接数
    3. 所有者
    4. 所有组
    5. 文件大小
    6. 上次修改时间
    7. 文件名

```sh
# drwxr-xr-x  2 sean  staff  68 Jan 24 12:31 Code
# drwxr-xr-x  2 sean  staff  94 Jan 20 12:44 Desktop
# drwxr-xr-x  2 sean  staff  24 Jan 20 12:44 Documents
# drwxr-xr-x  2 sean  staff  68 Jan 20 12:36 Music
# drwxr-xr-x  2 sean  staff  68 Jan 20 12:35 Photos
# -rw-r--r--  1 sean  staff  90 Jan 24 11:33 journal-2017-01-24.txt
# -rw-r--r--  1 sean  staff  70 Jan 24 10:58 todo.txt
```

4. `wc` 命令 (word count) 可以用来计算文件的行数、单词数、字符数。
5. `cat` 命令 (concatenate) 可将文件内容丢给标准输出，可以拼接多个文件。
6. `less` 命令用来查看文件内容，空格键或 `b` 键用来翻页，`q` 用来退出。可以看到，`less` 程序会接管 (take over) 终端。
7. `head` 和 `tail` 命令分布用来查看文件的开头和结尾，`-n` 选项可以指定查看的行数。
8. `>` 用来输出重定向，比如原本输出到标准输出文件（即终端屏幕），可指定输出到某文件。但 `>` 会覆盖原有文件内容，而使用 `>>` 则会在文件末尾追加。
9. `vim` 和 `nano` 是常用的文本编辑器。

### 3.4 Migration and Destruction

1. `mv` 命令 (move) 可用来移动文件或是重命名。
2. `cp` 命令 (copy) 可用来拷贝文件，`-r` 选项用来递归地拷贝，如拷贝某个目录及其下面所有子目录和子文件。
3. `rm` 命令 (remove) 可用来删除文件，同理 `-r` 选项表示递归，`-f` 选项表示强制。注意，`rm` 命令不可撤销，执行有风险，每次删除文件请三思后再进行。
4. 另一种替代删除文件的方法：将文件移动到回收站/废纸篓。Mac 上是 `~/.Trash` ，Unbantu 上是 `~/.local/share/Trash` 。

## 第四章 Working with Unix

### 4.1 Self-Help

1. `man` 命令可用于展示其他命令的手册。同样，该程序会接管终端。`q` 用于退出，`/` 后跟字符串可用来搜索，`n` 用于找下一个匹配内容，`N` 用于找上一个匹配内容。
2. `apropos` 命令用来查询相关的命令。如 `apropos editor` 会列出与编辑器相关的命令/程序。

### 4.2 Get Wild

1. 通配符 (wildcard) `*` 代表 0 个或多个字符。如 `mv *.jpg Pic/` 将当前目录下以 `.jpg` 结尾的文件移到 `Pic` 目录下。

### 4.3 Search

#### 4.3.1 Regular Expressions

1. 正则表达式是一种定义了其他字符串模式 (Patterns) 的字符串。
2. `grep` 命令用于搜索文件中符合某模式的行。

#### 4.3.2 Metacharacters

1. `grep` 的 `-e` 选项使其进入正则表达式模式。正则表达式配合元字符，可以发挥巨大作用。
2. 元字符 `.` 表示任意的一个字符。
3. 元字符 `+` 表示前一个字符出现**一**次或多次。
4. 元字符 `*` 表示前一个字符出现**零**次或多次。
5. 元字符 `?` 表示前一个字符出现**零**次或**一**次。
6. `{m}` 表示前一个字符精确出现**m**次。
7. `{m,}` 表示前一个字符至少出现**m**次。
8. `{m,n}` 表示前一个字符至少出现 **m** 次，至多出现 **n** 次。
9. `( )` 将多个字符作为一组，配合上面几种方式，将对前一个字符的生效作用，转为对前面一组进行生效 (capturing group) 。

#### 4.3.3 Character Sets

1. `grep` 的 `-v` 选项输出文件中**不**满足模式的行。
2. `[ ]` 表示被括起来的字符中的其中一个，如 `[abc]` 表示 `a` 或 `b` 或 `c` 。
3. `^` 表示取反，`[^abc]` 表示除了 `a` 或 `b` 或 `c` 外的任意字符。
4. `-` 可以表示连续的多个字符，如 `[A-Z]` 表示从 `A` 到 `Z` 所有大写字母。
5. `grep` 的 `-i` 选项表示忽略大小写。
6. `\w` 表示单词 (word) 字符，包括字母、数字和下划线。`\W` 表示非单词字符。
7. `\d` 表示数字 (digit) 字符。`\D` 表示非数字字符。
8. `\s` 表示空白字符。`\S` 表示非空白字符。

#### 4.3.4 Escaping, Anchors, Odds, and Ends

1. `\` 用来转义 (escaping) ，让后面跟着的特殊字符回归它原本的含义，比如 `\+` 表示匹配字符 `+`。
2. `^` 用来匹配行起始，`$` 用来匹配行结束。
3. `|` 用来连接多个正则表达式，表示或。
4. `grep` 的 `-n` 选项表示统计匹配出现的次数。
5. `grep` 后面可以加多个文件，打印内容也会指示匹配行出现在哪个文件。
6. 推荐一个[正则表达式学习网站](https://regexr.com/)。

#### 4.3.5 find

1. 打印当前目录下名字为 `states.txt` 的文件路径。

```sh
find . -name "states.txt"
```

2. 打印当前目录下以 `.jpg` 结尾的文件路径。

```sh
find . -name "*.jpg"
```

### 4.4 Configure

#### 4.4.1 History

1. `history` 命令输出在终端中使用过的命令。这些命令被保存在文件 `~/.bash_history` 中。

#### 4.4.3 Customizing Bash

1. `~/.bash_profile` 是终端的配置文件，可以用 `alias` 命令在其中为长命令起别名，在终端中输入别名能达到对应长命令相同的效果。再修改完配置文件后，别忘了用 `source` 命令重新加载配置文件，使其中新加的配置生效。

### 4.5 Differentiate

1. `diff` 命令打印两个文件不同的行。
2. `sdiff` 命令打印两个文件，并标识不同的行。
3. 文件内容唯一性可用 **checksum** 或 **hash** 标识。`md5` 和 `shasum` 命令用不同的算法，根据文件内容生成唯一标识，相同内容的文件，生成的结果也相同。

### 4.6 Pipes

1. `|` 表示管道 (pipe) ，能将管道左边的输出，当成管道右边的输入。
2. `sort` 命令可用来排序行，`-n` 选项表示按数字比较，`-k` 选项指定要比较的列。
3. `uniq` 命令将行进行去重，前提是要先排序。

### 4.7 Make

1. `make` 命令用来构建大型程序，需要与名为 `makefile` 的文件进行配合。
2. `makefile` 文件中有符合如下规则的模块。

```sh
[target]: [dependencies...]
  [commands...]
```

3. `make target` 在 dependencies 准备好时，执行对应的 commands 。当依赖准备好且距离上次 `make` 没更新过，则对应的 commands 不会执行。
4. 不带参数的 `make` 默认执行目标 `all` 。
5. 更多关于 `make` 的知识可以看[这里](http://makefiletutorial.com/)。

## 第五章 Bash Programming

推荐编辑器 [Atom](https://atom.io/) 。

### 5.1 Math

1. 创建文件 `math.sh` ，内容如下。通过命令 `bash math.sh` 执行该 Bash 脚本。

```sh
#!/usr/bin/env bash
# File: math.sh

expr 5 + 2
expr 5 - 2
expr 5 \* 2     # 符号 * 在 Bash 中正常含义是通配符，这里要转义
expr 5 / 2      # 这里是整除
expr 5 % 2      # 取余运算，mod
```

2. 第一行以 `#!` 开头，表明了脚本该用 `bash` 来运行它。井号之后的内容都是注释 (comment) ，会被 bash 程序忽略。
3. 创建文件 `bigmath.sh` ，内容如下。将复杂公式输给 `bc` 程序进行计算。

```sh
# !/usr/bin/env bash
# File: bigmath.sh

echo "22 / 7" | bc -l
echo "4.2 * 9.15" ｜ bc -l
echo "(6.5 / 0.5) + (6 * 2.2)" | bc -l
```

### 5.2 Variables

1. 自定义变量命名规则：

- 字母全小写，能避免和环境变量冲突。
- 以字母开头，只包含字母和下划线。
- 单词之间以下划线分隔。

2. 通过如下代码，命名变量 `chapter_number` ，注意 `=` 两边不能有空格。

```sh
chapter_number=5
```

3. 通过 `$` 符号加变量名，取出变量的值。

```sh
echo $chapter_number
```

4. 改变变量的值：

```sh
let chapter_number=$chapter_number+1
```

5. 变量也能存储字符串：

```sh
the_empire_state="New York"
```

6. `$( )` 可用于命令替换，运行括号中的命令，用结果替换 `$( )` 。

```sh
math_lines=$(cat math.sh | wc -l)
```

7. 字符串中使用变量：

```sh
echo "I went to school in $the_empire_state."
```

8. 运行脚本时可以指定多个参数，如 `bash vars.sh red blue` ，然后脚本代码里，`$@` 表示全部参数（是个数组？），`$1` 表示第 1 个参数，`$2` 表示第 2 个参数，以此类推，`$#` 表示参数个数。

```sh
#!/usr/bin/env bash
# File: vars.sh

echo "Script arguments: $@"
echo "First arg: $1. Second arg: $2."
echo "Number of arguments: $#"
```

### 5.3 User Input

1. 获取用户输入。脚本执行到 `read` 命令，终端会等待键盘输入，输入结果会保存到 `response` 变量中：

```sh
#!/usr/bin/env bash
# File: letsread.sh

echo "Type in a string and the press Enter:"
read response
echo "You entered: $response"
```

### 5.4 Logic and If/Else

#### 5.4.1 Conditional Execution

1. 逻辑/条件表达式，结果要么为 `true` ，要么为 `false` 。
2. `$?` 可以获取上一条命令/脚本的执行结果，也称退出状态。如果执行成功，则为 `true` ，对应数字 `0` ; 如果执行成功，则为 `false` ，对应数字 `1` 。
3. 逻辑运算符 `||` 和 `&&` 表示“或”和“且”，具有短路特性。如果没有括号，则从左到右进行判断，在能判断逻辑表达式结果时，不会继续接下来的运算。

#### 5.4.2 Conditional Expressions

1. 条件表达式会用双层的中括号 `[[ ]]` 包围起来，并且可以搭配逻辑运算符。下面列出常见的使用方法：

| Logical Flag | Meaning | Usage |
|:-------------|:--------|:------|
| -gt | **G**reater **T**han | `[[ $planets -gt 8 ]]` |
| -ge | **G**reater Than or **E**qual To | `[[ $votes -ge 270 ]]` |
| -eq | **Eq**ual | `[[ $fingers -eq 10 ]]` |
| -ne | **N**ot **E**qual | `[[ $pages -ne 0 ]]` |
| -le | **L**ess Than or **E**qual To | `[[ $candles -le 9 ]]` |
| -lt | **L**ess **T**han | `[[ $wives -lt 2 ]]` |
| -e | A File **E**xists | `[[ -e $taxes_2016 ]]` |
| -d | A **D**irectory Exists | `[[ -d $photos ]]` |
| -z | Length of String is **Z**ero | `[[ -z $name ]]` |
| -n | Length of String is **N**on-Zero | `[[ -n $name ]]` |

| Logical Operator | Meaning | Usage |
|:-------------|:--------|:------|
| =~ | Matches Regular Expression | `[[ $consonants =~ [aeiou] ]]` |
| = | String Equal To | `[[ $password = "pegasus" ]]` |
| != | String Not Equal To | `[[ $fruit != "banana" ]]` |
| ! | Not | `[[ ! "apple" =~ ^b ]]` |

#### 5.4.2 If and Else

1. `if` 后面的条件表达式成立，则执行 `then` 之后的内容，否则跳过。

```sh
#/usr/bin/env bash
# File: simpleif.sh

echo "Start program"

if [[ $1 -eq 4 ]]
then
    echo "You entered $1"
fi

echo "End program"
```

2. `if` 后面的条件表达式成立，则执行 `then` 之后的内容，否则执行 `else` 后面的内容。

```sh
#/usr/bin/env bash
# File: simpleifelse.sh

echo "Start program"

if [[ $1 -eq 4 ]]
then
    echo "Thanks for entering $1"
else
    echo "You entered $1, not what I was looking for."
fi

echo "End program"
```

3. `if` 后面的条件表达式成立，则执行对应 `then` 之后的内容，否则判断 `elif` 后面的条件表示是否成立，成立则执行对应 `then` 之后的内容，否则执行最后的 `else` 之后的内容。

```sh
#!/usr/bin/env bash
# File: simpleelif.sh

if [[ $1 -eq 4 ]]
then
    echo "$1 is my favorite number"
elif [[ $1 -gt 3 ]]
then
    echo "$1 is a great number"
else
    echo "You entered: $1, not what I was looking for."
fi
```

4. `if-elif-else` 结构，配合之前介绍的逻辑操作符：

```sh
#!/usr/bin/env bash
# File: condexif.sh

if [[ $1 -gt 3 ]] && [[ $1 -lt 7 ]]
then
    echo "$1 is between 3 and 7"
elif [[ $1 =~ "Jeff" ]] || [[ $1 =~ "Roger" ]] || [[ $1 =~ "Brian" ]]
then
    echo "$1 works in the Data Science Lab"
else
    echo "You entered: $1, not what I was looking for."
fi
```

5. `if-elif-else` 可以嵌套使用，结合遵循就近原则：

```sh
#!/usr/bin/env Bash
# File: nested.sh

if [[ $1 -gt 3 ]] && [[ $1 -lt 7 ]]
then
    if [[ $1 -eq 4 ]]
    then
        echo "four"
    elif [[ $1 -eq 5 ]]
    then
        echo "five"
    else
        echo "six"
    fi
else
    echo "You entered: $1, not what I was looking for."
fi
```

### 5.5 Arrays

1. 数组变量声明用小括号 `( )` ，元素之间用空格区分:

```sh
plagues=(blood frogs lice flies sickness boils hail locusts darkness death)
```

2. 引用数组元素要用到参数扩展 (parameter expansion) ，使用 `${ }` 结构：

```sh
echo ${plagues[0]}
echo ${plagues[*]} # 打印全部元素

plagues[4]=disease # 改变某个元素的值

echo ${plagues[*]:5:3} # 打印第 5 个元素开始的 3 个元素
```

3. 数组末尾添加元素用 `+=` ：

```sh
dwarfs=(grumpy sleepy sneezy doc)
echo ${dwarfs[*]}
dwarfs+=(bashful dopey happy)
echo ${dwarfs[*]}
```

### 5.6 Braces

1. 花括号扩展 (brace expansion) ：

```sh
echo {0..9} # 打印 0 到 9
echo {a..e} # 打印 a 到 e
echo a{0..4} # 打印 a0 到 a4
echo b{0..4}c # 打印 b0c 到 b4c
echo {1..3}{A..C} # 类似笛卡尔积，打印 1A 1B 1C 2A 2B 2C 3A 3B 3C
```

2. 花括号中用到变量，则需要用到 `eval` 命令：

```sh
start=4
end=9
echo {$start..$end}
eval echo {$start..$end}

# 输出结果：
# {4..9}
# 4 5 6 7 8 9
```

3. 不连续的情况，则用逗号分隔元素：

```sh
echo {Who,What,Why,When,How}?

# Who? What? Why? When? How?
```

### 5.7 Loops

#### 5.7.1 for

1. `for` 循环：

```sh
#!/usr/bin/env bash
# File: forloop.sh

echo "Before Loop"

for i in {1..3}
do
    echo "i is equal to $i"
done

echo "After Loop"
```

2. 更多例子：

```sh
#!/usr/bin/env bash
# File: manyloops.sh

echo "Explicit list:"

for picture in img001.jpg img002.jpg img451.jpg
do
    echo "picture is equal to $picture"
done

echo ""
echo "Array:"

stooges=(curly larry moe)

for stooges in ${stooges[*]}
do
    echo "Current stooge: $stooge"
done

echo ""
echo "Command substitution:"

for code in $(ls)
do
    echo "$code is a bash script"
done
```

#### 5.7.2 while

1. `while` 循环：

```sh
#!/usr/bin/env bash
# File: whileloop.sh

count=3

while [[ $count -gt 0 ]]
do
    echo "count is equal to $count"
    let count=$count-1
done
```

#### 5.7.3 Nesting

1. 嵌套循环：

```sh
#/usr/bin/env bash
# File: nestedloops.sh

for number in {1..3}
do
    for letter in a b
    do
        echo "number is $number, letter is $letter"
    done
done
```

2. 循环体中加入 `if-else` 结构：

```sh
#!/usr/bin/env bash
# File: ifloop.sh

for number in {1..10}
do
    if [[ $number -lt 3 ]] || [[ $number -gt 8 ]]
    then
        echo $number
    fi
done
```

### 5.8 Functions

#### 5.8.1 Writing Functions

1. 函数结构：

```sh
function [name of function] {
    # code here
}
```

2. 一个简单的函数：

```sh
#!/usr/bin/env bash
# File: hello.sh

# 函数定义
function hello {
    echo "Hello"
}

# 通过函数名直接调用 3 次
hello
hello
hello
```

3. 函数内部同样可以用之前介绍过的 `$#`、`$@`、`$1`、`$2`、... 。先定义如下脚本文件，然后通过 `source ntmy.sh` 将函数定义加入当前环境中，于是就可以通过函数名直接调用函数，并可以在其后跟着参数。

```sh
#!/usr/bin/env bash
# File: ntmy.sh

function ntmy {
    echo "Nice to meet you $1"
}
```

4. 另一个例子：

```sh
#!/usr/bin/env bash
# File: addseq.sh

function addseq {
    sum=0

    for element in $@
    do
        let sum=sum+$element
    done

    echo $sum
}
```

#### 5.8.2 Getting Values from Functions

1. 函数有两个作用：计算值 (computing values) 和副作用 (side effects) 。如 `pwd` 打印当前路径，对计算机没有任何影响，是纯计算；而 `mv` 和 `cp` 则会改变计算机，有副作用。函数只要对计算机上的文件进行了创建或改动，我们就说产生了副作用。

2. 在 `addseq.sh` 的函数中，我们定义了变量 `sum` ，这是一个全局变量，在函数外也能访问到（前提是脚本被加载）。比如直接在命令行中 `echo $sum` 。

3. 全局变量被环境共享，容易被破坏。故用 `local` 关键字标注的变量，即局部变量，有时会更有用：

```sh
#!/usr/bin/env bash
# File: addseq2.sh

function addseq2 {
    local sum=0

    for element in $@
    do
        let sum=sum+$element
    done

    echo $sum
}
```

4. 为了获取局部变量的值，我们可以：

```sh
my_sum=$(addseq2 5 10 15 20)
echo $my_sum
```

### 5.9 Writing Programs

#### 5.9.1 The Unix Philosophy

1. Unix程序只做一件事：

- 越短的程序越好修复。
- 越短的程序越好理解。
- 对不读源码的人来说，它理解程序输入、输出和副作用也更容易。
- 使用小程序构筑 (composability) 的新程序也会更小。

2. 结合管道 `|` 能更好发挥程序的作用。
3. 程序应该安静 (quietness) 。除非必要，不要向控制台打印东西。

#### 5.9.2 Making Programs Executable

1. `chmod` 命令能够更改文件权限。该命令需要两个参数，第一个参数指示要改成什么权限，第二个参数指示改变哪个文件的权限。

2. 第一个参数由三部分构成，依次如下：

|Character  |Meaning |
|:----------|:-------|
|`u` |The owner of the file |
|`g` |The group that the file belongs to |
|`o` |Everyone else  |
|`a` |Everyone above |

|Character  |Meaning |
|:----------|:-------|
|`+` |Add permission |
|`-` |Remove permission |
|`=` |Set permission  |

|Character  |Meaning |
|:----------|:-------|
|`r` |Read a file |
|`w` |Write to or edit a file |
|`x` |Execute a file  |

3. 将一个文件设为可执行：`chmod u+x short` ，然后通过 `./short` 的方式执行它。

4. 有时候 Bash 不一定知道如何执行可执行文件。那么，就需要在可执行文件第一行进行指定，称为 **shebang** ，以 `#!` 开头。

#### 5.9.3 Environmental Variables

1. 环境变量是 Bash 创建，用来保存当前计算环境相关数据的。环境变量全大写，如 `HOME` 保存了当前的家目录，`PWD` 保存了当前的工作目录。

2. 环境变量 `PATH` 的内容为冒号分隔的多个路径。当 Shell 开始解释命令时，会从这个路径搜索可执行文件和命令。将我们存放自定义命令/脚本的路径加入到 `PATH` 变量中，就可以在 Shell 中，通过直接键入命令/脚本名的方式进行执行。

3. 在 Shell 中修改环境变量后，要用 `export` 命令使其生效。但这种方式关闭了 Shell ，修改就失效了。所以最好的方式是在 ～/.bash_profile 中进行环境变量的修改。

```sh
nano ~/.bash_profile
```

```sh
alias docs='cd ~/Documents'
alias edbp='nano ~/.bash_profile'

export PATH=~/Code/Commands:$PATH
source ~/Code/addseq2.sh
```

```sh
source ~/.bash_profile
addseq2 9 8 7
```

## 第六章 Git and GitHub

### 6.1 What are Git and GitHub?

1. Git is a command line program which allows you to track versions of any code or plain text documents that you create. - 分布式版本控制；追踪文件修改历史；团队协作

2. GitHub is a website that provides remote Git repositories.

### 6.2 Setting Up Git and GitHub

1. `git --version` 查看 Git 版本，也可用来判断安装成功。

2. 配置 GitHub 用户名和账户名。

```sh
git config --global user.name "myUserName"
git config --global user.email myName@email.com
```

### 6.3 Getting Started with Git

1. 创建文件夹（本地仓库）：

```sh
cd
mkdir my-first-repo
cd my-first-repo
```

2. 初始化 Git，管理当前文件夹（在当前目录下生成了 .git 目录，保存了 Git 所需的所有信息）：

```sh
git init
```

3. 文件夹下工作，比如创建文件：

```sh
echo "Welcome to My First Repo" > readme.txt
```

4. 通过命令 `git status` 查看仓库状态，可以看到 `readme.txt` 未被追踪。为了让 Git “知道”它，使用 `git add readme.txt` 命令。再用 `git status` 看下仓库状态，可以发现该文件被暂存 (**staged**) 。如果有多个文件需要追踪，则可用 `git add -A` 命令。

5. 这时，可用命令 `git rm --cached readme.txt` 将其移出暂存区，就又回到了 `git add` 之前的状态了。

6. 通过 `git commit -m "added readme.txt"` 命令，可以将暂存区的内容形成一次提交。

7. 撤销一次上一次提交：

```sh
git reset --soft HEAD~
```

### 6.4 Important Git Features

#### 6.4.1 Getting Help, Logs, and Diffs

1. 查看某个 Git 命令的手册：

```sh
git help [name of command]
```

2. 查看提交列表，每个提交都有它的时间、日期、提交信息和唯一标识的 SHA-1 哈希码：

```sh
git log
```

3. 查看当前文件和上一次提交之间的差异：

```sh
echo "The third line." >> readme.txt
git diff readme.txt
```

4. 删除文件未加入暂存区的改动：

```sh
git checkout readme.txt
```

#### 6.4.2 Ignoring Files

1. `.gitignore` 文件，记录不想被 git 追踪的文件路径。

### 6.5 Branching

1. 列出当前可用全部分支，输出结果中前面带 * 的是当前分支：

```sh
git branch
```

2. 创建分支：

```sh
git branch [name-of-branch]
```

3. 切换分支：

```sh
git checkout [name-of-branch]
```

4. 删除分支：

```sh
git branch -d [name-of-branch]
```

5. 创建并切换分支：

```sh
git branch -d [name-of-branch]
```

6. 一个分支上的修改、提交，不会影响另一个分支。为了让一个分支上的变动加入到主分支，可进行如下命令：

```sh
git checkout master # 先切换到合并的基 (base) 分支
git merge update-readme
```

7. 解决冲突。合并分支的时候会出现冲突，即两个分支在同一行上都出现了修改。当执行合并操作后，会看到文件内容如下。在 `<<<<<<< HEAD` 和 `=======` 之间，是主分支下对该文件作出的修改；在 `>>>>>>> update-readme` 和 `=======` 之间，是 `update-readme` 分支下对文件作出的修改。我们只需要对这部分进行视情况修改：保留主分支修改或者保留其他分支修改，或是都保留。然后执行 `add` 和 `commit` 命令即可。

```sh
## Welcome to My First Repo
## Learning Git is going well so far.
## I added this line in the update-readme branch.
## <<<<<<< HEAD
## It's windy outside today.
## =======
## It's cloudy outside today.
## >>>>>>> update-readme
```

```sh
git add -A
git commit -m "resolved conflict"
```

8. 推荐参考书 [Pro Git](https://git-scm.com/book/en/v2) 。

### 6.6 GitHub

1. GitHub 上创建仓库。

2. 关联 GitHub 上的仓库。

```sh
# origin 是给远程仓库做的命名
git remote add origin https://github.com/Seventeen1Gx/My-Notebook.git
```

3. 展示当前本地仓库的远程仓库：

```sh
git remote
```

4. 提交本地仓库到远程仓库。

```sh
# -u 将 origin 设为默认远程仓库
git push -u origin master
```

#### 6.6.1 Markdown

1. Markdown is a markup language.
2. 一些规则：

- 标题用 `#`、`##`、... 表示。
- 斜体用 `*word*` 表示。
- 加粗用 `**word**` 表示。
- 列表用 `-` 或 `1.`、`2.`、`3.`、... 。
- 单行代码用 `` `code` `` 。
- 多行代码用 `` ``` `` 。
- 链接用 `[Link text here](http://jhu.edu)` 。
- 图片用 `![Alt text here](http://jhu.edu/jeff.jpg)` 。

3. [在线编辑器](https://jbt.github.io/markdown-editor/)以及[教程](https://guides.github.com/features/mastering-markdown/)。

#### 6.6.2 Pull Requests

1. 本地创建分支：

```sh
git checkout update-readme
```

2. 拉取远程主分支内容，保持同步：

```sh
git merge master
```

3. 在本地分支上修改并提交到远程对应分支：

```sh
git add -A
git commit -m "made readme more personal"
git push origin update-readme
```

4. 在 GitHub 对应远程仓库上，可以看到我们的分支。转到这个分支，可以看到相应的修改。

![](https://seankross.com/the-unix-workbench/images/branch-button.png)

5. 为了把这个分支合并到主分支，需要在 GitHub 上发起拉取请求，就像在 GitHub 这边执行 `merge` 命令。点击 "New pull requst" 按钮，将会看到如下画面：

![](https://seankross.com/the-unix-workbench/images/create-pr.png)

6. 填好信息后，点击 "Create pull request" 按钮，来到如下画面：

![](https://seankross.com/the-unix-workbench/images/opened-pr.png)

7. 这时已经将本地修改合并到主分支。然后本地可以执行 `git pull` 拉取最新代码。

#### 6.6.3 Pages

1. GitHub Pages allows you to create and host a website on GitHub using only Git and Markdown. - 构建网站
2. 远程仓库的 setting 标签页，可以看到 GitHub Pages 的 Source 为 None 。将其改为主分支，就可以根据主分支内容来生成页面。

![](https://seankross.com/the-unix-workbench/images/select-pages.png)

3. 通过域名 [your-github-username].github.io/my-first-repo 可以访问对应页面。

#### 6.6.4 Forking

1. 通过 **fork** 可以轻松地修改其他人的软件。fork 一个 GitHub 仓库，就是把这个仓库复制到自己的 GitHub 账户下。
2. 在自己的 GitHub 仓库下可以随意修改，保持新特性，与其他人共享，或是将新特性通过 pull request 合并到原仓库。原仓库也被称作上游 (upstream) 仓库。
3. 在对应仓库上有 fork 按钮可以按，按了之后让你选要拷贝的账户，选完了在自己账户下就能看到对应仓库了。然后可以通过 `git clone` 将代码克隆到本地。
4. 通过如下命令，可以看到克隆代码追踪的远程仓库。

```sh
git remote -v
```

5. 在克隆仓库做的修改，也可以通过上一节介绍的 pull request 合并到原仓库。
6. [参考资料](https://docs.github.com/cn)。

## 第七章 Nephology

### 7.1 Introduction to Cloud Computing

1. 云只是“一台”我们可以通过互联网访问的计算机。
2. 本文借助 [DigitalOcean](https://www.digitalocean.com/) 来提供一台服务器，这在 DigitalOcean 上称为 droplets 。

### 7.2 Setting Up DigitalOcean

1. 点击这个[链接](https://m.do.co/c/530d6cfa2b37)，作者给我们提供了可以 2 个月的免费使用的服务器。
2. 右上角登录。填写了账户信息后，来到个人页面。点击 "Create a new Droplet" ，然后选择 Ubantu 发行版和 5 美元每月的规格。再选择服务器地区（没有中国，跟着作者选美国吧）。选择完毕，点击最后的创建按钮，等待几分钟，服务器初始化完成并启动。然后注册账户的邮箱就会收到 IP 地址、用户名（默认是 root）和随机密码。

### 7.3 Connecting to the Cloud

1. 通过 `ssh` 程序 (Secure Shell) 连接远程服务器。

```sh
ssh [username]@[IP address]
```

2. 第一次登录会提示如下，输入 `yes` 后继续，然后就是输入密码。

```sh
## The authenticity of host '159.203.134.88 (159.203.134.88)' can't be established.
## ECDSA key fingerprint is SHA256:UhtoIx/3c6/MmAIE+H8w5oGE06PsbXdzRRsAUhKtjhs.
## Are you sure you want to continue connecting (yes/no)?
```

```sh
## Warning: Permanently added '159.203.134.88' (ECDSA) to the list of known hosts.
## root@159.203.134.88's password:
```

3. 密码正确后，就来到了远程服务器的 Shell 。第一次进来需要改密码。
4. 通过 `log out` 命令，断开与服务器的连接。

### 7.4 Cloud Computing Basics

#### 7.4.1 Moving Files In and Out of the Cloud

1. 通过 `scp` 命令，可以在本地主机和服务器之间传递文件。

 ```sh
scp [username]@[IP address]:path/to/file/on/server path/on/my/computer
scp -r [username]@[IP address]:path/to/folder/on/server folder/on/my/computer

scp path/on/my/computer [username]@[IP address]:path/to/file/on/server 
 ```

#### 7.4.2 Talking to Other Servers

1. 通过 `curl` 程序，发送请求或信息给其他服务器。
2. 下载文件：

```sh
curl -O http://website.org/textfile.txt
```

3. 请求 API (application programming interface) ：

```sh
# Get
curl https://api.github.com/repos/seankross/the-unix-workbench/languages
curl http://httpbin.org/ip
curl http://httpbin.org/get

# 传参数
curl http://httpbin.org/get?Baltimore
curl http://httpbin.org/get?city=Baltimore
curl "http://httpbin.org/get?city=Baltimore&state=Maryland"
 ```

#### 7.4.3 Automating Tasks

1. 远程服务器总是开着机，总是连着网。所以，很适合设定一些自动任务。这可以通过 `cron` 程序办到。
2. `cron` 程序是守护进程 (daemons) ，即后台进程。可通过 `ps -A | grep "cron"` 找到。
3. 先设定默认编辑器，然后通过 `crontab -e` 命令，就会进入编辑器编辑  `cron` 表达式。
4. 表达式每一列的含义依次如下：

- Minute (m)
- Hour (h)
- Day of Month (dom)
- Month (mon)
- Day of Week (dow)
- Command to be run (command)

5. 前 5 列的取值范围如下，并且可以用 `*` 表示全选：

- Minute: 00 - 59 (A particular minute in an hour)
- Hour: 00 - 23 (0 is the midnight hour)
- Day of Month: 01 - 31 (1 is the first day of the month)
- Month: 01 - 12 (1 is January)
- Day of Week 0 - 6 (0 is Sunday)

6. 一些例子：

 ```sh
# m h dom mon dow command
00 * * * * bash /path/to/script.sh     # Runs every hour at the start of the hour
00 12 * * * bash /path/to/script.sh    # Runs every day at noon
* 12 * * * bash /path/to/script.sh     # Runs every minute between 12pm and 12:59pm
00 00 05 * * bash /path/to/script.sh   # Runs the 5th day of every month at midnight
00 00 * 07 * bash /path/to/script.sh   # Runs every day in the month of July at midnight
00 00 * * 2 bash /path/to/script.sh    # Runs every Tuesday at midnight
```

7. 此外，还可以用 `-` 和 `,` 表示多选：

```sh
# m h dom mon dow command
00-04 * * * * bash /path/to/script.sh       # Runs every minute for the first five minutes of every hour
00 00 * * 0,6 bash /path/to/script.sh       # Runs at midnight every Saturday and Sunday
00 03 01-15 * * bash /path/to/script.sh     # Runs at 3am for the first fifteen days of every month 
00,30 * * * * bash /path/to/script.sh       # Runs at the start and middle of every hour
00 00,12 * * * bash /path/to/script.sh      # Runs every day at midnight and noon
00 * 01-07 01,06 * bash /path/to/script.sh  # Runs at the start of every hour for the first seven days of the months of January and June
 ```

### 7.5 Shutting Down a Server

1. 销毁 DigitalOcean 上创建的 droplets ，避免过期后还扣钱。

## 第八章 Start Building

### 8.1 Next Steps

1. [Python](https://www.python.org/) 语言。 推荐教程 [Learn Python the Hard Way](https://learnpythonthehardway.org/book/) 和 [Python Tutor](https://pythontutor.com/)。学会之后可以用 [Flask](http://flask.pocoo.org/) 搭建 HTTP API 。
2. [R] 语言。适合数据分析、建模和可视化。推荐材料有 [R Programming for Data Science](https://leanpub.com/rprogramming) 、[Swirl](http://swirlstats.com/) 软件包和交互式学习站点 [DataCamp](https://www.datacamp.com/) 。
3. [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) 语言。