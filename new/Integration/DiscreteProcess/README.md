# 离散型流程

例如在订单成交之后，给中介分佣这一类的业务。它们有三个特点

* 不需要返回值。也就是只需要在时间顺序上，安排在之后发生。
* 不精确要求立即执行。稍微晚个几秒是可以忍受的。
* 不影响事务结果。不因为分佣服务挂了，导致订单无法成交。