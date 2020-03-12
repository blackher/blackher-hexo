---
title: elastic-error-unassigned
date: 2019-12-17 14:03:01
tags:
---

## elastic unassigned 分片错误

`通过elastic监控发现新建的index的切片无法unassigned，也就是无法存储切片的副本，影响可以高可以用性`
`查找文档 https://www.elastic.co/guide/en/elasticsearch/reference/current/cluster-allocation-explain.html`
`磁盘券用超过85% elasticsearch策略 停止副本切片`
