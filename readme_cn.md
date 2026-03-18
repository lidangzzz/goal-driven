# Goal-Driven（目标驱动）


Goal-Driven（目标驱动）方法的目的是让你的多智能体系统（例如 Claude Code、Codex、OpenClaw）能够持续投入超过 300 小时来解决一个具有明确目标和一套严格、明确定义成功标准的极其复杂问题。

Goal-Driven 最适合那些高度复杂、耗时、逻辑抽象——但可以彻底评估是否成功的任务。典型示例包括编译器设计、数学定理证明、计算问题、数据库架构、复杂的系统级设计以及 EDA 仿真挑战。

Goal-Driven 的核心概念如下：

1. **目标（Goal）**——整个系统的最终目的，也是所有子智能体的核心任务。

2. **成功标准（Criteria）**——一套清晰的条件，让主智能体能够判断任务是否完成、目标是否达成。

3. **子智能体（Subagent）**——负责持续致力于解决问题并实现所分配目标的智能体。

4. **主智能体（Master Agent）**——子智能体的唯一控制者，负责根据定义的标准独立评估目标是否达成。它是系统流程的最终决策者。

Goal-Driven 的核心理念非常简单：

1. 当 Goal-Driven 流程启动时，主智能体创建一个子智能体，并指示它持续致力于解决问题并达成目标。

2. 主智能体定期检查子智能体是否活跃。如果子智能体变得不活跃、声称完成或进入空闲状态，主智能体必须根据标准评估当前结果。如果结果未能满足标准，它会命令子智能体继续工作，重复这个循环直到标准被满足。

3. 一旦子智能体的输出满足标准，系统停止并宣布成功完成。

该流程的伪代码表示如下：
```
while (criteria not met)
{
    let the subagent work on solving the problem and achieving the Goal
}
```

## 使用 Goal-Driven 系统开发的开源项目示例

C++ 实现的 TypeScript 编译器（约 100 小时）[https://github.com/lidangzzz/TypeScript-C-Implementation-by-OnlySpecs](https://github.com/lidangzzz/TypeScript-C-Implementation-by-OnlySpecs)

Rust 实现的 SQLite（约 30 小时）[https://github.com/lidangzzz/sqlite-rust-by-OnlySpecs](https://github.com/lidangzzz/sqlite-rust-by-OnlySpecs)


## 使用方法：
将以下提示词复制到你的文本编辑器中。仔细填写目标和成功标准的空白部分，然后使用支持多智能体的工具（例如 Claude Code、Codex、OpenClaw 等）运行它。

## 示例：

Goal: [[[[[用 C++ 编写一个 TypeScript 编译器，能够正确地将 TypeScript 转译为 JavaScript，包括完整的文档和单元测试。]]]]]

Criteria for success: [[[[[确保 TypeScript 编译器成功编译并生成 2,000 个涵盖尽可能多 TypeScript 语法特性的综合测试用例文件。确认 C++ TypeScript 编译器能正确将代码转译为 JavaScript。然后，在 Node.js 上运行此编译器的输出和官方 tsc 转译器的输出，并验证两个生成的 JavaScript 文件产生相同的输出。]]]]]


## 注意事项：

1. 我强烈建议不要将此提示词添加到任何 AI 智能体的技能或插件中，因为这可能会污染你的上下文窗口。

2. Goal-Driven 流程可能会消耗大量时间和 LLM tokens；请确保你的 AI 智能体的 API 计划或订阅余额充足。



-----

# Goal-Driven 提示词模板（1 个主智能体 + 1 个子智能体）

```
# Goal-Driven(1 master agent + 1 subagent) System

Here we define a goal-driven multi-agent system for solving any problem.

Goal: [[[[[在此定义你的目标]]]]]

Criteria for success: [[[[[在此定义你的成功标准]]]]]

Here is the System: The system contains a master agent and a subagent. You are the master agent, and you need to create 1 subagent to help you complete the task.

## Subagent's description:

The subagent's goal is to complete the task assigned by the master agent. The goal defined above is the final and the only goal for the subagent. The subagent should have the ability to break down the task into smaller sub-tasks, and assign the sub-tasks to itself or other subagents if necessary. The subagent should also have the ability to monitor the progress of each sub-task and update the master agent accordingly. The subagent should continue to work on the task until the criteria for success are met.

## Master agent's description:

The master agent is responsible for overseeing the entire process and ensuring that the subagent is working towards the goal. The only 3 tasks that the main agent need to do are:

1. Create subagents to complete the task.
2. If the subagent finishes the task successfully or fails to complete the task, the master agent should evaluate the result by checking the criteria for success. If the criteria for success are met, the master agent should stop all subagents and end the process. If the criteria for success are not met, the master agent should ask the subagent to continue working on the task until the criteria for success are met.
3. The master agent should check the activities of each subagent for every 5 minutes, and if the subagent is inactive, please check if the current goal is reached and verify the status. If the goal is not reached, restart a new subagent with the same name to replace the inactive subagent. The new subagent should continue to work on the task and update the master agent accordingly.
4. This process should continue until the criteria for success are met. DO NOT STOP THE AGENTS UNTIL THE USER STOPS THEM MANUALLY FROM OUTSIDE.

## Basic design of the goal-driven double agent system in pseudocode:

create a subagent to complete the goal

while (criteria are not met) {
  check the activty of the subagent every 5 minutes
  if (the subagent is inactive or declares that it has reached the goal) {
    check if the current goal is reached and verify the status
    if (criteria are not met) {
      restart a new subagent with the same name to replace the inactive subagent
    }
    else {
      stop all subagents and end the process
    }
  }
}
```
