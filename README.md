# java-face
java面试题

一、Java 基础
1.JDK 和 JRE 有什么区别？
	JDK是java的开发工具包,包含各种类库,并且包含了JRE,javac是在JDK中的;
	JREjava程序的运行环境,安装过程中自动添加PATH.
2. == 和 equals 的区别是什么？
	一.	对于==,比较的是值是否相等,如果比较的是基本数据类型的变量,则直接比较其存储的值是否相等,
	   	如果比较的是引用数据类型,则比较的是所指向的对象的地址值.
	二.	equals不能作用于基本数据类型,它比较的是是否是同一个对象
		如果没有对equals方法进行重写,则比较的是引用类型的变量所指向的对象的地址值.
		如String,Date等类对equals方法进行了重写,比较的则是所指向的对象的内容
3. 两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？
	首先,两个对象equals相等,hashcode一定相等;但是hashcode相等时,equals不一定相等.
	其次,两个不同的对象,因为可能存在哈希碰撞,所以hashcode可能是相等的,但是显然equals不为true.
	还有就是,在object类中,euqals方法还是用的==来判断的,==对于对象而言比较的是地址值,所以equals相等
	hashcode一定一样,反之就不一定了.
4. final 在 java 中有什么作用？
	final关键字可作用于类,类属性和方法;
	作用于类上时,该类不能被继承
	作用于属性时,该属性不能被重新复制
	作用于方法时,该方法不能被重写
5. java 中的 Math.round(-1.5) 等于多少？
	Math的round方法是四舍五入,如果参数是负数,则往大的数如,Math.round(-1.5)=-1
6. String 属于基础的数据类型吗？
	不是,String是一个类,是引用数据类型.
7. java 中操作字符串都有哪些类？它们之间有什么区别？
	有String,StringBuilder,StringBuffer
	1.	String是不可变的,每次对String的操作都会产生一个String对象
	2.	StringBuilder和StringBuffer是可变的,能够被多次修改,并不会产生新的对象.
	3.	StringBuilder是线程不安全的,StringBuffer是线程安全的.
	4.	StringBuilder的处理速度比StringBuffer要快
8. String str="i"与 String str=new String(“i”)一样吗？
	他们的值相等,用equals得到true,但是他们是两个对象,如果用==判断返回false.
	且str="i"是直接在常量池中引用字符串,而new String("i")是在堆中根据i再创建一个对象.
9. 如何将字符串反转？
	1.	通过StringBuilder的reverse()方法可以直接反转
		StringBuilder sb = new StringBuilder("abc");
		sb.reverse().toString();
	2.	通过String的toCharArray方法可以获得字符串每一个字符并且转换为字符数组
		然后循环从后往拼接即可
	3.	递归的方法反转(当只有一个字符时,返回原字符;当有两个以上的字符时,返回结果为第二个字符串开始的子串+第一个字符)
		public String reverseString(String str) {
			if ((null == str) || str.length()<2) {
				return str;
			}
			return reverseString(str.subString(1)) +str.charAt(0);
		}	
10. String 类的常用方法都有那些？
	charAt(int index)返回指定索引处的字符
	length()返回字符串长度
	split()根据给定的正则表达式拆分字符串
	toString()返回此对象本身
11. 抽象类必须要有抽象方法吗？
	抽象类可以没有抽象方法,但是如果一个类已经声明为抽象类,那么它也不能再实例化,不能直接构造该类对象.
12. 普通类和抽象类有哪些区别？
	1.	抽象类不能被实例化,普通类反之
	2.	抽象类的访问权限限于public和protected,如果为private的话,就不能被子类继承了.
	3.	如果一个类继承于抽象类,则它必须实现父类的抽象方法.如果不想实现,那么子类也必须是抽象类.
13. 抽象类能使用 final 修饰吗？
	不能,final修饰的类是不能被继承的,如果抽象类不能继承,就没有意义了.
14. 接口和抽象类有什么区别？
	1.	抽象类可以有构造方法,接口不能有构造方法.
	2.	抽象类可以包含非抽象方法,接口则不能.
	3.	抽象类方法访问权限是public、protected,接口中只能是public.
	4.	只能单继承,但是可以多实现.
15. java 中 IO 流分为几种？
	大的方面来说有两种:字节流和字符流
	字节流继承于InputStream、OutputStream
	字符流继承于Reader、Writer

16. BIO、NIO、AIO 有什么区别？
	1.	BIO表示同步阻塞式IO,交互方式是同步、阻塞方式,即客户端有连接请求时服务端就需要启动一个线程进行处理,
		如果这个连接不做任何事情会造成不必要的开支.
	2.	NIO表示同步非阻塞IO,客户端发送的连接请求都会注册到多路复用器上,多路复用器轮询到连接有I/O请求
		时才启动一个线程处理.
	3.	AIO表示异步非阻塞IO,客户端的I/O请求都是由操作系统先完成IO操作后再通知服务器应用来启动线程处理.
17. Files的常用方法都有哪些？
	String getName():返回File对象所表示的文件名或文件路径
	String getPath():返回File对象所对应的相对路径
	boolean exists():判断File对象的文件或者目录是否存在
	boolean isDirectory():判断File对象是否是目录

二、容器
18. java 容器都有哪些？
	String,数组以及java.util下面的集合类
	List:存放有序,列表存储,元素可重复
		ArrayList	LinkedList Vector
	Set:无序,元素不可重复
		HashSet		TreeSet
	Map:无序,元素可重复
		HashMap		TreeMap 	LinkedHashMap	HashTable
19. Collection 和 Collections 有什么区别？
	Collection是集合类的一个顶级接口,它提供了对集合对象进行基本操作的通用接口方法.
	Collections是集合类的一个工具类,它提供了一系列的静态方法,用于对集合中元素进行排序,搜索以及线程同步等操作.
20. List、Set、Map 之间的区别是什么？
	List:	可以允许重复的对象;
			可以插入多个null元素;
			有序,输入顺序就是输出顺序;
	Set:	不允许重复对象;
			无序,且只允许一个null对象;
	Map:	存储键值对,只能有唯一的key,value可以重复
			只能有一个null键
21. HashMap 和 Hashtable 有什么区别？
	一.	HashMap可以接受null键和值,HashTable不行
	二.	HashTable是线程安全的,通过synchronized来保证,而HashMap线程不安全
	三.	HashMap的迭代器是fail-fast迭代器,而HashTable的enumerator迭代器不是fail-fast.
22. 如何决定使用 HashMap 还是 TreeMap？
	HashMap基于散列表实现,适用于查询频繁的情况
	TreeMap基于红黑树实现,适用于创建比较多的情况.且TreeMap存储数据是按照字母表的顺序存储的,
	如果对顺序有要求也可以选用TreeMap.
23. 说一下 HashMap 的实现原理？
	数组+链表,初始16,75扩容,数据存在内部类Map.Entry中,其中包含key value hashcode和next.
24. 说一下 HashSet 的实现原理？
	HashSet基于HashMap实现,默认构造函数是构造一个初始容量为16的HashMap,所有放入HashSet
	集合的元素实际上由HashMap的key来保存,而value则保存了一个PRESENT的静态Object对象,因为元素都保存在key
	中,所以才能不重复.
25. ArrayList 和 LinkedList 的区别是什么？
	1.	ArrayList底层基于动态数组,LinkedList基于链表实现,底层是循环双向链表
	2.	对于随机访问get和set,ArrayList优于LinkedList.
	3.	对于新增add和删除remove,LinkedList比较快
26. 如何实现数组和 List 之间的转换？
	List转数组:toArray()方法.在方法参数中指定原集合的长度的数组即可.
	数组转List:Arrays的asList()方法.
27. ArrayList 和 Vector 的区别是什么？
	1.	Vector的方法都是同步的,是线程安全的,ArrayList则不是.
	2.	在进行扩容的时候,Vector扩容至原来的一倍,ArrayList增加至原来的0.5倍.
28. Array 和 ArrayList 有何区别？
	1.	Array(数组)可以包含基本数据类型和对象类型,ArrayList只能包含对象类型.
	2.	ArrayList可以自动扩容,Array则不行.
29. 在 Queue 中 poll()和 remove()有什么区别？
	Queue中,add方法和offer方法都可以添加元素,而remove和poll都是删除队列的头元素,区别在于:
	add方法在队列满的情况下抛异常,而offer方法则返回false.
	remove方法在队列为空时抛异常,poll方法将返回null.
30. 哪些集合类是线程安全的？
	Vector    HashTable    ConcurrentHashMap
	Stack	  
31. 迭代器 Iterator 是什么？
	Iterator是个接口,它提供了很多对元素进行迭代的方法.迭代器可以在迭代过程中删除
	底层集合的元素,可以直接调用Iterator的remove()方法来删除.
	因为在Conllection接口中定义了获取集合迭代器的方法,所以每一个集合都包括了可以返回迭代器实例的方法.	
32. Iterator 怎么使用？有什么特点？
	每个集合都可以用iterator()方法一个Iterator实例.
	使用next()方法获取序列中的下一个元素,使用hasNext()方法检查序列中是否有元素
	使用remove()方法将迭代器新返回的方法删除.
	特点:Iterator将集合的遍历和其底层的结构分离.
33. Iterator 和 ListIterator 有什么区别？
	ListIterator是Iterator的子接口,用于扩展Iterator.
	在Iterator中,我们只能向前移动,无法操纵或者修改集合中的元素.ListIterator弥补了这种缺点
	区别:	1.范围不同,Iterator适用于所有集合,而ListIterator只适用于List及其子类
			2.ListIterator有add方法可以添加元素,Iterator则不行.
			3.ListIterator可以实现双向遍历,Iterator则不行.
			4.ListIterator可以实现对象的修改,Iterator不行
			5.ListIterator可以获取集合中的所有,Iterator不行.
