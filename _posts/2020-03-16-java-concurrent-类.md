
locks部分：显式锁(互斥锁和速写锁)相关；
atomic部分：原子变量类相关，是构建非阻塞算法的基础；
executor部分：线程池相关；
collections部分：并发容器相关；
tools部分：同步工具相关，如信号量、闭锁、栅栏等功能；

Executor
        建立线程池，执行线程
        ThreadPoolExecutor：线程池的实现类
        ExecutorService：建立线程池
        Future：对Runnable或Callable执行结果进行取消、查询是否完成、获取结果
        Callable：与Runnable功能一样，有返回值
BlockingQueue
        阻塞队列
        场景：socket客户端数据的读取和解析，生产者消费者问题
ConcurrentMap
        对访问进行并发处理
        ConcurrentMap与HashTable对比
Semphore
        信号量，保护对一个或多个共享资源的访问
CountDownLatch
        在完成一组正在其他线程执行的操作之前，允许线程一直等待



ReentrantLock 
Condition 
Semaphore 
ReadWriteLock  
CountDownLatch 
CyclicBarrier 
LockSupport 
concurrentHashMap
blockingQueue
