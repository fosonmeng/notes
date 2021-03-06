- 数据库系统实现是离不开具体的计算机的，在实现数据库逻辑结构设计之后，就要确定数据库在计算机中的具体存储。数据库在物理设备上的存储结构与存取方法称为数据库的物理结构，它依赖于给定的计算机系统。为一个给定的逻辑数据模型设计一个最适合应用要求的物理结构的过程，就是数据库的物理设计。
- 在数据库的物理结构中，数据的基本单位是记录，记录是以文件的形式存储的，一条存储记录就对应着关系模式中的一条逻辑记录。在文件中还要存储记录的结构，如各字段长度、记录长度等，增加必要的指针及存储特征的描述。
- 数据库的物理设计是离不开具体的DBMS的，不同的DBMS对物理文件存取方式的支持是不同的，设计人员必须充分了解所用DBMS的内部特征，根据系统的处理要求和数据的特点来确定物理结构。数据库的物理设计工作过程如图12-10所示。
  ![image-20211020110406678](https://img.mhugh.net/typora/image-20211020110406678.png)
- 一般来说，物理设计包括确定数据分布、存储结构和访问方式的工作。
- 确定数据分布：从企业计算机应用环境出发，需要确定数据是集中管理还是分布式管理，但目前企业内部网及因特网的应用越来越广泛，大都采用分布式管理。对于数据如何分布需要从以下几个方面考虑。
	- 根据不同应用分布数据。企业的不同部门一般会使用不同数据，将与部门应用相关的数据存储在相应的场地，使得不同的场地上处理不同的业务，对于应用多个场地的业务，可以通过网络进行数据处理。
	- 根据处理要求确定数据的分布。对于不同的处理要求，也会有不同的使用频度和响应时间，对于使用频度高、响应时间短的数据，应存储在高速设备上。
	- 对数据的分布存储必然会导致数据的逻辑结构的变化，要对关系模式作新的调整，回到数据库逻辑设计阶段作必要的修改。
- 确定数据的存储结构：
	- 存储结构具体指数据文件记录之间的物理结构。在文件中，数据是以记录为单位存储的，可以是顺序存储、哈希存储、堆存储和B+树存储等，要根据数据的处理要求和变更频度选定合理的物理结构。
	- 为提高数据的访问速度，通常会采用索引技术。在物理设计阶段，要根据数据处理和修改要求，确定数据库文件的索引字段和索引类型。
- 确定数据的访问方式：
	- 数据的访问方式是由其存储结构所决定的，采用什么样的存储结构，就使用什么样的访问方式。数据库物理结构主要由存储记录格式、记录在物理设备上的安排及访问路径（存取方法）等构成。
	- 存储记录结构设计：
		- 存储记录结构包括记录的组成、数据项的类型、长度和数据项间的联系，以及逻辑记录到存储记录的映射。在设计记录的存储结构时，并不改变数据库的逻辑结构，但可以在物理上对记录进行分割。数据库中数据项的被访问频率是很不均匀的，基本上符合公认的“80/20规则”，即“从数据库中检索的80%的数据由其中的20%的数据项组成”。
		- 当多个用户同时访问常用数据项时，会因访盘冲突而等待。如果将这些数据分布在不同的磁盘组上，当用户同时访问时，系统可并行地执行I/O，减少访盘冲突，提高数据库的性能。所以对于常用关系，最好将其水平分割成多个裂片，分布到多个磁盘组上，以均衡各个磁盘组的负荷，发挥多磁盘组并行操作的优势。
	- 存储记录布局：
		- 存储记录的布局，就是确定数据的存放位置。存储记录作为一个整体，如何分布在物理区域上，是数据库物理结构设计的重要一环。聚簇功能可以大大提高按聚簇码进行查询的效率。聚簇功能不但可用于单个关系，也适用于多个关系。设有职工表和部门表，其中部门号是这两个表的公共属性。如果查询涉及到这两个表的连接操作，可以把部门号相同的职工元组和部门元组在物理上聚簇在一起，既可显著提高连接操作的速度，又可节省存储空间。建立**聚簇索引**的原则如下。
		  1. 聚簇码的值相对稳定，没有或很少需要进行修改
		  2. 表主要用于查询，并且通过聚簇码进行访问或连接是该表的主要应用。
		  3. 对应每个聚簇码值的平均元组数既不太多，也不太少。
		- 任何事物都有两面性，聚簇对于某些特定的应用可以明显地提高性能，但对于与聚簇码无关的查询却毫无益处。相反地，当表中数据有插入、删除、修改时，关系中有些元组就要被搬动后重新存储，所以建立聚簇的维护代价是很大的。
	- 存取方法的设计：
		- 存取方法是为存储在物理设备（通常是外存储器）上的数据提供存储和检索的能力。存取方法包括存储结构和检索机制两部分。存储结构限定了可能访问的路径和存储记录；检索机制定义每个应用的访问路径。
		- 存取方法是快速存取数据库中数据的技术。数据库系统是多用户共享系统，对同一个关系建立多条存取路径才能满足多用户的多种应用要求。为关系建立多种存取路径是数据库物理设计的另一个任务。在数据库中建立存取路径最普遍的方法是建立索引。确定索引的一般顺序如下：
		  1. 首先可确定关系的存储结构，即记录的存放是无序的，还是按某属性（或属性组）聚簇存放。这在前面已讨论过，这里不再重复。
		  2. 确定不宜建立索引的属性或表。对于太小的表、经常更新的属性或表、属性值很少的表、过长的属性、一些特殊数据类型的属性（大文本、多媒体数据）和不出现或很少出现在查询条件中的属性不宜建立索引。
		  3. 确定宜建立索引的属性。例如关系的主码或外部码、以查询为主或只读的表、范围查询、聚集函数（Min、Max、Avg、Sum、Count）或需要排序输出的属性可以考虑建立索引。
		- 索引一般还需在数据库运行测试后，再加以调整。在RDBMS中，索引是改善存取路径的重要手段。使用索引的最大优点是可以减少检索的CPU服务时间和I/O时间，改善检索效率。但是，不能对进行频繁存储操作的关系建立过多的索引，因为过多的索引也会影响存取操作的性能。