- 序列图是以图形化的方式描述了在一个用例或操作的执行过程中对象如何通过消息互相交互，说明了消息在对象之间被发送和接收以及发送的顺序。根据分析设计的迭代演化需求，最初可以绘制系统序列图。系统序列图是一副描述角色和系统在用例场景下交互的图形，有助于确定进入和退出系统的高层信息。
- 以审稿人获取已分配给自己的稿件的执行序列，浏览会议主页，看到主页后，从导航条浏览已分配给自己的稿件，可循环进行选择，创建已分配稿件并显示给审阅人。得出图12-19所示的审稿人获取分配给自己的稿件列表。
  ![image-20211021065942845](https://img.mhugh.net/typora/image-20211021065942845.png)
- 建模序列图应该遵循如下指导原则。
	- 确定顺序图的范围，描述这个用例场景或一个步骤。
	- 绘制参与者和接口类，如果范围包括这些内容的话。
	- 沿左手边列出用例步骤。
	- 对控制器类及必须在顺序中协作的每个实体类，基于它拥有的属性或已经分配给它的行为绘制框。
	- 为持续类和系统类绘制框。
	- 绘制所需消息，并把每条消息指到将实现响应消息的责任的类上。
	- 添加活动条指示每个对象实例的生命期。
	- 为清晰起见，添加所需的返回消息。
	- 如果需要，为循环、可选步骤和替代步骤等添加框架。