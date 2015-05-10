1. java.util.DateFormat是非线程安全的，在多线程环境下需要使用ThreadLocal保证线程安全。

2. C语言内存处理注意事项:

	malloc申请的内存在堆中，是不会自动释放的，用完之后需要free。
减少代码的malloc次数，堆中的内存即使free了，也不会真正的释放掉。
使用libuv异步机制，代码中没有并发，只有一个主循环，无需考虑并发处理。
3. 一个web框架考虑的几个点

	- mvc：分离model、view以及controller
	- filter
	- interceptor
	- 模板引擎
	- orm
	- 日志
	- 性能监控
4. 一门编程语言的几个维度

	- 编程泛型：面向对象、函数式、过程式。
	- 语言的类型模型：强类型（Java)/弱类型(c)；静态类型(java)/动态类型(ruby)
	- 语法：if while for这些常用的语法，以及代码语句的结束是分号还是无须分号。
	- 语义：一些关键字，比如const int等等
	- 基本数据类型：语言支持哪些基本数据类型，int long float double bool
	- 高级数据结构:语言支持的高级数据结构，如链表、数组、映射、元组等
	- 可用库：语言的外围扩展库，比如java的spring、hibernate框架，node的express等。
5. 如何有效阅读源代码：1) 先阅读架构文档 2) 根据架构，将源码文件以模块（或上下层级）分类 3) 从最独立（依赖性最小）的模块代码读起 4) 阅读该模块功能文档 5) 阅读该模块源代码 6) 一边阅读一边整理「调用关系表」7) goto 3

6. 【如何阅读 Rails 源代码】1、从单纯的部分切入，例如 Helper 2、从 request 开始，到 rack、到 routing、到 controller，最后再到 model 3、搞懂 Rails 的启动流程 4、实际写一个简单的 Rails Plugin 5、读别人（热门）的 Rails Plugin

7. SSH Public key denied on “git clone” command

		exec ssh-agent bash
  		ssh-add ~/.ssh/private-key-name

8. 心跳检测有三种
	- tcp层面
	- 协议层
	- 应用层
9. 转发80端口
		
		sudo ipfw add 100 fwd 127.0.0.1,7070 tcp from any to any 80 in

10. 通过调整GCTimeLimit和GCHeapFreeLimit参数来重新定义何时抛出OutOfMemoryError错误。GCTimeLimit 的默认值是98%，也就是说如果98%时间都用花在GC上，则会抛出OutOfMemoryError。GCHeapFreeLimit 是回收后可用堆的大小。默认值是2%。

11. lambda的使用方法如下：

		lambda [arg1[,arg2,arg3,...,argn]] : expression

12. nginx总的一个配置指令proxy_interceptor_errors设置为true，可以捕获后端服务器返回的错误码进行处理（使用nginx自己的错误显示页面）

13. spring是xml配置优先的

14. Java中静态属性和静态方法可以被继承，但是没有被重写(overwrite)而是被隐藏.

	静态方法和属性是属于类的，调用的时候直接通过类名.方法名完成对，不需要继承机制及可以调用。如果子类里面定义了静态方法和属性，那么这时候父类的静态方法或属性称之为”隐藏”。如果你想要调用父类的静态方法和属性，直接通过父类名.方法或变量名完成，至于是否继承一说，子类是有继承静态方法和属性，但是跟实例方法和属性不太一样，存在”隐藏”的这种情况。
	
	多态之所以能够实现依赖于继承、接口和重写、重载（继承和重写最为关键）。有了继承和重写就可以实现父类的引用指向不同子类的对象。重写的功能是：”重写”后子类的优先级要高于父类的优先级，但是“隐藏”是没有这个优先级之分的。
	
	静态属性、静态方法和非静态的属性都可以被继承和隐藏而不能被重写，因此不能实现多态，不能实现父类的引用可以指向不同子类的对象。非静态方法可以被继承和重写，因此可以实现多态。