34. 怎么确保一个集合不能被修改？
	可以使用Collections或者Guava来快速实现.如Collections.unmodifiableMap(xxxMap);
三、多线程
35. 并行和并发有什么区别？
	并行是多个事件同时进行,并发是多个事件在某一时间段内间隔发生.
	你吃饭吃到一半，电话来了，你停了下来接了电话，接完后继续吃饭，这说明你支持并发。
	你吃饭吃到一半，电话来了，你一边打电话一边吃饭，这说明你支持并行。
36. 线程和进程的区别？
	进程是操作系统资源分配的基本单位,线程是任务调度和执行的基本单位.
	进程有独立的地址空间,一个进程崩溃后在保护模式下不会对其他进程产生影响,而线程只是一个进程中的
	不同执行路径,线程有自己的堆栈和局部变量.在操作系统中能同时运行多个进程,而在同一个进程内有多个
	线程同时执行.
37. 守护线程是什么？
	守护线程是服务其他线程的,在java中,线程有两种:守护线程和用户线程.
	java中的jvm垃圾回收线程就是一个典型的守护线程.当用户线程全部执行完,包括main线程也执行完毕,那么
	jvm会自动退出,此时守护线程也就停止了.
38. 创建线程有哪几种方式？
	三种:	1.	继承Thread类,重写run方法,用子类实例调用start()方法;
			2.	实现Runnable接口并重写run方法,创建Thread实例并传入Runnable实例,代用Thread的start()方法
			3.	创建Callable接口的实现类,重写call方法;
				构造此实现类的实例,将其作为参数构造一个FutureTask类的实例;
				以FutureTask的实例为参数构造一个Thread对象执行start()方法.
	第三种方式可以允许有返回值,也可以声明抛出异常类.
39. 说一下 runnable 和 callable 有什么区别？
	runnable方式时,多个线程间可以共享实例变量,callable方式则不行
	runnable方式没有返回值,callable有返回值
	runnable方式run方法的异常只能在内部消化,callable的call()方法允许抛出异常
40. 线程有哪些状态？
	1.	NEW 	新建状态,此时线程还没有运行线程中的代码
	2.	RUNNABLE 	就绪状态;处于就绪状态的线程并不一定立即运行run方法,必须还要和其他线程竞争CPU时间
	3.	RUNNING 	运行状态;线程获得CPU时间后才进入运行状态,开始执行run方法
	4.	BLOCKED		阻塞状态;线程运行过程中会有各种原因来进入阻塞状态,如:调用sleep方法进入休眠;
							在IO操作中被阻塞;试图得到一个锁,该锁正被其他线程持有;等待某个触发条件.
							阻塞状态的线程此时没有结束,暂时让出CPU时间给其他线程.
	5.	DEAD		死亡状态;有两个原因导致线程死亡:第一是run方法正常退出自然死亡;第二是一个未捕获的
							异常终止了run方法使线程死亡.
	为了确定线程在当前是否存活着（就是要么是可运行的，要么是被阻塞了），需要使用isAlive方法，如果是可运行或被阻塞，这个方法返回true；如果线程仍旧是new状态且不是可运行的，或者线程死亡了，则返回false。
41. sleep() 和 wait() 有什么区别？
	1.	sleep方法使Thread类的,而wait方法使Object类中的
	2.	sleep方法使线程暂停指定的时间,让出CPU给其他线程,但是他的监控状态依然保持着,时间到了以后会自动恢复运行状态
		在这个过程中,线程不会释放同步对象锁.
		而调用wait方法,线程会放弃对象锁,进入等待队列,待调用notify/notifyAll方法后才会进入锁池,获取对象锁后才进入运行状态.
42. notify()和 notifyAll()有什么区别？
	notify()方法随机唤醒一个wait线程到锁池中去竞争锁,而notifyAll方法唤醒所有wait线程到锁池.
	notity()方法可能产生死锁,notifyAll则不会.
43. 线程的 run()和 start()有什么区别？
	run()方法只是定义了线程的执行单元并非直接开启了线程资源,只有start()方法被调用,才可以启动一个线程.
	如果直接调用run方法,会被当成普通方法在main线程执行,并不会创建线程.
44.创建线程池有哪几种方式？
	java中的Executors可以为我们创建现成的线程池,有以下几种:
	1.	newSingleThreadExecutor 创建一个单线程的线程池,它只有一个工作线程,操作无界工作队列,可以保证任务顺序
	2.	newFixedThreadPool	创建一个定长线程池,可控制线程最大并发数,超出的线程会在队列中等待
	3.	newCachedThreadPool	创建一个可缓存线程池,有空闲线程时会回收,但是任务过多,会一直创建,消耗资源
	4.	newScheduledThreadPool	创建一个大小无线的线程池,此线程池支持定时以及周期性任务的需求.
45.线程池都有哪些状态？
	1.	RUNNING:一旦被创建,就处于此状态,可以接受新任务以及对已经添加的任务进行处理.
	2.	SHUTDOWN:此时不接收新任务,但是可以处理已添加的任务
	3.	STOP:此状态不接收新任务,不处理已添加任务,并且会中断正在处理的任务.
	4.	TIDYING:当所有的任务已终止,ctl记录的任务数变为0,线程池会变成tidying状态.当线程池变为TIDYING状态会执行terminated()方法.
				当线程池在SHUTDOWN状态下，阻塞队列为空并且线程池中执行的任务也为空时，就会由 SHUTDOWN -> TIDYING。 
				当线程池在STOP状态下，线程池中执行的任务为空时，就会由STOP -> TIDYING。
	5.	TERMINATED:线程池彻底终止会变成这个状态.当在TIDYING状态,执行完terminated()函数后,就会由TIDYING状态变为TERMINATED状态.
46. 线程池中 submit()和 execute()方法有什么区别？
	1.	接受参数不一样,execute()方法接收Runnable类型的参数;submit()可以接收runnable和callable类型的参数
	2.	submit方法有返回值,返回一个Future类型的对象,execute方法没有返回值.
	3.	submit方法方便处理Exception异常.
47. 在 java 程序中怎么保证多线程的运行安全？
	1.	最简单的方式是加入synchronized关键字,在共享数据语句中加入该关键字可以在某一时段指挥让一个线程执行,其他线程不能执行.
	2.	使用锁Lock
	3.	redis?
48. 多线程锁的升级原理是什么？
	在java中,锁有三种状态,级别从低到高依次为:偏向锁、轻量级锁、重量级锁,这几个状态会随着竞争情况逐渐升级,但是不能降级.
	先说为什么要有锁升级:因为synchronized是重量级锁,每次在进行锁请求时,如果当前资源被其他线程占有,就要将当前线程阻塞,加入到阻塞队列中然后
	清空当前线程的缓存,等到锁释放时再通过notify或者notifyAll方法唤醒当前线程,让其处于就绪状态.在这个过程中是非常消耗资源的,而且有时候线程刚挂起,锁就释放了.
	而java的线程是映射到操作系统的原生线程之上的,每次线程的阻塞和唤醒都要在用户态和核心态之间转换,十分浪费资源.所以jvm对syncronized进行了优化,分为三种锁.
	1.	当锁对象第一次被线程获取的时候,虚拟机会将对象头中的锁标志位设置成01,并将偏向锁标志设置为1,线程通过CAS的方式将自己的ID值放到对象头中.这样每次该线程每次
		再进入锁对象的时候不用任何的同步操作,直接比较当前锁对象头中是不是该线程的ID,如果是就可以直接进入.当有其他线程来尝试获取锁的时候,发现偏向锁标示是1,说明
		锁已经被占用,则会使用CAS将对象头的偏向锁指向当前线程.
		需要注意的是,偏向锁使用一种等待竞争出现才会释放锁的机制,当有其他线程尝试获取锁的时候,才会释放锁.首先它会暂停拥有偏向锁的线程,然后检查持有偏向锁的线程
		是否活着,如果不处于活动状态,则将对象头设置为无锁状态;如果活着,那么拥有偏向锁的栈会被执行,遍历偏向对象的锁记录,使之要么恢复到无锁要么标记对象不适合作为
		偏向锁.最后唤醒暂停的线程.
	2. 	假设线程1持有偏向锁,线程2来竞争偏向锁:
		一. 首先线程2会检查偏向锁标记,如果是1,说明是偏向锁,那么JVM会找到线程1看其是否还活着.
		二. 如果线程1已经执行完毕,那么先将偏向锁置为0,对象头设置为无锁的状态,用CAS的方式尝试将线程2的ID放入对象头,此时锁不升级,还是偏向锁.
		三. 如果线程1还活着,先暂停线程1,将锁标志位变为00(轻量级锁),然后在线程1的栈帧中开辟出一块空间将对象头的Mark word置换到线程1的栈帧中,而对象头
			中存储的是指向当前线程栈帧的指针.此时变为轻量级锁,线程1继续执行,线程2采用CAS的方式尝试获取锁.
	3.	轻量级锁是通过CAS的方式尝试获取锁对象,一旦失败会先检查对象头中存储的是否是指向当前线程栈帧的指针,如果是,就可以获取锁对象,如果不是说明存在竞争那么久
		膨胀成为重量级锁.
	4.	一旦有两个以上的线程竞争锁,轻量级锁就会膨胀为重量级锁,锁的状态变为10,此时对象头中存储的就是指向重量级锁的栈帧的指针,而且其他等待所的线程要进入阻塞状态,
		等待重量级锁释放后被唤醒然后去竞争.重量级锁是由操作系统来负责线程的调度,会消耗大量的系统资源.

