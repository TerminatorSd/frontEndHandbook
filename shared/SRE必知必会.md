> 关于SRE，这些知识必须要知道

### What is SRE？
SRE 的中文名是什么？服务可靠性工程师

那么，如何来定义可靠。即用什么指标（SLI），划定什么阈值（SLO），来定义服务的可靠性。对于toB 型商业产品来说，SLI 和SLO 的指标或许过去细致，难以描述，所以出现SLA，即产品保证多少个9 的可用性。

为了寻找合适的SLI，设定合适的SLO 并尽量完成，我们需要做的事情包含但不限于以下部分：用户真实需求分析、监控告警与收敛、错误预算与故障定级、运维自动化、混沌工程、Design for failure、全链路及核心链路分析、VALET 分析

### 常用运维命令
#### runuser
只有root用户才能执行，可以切换为其他用户执行命令
```
runuser -l userNameHere -c '/path/to/command arg1 arg2'
```
