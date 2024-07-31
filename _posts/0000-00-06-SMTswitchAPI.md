---
layout: archive
title: "SMT Switch API 总结"
date: 2024-07-26
author_profile: true
---

首先假设我们有一个 TransitionSystem 叫做sts


### term.h
- to_string() 获取节点的字符串表示
- hash() 获取节点的哈希值
- get_id() 获取节点的唯一标识
- get_op() 获取节点的操作符
- get_sort() 获取节点类型
- 一系列判断节点类型的：
  - is_symbol() 是否为符号
  - is_param() 是否为参数
  - is_symbolic_const() 是否为符号变量
  - is_value() 是否为解释常量
- 遍历子节点
  - virtual TermIter begin() = 0;
  - virtual TermIter end() = 0;

### ops.h
- enum PrimOp：包括了一些逻辑操作，算术操作，位向量操作
- struct OP：表示一个操作符，并且可以带索引
- to_string(PrimOp op) 表示将Op转换为字符串
- operator==(Op o1, Op o2)判断两个操作是否相等
- operator!=(Op o1, Op o2)判断两个操作不等
- operator<<(std::ostream& output, const Op o);将Op输出到stream中


### solver.h
- virtual void set_opt(const std::string option, const std::string value) = 0 设置SMT求解器选项
- virtual void set_logic(const std::string logic) = 0 设置SMT逻辑
- assert_formula(const Term & t) 添加断言到solver
- virtual Result check_sat() = 0 检查当前断言的可满足性
- virtual Result check_sat_assuming(const TermVec & assumptions) = 0 在给定假设条件下检查可满足性
- virtual void push(uint64_t num = 1) = 0 压栈当前上下文
- virtual void pop(uint64_t num = 1) = 0 弹栈当前上下文
- virtual uint64_t get_context_level() const = 0 获取当前上下文级别
- 