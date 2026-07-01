# commonProject
自己日常工作总结

#MCP相关
- Spring AI Alibaba 开源项目地址：https://github.com/alibaba/spring-ai-alibaba
- 本文外网博客地址：https://java2ai.com
- 源码地址：https://github.com/springaialibaba/spring-ai-alibaba-examples/tree/main/spring-ai-alibaba-mcp-example


# 如何开始实践 Harness 工程
## 创造环境
- 一定要给 AI 创造一个环境，这个环境包括两方面：

- 研发工具链：我们要为 AI 提供研发工具，比如测试、部署、验证、查日志等。人用到的工具都要给它做一套 CLI，让它能具备人所拥有的所有上下文。

- 自主验证机制：要让 AI 自主完成工作，就势必要涉及如何验证。

- 对于业务需求，功能测试非常重要，且必须由人来定义和验收。

- 对于效果优化需求，核心则是构建评测集和自动化评测。

## 实践的技巧
在有了环境之后，关键在于如何把它用起来。我们实践下来的经验有两点：

- 使用顶级模型：一定要用业界目前最强的模型，比如 Claude Code 或 Codex 的官方订阅，如果是国产模型，可以用最近刚出的 GLM5.2。很多时候你试着让 AI 干一件事却干不成，可能不是 AI 做不到，而是因为模型太差。

- 建立 Skill 机制：很多人把 AI 当作“许愿机”，想着通过一句话需求就让它把所有事干完，这显然不现实。一种非常好的路径是像“带实习生”一样：你先给它具体步骤，手把手教它一步步做。带它做完这个过程后，你只需要加一句 Prompt，让它把这次聊天的过程总结为一个 Skill。模型就会把这段对话沉淀为一个技能，下一次让它做类似需求时，它就可以举一反三了。


 ## champion-challenger 机制：

Champion-Challenger 打擂台机制

champion = 未过拟合的历史最高分轮次；

challenger = 各轮次 prompt 改动

这其实就是一个“打擂台”的机制：历史上最好的一轮放在擂台上作为基准。

### 具体的迭代流程如下：
<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/46da0d03-a255-42d6-98ee-f282e3da5768" />


- AI 必须从当前的冠军策略（即冠军的 prompt）出发去做改进。

- 改进完成后，在验证集上将挑战者的 prompt 与冠军策略进行对比。

- 只有当挑战者在各个方面都完全超过了冠军策略时，它才能成为新的冠军。

- 接下来，AI 会继续从新的冠军策略出发进行下一轮优化。这种机制保证了每一次迭代的经验都能保留下来，让 AI 在一个比较稳定的基础上进行迭代，而不会一条路走到黑。
