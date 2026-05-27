# Java 学习体系

## JavaSE（重点）
- 集合
- 迭代器
- 泛型
- 反射
- 动态代理
- JDK 新特性

## JavaSE（扩展）
- String 类底层如何实现
- String 为什么设计为不可变的
- 字符串常量池
- String / StringBuffer / StringBuilder 的区别
- 深拷贝 & 浅拷贝
- Error 和 Exception 的区别
- 异常的分类和区别
- throw 与 throws 的核心区别
- finally 中的代码一定会被执行吗
- AIO / BIO / NIO

## JUC（重点）
- 线程
- 线程池
- 怎么理解线程安全
- ThreadLocal
- synchronized
- ReentrantLock
- CAS
- 乐观锁 & 悲观锁
- JMM
- 多线程交替打印
- 多线程交替打印 ABC

## JUC（扩展）
- 多线程的上下文切换
- 原子类
- Unsafe

## JVM（重点）
- 内存结构 / 运行时数据区
- 创建对象一定分配在堆里吗
- 垃圾回收
- 垃圾回收器
- 根可达性算法
- 三色标记法
- 双亲委派
- JVM 调优经验

## JVM（扩展）
- 编译 & 解释
- JIT 编译器
- 类的生命周期
- 为什么区分堆和栈
- 如何选择垃圾回收器

## MySQL（重点）
- 事务
- 如何理解 MVCC
- B+ 树索引
- 索引失效的情况
- 日志（RedoLog / UndoLog / BinLog）
- 执行 SQL 查询语句的过程
- 执行计划的分析
- SQL 优化最佳实践

## MySQL（扩展）
- InnoDB 和 MyISAM 的区别
- 主从复制
- RR 和 RC 的区别
- 为什么互联网公司选择使用 RC
- 查询关键字的执行顺序
- 聚簇索引和非聚簇索引

## Redis（重点）
- 数据类型
- 分布式锁
- 持久化
- 内存淘汰策略
- 缓存击穿 / 穿透 / 雪崩
- 热 Key 问题
- 大 Key 问题
- Redis 高可用
- 主从数据同步原理与优化实践

## Redis（扩展）
- Redis 为什么这么快
- Redis 是单线程还是多线程
- 为什么使用单线程执行命令
- 为什么引入多线程
- Redis 是 AP 还是 CP
- 是否支持事务 / 事务回滚

## Kafka（重点）
- Kafka 核心概念
- 消息不丢失
- 消息不重复消费
- 消息顺序消费
- Rebalance 机制
- 自动提交 offset
- 消息堆积

## Kafka（扩展）
- 消息队列的作用
- 消息队列对比 & 技术选型
- ISR 机制

## Spring 框架（重点）
- IOC 和 AOP
- 常见注解
- Spring 事务
- Bean 的作用域
- SpringBoot 自动装配原理
- Spring MVC 执行流程
- Spring 中的设计模式
- SpringBoot 启动流程

## Spring 框架（扩展）
- 循环依赖问题 & 三级缓存
- @Autowired 和 @Resource 的区别
- 事务失效的原因
- SpringBoot 如何优雅停机
- Spring 新特性

## 计算机网络（重点）
- HTTP & HTTPS
- TCP 三次握手、四次挥手
- TCP 可靠性保证
- TCP 粘包与拆包
- 键入网址到网页显示的全过程
- CDN

## 计算机网络（扩展）
- HTTP 状态码
- GET 与 POST 区别
- 半连接队列与全连接队列
- SYN 攻击及防御方法

## 操作系统（重点）
- 进程 / 线程 / 协程
- 内存管理
- 死锁
- IO 多路复用（select / poll / epoll）
- Linux 常用命令

## 操作系统（扩展）
- 中断
- 孤儿进程 & 僵尸进程
- 用户态 & 内核态
- 进程调度算法

## 分布式
- CAP 定理
- BASE 理论
- 微服务调用链日志追踪分析
- 负载均衡
- 全局分布式 ID
