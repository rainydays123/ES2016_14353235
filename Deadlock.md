#Lab 4 死锁
-------
###一、死锁产生的条件
######四个必要条件：
- 互斥条件：一个资源每次只能被一个进程使用。
- 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
- 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
- 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

###二、本次试验测试用代码
######Deadlock.java

	class Deadlock implements Runnable{
	A a=new A();
	B b=new B();

	Deadlock(){
		Thread t=new Thread(this);
		int count=2000;

		t.start();
		while(count-->0);
		a.methodA(b);
	}

	public void run(){
		b.methodB(a);
	}
	public static void main(String arg[]){
		new Deadlock();
	} 
	}

	class A{
	synchronized void methodA(B b){
		b.last();
	}

	synchronized void last(){
		System.out.println("Inside A.last()");
	}
	}

	class B{
	synchronized void methodB(A a){
		a.last();
	}

	synchronized void last(){
		System.out.println("Inside B.last()");
	}
	}

######Deadlock.bat(win)
>cd /d %~dp0
>
>@echo off
>
>:start
>
>set /a var+=1
>
>echo %var%
>
>java Deadlock
>
>if %var% leq 1000 GOTO start
>
>pause

###三、测试结果和分析
![](http://i.imgur.com/Et5A6Fb.png)
![](http://i.imgur.com/635TTYp.png)
######出现的结果有很大的随机性，可以看出两次停止的执行次数都不一样，一个36一个223，实验中也有跑了1000次最终都不出结果的时候。
######原因分析：代码中

	Thread t=new Thread(this);
	int count=40000;
	t.start();

######这几句是将deadlock弄成了一个t线程在跑，这样就形成了两个并行线程，通过start函数将运行这个线程：
	
	public void run(){
		b.methodB(a);
	}

######synchronized方法是只能被一个对象使用的。这句话的使用methodB时锁定B对象，然后又在其中调用A对象并将之锁定，函数的调用是有时间差的。

	while(count-->0);
		a.methodA(b);

######休眠一段时间让a对象去执行类似操作，不过是先将自己锁起来再尝试去锁B。可以想象，在.bat文件多次迭代的过程中这两个并行线程若同时发生，都是锁定了自己然后尝试去锁定对方..死锁就发生了。
######当然函数调用的时间还有电脑运行状况等对执行效果影响很大，所以带有一定的随机性质。