49. 什么是死锁？
	死锁是指两个或两个以上的进程或线程在执行过程中,因争夺资源而造成的一种相互等待的过程,如果没有外力作用,他们讲无法推进下去.
50. 怎么防止死锁？
	1.	以确定的顺序获取锁
	2.	超时放弃.(Lock锁中就使用了这种方式)
	3.	银行家算法
51. ThreadLocal 是什么？有哪些使用场景？
	也成为线程本地变量,ThreadLocal在每个线程中对一个变量创建了一个副本,且在线程内部任何地方都可以使用,线程间互不影响.
	应用场景:spring的声明式事物管理.
52. 说一下 synchronized 底层实现原理？
	首先,每个对象都有一个监视器锁(monitor),当monitor被占用时就会处于锁定状态,线程执行monitorenter指令时尝试获取monitor的所有权,过程如下:
	1.	如果monitor的进入数为0,则线程进入monitor,将进入数设置为1,该线程为monitor的所有者
	2.	如果线程已经占有monitor,只是重新进入,则进入数+1
	3.	如果其他线程已经占用了monitor,则该线程进入阻塞状态,直到monitor的进入数为0,再重新尝试获得所有权
	执行monitorexit的线程必须是objectref所对应的monitor的所有者.指令执行时,monitor的进入数-1,如果减为0,那么线程退出monitor,不再是持有者.
	在将synchronized代码块反编译以后,我们可以发现调用了monitorenter和monitorexit指令.
	所以如果synchronized同步代码块,底层是调用monitor的两个指令来实现锁
	如果synchronized同步方法,底层是读取运行时常量池的ACC_SYNCHRONIZED标志来实现的.
53. synchronized 和 volatile 的区别是什么？
	1.	volatile修饰的变量,jvm每次都从主内run读取,不会从工作内存读取
		而synchronized是锁住当前变量,同一时刻只有一个线程能访问当前变量.
	2.	volatile只是作用于变量,synchronized可以用在变量,方法中
	3.	valatile仅能实现变量修改的可见性,无法保证原子性.
		synchronized可以实现变量修改的可见性和原子性.
54. synchronized 和 Lock 有什么区别？
	1.	synchronized是java内置的关键字,Lock是个接口
	2.	synchronized无法判断是否获取锁的状态,Lock可以判断是否获取到锁.
	3.	synchronized会自动释放锁,Lock需要手动释放
	4.	synchronized可重入(同一个类中两个同步方法,获取到锁后不用每次都去获取),不可中断,非公平;Lock可判断可公平.
	5. 	synchronized获得锁的线程阻塞,其他线程都会无线等待,Lock不会
55. synchronized 和 ReentrantLock 区别是什么？
	1.	synchronized遇到异常不catch,锁会自动释放,ReentrantLock需要手动释放
	2.	synchronized是非公平锁,ReentrantLock可以实现公平锁.
	3. 	前者无法获取锁的状态,后者可以tryLock()方法可以返回是否获得了锁.
56. 说一下 atomic 的原理？
	atomic包用中的类可以实现多线程环境下的变量操作,底层是调用CPU的CAS指令来进实现线程安全的.
	CAS,比较并操作,每次在set前,对比一下当前值和预期值是否一样,一样则set,否则认为失败,循环对比直到成功.

四、反射
57. 什么是反射？
	在运行过程中,对任何一个类,都能知道这个类的所有属性和方法,对于任意一个对象,都能改变其属性.
58. 什么是 java 序列化？什么情况下需要序列化？
	序列化就是一种用来处理对象流的机制,简单来说,就是把对象存储在某一个地方,硬盘或者网络,即把对象的内容转变为字节序列.
	当想把内存中的对象状态保存在一个文件或者数据库,或者在网络上传输的时候,就需要序列化,在java中需要实现Serializable接口.
59. 动态代理是什么？有哪些应用？
	动态代理是将对象中不同方法的调用重新定向到一个统一处理函数,做自定义的逻辑处理,但是调用者察觉不到.
	应用: Spring的AOP,事物,权限,日志.RPC框架
60. 怎么实现动态代理？
	1.	利用JDK的反射机制实现
	2.	使用CGLIB代理.
五、对象拷贝
61. 为什么要使用克隆？
	想要对一个对象进行处理,但是又想保留原有的数据,这时可以使用克隆.
62. 如何实现对象克隆？
	1.	实现Cloneable接口并重写Object的clone()方法
	2.	实现Serializable接口,通过对象的序列化和反序列化实现深度克隆
63. 深拷贝和浅拷贝区别是什么？
	是否支持引用数据类型的成员变量的复制.
六、Java Web
64. jsp 和 servlet 有什么区别？
	1.	jsp擅长表现页面显示,servlet擅长逻辑控制
	2.	servlet没有内置对象,jsp有内置对象
	3.	servlet的应用逻辑在.java文件中,而jsp中,java和html组合为一个.jsp文件.
	4.	servlet在java代码中嵌入html代码,jsp是在html中嵌入java代码
65. jsp 有哪些内置对象？作用分别是什么？
	jsp有9个内置对象:
		request 用户端请求，此请求会包含来自GET/POST请求的参数
		response 网页传回用户端的回应
		pageContext 网页的属性是在这里管理
		session 与请求有关的会话期
		application  servlet正在执行的内容
		out 用来传送回应的输出
		config  servlet的构架部件
		page JSP网页本身
		exception 针对错误网页，未捕捉的例外
66. 说一下 jsp 的 4 种作用域？
	application:它的有效范围是整个应用。整个应用是指从应用启动.pplication里的变量可以被所有用户共用。如果用户甲的操作修改了application中的变量，用户乙访			 问时得到的是修改后的值。
	session:如果把变量放到session里，就说明它的作用域是session，它的有效范围是当前会话。所谓当前会话，就是指从用户打开浏览器开始，到用户关闭浏览器这中间		的过程。这个过程可能包含多个请求响应。也就是说，只要用户不关浏览器，服务器就有办法知道这些请求是一个人发起的，整个过程被称为一个会话（session）
	request:就说明它的作用域是request,它的有效范围是当前请求周期。所谓请求周期，就是指从http请求发起，到服务器处理结束，返回响应的整个过程。在这个过            程中可能使用forward的方式跳转了多个jsp页面，在这些页面里你都可以使用这个变量。
	page:代表变量只能在当前页面有效
67. session 和 cookie 有什么区别？
	1.	数据存放位置不同.session在服务器,cookie在客户端浏览器
	2.	安全程度不同,别人可以分析存放在本地的cookie进行cookie欺骗.
	3.	单个cookie保存的数据不能超过4k,而session是在服务器的,所以没有限制
	4.	cookie只能存储string类型的数据,session可以存储对象.
68. 说一下 session 的工作原理？
	当用户第一次访问一个服务器,服务器就会为该用户创建一个session,并生成一个和该session有关的session_id,
	这个id是唯一的,不可重复.这个id将会在本次响应中返回,保存在客户端的cookie中,下次方法的时候,客户端浏览器
	的cookie中含有session_id,服务器基于这个id就可以识别该用户.
69. 如果客户端禁止 cookie 能实现 session 还能用吗？
	可以,当cookie被禁用,我们可以使用"URL重写"来使session生效,简单来说就是将sessionid的信息作为请求地址的一部分
	这样服务器就可以解析URL,得到该sessionid,进而识别用户.
70. spring mvc 和 struts 的区别是什么？
	1.	mvc的入口是一个servlet,struts2的入口是一个filter
	2.	mvc是单例的,struts2是多例的
	3.	mvc面向方法开发,struts2面向类开发.
	4. 	struts2采用值栈存储请求和响应数据,mvc通过参数解析器将request请求解析.
71. 如何避免 sql 注入？
	1.	采用预编译语句
	2.	使用正则过滤传入的参数.
	3.	屏蔽不安全的字符
72. 什么是 XSS 攻击，如何避免？
	XSS攻击,即跨站脚本攻击.是指攻击者在用户端注入恶意的可运行脚本,让其在用户浏览网页时运行,从而通过脚本来获得用户的信息.
	避免: 	对用户输入和URL参数进行过滤,过滤掉脚本相关的内容
		  	对输出进行编码
73. 什么是 CSRF 攻击，如何避免？
	CSRF攻击也叫跨站请求伪造,攻击者通过伪造用户的浏览器请求,向用户自己曾经认证过的网站发送,使目标网站误以为
	是用户的真实操作而去执行命令.
	避免:1.令牌机制 2.token验证

七、异常
74. throw 和 throws 的区别？
	throws:用来声明一个方法可能抛出的所有异常信息,不会处理异常,只是将异常向上传,交给调用者
	throw:抛出一个具体的异常类型.
	throws出现在方法声头,而throw出现在函数体
	throws表示出现异常的可能,并不一定会发生,throw则是抛出了一个存在的异常实例.

75. final、finally、finalize 有什么区别？
	final: 	修饰类,表示该类不可继承
			修饰方法,表示该方法不可重写
			修饰变量,表示该变量不允许被修改
	finally:是保证代码一定要被执行的一种机制.常用来关闭连接资源或者解锁等.
	finalize:是Object的一个方法,它的目的是保证对象在被垃圾收集前完成特定资源的回收.1.9后已经过时.
76. try-catch-finally 中哪个部分可以省略？
	catch可以省略
	不管有没有捕获到异常,finally中的代码都会被执行;
	finally是在return之后执行的,程序在执行完return之后,会将值保存起来,当执行完finally中的代码之后再将return值返回
	如果finally中存在return,会导致最后返回的是finally中的值.
77. try-catch-finally 中，如果 catch 中 return 了，finally 还会执行吗？
	会执行,return的值会暂时保存.等到运行完finally中的代码块时才会返回return的值
