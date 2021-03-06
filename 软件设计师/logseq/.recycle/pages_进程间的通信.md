- 由于多个进程可以并发执行，故进程间必然存在资源共享和相互合作的问题。进程通信是指各个进程交换信息的过程。 _每个进程各自有不同的用户地址空间,任何一个进程的全局变量在另一个进程中都看不到。 所以进程之间要交换数据必须通过内核,在内核中开辟一块缓冲区,进程 A 把数据从用户空间拷到内核缓冲区, 进程 B 再从内核缓冲区把数据读走,内核提供的这种机制称为进程间通信。_
- 同步与互斥：同步是^^合作进程^^间的直接制约问题，互斥是^^申请临界资源进程间^^的间接制约问题。
	- 进程间的同步：
		- 多个进程可以并发执行，每个进程都以各自独立的、不可预知的速度向前推进，但是需要在某些确定点上协调相互合作进程间的工作。
		- 例如，进程A向缓冲区送数据，进程B从缓冲区取数据加工，当进程B要取数据加工时，必须是进程A完成了向缓冲区送数据的操作，否则进程B必须停下来等待进程A的操作结束。可见，进程间的同步是指进程间完成一期任务时直接发生相互作用的关系。
	- 进程间的互斥：
		- 各进程可以共享资源，但有些资源一次只能供一个进程使用，称为**临界资源**（Critical resource，CR），如打印机、公享变量和表格等。进程间的互斥是指系统中各进程互斥使用临界资源。
	- 临界区管理的原则：
		- 临界区（Critical section，CS）是进程中对临界资源实施操作的那段程序。
		- 对互斥临界区管理的4条原则如下：
		  > 1. ^^有空即进^^。当无进程处于临界区时，允许进程进入临界区，并且只能在临界区运行有限的时间。
		  > 2. ^^无空则等^^。当有一个进程在临界区时，其他欲进入临界区的进程必须等待，以保证进程互斥地访问临界资源。
		  > 3. ^^有限等待^^。对要求访问临界资源的进程，应保证进程能在有限时间进入临界区，以免陷入“饥饿”状态。
		  > 4. ^^让权等待^^。当进程不能进入自己的临界区时，应立即释放处理机，以免进程陷入忙等状态。
- 信号量机制：
	- 荷兰学者Dijkstra于1965年提出的信号量机制是一种有效的进程同步与互斥工具。主要有整型信号量（PV操作 #PV操作 ）、记录型信号量和信号量集机制。
- 高级通信原语：
	- PV操作属于低级通信方式，若用PV操作实现进程间通信，则存在如下问题：
	  > 1. 编程难度大，通信对用户不透明，即要用户利用低级通信工具实现进程间的同步与互斥。但是，PV操作使用不当容易引起死锁。
	  > 2. 效率低，生产者每次只能向缓冲区放一个消息，消费者只能从缓冲区取一个消息。
	- 为了提高信号通信的效率，传递大量数据，减轻程序编制的复杂度，系统引入了高级通信方式。高级通信方式主要分为共享存储模式 #共享存储模式 、消息传递模式 #消息传递模式 和管道通信 #管道通信 。
	  ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9ukNh6yrtBNpRCUh9_uRDfEv_kwUVIqefNUDgwySckrK_NpdZQjEBPYeKmuMVREfurhd-oPy7BXab8mi_NBNpPE1bY29T3Aj1mg0K0)
	- 管道通信：
		- 管道是一种半双工的通信方式，数据只能单向流动。管道通信分为命名管道和匿名管道。
		- 匿名只能在具有亲缘关系的进程间使用。进程的亲缘关系通常是指父子进程关系。 命名管道则可以在任何关系的进程之间通讯。 命名管道虽然可以在任意关系之间通信， 但是它会长期存在于系统之中，因此使用不当会容易对系统造成负担。
		- 父进程创建管道，得到两个⽂件描述符指向管道的两端 父进程 fork 出子进程，⼦进程也有两个⽂件描述符指向同⼀管道。 ⽗进程可以往管道⾥写,⼦进程可以从管道⾥读,管道是⽤环形队列实现的,数据从写端流⼊从读端流出,这样就实现了进程间通信。
	- 信号及信号量通信：
		- 信号 ( sinal ) ： 信号是一种比较复杂的通信方式，用于通知接收进程某个事件已经发生。
		- 信号量( semophore ) ： 信号量是一个计数器，可以用来控制`多个进程对共享资源的访问`。 它常作为一种`锁机制`，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内不同线程之间的同步手段。
		- 同样的，信号量是有限的，不能无限使用。
		- 消息队列( message queue ) ： 消息队列是由消息的链表，存放在内核中并由消息队列标识符标识。 消息队列克服了信号传递信息少、管道只能承载无格式字节流以及缓冲区大小受限等缺点。
	- 共享内存：
		- 共享内存( shared memory ) ：共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问。 共享内存是最快的 IPC 方式，它是针对其他进程间通信方式运行效率低而专门设计的。它往往与其他通信机制，如信号量配合使用来实现进程间的同步和通信。
	- socket：
		- 套接字( socket ) ： 套接口也是一种进程间通信机制，与其他通信机制不同的是，它`可用于不同机器间`的进程通信。
	- node进程通信的方式：
	  1. 通过stdin/stdout传递：最直接的方式，适用于能够拿到“子”进程句柄的场景
	  2. Node原生IPC支持：node封装了IPC的具体实现，暴露了exec, fork等方法，可以用于父子进程通讯
	  3. 通过sockets：最通用的方式，可以跨机器通讯
	  4. 借助message queue：最强大的方式，但是使用起来考虑的问题是最多的