- 图（diagram）是一组元素的图形表示，大多数情况下把图画成顶点（代表事物）和弧（代表关系）的连通图。为了对系统进行可视化，可以从不同的角度画图，这样图是对系统的投影。
- UML2.0提供了13种图，分别是类图、对象图、用例图、序列图、通信图、状态图、活动图、构件图、部署图、组合结构图、包图、交互概览图和时序图。
- 类图：
	- 类图（class diagram）展现了一组对象、接口、协作和它们之间的关系。在面向对象系统的建模中所建立的最常见的图就是类图。类图给出系统的静态设计视图。包含主动类的类图给出了系统的静态进程视图。
	- 类图中通常包括下述内容（如图10-17所示）。
	  ![image-20211016114218449](https://img.mhugh.net/typora/image-20211016114218449.png)
	  1. 类。
	  2. 接口
	  3. 协作。
	  4. 依赖、泛化和关联关系。
	- 类图中也可以包含注解和约束。类图还可以含有包或子系统，二者都用于把模型元素聚集成更大的组块。
	- 类图用于对系统的静态设计视图建模。这种视图主要支持系统的的功能需求，即系统要提供给最终用户的服务。当对系统的静态设计视图建模时，通常以下述三种方式之一使用类图。
		- ==对系统的词汇建模==。对系统的词汇建模涉及到做出这样的决定；哪些抽象是考虑中的系统的一部分，哪些抽象处于系统边界之外。用类图详细描述这些抽象和它们的职责。
		- ==对简单的协作建模==。协作是一些共同工作的类、接口和其他元素的群体，该群体提供的一些合作行为强于所有这些元素的行为之和。例如，当对分布式系统的事务语义建模时，不能仅仅盯着一个单独的类来推断要发生什么，而要有相互协作的一组类来实现这些语义。用类图对这组类以及它们之间的关系进行可视化和详述。
		- ==对逻辑数据库模式建模==。将模式看作为数据库的概念设计的蓝图。在很多领域中，要在关系数据库或面向对象数据库中存储永久信息，可以用类图对这些数据库的模式建模。
- 对象图：
	- 对象图（object diagram）展现了一组对象以及它们之间的关系。对象图描述了在类图所建立的事物的实例的静态快照。对象图一般包括对象和链。
	- 和类图一样，对象图给出系统的静态设计视图或静态进程视图，但它们是从真实的或原型案例的角度建立的。这种视图主要支持系统的功能需求，即系统应该提供给最终用户的服务。利用对象图可以对静态数据结构建模。
	- 当对系统的静态设计视图或静态进程视图建模时，主要是使用对象图对对象结构进行建模。对对象结构建模涉及到在给定时刻抓取系统中对象的快照。对象图表示了交互图表示的动态场景的一个静态画面。可以使用对象图可视化、详述、构造和文档化系统中存在的实例以及它们之间的相互关系。
- 用例图：
	- 用例图（use case diagram）展现了一组用例、参与者（Actor）以及它们之间的关系。
	- 用例图通常包括如下内容（如图10-18所示）。
	  ![image-20211017075905776](https://img.mhugh.net/typora/image-20211017075905776.png)
	  1. 用例。
	  2. 参与者。
	  3. 扩展关系、包含关系。
	- 用例图用于对系统的静态用例视图进行建模。这个视图主要支持系统的行为，即该系统在它的周边环境的语境中所提供的外部可见服务。
	- 当对系统的静态用例视图建模时，可以用下列两种方式来使用用例图。
		- 对系统的语境建模。对一个系统的语境建模，包括围绕整个系统画一条线，并声明有哪些参与者位于系统之外并与系统进行交互。在这里，用例图说明了参与者以及他们所扮演的角色的含义。
		- 对系统的需求建模。对一个系统的需求进行建模，包括说明这个系统应该做什么（从系统外部的一个视点出发），而不考虑系统应该怎样做。在这里，用例图说明了系统想要的行为。通过这种方式，用例图使我们能够把整个系统看作一个黑盒子。可以观察到系统外部有什么，系统怎样与哪些外部事物相互作用，但却看不到系统内部是如何工作的。
- 交互图：
	- 序列图、通信图、交互概览图和时序图均被称为交互图，它们用于对系统的动态方面进行建模。一张交互图显示的是一个交互，由一组对象和它们之间的关系组成，包含它们之间可能传递的消息。顺序图是强调消息时间顺序的交互图；通信图则是强调接收和发送消息的对象的结构组织的交互图。
	- 交互图用于对一个系统的动态方面建模。在多数情况下，它包括对类、接口、构件和节点的具体的或原型化的实例以及它们之间传递的消息进行建模，所有这些都位于一个表达行为的脚本的语境中。交互图可以单独使用，来可视化、详述、构造和文档化一个特定的对象群体的动态方面，也可以用来对一个用例的特定的控制流进行建模。
	- 交互图一般包含对象、链和消息。
	- **序列图**：
		- 序列图（sequence diagram）是场景（scenario）的图形化表示，描述了以时间顺序组织的对象之间的交互活动。如图10-19所示，形成序列图时，首先把参加交互的对象放在图的上方，沿x轴方向排列。通常把发起交互的对象放在左边，下级对象依次放在右边。然后，把这些对象发送和接收的消息沿Y轴方向按时间顺序从上到下放置。这样，就提供了控制流随时间推移的清晰的可视化轨迹。
		- 序列图有两个不同于通信图的特征。
			- 序列图有**对象生命线**。对象生命线是一条垂直的虚线，表示一个对象在一段时间内存在。在交互图中出现的大多数对象存在于整个交互过程中，所以这些对象全都排列在图的顶部，其生命线从图的顶部画到图的底部。但对象也可以在交互过程中创建，它们的生命线从接收到构造型为create的消息时开始。对象也可以在交互过程中撤销，它们的生命线在接收到构造型为destroy的消息时结束（并且给出一个大X的标记表明生命的结束）。
			  ![image-20211017082447754](https://img.mhugh.net/typora/image-20211017082447754.png)
			- 序列图有**控制焦点**。控制焦点是一个瘦高的矩形，表示一个对象执行一个动作所经历的时间段，既可以是直接执行，也可以是通过下级过程执行。矩形的顶部表示动作的开始，底部表示动作的结束（可以由一个返回消息来标记）。还可以通过将另一个控制焦点放在它的父控制焦点的右边来显示（由循环、自身操作调用或从另一个对象的回调所引起的）控制焦点的嵌套（其嵌套深度可以任意）。如果想特别精确地表示控制焦点在哪里，也可以在对象的方法被实际执行（并且控制还没传给另一个对象）期间，将那段矩形区域阴影化。
	- **通信图**：
		- 通信图（communication diagram）强调收发消息的对象的结构组织，在早期的版本中也被称作协作图。通信图强调参加交互的对象的组织。产生一张通信图，首先要将参加交互的对象作为图的顶点，然后把连接这些对象的链表示为图的弧，最后用对象发送和接收的消息来修饰这些链。这就提供了在协作对象的结构组织的语境中观察控制流的一个清晰的可视化轨迹。
		- 通信图有两个不同于序列图的特性。
			- 通信图有**路径**。为了指出一个对象如何与另一个对象链接，可以在链的末端附上一个路径构造型（如构造型《local》，表示指定对象对发送者而言是局部的）。通常只需要显式地表示以下几种链的路径：local（局部）、parameter（参数）、global（全局）以及self（自身），但不必表示association（关联）。
			- 通信图有**顺序号**。为表示一个消息的时间顺序，可以给消息加一个数字前缀（从1号消息开始），在控制流中，每个新消息的顺序号单调增加（如2，3等）。为了显示嵌套，可使用带小数点的号码（1表示第一个消息；1.1表示嵌套在消息1中的第一个消息，1.2表示嵌套在消息1中的第二个消息，等等）。嵌套可为任意深度。还要注意的是，沿同一个链可以显示许多消息（可能发自不同的方向），并且每个消息都有唯一的一个顺序号。
	- 序列图和通信图是同构的，它们之间可以相互转换。
	- **交互概览图**：
		- 交互概览图是UML2.0新增的交互图之一，它描述交互（特别是关注控制流），但是抽象掉了消息和生命线。它使用活动图的表示法。纯粹的交互概览图中所有的活动都是交互发生。另一种新增的、特别适合实时和嵌入式系统建模的交互图称为时序图，时序图关注沿着线性时间轴、生命线内部和生命线之间的条件改变。它描述对象状态随着时间改变的情况，很像示波器，适合分析周期和非周期性任务。
		- 交互概览图（Interaction Overview Diagram）是UML 2.0新增的交互图之一，它是活动图的变体，描述业务过程中的控制流概览，软件过程中的详细逻辑概览，以及将多个图进行连接，抽象掉了消息和生命线。它使用活动图的表示法，如图7-16所示。
	- **计时图**：
		- 计时图（Timing Diagram）是另一种新增的、特别适合实时和嵌入式系统建模的交互图，关注沿着线性时间轴、生命线内部和生命线之间的条件改变。它描述对象状态随着时间改变的情况，很像示波器，如图7-17所示，适合分析周期和非周期性任务。
- 状态图：
	- 状态图（state diagram）展现了一个状态机，它由状态、转换、事件和活动组成。状态图关注系统的动态视图，它对于接口、类和协作的行为建模尤为重要，强调对象行为的事件顺序。
	- 状态图通常包括简单状态和组合状态、转换（事件和动作）。如图10-20所示。
	  ![image-20211017085421374](https://img.mhugh.net/typora/image-20211017085421374.png)
	-
	- 可以用状态图对系统的动态方面建模。这些动态方面可以包括出现在系统体系结构的任何视图中的任何一种对象的按事件排序的行为，这些对象包括类（各主动类）、接口、构件和节点。
	- 当对系统、类或用例的动态方面建模时，通常是对反应型对象建模。
	- 一个反应型或事件驱动的对象是这样一个对象，其行为通常是由对来自语境外部的事件做出反应来刻画的。反应型对象在接收到一个事件之前通常处于空闲状态。当它接收到一个事件时，它的反应常常依赖于以前的事件。在这个对象对事件做出反应后，它就又变成闲状态，等待下一个事件。对于这种对象，将着眼于对象的稳定状态、能够触发从状态到状态的转换的事件，以及当每个状态改变时所发生的动作。
- 活动图：
	- 活动图（activity diagram）是一种特殊的状态图，它展现了在系统内从一个活动到另一个活动的流程。活动图专注于系统的动态视图，它对于系统的功能建模特别重要，并强调对象间的控制流程。
	- 活动图一般包括活动状态和动作状态、转换和对象。
	- 用活动图建模的控制流中，会发生一些事情。可能要对一个设置属性值或返回一些值的表达式求值；也可能要调用对象上的操作，发送一个消息给对象，甚至创建或销毁对象，这些可执行的原子计算被称为动作状态，因为它们是该系统的状态，每个原子计算都代表一个动作的执行。动作状态不能被分解。动作状态是原子的，也就是说事件可以发生，但动作状态的工作不能被中断。最后，动作状态的工作所占用的执行时间一般被看作是可忽略的。
	- 活动状态能够进一步被分解，它们的活动由其他的活动图表示。活动状态不是原子的，它们可以被中断。并且，一般来说，还要考虑到它需要花费一段时间来完成。可以把一个动作状态看作一个活动状态的特例。类似地，可以把一个活动状态看作一个组合，它的控制流由其他的活动状态和动作状态组成。
	- 活动图可以表示分支和汇合。
	- 当对一个系统的动态方面建模时，通常有两种使用活动图的方式。
		- 对**工作流**建模。此时所关注的是与系统进行协作的参与者所观察到的活动。工作流常常位于软件系统的边缘，用于可视化、详述、构造和文档化开发系统所涉及的业务过程。在活动图的这种用法中，对对象流的建模是特别重要的。
		- 对**操作**建模。此时是把活动图作为流程图使用，对一个计算的细节部分建模。在活动图的这种用法中，对分文、分叉和汇合状态的建模是特别重要的。用于这种方式的活动图语境包括该操作的参数和它的局部对象。
- 构件图：构件图（component diagram）展现了一组构件之间的组织和依赖。构件图专注于系统的静态实现视图。它与类图相关，通常把构件映射为一个或多个类、接口或协作。
- 组合结构图：组合结构图（Composite Structure Diagram）用于描述一个分类器（如类、构件或用例）的内部结构，分类器与系统中其他组成部分之间的交互端口，展示一组相互协作的实例如何完成特定的任务，描述设计、架构模式或策略。组合结构图的内部结构和协作使用图分别如图7-21和图7-22所示。
- 部署图：部署图（deployment diagram）展现了运行处理节点以及其中构件的配置。部署图给出了体系结构的静态实施视图。它与构件图相关，通常一个节点包含一个或多个构件。
- 包图：包图（Package Diagram）是用于把模型本身组织成层次结构的通用机制，不能执行，展现由模型本身分解而成的组织单元以及其间的依赖关系。