78. 常见的异常类有哪些？
	空指针异常类型：NullPointerException
	类型强制转换类型：ClassCastException
	数组下标越界异常：ArrayIndexOutOfBoundsException
	输入输出异常：IOException

八、网络
79. http 响应码 301 和 302 代表的是什么？有什么区别？
	301和302都是HTTP请求的状态码,其中301代表永久性转移,302代表暂时性转移.
	301代表转向前的网址不在了,就会把新的网址当做有效目标
	302只是代表临时性重定向,旧的网址会保留.
80. forward 和 redirect 的区别？
	forward:直接转发,客户端浏览器只发出一次请求,由第二个信息资源响应该请求,共享同一个request对象
	redirect:间接转发,服务端响应第一次请求的时候,让浏览器去访问另外一个URL,从而达到转发的目的.本质上是两次HTTP请求.
	forward地址栏不变,redirect地址栏改变
81. 简述 tcp 和 udp的区别？
	tcp基于连接,udp基于无连接
	tcp对系统资源要求高,udp少
	tcp基于字节流,udp基于数据报文
	tcp复杂,udp简单
82. tcp 为什么要三次握手，两次不行吗？为什么？
	1. 	为了实现可靠数据传输,TCP 协议的通信双方,都必须维护一个序列号以标识发送出去的数据包中哪些是已经被对方收到的。
		三次握手的过程即是通信双方相互告知序列号起始值,并确认对方已经收到了序列号起始值的必经步骤
	2.	如果只是两次握手,至多只有连接发起方的起始序列号能被确认,另一方选择的序列号则得不到确认
83. 说一下 tcp 粘包是怎么产生的？
	TCP粘包是指发送方发送的若干包数据到接收方接收时粘成一包，从接收缓冲区看，后一包数据的头紧接着前一包数据的尾。
	产生原因:
	1.	发送方原因:TCP默认会使用Nagle算法。而Nagle算法主要做两件事：1）只有上一个分组得到确认，才会发送下一个分组；2）收集多个小分组，
		在一个确认到来时一起发送。
	2.	接收方原因:TCP接收到分组时，并不会立刻送至应用层处理，或者说，应用层并不一定会立即处理；实际上，TCP将收到的分组保存至接收缓存里，
		然后应用程序主动从缓存里读收到的分组。这样一来，如果TCP接收分组的速度大于应用程序读分组的速度，多个包就会被存至缓存，
		应用程序读时，就会读到多个首尾相接粘到一起的包
84. OSI 的七层模型都有哪些？
	1:物理层		2:数据链层	3:网络层		4:传输层		5:会话层		6:表示层		7:应用层
85. get 和 post 请求有哪些区别？
	1.get产生一个TCP数据包,POST产生两个
	2.get将数据放在url中可以看到,post会放在html header中提交
	3.get数据大小有限制,最大1024字节,post没有限制
86. 如何实现跨域？
	1.JSONP技术
	2.CORS规范
	3.通过服务端实现
	4.websocket
87. 说一下 JSONP 实现原理？
	JSONP原理是动态添加一个<script>标签,在src属性中访问跨域地址,但是要携带一个回调函数名,服务器将返回的数据封装成js格式的文件返回给
	客户端后进行解析.
	如果是使用ajax的方式,需要添加jsonp属性,指定回调函数名;dataType属性值设置为'jsonp'.
九、设计模式
88. 说一下你熟悉的设计模式？
	单例模式,装饰者模式,代理模式,适配器模式,策略模式
89. 简单工厂和抽象工厂有什么区别？
	简单工厂只能生产同一等级结构中的任一产品
	抽象工厂用来生产不同产品族中的全部产品
十、Spring/Spring MVC
90. 为什么要使用 spring？
	1. 方便解耦,可以将对象间的依赖关系交给spring
	2. spring支持aop编程,可以很方便的对程序进行监控,拦截
	3. 方便测试,支持junit
	4. 集成其他框架比较方便
	5. 声明式事务
91. 解释一下什么是 aop？
	aop即面向切面编程,在原有功能的基础上通过aop添加新的功能,而原有的功能并不知道新添加的功能.
	简单来说,就是在某个类或者方法执行前后打个标记,声明在执行到这里之前要先执行什么,之后执行什么,插入了新的执行方法.
92. 解释一下什么是 ioc？
	ioc控制反转.即把创建对象和维护对象之间关系的权利交给spring容器去做,程序自己不再维护.
	传统:自己使用new 或者getInstance直接或者间接创建一个对象(高耦合,不易测试)
	spring:容器使用工厂模式为了创建了所需要的对象,我们不用自己创建,直接调用即可.
93. spring 有哪些主要模块？
	1. spring core:	core是spring的核心类库,它的所有功能都依赖于该类库,主要实现IOC功能.
	2. AOP:	spring aop提供了常用的拦截器供用户配置.
	3. ORM:	该模块提供对常用的ORM框架的管理和辅助支持.spring自己不实现ORM,只是对常见的ORM进行封装管理
	4. DAO: spring提供对jdbc的支持,统一管理jdbc事物,并不对其进行实现
	5. WEB:	提供对常用框架,如struts2的支持,将spring的资源注入给这些框架,也能在这些框架的前后插入拦截器
	6. Context: 提供框架式的bean访问方式,其他程序可以通过Context访问spring的bean资源
	7. MVC:	提供一套轻量级的MVC实现,简单方便.
94. spring 常用的注入方式有哪些？
	1.	构造器注入:可以在xml中通过constructor-arg标签来注入一个对象到构造器中
	2.	setter方法注入:	首先要配置被注入的bean，在该bean对应的类中，应该有要注入的对象属性或者基本数据类型的属性。
						例如：为UserBiz类注入UserDAO，同时为UserBiz注入基本数据类型String，那么这时，
						就要为UserDAO对象和String类型设置setter方法.，用于进行依赖注入。
	3.	注解注入:基于注解在xml文件中开启注解扫描以后,就可以在filed上使用注解@Autowired或者@Rsource来注入对象.
95. spring 中的 bean 是线程安全的吗？
	不是的,spring并没有对单例bean做多线程的封装.
96. spring 支持几种 bean 的作用域？
	1.singleton: 单例,默认作用域,在spring容器中此种类型的bean只有一个
	2.prototype: 原型,每次调用getBean方法就会产生一个新的实例.
	3.request: 每次HTTP请求都会产生不同的bean实例.
	4.session: 每次会话产生一个实例
	5.global-session: 所有会话共享一个实例
97. spring 自动装配 bean 有哪些方式？
	1.xml配置方式
	2.注解扫描方式
98. spring 事务实现方式有哪些？
	1.编程式事务 允许用户在代码中精确定义事务的边界
	2.声明式事务	基于AOP,将操作和事务管理分离.
99. 说一下 spring 的事务隔离？
	隔离级别定义了一个事务可能受其他并发事务影响的程度。 
	spring设置了五种事务个例级别:
	1.ISOLATION_DEFAULT:	使用数据库默认的隔离级别
	2.ISOLATION_READ_UNCOMMITTED:	最低的隔离级别,允许读未提交的数据变更,可能会导致脏读,幻读或不可重复读.
	3.ISOLATION_READ_COMMITTED:		允许读取已经提交的数据,可以阻止脏读,但是幻读和不可重复读有可能发生.
	4.ISOLATION_REPEATABLE_READ:	保证了一个事务不能读取另一个未提交的数据.可以避免不可重复读和脏读
	5.ISOLATION_SERIALIZABLE:		串行化,事务被处理为顺序执行,通过锁定事务相关的数据库来实现. 
100. 说一下 spring mvc 运行流程？
	1.用户向服务器发送请求,被springMVC的前端控制器拦截(DispatcherServlet)
	2.前端控制器对请求的URL进行解析,得到标识符URI,根据URI调用处理器映射器
	3.处理器映射器与该Handler有关的对象和拦截器信息返回给DispatcherServlet
	4.前端控制器根据获得的处理器信息,调用对应的处理器适配器HandlerAdapter处理数据
	5.处理器适配器提取request中的模型数据,开始执行Handler,在此之前还可以做数据合适的转换和数据验证等.
	  处理完成后向DispatcherServlet返回一个ModelAndView对象
	6.前端控制器根据ModelAndView选择合适的视图解析器ViewResolver处理数据
	7.视图解析器根据model和view渲染视图,将结果返回给客户端
101. spring mvc 有哪些组件？
	1. DispatcherServlet 前端控制器
	2. HandlerMapping 请求派发,建立请求和处理器的映射
	3. Controller	处理器
	4. ModelAndView 封装模型和试图信息
	4. ViewResolver 视图处理器,定位页面
102. @RequestMapping 的作用是什么？
	映射请求,指定哪些URL可以被该处理器处理.
103. @Autowired 的作用是什么？
	根绝类型从容器中取出对象进行注入
十一、Spring Boot/Spring Cloud
104. 什么是 spring boot？
	可以认为是一个服务于框架的框架,简化了配置文件.整合了所有的框架
105. 为什么要用 spring boot？
	开发速度快
	测试简单
	配置简单
	部署简单
	可以基于springboot来构建springcloud生态
106. spring boot 核心配置文件是什么？
	application和bootstrap,application配置文件主要用于SpringBoot项目的自动化配置.
	bootstrap配置文件在使用spring cloud配置时使用
107. spring boot 配置文件有哪几种类型？它们有什么区别？
	两种:properties和yml.区别是格式不同
108. spring boot 有哪些方式可以实现热部署？
	两种方式:1:	Spring Loaded
			2:	Spring-boot-devtools
