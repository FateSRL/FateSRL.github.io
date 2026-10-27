+++
title = '论文调研助手'
description = '支持论文版本过滤与引用校验的 RAG 问答助手，正在向论文调研 Agent 扩展。'
date = 2026-10-26
lastmod = 2026-10-26
weight = 1
category = 'AI 应用'
icon = 'spark'
status = '开发中'
tags = ['Python', 'RAG', 'Qdrant', 'SQLite']
repo = 'https://github.com/FateSRL/paper-research-assistant'
featured = true
show_update = true
+++

## 项目概览

面向论文检索与问答的个人项目，技术栈为 Python、RAG、Qdrant 和 SQLite。目前已实现核心问答流程，后续计划扩展为论文调研 Agent。

## 已实现

### 检索问答与引用校验

构建支持论文版本过滤的 RAG 问答流程，实现引用与原文、PDF 页码的关联及校验，拦截超出本轮证据范围或来源不一致的引用。

### 调用预算与异常处理

为答案生成、格式修复和网络重试设置统一调用预算，约束请求次数，完成核心流程及异常分支验证。

## 后续规划

扩展为支持多论文对比、证据不足时自动补检索的论文调研 Agent，接入交互界面，并建立检索效果与引用质量评测体系。

