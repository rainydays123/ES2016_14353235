#DOL实例分析&编程
----------------
###一、实验说明
#####example文件理解
##########文件夹中有generator、square、consumer三种.c文件，依次执行生产者、处理者和消费者三种角色。

- example1
 squre.c 中的函数
	>int square_fire(DOLProcess *p) {
    >float i;
	>
    >if (p->local->index < p->local->len) {
    >    DOL_read((void*)PORT_IN, &i, sizeof(float), p);
    >    i = i*i;
    >    DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
    >    p->local->index++;
    >}
	>
    >if (p->local->index >= p->local->len) {
    >    DOL_detach(p);
    >    return -1;
    >}
	>
    >return 0;
	>}

其中有i=i*i的平方处理。
终端运行命令
>ant -f runexample.xml -Dnumber=1”

得到example1整体的运行结果，如下：

![](http://a4.qpic.cn/psb?/V13kR9XZ3oLApq/lQlFFls5h7fQcCZxxoJxBoCeSZnjJdCYZwy0OzI3lK8!/m/dHcBAAAAAAAAnull&bo=uAGdAQAAAAADBwc!&rf=photolist&t=5)

可见消费者产生的0~19的数都被处理者做了平方处理，最后被消费者输出。


- example2 

同上，squre中的函数

	>int square_fire(DOLProcess *p) {
    >float i;
	>
    >if (p->local->index < p->local->len) {
    >    DOL_read((void*)PORT_IN, &i, sizeof(float), p);
    >    i = i*i;
    >    DOL_write((void*)PORT_OUT, &i, sizeof(float), p);
    >    p->local->index++;
    >}
	>
    >if (p->local->index >= p->local->len) {
    >    DOL_detach(p);
    >    return -1;
    >}
	>
    >return 0;
	>}
也是平方操作，但是xml文件的接口配置中，利用iteration迭代器生成了3个squre和3+1个连接器，其中square迭代代码：
>iterator variable="i" range="N"
>process name="square"
>append function="i"
>port type="input" name="0"
>port type="output" name="1"
>source type="c" location="square.c"
>/process
>/iterator

dot图：

![](http://a2.qpic.cn/psb?/V13kR9XZ3oLApq/NXbEx4TYlM.T0YB*JRZuwXW70uZxrEeFUqdt.vaf54U!/m/dAkBAAAAAAAAnull&bo=EgWeAAAAAAADB6s!&rf=photolist&t=5)

###二、实验任务
#####1.修改example1，使之由输出平方数变为输出立方数
##########做法：修改处理者函数，对i的平方处理变为i=i×i×i；
#####2.修改example2，使square个数变为2个
##########做法：修改xml文件中对于i的定义：variable value="3" 变为 variable value="2"
###二、实验结果
#####1.example1的立方数
![](http://a2.qpic.cn/psb?/V13kR9XZ3oLApq/upnw6DKqsdj9taKj1uMl3GfE2aft82RAXyxbdIfzebU!/m/dAkBAAAAAAAAnull&bo=IANYAgAAAAADB1s!&rf=photolist&t=5)
############可以看出所有的输出变为立方了
#####2.修改example2，使square个数变为2个
![](http://a4.qpic.cn/psb?/V13kR9XZ3oLApq/oWoy4SH8PFdXNfrbsQi1p4eEw1MGRuhEcZ3WXe*ElzY!/m/dHcBAAAAAAAAnull&bo=IANYAgAAAAADB1s!&rf=photolist&t=5)

example2修改后的dot图：

![](http://a3.qpic.cn/psb?/V13kR9XZ3oLApq/rZ2ftJoPsCHSwhC5aZ5dTslV8czfuKwWrss55nxvaaA!/m/dAoBAAAAAAAAnull&bo=AQL7AQAAAAADB9s!&rf=photolist&t=5)