109. jpa 和 hibernate 有什么区别？
	jpa是一种规范,提供了一些列操作数据库的接口,本事不能直接使用
	hibernate是jpa的一种实现,是可以直接使用操作数据库的ORM框架
110. 什么是 spring cloud？
	springcloud是一个微服务框架,提供全套的分布式系统解决方案,它为微服务架构开发提供配置管理、服务治理、熔断机制、智能路由
	控制总线等一系列的管理操作.
111. spring cloud 断路器的作用是什么？
	在微服务架构中,存在很多的微服务,彼此之间存在依赖关系,当某个单元出现故障时,就会因为依赖关系导致整个系统的瘫痪.
	断路器的作用是当某个微服务发生故障时,通过断路器的故障监控,向调用方返回一个错误响应,使之不至于长时间等待,避免了故障在分布式系统中的蔓延
112. spring cloud 的核心组件有哪些？
	服务发现:	Netflix Eureka
	客户端负载均衡:	Netflix Ribbon
	断路器:	Netflix Hystrix
	服务网关:	Netflix Zuul
	分布式配置:	Spring cloud Config

十二、Hibernate
113. 为什么要使用 hibernate？
	1.对JDBC访问数据库的代码做了大量的封装,简化开发
	2.性能好,支持各种关系数据库.
114. 什么是 ORM 框架？
	ORM的意思是对象关系映射,它的作用是在关系型数据库和业务实体对象之间做映射
	这样我们在操作具体业务对象的时候,就不需要去和具体的SQL语句打交道,只需要操作对象的属性和方法.
115. hibernate 中如何在控制台查看打印的 sql 语句？
	在hibernate配置文件中配置hibernate.show_sql属性
116. hibernate 有几种查询方式？
	三种:HQL查询	QBC查询(也叫Criteria查询)  本地SQL查询
117. hibernate 实体类可以被定义为 final 吗？
	不能,因为hibernate使用代理方式在延迟加载的情况下提高性能,如果定义为final
	就不能继承,也就无法实现代理.
118. 在 hibernate 中使用 Integer 和 int 做映射有什么区别？
	1.如果数据库返回字段值是null的话,int类型会报错,Integer则不会
119. hibernate 是如何工作的？
	1.	通过Configuration config = new Configuration().configure();解析配置文件
	2.	由hibernate.cfg.xml中的<mapping resource="com/xx/User.hbm.xml"/>读取并解析映射信息
	3.	通过SessionFactory sf = config.buildSessionFactory();//创建SessionFactory
	4.	Session session = sf.openSession();//打开Sesssion
	5.	Transaction tx = session.beginTransaction();//创建并启动事务Transation
	6.	persistent operate操作数据，持久化操作
	7.	tx.commit();//提交事务
	8.	关闭session和sessionFactory
120. get()和 load()的区别？
	1.	get方式会直接触发sql语句查出对象,load方式会使用延迟加载的机制加载这个对象,此时是个代理对象
		只保存实体对象的id值,只有用到其他属性的时候才会调用sql查出来.
	2.	如果对象不存在,get方式会抛出空指针异常,load方式会抛出ObjectNotFoundException
121. 说一下 hibernate 的缓存机制？
	hibernate为了降低对数据库访问的频率,加入了缓存机制.缓存内的数据是对物理数据库数据的复制,
	应用程序在运行时,从缓存中读写数据.
	Hibernate的缓存包括两大类:session一级缓存和sessionFactory二级缓存.一级缓存不可卸载.
	当根据ID查询数据的时候,首先从session缓存中查,查不到,如果设置了二级缓存,那么从二级缓存中查,
	如果都查不到,再查数据库.将查到的数据按照ID放入缓存中,在删除,更新,增加数据的时候更新缓存.

122. hibernate 对象有哪些状态？
	Hibernate对象有三种状态
	1.	Transient 瞬时态, 此时对象刚new出来,还没有save()
	2.	Persistent 持久态, 调用了save方法或者游离态的对象调用了update方法后会变成持久态
		如果对象是持久化对象时，那么对该对象的任何修改，都会在提交事务时才会与之进行比较
	3.	当调用了session.clear()方法,以后 对象就会变成游离态
123. 在 hibernate 中 getCurrentSession 和 openSession 的区别是什么？
	1.	采用getCurrentSession()获得的session会绑定到当前线程,而openSession则不会
	2.	getCurrentSession()获得的session在commit或者rollback后会自动关闭,而openSession必须手动关闭
124. hibernate 实体类必须要有无参构造函数吗？为什么？
	必须要有,以为hibernate是通过反射的方式来获得对象实例的,此时会调用默认的无参构造.
十三、Mybatis
125. mybatis 中 #{}和 ${}的区别是什么？
	1.	前者会将传入的数据当成字符串,在之前加入双引号,后者是直接将数据显示在sql中
	2.	前者会当做占位符,防sql注入,后者不能
126. mybatis 有几种分页方式？
	两种,一种是内存分页,一种是物理分页
	内存分页:	一次性查询出所有满足条件的数据,临时保存在集合中,通过List的subList的方式获取分页数据.
	物理分页:	借助sql进行分页或者利用拦截器分页
127. RowBounds 是一次性查询全部结果吗？为什么？
	不是,因为mybatis是对JDBC的封装,在JDBC的驱动中有一个Fetch Size的配置,它规定了每次最多从数据库查询多少条数据.这样做可以防止内存溢出.
128. mybatis 逻辑分页和物理分页的区别是什么？
	1.	逻辑分页一次性查询很多数据,然后再结果中检索分页的数据,消耗内存.
	2.	物理分页是从数据库查询指定条数的数据.
129. mybatis 是否支持延迟加载？延迟加载的原理是什么？
	支持,在配置文件的<settings/>标签中设置<setting name="lazyLoadingEnabled" value="true"/>就可以激活
	原理:	在调用的时候出发加载,而不是在初始化的时候加载信息.如a.getB().getName(),如果a.getB()的值为null,会触发保存好的关联B对象的sql语句查询出B,然后再调用getName().

130. 说一下 mybatis 的一级缓存和二级缓存？
	1.	一级缓存是SqlSession级别的,在一个sqlsession中,第一次查询缓存中是否有数据,没有就会查询数据库,并将数据保存在一级缓存中.第二次去查的时候会直接从缓存中查询.如果这中间sqlsession进行了commit操作则会清空缓存.
	2.	二级缓存是Mapper级别的,多个sqlsession共享,默认关闭.它基于Mapper文件的namespace,如果两个mapper的namespace相同,那么会共享缓存的数据.使用二级缓存要在配置文件中开启,并且序列化po类.
131. mybatis 和 hibernate 的区别有哪些？
	1.	mybatis灵活,可以写sql,hibernate学习困难
132. mybatis 有哪些执行器（Executor）？
	1.	SimpleExecutor:每执行一次 update 或 select 就开启一个 Statement 对象，用完立刻关闭 Statement 对象
	2.	ReuseExecutor:执行update或select以SQL作为key查找Statement对象，存在就使用，不存在就创建，用完后不关闭,可以重复使用
	3.	BatchExecutor:执行update(没有select,jdbc批处理不支持select)时,将所有SQL都添加到批处理中(addBatch()),等待统一执行(executeBatch()),它缓存了多个Statement对象.
133. mybatis 分页插件的实现原理是什么？
	分页插件的基本原理是使用 MyBatis 提供的插件接口,实现自定义插件,在插件的拦截方法内拦截待执行的SQL,然后重写SQL,根据dialect方言,添加对应的物理分页语句和参数
134. mybatis 如何编写一个自定义插件？
	只需实现Interceptor接口，并指定要拦截的方法签名
	@Intercepts({
    @Signature(
        type=Executor.class,method="update",args={ MappedStatement.class,Object.class })})
	public class ExamplePlugin implements Interceptor {
	    public Object intercept(Invocation invocation) throws Throwable {
	       //自定义实现
	       return invocation.proceed();
	    }
	    public Object plugin(Object target){
	        return Plugin.wrap(target,this)
	    }
	    public void setProperties(Properties properties){
	      //传入配置项
	      String size = properties.getProperty("size");
	    }
	}
	<!-- mybatis-config.xml -->
	<plugins>
	    <plugin interceptor="org.mybatis.example.ExamplePlugin">
	        <!-- 这里的配置项就传入setProperties方法中 -->
	        <property name="size" value="100">
	    </plugin>
	</plugins>

十四、RabbitMQ
135. rabbitmq 的使用场景有哪些？
	1.	抢购活动，削峰填谷，防止系统崩塌。
	2.	延迟信息处理，比如 10 分钟之后给下单未付款的用户发送邮件提醒。
	3.	解耦系统
136. rabbitmq 有哪些重要的角色？
	生产者:	消息的创建者,负责创建和推送数据到消息服务器
	消费者:	消息的接收方,用于处理数据.
	代理:	MQ本身.
137. rabbitmq 有哪些重要的组件？
	ConnectionFactory(连接管理器):应用程序与Rabbit之间建立连接的管理器，程序代码中使用。
	Channel(信道):消息推送使用的通道.
	Exchange(交换器):用于接受、分配消息.
	Queue(队列):用于存储生产者的消息.
	RoutingKey(路由键):用于把生成者的数据分配到交换器上.
	BindingKey(绑定键):用于把交换器的消息绑定到队列上
138. rabbitmq 中 vhost 的作用是什么？
	每个 RabbitMQ 都能创建很多 vhost,我们称之为虚拟主机,每个虚拟主机其实都是 mini 版的RabbitMQ,它拥有自己的队列，交换器和绑定，拥有自己的权限机制。
