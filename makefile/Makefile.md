# [Makefile教程](https://www.ruanyifeng.com/blog/2015/02/make.html)
https://www.ruanyifeng.com/blog/2015/02/make.html
https://www.zhaixue.cc/makefile/makefile-if-function.html

## Makefile介绍
Makefile可以让工程完成自动化变异，解放程序员，提高生产力。要使用Makefile自动化编译工程，需要一个Makefile文件，并编写编译规则。

### Makefile的规则
Makefile文件由一系列规则构成，每条规则的形式如下：
```Makefile
<target>: <prerequisites>
[tab] <commands>
```
- target：叫做目标
- prerequisites：前置条件
- tab: 标签
- commands：命令
含义如下：构建目标的前置条件是什么，如何构建。但是构建目标的前置条件和如何构建二者至少有一个存在。即：
- 第一种：
	```Makefile
	<target>: <prerequisites>
		<commands>
	```
- 第二种：
	```Makefile
	<target>: 
	<tab>	<commands>
	```
- 第三种：
	```Makefile
	<target>: <prerequisites>
	<tab>	<commands>
	```

#### target 目标
一个目标构成一条规则。target可以是一个文件名，多个文件名，或者操作名（伪目标：phony target），其中多个文件名时用逗号隔开。
**执行make时，如果target对于的名称文件已经存在了，则当前执行不会生效，make会认为文件已存在无需执行制作。**示例：
```Makefile
clean:
	echo "clean"
```

```shell
make clean
```
执行shell命令，如果当前目录存在一个叫clean的文件，则 make clean 不会执行，否则则会执行并输出：clean
要每次都执行，则需要强调clean是伪命令：
```Makefile
.PHONY: clean
clean:
	echo "clean"
```
.PHONY标记冒号后面的命令为伪命令，执行时不检查文件是否存在

#### .PHONY 伪命令
[更多伪命令](https://www.gnu.org/software/make/manual/html_node/Special-Targets.html#Special-Targets)
.PHONY标记其冒号:后面的命令为伪命令，执行时无需检查文件是否存在，始终执行该命令

#### prerequisites 前置条件
前置条件通常是一组文件名，用空格隔开。其作用是要执行当前规则的命令，需要首先检查前置条件是否满足，只有满足时才会执行命令，不满足是退出执行。示例：
```Makefile
clean: a.txt b.txt c.txt
	echo "clean"
```
- 这条命令如果 a.txt ，b.txt ，c.txt 文件都不存在，则执行命令make clean 会报错：make: *** No rule to make target 'a.txt', needed by 'source'.  Stop.
- 此时需要增加生成 a.txt b.txt c.txt的规则，如下示例：
```Makefile
create:
a.txt:
	echo "create" > a.txt
b.txt:
	echo "create" > b.txt
c.txt:
	echo "create" > c.txt

source: a.txt b.txt c.txt
	echo "abc"
```
此时执行 make source 命令会首先执行前置条件生成 a.txt,b.txt,c.txt文件，在执行source的命令：echo "abc"，最终输出结果：
```shell
$ make source
echo "create" > a.txt
echo "create" > b.txt
echo "create" > c.txt
echo "abc"
abc
```
- 任意一个有任何变动，包括文件的最后更新时间戳（内容不变）仍然会执行，如果两个文件都没有任何变更，那么这条命令就会输出abc。

#### tab 标签
tag可有可无，不存在时，前置条件prerequisites必须存在。

#### commands 命令
命令commands表示如何更新目标文件，由一行或多行shell命令组成。它是构建目标的具体指令，结果通常是生成目标文件。**每行命令之前必须有一个tab键**，可以用内置变量 **.RECIPEPRERIX** 声明。示例：
```makefile
.RECIPEPREFIX = >
all:
> echo hello world
> echo 134
```
每一行命令在一个单独的shell中执行，不同行之间的shell没有继承关系，第二行中无法使用其他行的变量。解决办法，写在同一行，不同shell之间用 **;** 分号隔开，或者使用 **\\** 换行符， 或加上 **.ONESHELL:** 命令。综上：
- **;** 分号隔开
- **\\** 换行符换行
- **.ONESHELL:** 命令

## Makefile语法
### 注释
```makefile
# 这是注释
result.txt: source.txt
    # 注释
    cp source.txt result.txt # 注释
```

### 回声 echoing
makefile会先打印每条命令，然后再执行就叫回声echoing。

#### 关闭回声
在命令前面加上@符号，可以关闭回声。示例：
```makefile
test:
    @# 这是测试
    @echo todo
```

### 通配符
- *
- ?
- [...]

### 模式匹配
- %
示例：
```makefile
%.o: %.c
类似
a.o: a.c
b.o: b.c
```


### 变量和赋值
使用等号=自定义变量。变量需要放在 $( ) 之中使用
示例：
```makefile
txt = hello
test:
    echo $(txt)
```

#### 赋值运算符
- =
在执行时扩展
- :=
在定义时扩展
- ?=
只有在该变量为空时才设置值
- +=
将值追加到变量的尾部

#### 内置变量
- $(CC) 指向当前使用的编译器
- $(MAKE) 指向当前使用的Make工具

#### 自动变量
- $@ 指代当前构建的目标，如make foo，则$@指代 foo
- $< 指代第一个前置条件，如规则为 t: a b ，则$<指代 a
- $? 指代比目标更新的所有前置条件，之间以空格分隔。如规则为：t: p1 p2

#### 判断和循环
Makefile使用Bash语法，完成判断和循环，其中需要特别注意：***ifeq不能缩减，且后面需要空格，即需要贴墙写***
- 判断model是否为空字符
```bash
.PHONY: test
test:
ifeq ($(model),)
	echo "没有输入"
else
	echo $(model)
endif
```



- 循环
```Makefile
LIST= 1 2 3
all:
	for i in $(LIST); do \
		echo $$i; \
	done
```
或
```Makefile
all:
	for i in 1 2 3; do \
		echo $i; \
	done
```

#### [函数](http://www.gnu.org/software/make/manual/html_node/Functions.html)
使用函数格式如下：
```Makefile
$(functionname arguments)
或
${functionname arguments}
```

##### shell 函数
shell函数用来执行shell命令
```Makefile
sr := $(shell echo xxx)
```

##### wildcard 函数
wildcard用来在Makefile中替换Bash的通配符
```Makefile
sr := $(wildcard src/*.txt)
```

##### subst 函数
用于文本替换，格式如下：$(subst from, to, text)，示例：
```Makefile
$(subst ee,EE,feet on the street)
```
输出：fEEt on the strEEt

下面是一个稍微复杂的例子。
```Makefile
comma:= ,
empty:=
# space变量用两个空变量作为标识符，当中是一个空格
space:= $(empty) $(empty)
foo:= a b c
bar:= $(subst $(space),$(comma),$(foo))
```
输出：bar is now `a,b,c'.

##### patsubst 函数
用于模式匹配替换，格式如下：$(patsubst pattern,replacement,text)
下面的例子将文件名"x.c.c bar.c"，替换成"x.c.o bar.o"。
```Makefile
$(patsubst %.c,%.o,x.c.c bar.c)
```

##### 替换后缀名
替换后缀名函数的写法是：变量名 + 冒号 + 后缀名替换规则。它实际上patsubst函数的一种简写形式。
```Makefile
min: $(OUTPUT:.js=.min.js)
```
上面代码的意思是，将变量OUTPUT中的后缀名 .js 全部替换成 .min.js 。

