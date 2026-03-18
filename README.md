[中文版](readme_cn.md)

# Goal-Driven


The purpose of the Goal-Driven approach is to enable your multi-agent system (e.g., Claude Code, Codex, OpenClaw) to sustain more than 300 hours of continuous effort in solving an extremely complex problem that has a specific objective and a set of strict, well-defined criteria.

Goal-Driven is best suited for tasks that are highly intricate, time-consuming, logically complex, and abstract—yet can be thoroughly evaluated for success. Typical examples include compiler design, mathematical theorem proving, computational problems, database architecture, sophisticated system-level design, and EDA simulation challenges.

The core concepts of Goal-Driven are as follows:

1. Goal – the ultimate objective of the entire system and the central task of all subagents.

2. Criteria – a clear set of conditions that allow the master agent to determine whether the task is completed and the goal has been achieved.

3. Subagent – an agent responsible for continuously working toward solving the problem and achieving the assigned goal.

4. Master Agent – the only controller of subagents, responsible for independently evaluating whether the goal has been reached based on the defined criteria. It acts as the final decision-maker for the system’s process.

The core philosophy of Goal-Driven is straightforward:

1. When the Goal-Driven process starts, the master agent creates a subagent and instructs it to persistently work toward solving the problem and reaching the goal.

2. The master agent periodically checks whether the subagent is active. If the subagent becomes inactive, claims completion, or enters an idle state, the master agent must evaluate the current result according to the criteria. If the result fails to meet the criteria, it commands the subagent to continue working, repeating this cycle until the criteria are satisfied.

3. Once the subagent’s output meets the criteria, the system halts and announces successful completion.

The pseudocode representation of this process is as follows:
```
while (criteria not met)
{
    let the subagent work on solving the problem and achieving the Goal
}
```

## Example of open source projects developed by Goal-Driven system

TypeScript compiler in C++(in ~100 hours) [https://github.com/lidangzzz/TypeScript-C-Implementation-by-OnlySpecs](https://github.com/lidangzzz/TypeScript-C-Implementation-by-OnlySpecs)

SQLite in Rust(in ~30 hours) [https://github.com/lidangzzz/sqlite-rust-by-OnlySpecs](https://github.com/lidangzzz/sqlite-rust-by-OnlySpecs)

Lean4 compiler in TypeScript (in progress) [https://github.com/lidangzzz/Lean4-ts](https://github.com/lidangzzz/Lean4-ts)


## Usage:
Copy the following prompt into your text editor. Carefully fill in the blanks for both goal and criteria, then run it using your multi-agent–supported tool (for example, Claude Code, Codex, OpenClaw, etc.).

## Example:

Goal: [[[[[Write a TypeScript compiler in C++ that correctly transpiles TypeScript into JavaScript, including complete documentation and unit tests.]]]]]

Criteria for success: [[[[[Ensure that the TypeScript compiler successfully compiles and generates 2,000 comprehensive TypeScript test case files covering as many TypeScript syntax features as possible. Confirm that the C++ TypeScript compiler correctly transpiles the code into JavaScript. Then, run both the outputs from this compiler and the official tsc transpiler on Node.js, and verify that the two resulting JavaScript files produce identical outputs.]]]]]


## Notes:

1. I strongly advise not adding this prompt to any AI agent’s skills or plugins, as doing so could contaminate your context window.

2. Goal-Driven processes may consume significant time and LLM tokens; please make sure your AI agent’s API plan or subscription balance is sufficient.



-----

# The Goal-Driven Prompt Template (1 master agent + 1 subagent)

```
# Goal-Driven(1 master agent + 1 subagent) System

Here we define a goal-driven multi-agent system for solving any problem.

Goal: [[[[[DEFINE YOUR GOAL HERE]]]]]

Criteria for success: [[[[[DEFINE YOUR CRITERIA FOR SUCCESS HERE]]]]]

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