139. rabbitmq 的消息是怎么发送的？
	首先客户端必须连接到 RabbitMQ 服务器才能发布和消费消息，客户端和 rabbit server 之间会创建一个 tcp 连接，一旦 tcp 打开并通过了认证（认证就是你发送给 rabbit 服务器的用户名和密码），你的客户端和 RabbitMQ 就创建了一条 amqp 信道（channel），信道是创建在“真实” tcp 上的虚拟连接，amqp 命令都是通过信道发送出去的，每个信道都会有一个唯一的 id，不论是发布消息，订阅队列都是通过这个信道完成的。
140. rabbitmq 怎么保证消息的稳定性？
	1.	提供了事物功能
	2.	通过将 channel 设置为 confirm（确认）模式。
141.rabbitmq 怎么避免消息丢失？
	1.	把消息持久化磁盘，保证服务器重启消息不丢失。
	2.	每个集群中至少有一个物理磁盘，保证消息落入磁盘
142. 要保证消息持久化成功的条件有哪些？
	1.	声明队列必须设置持久化 durable 设置为 true.
	2.	消息推送投递模式必须设置持久化，deliveryMode 设置为 2（持久）。
	3.	消息已经到达持久化交换器。
	4.	消息已经到达持久化队列。
	以上四个条件都满足才能保证消息持久化成功
143. rabbitmq 持久化有什么缺点？
	因为使用了磁盘来存储而不是内存,所以降低了服务器的吞吐量.
144. rabbitmq 有几种广播类型？
	direct(默认方式):	最基础最简单的模式，发送方把消息发送给订阅方，如果有多个订阅者，默认采取轮询的方式进行消息发送。
	headers:	与 direct 类似，只是性能很差
	fanout(分发模式):	把消费分发给所有订阅者
	topic:	匹配订阅模式，使用正则匹配到消息队列，能匹配到的都能接收到。
145. rabbitmq 怎么实现延迟消息队列？
	1.	通过消息过期后进入死信交换器，再由交换器转发到延迟消费队列，实现延迟功能
	2.	使用 RabbitMQ-delayed-message-exchange 插件实现延迟功能。
146. rabbitmq 集群有什么用？
	高可用：某个服务器出现问题，整个 RabbitMQ 还可以继续使用；
	高容量：集群可以承载更多的消息量。
147. rabbitmq 节点的类型有哪些？
	磁盘节点：消息会存储到磁盘
	内存节点：消息都存储在内存中，重启服务器消息丢失，性能高于磁盘类型
148. rabbitmq 集群搭建需要注意哪些问题？
	1.	各节点之间使用“--link”连接，此属性不能忽略。
	2.	各节点使用的 erlang cookie 值必须相同，此值相当于“秘钥”的功能，用于各节点的认证。
	3.	整个集群中必须包含一个磁盘节点。
149. rabbitmq 每个节点是其他节点的完整拷贝吗？为什么？
	不是,原因如下:
		存储空间的考虑：如果每个节点都拥有所有队列的完全拷贝，这样新增节点不但没有新增存储空间，反而增加了更多的冗余数据；
		性能的考虑：如果每条消息都需要完整拷贝到每一个集群节点，那新增节点并没有提升处理消息的能力，最多是保持和单节点相同的性能甚至是更糟。
150. rabbitmq 集群中唯一一个磁盘节点崩溃了会发生什么情况？
	唯一磁盘节点崩溃了，集群是可以保持运行的，但你不能更改任何东西。
	不能创建队列
	不能创建交换器
	不能创建绑定
	不能添加用户
	不能更改权限
	不能添加和删除集群节点
151. rabbitmq 对集群节点停止顺序有要求吗？
	有要求,应该先关闭内存节点,最后关闭磁盘节点,如果顺序相反可能会造成消息丢失.
十五、Kafka
152. kafka 可以脱离 zookeeper 单独使用吗？为什么？
	不能,因为zookeeper管理和协调kafka的节点服务器.
153. kafka 有几种数据保留的策略？
	两种,一种是按照过期时间保留,一种是按照存储消息的大小保留.
154. kafka 同时设置了 7 天和 10G 清除数据，到第五天的时候消息达到了 10G，这个时候 kafka 将如何处理？
	会执行清除,时间和大小满足一个就会执行清除.
155. 什么情况会导致 kafka 运行变慢？
	cpu 性能瓶颈
	磁盘读写瓶颈
	网络瓶颈
156. 使用 kafka 集群需要注意什么？
	集群的数量不是越多越好，最好不要超过 7 个，因为节点越多，消息复制需要的时间就越长，整个群组的吞吐量就越低。
	集群数量最好是单数，因为超过一半故障集群就不能用了，设置为单数容错率更高。
十六、Zookeeper
157. zookeeper 是什么？
	zookeeper 是一个分布式的，开放源码的分布式应用程序协调服务,是 hadoop 和 hbase 的重要组件,提供的功能包括：配置维护、域名服务、分布式同步、组服务等。
158. zookeeper 都有哪些功能？
	集群管理：监控节点存活状态、运行请求等
	主节点选举：主节点挂掉了之后可以从备用的节点开始新一轮选主，主节点选举说的就是这个选举的过程，使用 zookeeper 可以协助完成这个过程。
	分布式锁：zookeeper 提供两种锁：独占锁、共享锁。独占锁即一次只能有一个线程使用资源，共享锁是读锁共享，读写互斥，即可以有多线线程同时读同一个资源，如果要使用写锁也只能有一个线程使用。zookeeper可以对分布式锁进行控制
159. zookeeper 有几种部署模式？
	三种:
	单机部署：一台集群上运行；
	集群部署：多台集群运行；
	伪集群部署：一台集群启动多个 zookeeper 实例运行。
160. zookeeper 怎么保证主从节点的状态同步？
	zookeeper 的核心是原子广播，这个机制保证了各个 server 之间的同步。实现这个机制的协议叫做 zab 协议。zab 协议有两种模式，分别是恢复模式（选主）和广播模式（同步）。当服务启动或者在领导者崩溃后，zab 就进入了恢复模式，当领导者被选举出来，且大多数 server 完成了和 leader 的状态同步以后，恢复模式就结束了。状态同步保证了 leader 和 server 具有相同的系统状态。
161. 集群中为什么要有主节点？
	在分布式环境中，有些业务逻辑只需要集群中的某一台机器进行执行，其他的机器可以共享这个结果，这样可以大大减少重复计算，提高性能，所以就需要主节点。
162. 集群中有 3 台服务器，其中一个节点宕机，这个时候 zookeeper 还可以使用吗？
	可以继续使用，单数服务器只要没超过一半的服务器宕机就可以继续使用。
163. 说一下 zookeeper 的通知机制？
	客户端端会对某个 znode 建立一个 watcher 事件，当该 znode 发生变化时，这些客户端会收到 zookeeper 的通知，然后客户端可以根据 znode 变化来做出业务上的改变。
十七、MySql
164. 数据库的三范式是什么？
	第一范式：强调的是列的原子性，即数据库表的每一列都是不可分割的原子数据项。
	第二范式：要求实体的属性完全依赖于主关键字。所谓完全依赖是指不能存在仅依赖主关键字一部分的属性。
	第三范式：任何非主属性不依赖于其它非主属性
165. 一张自增表里面总共有 7 条数据，删除了最后 2 条数据，重启 mysql 数据库，又插入了一条数据，此时 id 是几？
	表类型如果是 MyISAM ，那 id 就是 8。
	表类型如果是 InnoDB，那 id 就是 6。
	InnoDB 表只会把自增主键的最大 id 记录在内存中，所以重启之后会导致最大 id 丢失。
166. 如何获取当前数据库版本？
	使用 select version() 获取当前 MySQL 数据库版本。
167. 说一下 ACID 是什么？
	Atomicity（原子性）	一个事务（transaction）中的所有操作，或者全部完成，或者全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被恢复（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。即，事务不可分割、不可约简。
	Consistency（一致性）	在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设约束、触发器、级联回滚等。
	Isolation（隔离性）	数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
	Durability（持久性）	事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。
168. char 和 varchar 的区别是什么？
	char固定长度,比如char(10) 当输入abc三个字符时,他们占的空间还是10个字节,其他7个字节是空的.
	chat 优点：效率高；缺点：占用空间；适用场景：存储密码的 md5 值，固定长度的，使用 char 非常合适。
	varchar(n) ：可变长度，存储的值是每个值占用的字节再加上一个用来记录其长度的字节的长度。
169. float 和 double 的区别是什么？
	float 最多可以存储 8 位的十进制数，并在内存中占 4 字节。
	double 最可可以存储 16 位的十进制数，并在内存中占 8 字节。
170. mysql 的内连接、左连接、右连接有什么区别？
	1.	关键字不一样.	内连接关键字：inner join；左连接：left join；右连接：right join。
	2.	内连接是把匹配的关联数据显示出来；左连接是左边的表全部显示出来，右边的表显示出符合条件的数据；右连接正好相反。
171. mysql 索引是怎么实现的？
	索引是满足某种特定查找算法的数据结构，而这些数据结构会以某种方式指向数据，从而实现高效查找数据。
	具体来说 MySQL 中的索引，不同的数据引擎实现有所不同，但目前主流的数据库引擎的索引都是 B+ 树实现的，B+ 树的搜索效率，可以到达二分法的性能，找到数据区域之后就找到了完整的数据结构了，所有索引的性能也是更好的。
172. 怎么验证 mysql 的索引是否满足需求？
	使用 explain 查看 SQL 是如何执行查询语句的，从而分析你的索引是否满足需求。
	explain 语法：explain select * from table where type=1。
