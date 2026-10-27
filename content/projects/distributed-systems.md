+++
title = 'MIT 6.5840 分布式系统实验'
description = '使用 Go 实现 MapReduce、Raft 与线性一致性 KV 服务，涵盖日志同步、快照恢复与故障测试。'
date = 2026-10-26
lastmod = 2026-10-26
weight = 2
category = '分布式系统'
categories = ['项目']
icon = 'nodes'
status = '课程实验'
tags = ['Go', 'Raft', 'RPC', 'KV Store']
source_note = '遵循课程要求，实验源码暂不公开。'
featured = true
show_update = true
+++

> 遵循课程要求，实验源码暂不公开。

## 项目概览

分布式系统课程实验，参考 MIT 6.824 Labs。使用 Go 实现 MapReduce 调度、Raft 共识与线性一致性 KV 服务。

## 分布式调度与故障处理

基于 Go 实现 Coordinator/Worker 调度框架，通过 RPC 完成 Map/Reduce 任务分发与完成状态上报；维护空闲、执行中、已完成三种任务状态及阶段切换，以超时重分配处理 Worker 故障，并通过 Key 哈希分区、排序聚合及临时文件重命名完成数据处理。

## Raft 共识与日志同步

实现随机超时选举、周期心跳、日志复制与状态保存恢复，通过任期检查、日志前缀校验及当前任期日志的多数派提交维护一致性；引入 **快速回退优化（Fast Backup）**，根据冲突任期与起始索引调整 nextIndex，跳过不匹配日志区间，减少日志对齐时的 RPC 重试。

## 线性一致性 KV 与请求去重

实现 Get/Put/Append 接口，将读写请求统一提交至 Raft 日志，由 applyCh 驱动状态机按序处理；客户端缓存 Leader，失败后切换节点并保持同一请求的 ClientID 与 SeqID 重试，服务端记录各客户端已执行的写请求序号，避免重复追加，实现 **幂等性**。

## 快照压缩与节点恢复

按 Raft 状态大小触发快照，将 KV 数据与请求去重记录一并编码保存；以快照边界转换日志编号与切片下标，截断已执行的日志前缀，利用 InstallSnapshot 恢复落后节点的状态并继续同步后续日志，减少历史日志占用。

## 并发控制与可靠性验证

使用互斥锁保护共享状态，在锁外执行 RPC 并校验回复的角色与任期；以日志索引关联带缓冲 Channel，结合 select 超时等待、请求身份校验与通道清理管理应用通知；使用 LabRPC 模拟丢包、延迟、乱序及网络分区，验证容错，通过 Raft 与 KV-Raft 共 **51 项 -race 测试**。

