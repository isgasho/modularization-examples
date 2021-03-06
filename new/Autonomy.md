我们担心这样的症状：

* 沟通多：做新需求很难，因为需要牵涉到很多的团队，要和大量的人去沟通才能把需求落地。
* 需求做了就删不掉：一旦需求做进去了之后，即便愿意把这个功能下线也非常困难。遗留代码日积月累。

Autonomy 的愿景就是尽量减轻上述的症状，让拆分出来的代码更独立（更具有Autonomy）。从而新需求需要的沟通可以更少，不需要的功能也可以比较容易被干掉。

假定业务逻辑肯定要拆分，拆分成

* 文件
* 文件夹
* Git仓库

以 Autonomy 为目标的话，我们可以很容易判断 Git 仓库是主要的着手点。为了减少沟通，每个块业务和产品经理，应该有个对口的 Git 仓库。不选择文件和文件夹的主要原因是 Git 仓库一般对应了编程语言的 Package 的概念，如果是 JavaScript 的话，对应的有 package.json 文件。使用 Git 仓库比较容易依赖编译器进行依赖检查。而选择了文件或者文件夹，则很容易变成表面上拆开了，但是仍然有调用关系，实际上仍然和写在一起没有区别。

但是拆分成多个 Git 仓库不是免费的。拆分之后就有组合的问题。怎么能把多个 Git 仓库又[集成](./Integration.md)回去呢? 这个装配应该拿什么描述。

我们又如何能度量在 Autonomy 这个维度，现在的问题有多严重。或者换句话说，当我们做出了一些改进，如何[度量](./AutonomyMetrics.md)有改善呢?