173. 说一下数据库的事务隔离？
	MySQL 的事务隔离是在 MySQL. ini 配置文件里添加的，在文件的最后添加：
	transaction-isolation = REPEATABLE-READ
	可用的配置值：READ-UNCOMMITTED、READ-COMMITTED、REPEATABLE-READ、SERIALIZABLE。
174. 说一下 mysql 常用的引擎？
	InnoDB 引擎：InnoDB 引擎提供了对数据库 acid 事务的支持，并且还提供了行级锁和外键的约束，它的设计的目标就是处理大数据容量的数据库系统。MySQL 运行的时候，InnoDB 会在内存中建立缓冲池，用于缓冲数据和索引。但是该引擎是不支持全文搜索，同时启动也比较的慢，它是不会保存表的行数的，所以当进行 select count(*) from table 指令的时候，需要进行扫描全表。由于锁的粒度小，写操作是不会锁定全表的,所以在并发度较高的场景下使用会提升效率的。
	MyIASM 引擎：MySQL 的默认引擎，但不提供事务的支持，也不支持行级锁和外键。因此当执行插入和更新语句时，即执行写操作的时候需要锁定这个表，所以会导致效率会降低。不过和 InnoDB 不同的是，MyIASM 引擎是保存了表的行数，于是当进行 select count(*) from table 语句时，可以直接的读取已经保存的值而不需要进行扫描全表。所以，如果表的读操作远远多于写操作时，并且不需要事务的支持的，可以将 MyIASM 作为数据库引擎的首选。
175. 说一下 mysql 的行锁和表锁？
	表级锁：开销小，加锁快，不会出现死锁。锁定粒度大，发生锁冲突的概率最高，并发量最低
	行级锁：开销大，加锁慢，会出现死锁。锁力度小，发生锁冲突的概率小，并发度最高。
176. 说一下乐观锁和悲观锁？
	乐观锁：每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在提交更新的时候会判断一下在此期间别人有没有去更新这个数据。
	悲观锁：每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻止，直到这个锁被释放。
	数据库的乐观锁需要自己实现，在表里面添加一个 version 字段，每次修改成功值加 1，这样每次修改的时候先对比一下，自己拥有的 version 和数据库现在的 version 是否一致，如果不一致就不修改，这样就实现了乐观锁。
177. mysql 问题排查都有哪些手段？
	使用 show processlist 命令查看当前所有连接信息。
	使用 explain 命令查询 SQL 语句执行计划。
	开启慢查询日志，查看慢查询的 SQL。
178. 如何做 mysql 的性能优化？
	为搜索字段创建索引。
	避免使用 select *，列出需要查询的字段。
	垂直分割分表。
	选择正确的存储引擎。
十八、Redis
179. redis 是什么？都有哪些使用场景？
	Redis 是一个使用 C 语言开发的高速缓存数据库。
	记录帖子点赞数、点击数、评论数；
	缓存近期热帖；
	缓存文章详情信息；
	记录用户会话信息。
180. redis 有哪些功能？
	数据缓存功能
	分布式锁的功能
	支持数据持久化
	支持事务
	支持消息队列
181. redis 和 memecache 有什么区别？
	存储方式不同：memcache 把数据全部存在内存之中，断电后会挂掉，数据不能超过内存大小；Redis 有部份存在硬盘上，这样能保证数据的持久性。
	数据支持类型：memcache 对数据类型支持相对简单；Redis 有复杂的数据类型
	value 值大小不同：Redis 最大可以达到 1gb；memcache 只有 1mb。
182. redis 为什么是单线程的？
	因为 cpu 不是 Redis 的瓶颈，Redis 的瓶颈最有可能是机器内存或者网络带宽。既然单线程容易实现，而且 cpu 又不会成为瓶颈，那就顺理成章地采用单线程的方案了。
183. 什么是缓存穿透？怎么解决？
	缓存穿透：指查询一个一定不存在的数据，由于缓存是不命中时需要从数据库查询，查不到数据则不写入缓存，这将导致这个不存在的数据每次请求都要到数据库去查询，造成缓存穿透。
	解决方案：最简单粗暴的方法如果一个查询返回的数据为空（不管是数据不存在，还是系统故障），我们就把这个空结果进行缓存，但它的过期时间会很短，最长不超过五分钟。
184. redis 支持的数据类型有哪些？
	edis 支持的数据类型：string（字符串）、list（列表）、hash（字典）、set（集合）、zset（有序集合）。
185. redis 支持的 java 客户端都有哪些？
	支持的 Java 客户端有 Redisson、jedis、lettuce 等。
186. jedis 和 redisson 有哪些区别？
	jedis：提供了比较全面的 Redis 命令的支持。
	Redisson：实现了分布式和可扩展的 Java 数据结构，与 jedis 相比 Redisson 的功能相对简单，不支持排序、事务、管道、分区等 Redis 特性。
187. 怎么保证缓存和数据库数据的一致性？
	合理设置缓存的过期时间
	新增、更改、删除数据库操作时同步更新 Redis，可以使用事物机制来保证数据的一致性。
188. redis 持久化有几种方式？
	RDB（Redis Database）：指定的时间间隔能对你的数据进行快照存储。
	AOF（Append Only File）：每一个收到的写命令都通过write函数追加到文件中。
189.redis 怎么实现分布式锁？
	Redis 分布式锁其实就是在系统里面占一个“坑”，其他程序也要占“坑”的时候，占用成功了就可以继续执行，失败了就只能放弃或稍后重试。
	一般使用 setnx(set if not exists)指令,只允许被一个程序占有，使用完调用 del 释放锁。
190. redis 分布式锁有什么缺陷？
	Redis 分布式锁不能解决超时的问题，分布式锁有一个超时时间，程序的执行如果超出了锁的超时时间就会出现问题。
191. redis 如何做内存优化？
	尽量使用 Redis 的散列表，把相关的信息放到散列表里面存储，而不是把每个字段单独存储，这样可以有效的减少内存使用。比如将 Web 系统的用户对象，应该放到散列表里面再整体存储到 Redis，而不是把用户的姓名、年龄、密码、邮箱等字段分别设置 key 进行存储。
192. redis 淘汰策略有哪些？
	volatile-lru：从已设置过期时间的数据集（server. db[i]. expires）中挑选最近最少使用的数据淘汰。
	volatile-ttl：从已设置过期时间的数据集（server. db[i]. expires）中挑选将要过期的数据淘汰。
	volatile-random：从已设置过期时间的数据集（server. db[i]. expires）中任意选择数据淘汰。
	allkeys-lru：从数据集（server. db[i]. dict）中挑选最近最少使用的数据淘汰。
	allkeys-random：从数据集（server. db[i]. dict）中任意选择数据淘汰。
	no-enviction（驱逐）：禁止驱逐数据。
193. redis 常见的性能问题有哪些？该如何解决？
	主服务器写内存快照，会阻塞主线程的工作，当快照比较大时对性能影响是非常大的，会间断性暂停服务，所以主服务器最好不要写内存快照。
	Redis 主从复制的性能问题，为了主从复制的速度和连接的稳定性，主从库最好在同一个局域网内。

十九、JVM
194. 说一下 jvm 的主要组成部分？及其作用？
	类加载器（ClassLoader）
	运行时数据区（Runtime Data Area）
	执行引擎（Execution Engine）
	本地库接口（Native Interface）
	首先通过类加载器（ClassLoader）会把 Java 代码转换成字节码，运行时数据区（Runtime Data Area）再把字节码加载到内存中，而字节码文件只是 JVM 的一套指令集规范，并不能直接交个底层操作系统去执行，因此需要特定的命令解析器执行引擎（Execution Engine），将字节码翻译成底层系统指令，再交由 CPU 去执行，而这个过程中需要调用其他语言的本地库接口（Native Interface）来实现整个程序的功能。
195. 说一下 jvm 运行时数据区？
	不同虚拟机的运行时数据区可能略微有所不同，但都会遵从 Java 虚拟机规范， Java 虚拟机规范规定的区域分为以下 5 个部分：
	程序计数器（Program Counter Register）：当前线程所执行的字节码的行号指示器，字节码解析器的工作是通过改变这个计数器的值，来选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复等基础功能，都需要依赖这个计数器来完成
	Java 虚拟机栈（Java Virtual Machine Stacks）：用于存储局部变量表、操作数栈、动态链接、方法出口等信息；
	本地方法栈（Native Method Stack）：与虚拟机栈的作用是一样的，只不过虚拟机栈是服务 Java 方法的，而本地方法栈是为虚拟机调用 Native 方法服务的
	Java 堆（Java Heap）：Java 虚拟机中内存最大的一块，是被所有线程共享的，几乎所有的对象实例都在这里分配内存；
	方法区（Methed Area）：用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译后的代码等数据。
196. 说一下堆栈的区别？
	功能方面：堆是用来存放对象的，栈是用来执行程序的。
	共享性：堆是线程共享的，栈是线程私有的。
	空间大小：堆大小远远大于栈。
197. 队列和栈是什么？有什么区别？
	队列和栈都是被用来预存储数据的。
	队列允许先进先出检索元素，但也有例外的情况，Deque 接口允许从两端检索元素。
	栈和队列很相似，但它运行对元素进行后进先出进行检索。
