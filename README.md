基于系统负载的动态限流组件 dynamic-limiter

一个系统的处理能力是有限的，当请求量超过处理能力时，通常会引起排队，造成响应时间迅速提升。如果对服务占用的资源量没有约束，还可能因为系统资源占用过多而宕机。因此，为了保证系统在遭遇突发流量时，能够正常运行，需要为你的服务加上限流。

通常限流可以分为两类：单机限流、全局限流。常见的单机限流工具有 Guava RateLimiter 和 Java Semaphore，全局限流可以用 Redis 做全局计数器来实现，基础架构组也提供了一个灵活的全局限流组件 common-blocking。这些限流工具有一个共同的缺点：都需要手动设置一个固定的限流阈值。

首先，手动设置固定阈值需要做容量评估，准确的容量评估是比较难的。其次，在每次系统更新升级后，阈值会变得不再准确，需要重新调整，比较繁琐。再次，固定阈值也不能应对服务器性能波动的情况，对于一些日志量比较大的应用，整点日志压缩时，会消耗较多性能，此时系统的处理能力肯定比其他时候要稍差一些。最后，应用大多运行在虚拟机上，同一个实体机上的虚拟机之间也会相互影响，这个体现在监控上就是 CPU 使用率里的 steal 值了。

既然固定阈值有这么多缺点，我们就想有没有什么办法能够自动计算限流阈值呢？

详细内容请看[基于系统负载的动态限流组件 dynamic-limiter](https://arith.blog.csdn.net/article/details/78985877)。