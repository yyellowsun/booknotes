OTP的理解：

OTP：open telephone platform

对于



#### 不变性的理解：

在elixir，所有的数据结构是不变的，所有的修改对原有的数据是不会改变的，只会返回一个修改之后的复制。要保存修改后的复制，就需要重新绑定

异步调用和同步调用

异步调用：向服务器发送命令，命令对服务器的状态造成了副作用



&1 匿名函数的语法糖

#### 模式匹配：
=是匹配操作符，而不是赋值操作符
1、只有当=的左边是变量名的时候，才进行变量赋值。
2、Destructuring:在绑定      变量的集合到对应的值的集合 （set to set)的情况下，
可以绑定 单个变量到单个值(one to one )

3、《》	用来表示elixir的二进制文件,::用来指定一个位串的大小，比如说1::2，指定，用两个bit去表示1

常见的用法：::binary-size(30)，指定用30个bytes的内存，::binary，用8*n个bit的内存

binary，是用8*n个bit的内存实现的位串，位串不一定是binary，但binary一定是位串

#### Function:
1、同名函数在定义时需要group
2、函数定义的时候出现的次序很重要

3、参数列表里面出现 （result  \\\ []）表示result的默认值为[]

#### String（双括号括起来）

char list是用单引号括起来的

1、字符串是binary。binary是一串字节序列。

二进制连接符<>     “hello”<> 《0》

2、单引号括起来的是char list，双引号括起来的是string

#### Guards:
when is_type(arguments) do 提供检测arguments是否是某种类型

注意

#### Atoms:
原子类型：其值等于其名字的常量。boolean类型也是原子类型。通常true,false,nil前面的:可以省略，其他原子类型则要保留
#### Lists:
List是递归定义的：[1,2,3] == [1 | [ 2 | [ 3 | [ ] ] ] 

连接和删除操作：

cons 操作符 | :用来解构list

a ++ b,连接两个list,
a -- b，删除a中b中的元素，操作不会修改原有的list，而是返回一个新的list
单引号括住的是charlist，双引号括住的是string。

#### Tuple
elem/2, tuple,index :返回tuple里面的元素
 elem({404, "http://www.php-is-awesome.org"}, 1)  返回"http://www.php-is-awesome.org"

put_elem/3 tuple,index,element    :  用elemet替换tuple[index]原来的元素，返回一个新的tuple。
put_elem({404, “http://www.php-is-awesome.org”}, 0, 503)  返回{503,"“http://www.php-is-awesome.org”}

list的内存管理相当于链表，tuple相当于数组。
使用tuple从一个函数中返回一些额外的信息。{200, "http://www.elixir-lang.org"}
Elixi 引导我们做正确的事情。size用于已经事先计算好值的情况去计数，length用于线性操作的计数。
任何类型都可以比较：number < atom < reference < function < port < pid < tuple < map < list < bitstring

#### 对于spawn,receive,send的理解

spawn(module, fun, args),创建一个进程，调用module.fun传入的参数为args,args一般用[]表示，返回创建的进程的pid

receive，一般用在module.fun里面用来对于接收到的消息进行模式匹配。

receive do

after 

end

after是可选字段，可选值为

1、:infinity，表示一直进程一直等待，直到有模式匹配通过

2、0，一旦不匹配就显示超时。

3、小于0xffffffff的正整数，以毫秒为单位



send(dest,message)

向dest，发送message，返回值为message。一般会在message里面包含发送者的pidl例如send(dest,{sender_pid,message})这样用

dest可选值为

1、pid

2、局部端口

3、局部已经注册的名字

4、{registered_name,node}在另一个node注册的名字