198. 什么是双亲委派模型？
	在介绍双亲委派模型之前先说下类加载器。对于任意一个类，都需要由加载它的类加载器和这个类本身一同确立在 JVM 中的唯一性，每一个类加载器，都有一个独立的类名称空间。类加载器就是根据指定全限定名称将 class 文件加载到 JVM 内存，然后再转化为 class 对象。
	启动类加载器（Bootstrap ClassLoader），是虚拟机自身的一部分，用来加载Java_HOME/lib/目录中的，或者被 -Xbootclasspath 参数所指定的路径中并且被虚拟机识别的类库；
	扩展类加载器（Extension ClassLoader）：负责加载\lib\ext目录或Java. ext. dirs系统变量指定的路径中的所有类库；
	应用程序类加载器（Application ClassLoader）。负责加载用户类路径（classpath）上的指定类库，我们可以直接使用这个类加载器。一般情况，如果我们没有自定义类加载器默认就是用这个加载器。
	双亲委派模型：如果一个类加载器收到了类加载的请求，它首先不会自己去加载这个类，而是把这个请求委派给父类加载器去完成，每一层的类加载器都是如此，这样所有的加载请求都会被传送到顶层的启动类加载器中，只有当父加载无法完成加载请求（它的搜索范围中没找到所需的类）时，子加载器才会尝试去加载类。
199. 说一下类加载的执行过程？
	加载：根据查找路径找到相应的 class 文件然后导入；
	检查：检查加载的 class 文件的正确性;
	准备：给类中的静态变量分配内存空间；
	解析：虚拟机将常量池中的符号引用替换成直接引用的过程。符号引用就理解为一个标示，而在直接引用直接指向内存中的地址
	初始化：对静态变量和静态代码块执行初始化工作。
200. 怎么判断对象是否可以被回收？
	一般有两种方法来判断：
	引用计数器：为每个对象创建一个引用计数，有对象引用时计数器 +1，引用被释放时计数 -1，当计数器为 0 时就可以被回收。它有一个缺点不能解决循环引用的问题；
	可达性分析：从 GC Roots 开始向下搜索，搜索所走过的路径称为引用链。当一个对象到 GC Roots 没有任何引用链相连时，则证明此对象是可以被回收的。
201. java 中都有哪些引用类型？
	强引用：发生 gc 的时候不会被回收
	软引用：有用但不是必须的对象，在发生内存溢出之前会被回收。
	弱引用：有用但不是必须的对象，在下一次GC时会被回收。
	虚引用（幽灵引用/幻影引用）：无法通过虚引用获得对象，用 PhantomReference 实现虚引用，虚引用的用途是在 gc 时返回一个通知。
202. 说一下 jvm 有哪些垃圾回收算法？
	标记-清除算法：标记无用对象，然后进行清除回收。缺点：效率不高，无法清除垃圾碎片。
	标记-整理算法：标记无用对象，让所有存活的对象都向一端移动，然后直接清除掉端边界以外的内存。
	复制算法：按照容量划分二个大小相等的内存区域，当一块用完的时候将活着的对象复制到另一块上，然后再把已使用的内存空间一次清理掉。缺点：内存使用率不高，只有原来的一半。
	分代算法：根据对象存活周期的不同将内存划分为几块，一般是新生代和老年代，新生代基本采用复制算法，老年代采用标记整理算法。
203. 说一下 jvm 有哪些垃圾回收器？
	Serial：最早的单线程串行垃圾回收器。
	Serial Old：Serial 垃圾回收器的老年版本，同样也是单线程的，可以作为 CMS 垃圾回收器的备选预案。
	ParNew：是 Serial 的多线程版本。
	Parallel 和 ParNew 收集器类似是多线程的，但 Parallel 是吞吐量优先的收集器，可以牺牲等待时间换取系统的吞吐量。
	Parallel Old 是 Parallel 老生代版本，Parallel 使用的是复制的内存回收算法，Parallel Old 使用的是标记-整理的内存回收算法。
	CMS：一种以获得最短停顿时间为目标的收集器，非常适用 B/S 系统。
	G1：一种兼顾吞吐量和停顿时间的 GC 实现，是 JDK 9 以后的默认 GC 选项。
204. 详细介绍一下 CMS 垃圾回收器？
	CMS 是英文 Concurrent Mark-Sweep 的简称，是以牺牲吞吐量为代价来获得最短回收停顿时间的垃圾回收器。对于要求服务器响应速度的应用上，这种垃圾回收器非常适合。在启动 JVM 的参数加上“-XX:+UseConcMarkSweepGC”来指定使用 CMS 垃圾回收器。
	CMS 使用的是标记-清除的算法实现的，所以在 gc 的时候回产生大量的内存碎片，当剩余内存不能满足程序运行要求时，系统将会出现 Concurrent Mode Failure，临时 CMS 会采用 Serial Old 回收器进行垃圾清除，此时的性能将会被降低。
205. 新生代垃圾回收器和老生代垃圾回收器都有哪些？有什么区别？
	新生代回收器：Serial、ParNew、Parallel Scavenge
	老年代回收器：Serial Old、Parallel Old、CMS
	整堆回收器：G1
206. 简述分代垃圾回收器是怎么工作的？
	分代回收器有两个分区：老生代和新生代，新生代默认的空间占比总空间的 1/3，老生代的默认占比是 2/3。
	新生代使用的是复制算法，新生代里有 3 个分区：Eden、To Survivor、From Survivor，它们的默认占比是 8:1:1，它的执行流程如下：
		把 Eden + From Survivor 存活的对象放入 To Survivor 区；
		清空 Eden 和 From Survivor 分区；
		From Survivor 和 To Survivor 分区交换，From Survivor 变 To Survivor，To Survivor 变 From Survivor。
	每次在 From Survivor 到 To Survivor 移动时都存活的对象，年龄就 +1，当年龄到达 15（默认配置是 15）时，升级为老生代。大对象也会直接进入老生代。
	老生代当空间占用到达某个值之后就会触发全局垃圾收回，一般使用标记整理的执行算法。以上这些循环往复就构成了整个分代垃圾回收的整体执行流程。	
207. 说一下 jvm 调优的工具？
	jconsole：用于对 JVM 中的内存、线程和类等进行监控；
	jvisualvm：JDK 自带的全能分析工具，可以分析：内存快照、线程快照、程序死锁、监控内存的变化、gc 变化等。
208. 常用的 jvm 调优的参数都有哪些？
	-Xms2g：初始化推大小为 2g；
	-Xmx2g：堆最大内存为 2g；
	-XX:NewRatio=4：设置年轻的和老年代的内存比例为 1:4
	-XX:SurvivorRatio=8：设置新生代 Eden 和 Survivor 比例为 8:2；
	–XX:+UseParNewGC：指定使用 ParNew + Serial Old 垃圾回收器组合；
	-XX:+UseParallelOldGC：指定使用 ParNew + ParNew Old 垃圾回收器组合；
	-XX:+UseConcMarkSweepGC：指定使用 CMS + Serial Old 垃圾回收器组合；
	-XX:+PrintGC：开启打印 gc 信息；
	-XX:+PrintGCDetails：打印 gc 详细信息。
--------------------- 
209. CAS的缺点.
	java中的Atomic类可以保证对数据操作的原子性.
	比如i++这种操作,可以使用AtomicInteger类来保证
	在AtomicInteger类的getAndIncrement()方法中,使用了CAS的思想
	底层依靠Unsafe来实现的.
	缺点: 	1.循环时间长,开销大
			2.只能保证一个共享变量的原子操作
			3.会出现ABA问题	
210. ABA问题是什么?如何规避?
	比如两个线程a和b, 他们都从主内存中拷贝一个int i = 5进行操作.
	其中因为线程b的逻辑比较简单,先将i变成了8,此时,a线程还没有运行完,在这个时候
	b线程又将i变成了5.此时a线程进行CAS自旋发现i=5,没有变化,因此进行了更新.但是
	在这个中间,变量i是有变化的.

	如何解决ABA问题?------------------对值的修改加版本号(类似时间戳)就可以解决.
	可以使用j.u.c中的AtomicStampedReference来解决.
	AtomicStampedReference采用原子引用+版本的号的方式,在构造AtomincStamicRefrence的
	时候可以指定多个参数,包含要包括的引用,还有初始版本号,在使用的时候要指定期望的版本号和要修改的版本号
211. 公平锁、非公平锁、可重入锁、递归锁、自旋锁的理解?
	公平锁:		多个线程按照申请锁的顺序来获取锁.
	非公平锁:	多个线程获取锁的顺序并不是按照申请锁的顺序,在高并发情况下,有可能后申请的先获得锁
	在Lock lock = new ReentrantLock()中,构造中传入true代表公平锁,false代表非公平锁.默认非公平
	Synchronized是一种非公平锁

	可重入锁,也叫递归锁:	同一线程外层函数获得锁以后,内层递归函数仍然能够获取该锁的代码
							即,线程可以进入任何一个它已经拥有的锁同步着的代码块.
							ReentrantLock和Synchronized都是可重入锁

	自旋锁:		尝试获取锁的线程不会立即阻塞,而是采用循环的方式去尝试获取锁,这样可以减少
				上线文切换的消耗,但是循环会消耗CPU.
	自己实现自旋锁:
		public class LockDemo {
			AtominReference<Thread> atomic = new AtomicReference<>();

			public void myLock() {
				//获得当前线程
				Thread thread = Thread.currentThread();
				while (!atomic.compareAndSet(null, thread)) {

				}
			}

			public void myUnlock() {
				Thread thread = Thread.currentThread();
				atomic.compareAndSet(thread, null);
			}
		}

	独占锁:		锁一次只能被一个线程所持有.ReentrantLock和synchronized都是独占锁
	共享锁:		锁可以被多个线程持有.
	读写锁:		多个线程共享一个资源类,读操作允许多线程共同执行,但是写操作只允许一个线程操作
			自定义实现读写锁:可以使用j.u.c包下的ReentrantReadWriteLock类来实现读写锁
			ReentrantReadWriteLock.writeLock().lock()添加在写操作的方法中,并在finally中释放锁.
			ReentrantReadWriteLock.readLock().lock()添加在读操作中,就可以实现读操作共享.