静态方法类一定要注意是不是线程安全的
15. HttpServlet的service方法接受请求转发到doPost\doGet\….
16. Servlet和Filter的URL匹配规则：① 完全匹配 /test/list.do② 目录匹配 /test/* ③ 扩展名匹配 *.do 
17. servlet-mapping的重要规则： ☆ 容器会首先查找完全匹配，如果找不到，再查找目录匹配，如果也找不到，就查找扩展名匹配。 ☆ 如果一个请求匹配多个“目录匹配”，容器会选择最长的匹配。
18. 一般UGC系统的设计方针就是通过降低系统次要环节的实时一致性，在合理的成本范围内，尽量提高系统响应性能，而提高响应性能的手段归根结底就是三板斧：队列（Queue）、缓存（Cache）和分区（Sharding）：

	- 队列：可以缓解并发写操作的压力，提高系统伸缩性，同时也是异步化系统的最常见实现手段；
	- 缓存：从文件系统到数据库再到内存的各级缓存模块，解决了数据就近读取的需求；
	- 分区：保证了系统规模扩张和长期数据积累时，频繁操作的数据集规模在合理范围。
19. 静态工具类、单例务必要注意是否是线程安全、集合类的线程安全性
20. 亿级用户 千万并发 程序编写时对性能的考虑
21. 解决耗时问题：异步 并发 减少IO
22. request.setCharacterEncoding必须在所有filter最开始执行，否则只要调用过request相关方法，此方法则失效。
23. 缓存五分钟法则法则：如果一个数据频繁被访问，那么就应该放内存中。
24. 线程间通信机制：共享内存、消息队列、socketpair、管道、25. socket(unix域socket socketpair是域socket的一种)
25. ACID，是指在数据库管理系统（DBMS）中事务所具有的四个特性：原子性（Atomicity）、一致性（Consistency）、隔离性（Isolation，又称独立性）、持久性（Durability）。
26. redis命令行命令末尾不带;
27. Spring容器中的Bean几种初始化方法和销毁方法的先后顺序:
在实例化的过程中：
		
		Constructor > @PostConstruct >InitializingBean > init-method
	
	在销毁的过程中：
			
		@PreDestroy > DisposableBean > destroy-method
28. JVM术语：

		sticky-reference-count：这个词让我很头疼，在另一篇英文论文中的解释是：The sticky-reference-count problem refers to the question of how the system could still detect and collect garbage if the reference count is saturated.也就是说对于使用“引用计数”（reference count）算法的GC，如果对象的计数器溢出，则起不到标记某个对象是垃圾的作用了，这种错误称为sticky-reference-count problem，通常可以增加计数器的bit数来减少出现这个问题的几率，但是那样会占用更多空间。一般如果GC算法能迅速清理完对象，也不容易出现这个问题。我最后还是直接按单词翻译了：粘性引用。
		mutator：这个的英文解释相对比较多，只要是mark-sweep类型的GC都会用到这个术语，我直接使用英文了。mutate的中文是变异，在GC中即是指一种JVM程序，专门更新对象的状态的，也就是让对象“变异”成为另一种类型，比如变为垃圾。
		on-the-fly：这个词不算计算机术语，金山的翻译是“飞行中、闲混”，不过我们这里是用来描述某个GC的类型：on-the-fly reference count garbage collector。其实on-the-fly还有“做某种事情很轻易、很熟练”的意思，我猜是因为此GC不用标记而是通过引用计数来识别垃圾，如某论文上所说，it is the reference count that detects garbage on-the-fly.
		generational gc：这是一种相对于传统的“标记-清理”技术来说，比较先进的gc，特点是把对象分成不同的generation，即分成几代人，有年轻的，有年老的。这类gc主要是利用计算机程序的一个特点，即“越年轻的对象越容易死亡”，也就是存活的越久的对象越有机会存活下去（姜是老的辣）。思前想后，把它翻译为“世代型GC”
29. RabbitMQ是一个AMQP实现，传统的messaging queue系统实现，基于Erlang。老牌MQ产品了。AMQP协议更多用在企业系统内，对数据一致性、稳定性和可靠性要求很高的场景，对性能和吞吐量还在其次。

	Kafka是linkedin开源的MQ系统，主要特点是基于Pull的模式来处理消息消费，追求高吞吐量，一开始的目的就是用于日志收集和传输，0.8开始支持复制，不支持事务，适合产生大量数据的互联网服务的数据收集业务。

	ZeroMQ只是一个网络编程的Pattern库，将常见的网络请求形式（分组管理，链接管理，发布订阅等）模式化、组件化，简而言之socket之上、MQ之下。对于MQ来说，网络传输只是它的一部分，更多需要处理的是消息存储、路由、Broker服务发现和查找、事务、消费模式（ack、重投等）、集群服务等。
