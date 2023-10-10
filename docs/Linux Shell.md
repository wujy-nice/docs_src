# shell



变量：

- 局部变量，仅本 shell 可用变量
- 环境变量
- shell 变量，shell 程序自己设定的变量

变量使用：

- value="val"，=两旁不可有空格
- 变量前加 local，只能在该函数中使用
- $value 或 ${value} 获取变量值
- 只读变量：value="value" -> readonly value
- unset value 删除 value 变量

字符串：

- 单引号 'str'，原样输出 

- 双引号 "str"，可包括变量

- 获取字符串长度：${#str}

  ```sh
  str='str'
  echo ${#str}
  ```

  输出3

- 截取

  使用范围 n:m，标识从下标n以后的m个字符，如果从头开始截取 可省略 ::m

  ```
  str="is a string"
  echo ${str:2:4}	# 输出'a string'
  echo ${str::4} # 输出'is a'
  ```

数组：

- 只支持一维数组

- 定义方式

  - arr1=(e1 e2 e3)
  - arr2[2]="e2"

- 取值，使用[]加下标的方式

- 元素个数：与字符串类似

  - ${#arr[@]}
  - ${#arr}

- 元素的长度

  ${#arr[1]}



传递参数

- $0 固定标识文件名
- $1..$n 指传入的第n个参数
- $# 传递的参数个数
- $@ 传递的参数列表
- $* 传递的参数，视为整体



算数运算：

- `+ - * \`，注意`*`需要加转义符才可以进行惩罚运算



关系运算：

- -eq
- -ne
- -gt
- -lt
- -ge
- -le



字符串运算：

- =
- !=
- -z 长度为0是true，-n相反
- =~ 是否包含某个字符串



布尔：

- !
- -o 或
- -a 与

逻辑运算：

- &&
- ||

文件运算（常用）：

- -b 块设备
- -c 字符设备
- -d 目录
- -f 普通文件
- -r -w -x 是否可读、写、执行
- -e 是否存在 ,存在 true
- -s 是否为空文件，非空true

命令：

- 使用反引号包括 \`ls /etc\`
- $() 包括，如 $(ls /etc)

可以混合使用，如

````sh
path=$(cd 'dirname $0';pwd)
````

切换到本文件所在目录，然后pwd获取路径，赋值给path



逻辑判断：

- [] 数字和字符串都可以，但容易出现逻辑错误

- [[]] 用于字符串验证 需要加空格 

  ```
  [[ $str1 != 1 && $str1 != 2 ]]
  ```

- (()) 用于数字验证 需要空格

  ```
  (( $n1 -eq 2 -a $n2 -ne 2 ))
  ```



输出：

- echo 自动换行
- printf 格式化输出，不会自动换行，与 c 类似



流程控制：

- if else

  ```sh
  if condition then cmd1..cmdn fi
  ```

  流程不可为空，即一定要有执行语句

- for

  ```
  for var in item1..itemn do cmd1..cmdn done
  ```

- while

  ```sh
  while condition do cmd1..cmdn done
  ```

  ```sh
  while:do cmd done
  ```

- until

  与 while 相反，意思是直到为真才停止

  ```sh
  until condition do cmd done
  ```

- case

  ```
  case val in case1) cmd;;  esac
  ```

  每个匹配用右括号结尾，用;;表示break

`$?` 最后一次执行的命令的结果，非 0 代表错误

`:-` 缺省值

`:+ ` 替换



获取输入值：read

-p 说明

-t 等待时间，秒

```sh
read -t 10 -p "输入选项：" NUM
echo ${NUM}
```



获取文件名：basename

只保留最后一个 `/` 后面的部分，指定后缀时，会将后缀忽略

```
basename /path/main.c
main.c

basename /path/main.c .c
main
```



获取路径名：dirname

获取指定路径字符串的路径前缀

```
dirname /usr/bin/ 
/usr

dirname /usr/bin/a
/usr/bin

dirname a
.
```





文本处理：sed

常用参数：

​	-r 使用正则

​	-i 直接对内容修改，不加此参数是预览修改

​	-n 只输出修改的行，不加会输出所有行

​	-f 存有修改指令的文件

编辑命令：

​	a 向匹配行之后追加内容

​	i 向匹配行之前追加内容

​	d 删除匹配内容

​	!d 删除匹配内容之外的内容

​	c 更改匹配行内容

​	n 跳到下一行

​	s 替换匹配内容

​	p 打印匹配的内容

​	= 打印匹配行的行号

​	/str/ 匹配str字符串

​	$ 最后一行