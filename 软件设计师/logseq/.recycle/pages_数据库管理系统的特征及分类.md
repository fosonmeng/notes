- DBMS的特征：通过DBMS来管理数据具有如下特点：
	- ==数据结构化且统一管理==。数据库中的数据由DBMS统一管理。由于数据库系统采用复杂的数据模型表示数据结构，数据模型不仅描述数据本身的特点，还描述数据之间的联系。数据不再面向某个应用，而是面向整个应用系统。数据易维护、易扩展，数据冗余明显减少，真正实现了数据的共享。
	- ==有较高的数据独立性==。数据的独立性是指数据与程序独立，将数据的定义从程序中分离出去，由DBMS负责数据的存储，应用程序关心的只是数据的逻辑结构，无须了解数据在磁盘上的数据库中的存储形式，从而简化应用程序，大大减少应用程序编制的工作量。数据的独立性包括数据的物理独立性和数据的逻辑独立性。
	- ==数据控制功能==。DBMS提供了数据控制功能，以适应共享数据的环境。数据控制功能包括对数据库中数据的安全性、完整性、并发和恢复的控制。
		- ==数据库的安全性保护==。数据库的安全性是指保护数据库以防止不合法的使用所造成的数据泄漏、更改或破坏。这样，用户只能按规定对数据处理，例如，划分了不同的权限，有的用户只能有读数据的权限，有的用户有修改数据的权限，用户只能在规定的权限范围内操纵数据库。
		- ==数据的完整性==。数据库的完整性是指数据库正确性和相容性，是防止合法用户使用数据库时向数据库加入不符合语义的数据。保证数据中数据是正确的，避免非法的更新。
		- ==并发控制==。在多用户共享的系统中，许多用户可能同时对同一数据进行操作。DBMS的并发控制子系统负责协调并发事务的执行，保证数据库的完整性不受破坏，避免用户得到不正确的数据。
		- ==故障恢复==。数据库中的4类故障是事务内部故障、系统故障、介质故障及计算机病毒。故障恢复主要是指恢复数据库本身，即在故障引起数据库当前状态不一致后，将数据库恢复到某个正确状态或一致状态。恢复的原理非常简单，就是要建立<u>冗余数据</u>。换句话说，确定数据库是否可恢复的方法就是其包含的每一条信息是否都可以利用冗余地存储在别处的信息重构。冗余是物理级的，通常认为逻辑级是没有冗余的。
- DBMS分类：
	- **关系数据库系统**：Relation DataBase System，RDBMS。是支持关系模型的数据库系统。在关系模型中，实体以及实体间的联系都是用关系来表示。在一个给定的现实世界领域中，相应于所有实体及实体之间联系的关系的集合构成一个关系数据库，也有型和值之分。关系数据库的型也称为关系数据库模式，是对关系数据库的描述，是关系模式的集合。关系数据库的值也称为关系数据库，是关系的集合。关系数据模式与关系数据库通常统称为关系数据库。在计算机方式下常见的FOXPRO和ACCESS等DBMS，严格地讲不能算是真正的关系型数据库，对许多关系类型的概念并不支持，但它却因为简单实用、价格低廉，目前拥有很大的用户市场。
	- 面向对象的数据库系统：Object-Oriented DataBase System，OODBS。是支持以对象形式对数据建模的数据库管理系统，这包括对对象的**类**、类属性的**继承**、**子类**的支持。面向对象数据库系统主要有两个特点：一是面向对象数据模型能完整描述现实世界的数据结构，能表达数据间的嵌套、递归的联系；二是具有面向对象技术的封装性和继承性，提高了软件的可重用性。
	- 对象关系数据库系统：Object-Oriented Relation DataBase System，ORDBS。是在传统的关系数据模型基础上，提供元组、数组、集合一类更为丰富的数据类型以及处理新的数据类型操作的能力，这样形成的数据模型被称为“对象关系数据模型”，基于对象关系数据模型的DBS称为对象关系数据库系统。