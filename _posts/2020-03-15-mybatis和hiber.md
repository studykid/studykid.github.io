# mybatis 中 #{}和 ${}的区别是什么？1.#{}是预编译处理，${}是字符串替换。
Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；
Mybatis在处理${}时，就是把${}替换成变量的值。


2.使用#{}可以有效的防止SQL注入，提高系统安全性。
MyBatis排序时使用order by 动态参数时需要注意，用$而不是#

1. #将传入的数据都当成一个字符串，会对自动传入的数据加一个双引号。
2. $将传入的数据直接显示生成在sql中。
3. #方式能够很大程度防止sql注入。
4.$方式无法防止Sql注入。
5.$方式一般用于传入数据库对象，例如传入表名。
6. #{}方式一般用于传入字段值。
7.一般能用#的就别用$

# mybatis 有几种分页方式？
mubatis generator

pagehelper
RowBounds
或者是参数pagenum pagesize
# RowBounds 是一次性查询全部结果吗？为什么？
RowBounds 表面是在“所有”数据中检索数据，其实并非是一次性查询出所有数据，因为 MyBatis 是对 jdbc 的封装，在 jdbc 驱动中有一个 Fetch Size 的配置，它规定了每次最多从数据库查询多少条数据，假如你要查询更多数据，它会在你执行 next()的时候，去查询更多的数据。就好比你去自动取款机取 10000 元，但取款机每次最多能取 2500 元，所以你要取 4 次才能把钱取完。只是对于 jdbc 来说，当你调用 next()的时候会自动帮你完成查询工作。这样做的好处可以有效的防止内存溢出。

# mybatis 逻辑分页和物理分页的区别是什么？
分页方式：逻辑分页和物理分页。

逻辑分页： 使用 MyBatis 自带的 RowBounds 进行分页，它是一次性查询很多数据，然后在数据中再进行检索。

物理分页： 自己手写 SQL 分页或使用分页插件 PageHelper，去数据库查询指定条数的分页数据的形式。
    逻辑分页是一次性查询很多数据，然后再在结果中检索分页的数据。这样做弊端是需要消耗大量的内存、有内存溢出的风险、对数据库压力较大。
    物理分页是从数据库查询指定条数的数据，弥补了一次性全部查出的所有数据的种种缺点，比如需要大量的内存，对数据库查询压力较大等问题。




# mybatis 是否支持延迟加载？延迟加载的原理是什么？
MyBatis 支持延迟加载，设置 lazyLoadingEnabled=true 即可。

延迟加载的原理的是调用的时候触发加载，而不是在初始化的时候就加载信息。比如调用 a. getB(). getName()，这个时候发现 a. getB() 的值为 null，此时会单独触发事先保存好的关联 B 对象的 SQL，先查询出来 B，然后再调用 a. setB(b)，而这时候再调用 a. getB(). getName() 就有值了，这就是延迟加载的基本原理。


# 说一下 mybatis 的一级缓存和二级缓存？    一级缓存：基于 PerpetualCache 的 HashMap 本地缓存，它的声明周期是和 SQLSession 一致的，有多个 SQLSession 或者分布式的环境中数据库操作，可能会出现脏数据。当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认一级缓存是开启的。
    二级缓存：也是基于 PerpetualCache 的 HashMap 本地缓存，不同在于其存储作用域为 Mapper 级别的，如果多个SQLSession之间需要共享缓存，则需要使用到二级缓存，并且二级缓存可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现 Serializable 序列化接口(可用来保存对象的状态)。

开启二级缓存数据查询流程：二级缓存 -> 一级缓存 -> 数据库。

缓存更新机制：当某一个作用域(一级缓存 Session/二级缓存 Mapper)进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear。


# mybatis 和 hibernate 的区别有哪些？
灵活性：MyBatis 更加灵活，自己可以写 SQL 语句，使用起来比较方便。
可移植性：MyBatis 有很多自己写的 SQL，因为每个数据库的 SQL 可以不相同，所以可移植性比较差。
学习和使用门槛：MyBatis 入门比较简单，使用门槛也更低。
二级缓存：hibernate 拥有更好的二级缓存，它的二级缓存可以自行更换为第三方的二级缓存。


# mybatis 有哪些执行器（Executor）？

Mybatis有三种基本的Executor执行器:
          SimpleExecutor、ReuseExecutor、BatchExecutor。

SimpleExecutor：每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。

ReuseExecutor：执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map内，供下一次使用。简言之，就是重复使用Statement对象。

BatchExecutor：执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。与JDBC批处理相同。




# 、Hibernate
# .为什么要使用 hibernate？
# 115.hibernate 中如何在控制台查看打印的 sql 语句？
# .hibernate 有几种查询方式？
# .hibernate 实体类可以被定义为 final 吗？
# 119.hibernate 是如何工作的？
# .get()和 load()的区别？
# .说一下 hibernate 的缓存机制？
# .hibernate 对象有哪些状态？
# .在 hibernate 中 getCurrentSession 和 openSession 的区别是什么？
# .hibernate 实体类必须要有无参构造函数吗？为什么？


作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。

Mybatis中如何指定使用哪一种Executor执行器？

答：在Mybatis配置文件中，可以指定默认的ExecutorType执行器类型，也可以手动给DefaultSqlSessionFactory的创建SqlSession的方法传递ExecutorType类型参数。

# mybatis 分页插件的实现原理是什么？

# mybatis 如何编写一个自定义插件？
