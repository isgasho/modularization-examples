假设有如下虚构的外卖业务，其现有的模块划分如下图所示

![dependency](dependency.drawio.svg)

用户先在商品陈列模块里完成商品的选购，然后去结算页选择优惠。下单之后，骑手配送到你家，点收货。如果产生了异常，例如取消订单，由售后模块负责退款。

为了在业务低峰期促进高价值订单的成交。产品经理想要给外卖业务添加一个惊喜折扣的功能。大概的需求是先根据用户的浏览记录，选择命中的用户。在用户浏览商品陈列的时候，以天降红包的形式提示你被惊喜砸中了。在砸中之后，商品会出现一个额外的折扣价格。然后在结算页也需要提示这个折后价格帮你省了多少钱。但是这个折扣价，必须用一张会员红包进行抵扣。如果支付了之后，用户想要取消订单。订单使用的会员红包应该原路退回，实际退款金额应该等于当时支付金额。

为了实现这个需求，这些模块约定了在订单上添加一个字段表示这个是天降红包类型的订单。然后每个模块各自按照约定的字段，进行本模块所需的修改。

活动上线了几天之后，发现一些用户在被红包砸中之后没有立即下单。而是过了两个小时才下单。这个时候因为业务已经处于高峰期了，商家并不愿意亏本接这样的订单。产品提出需要给这个惊喜折扣加上时间限制，不是出现一次之后就一直可以享用。商品陈列模块和结算模块约定，必须传一个“天降红包权益”的id过来，在做下单的时候校验一下这个权益是否仍然处于有效的状态。

然后过了两天，发现这个功能很受欢迎。部分用户表示，能否一次多抵扣几张会员红包，享受更大的折扣?但是在第一次实现的时候，订单上添加的字段为“是否使用了红包”，没有考虑到需要改成数量。于是各个模块需要按照新的接口重新进行适配，又改一轮。

从这个例子我们可以看到两点

* 在前面的案例里，我们看到每次做需求，都改同一个模块是有问题的。这个业务里，通过模块拆分，避免了大家都改同一个模块的问题。这是做的好的地方，把工作平摊了出去。
* 但是在多轮的需求修改里，整个交易链路上的多个模块需要反复被修改，不断适配新的业务形态。

从“天降红包”这个项目组的角度来说，他们是非常希望能够有一个独立的模块来对他们这块业务负责的。从权益的发放，消费，到回滚，整个流程的业务都收敛到一起。识别这个模块的过程，就是我们识别“易变性”的过程。当我们发现这些地方经常同时被修改的时候，那么独立出一个模块来就比较合适。