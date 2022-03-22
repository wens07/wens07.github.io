---
title: perf_analysis
date: 2021-11-30 10:15:00
updated: 2021-01-30 10:15:00
categories: technique
tags: [tool]
keywords: [perf, analysis]
toc:
---

### 使用perf分析cpu热点
1. 使用top -H 和 top先查看cpu分布(用户，系统， i/o), 如果有 i/o比较高的情况，可使用iotop查看下disk的读写情况
2. 使用sudo perf top 找出cpu最忙的函数清单
3. 进行perf录制：
   `perf record -F 99 -p process_id --call-graph dwarf --sleep 30`
4. perf report -g -i ./perf.data
    找出叠加后的耗费cpu的各个颗粒度入口

### 用perf采集火焰图
1. install necessary
`sudo yum install perf -y`
`sudo yum install perf-DBD-mysql perl-DBI -y`

`git clone https://github.com/brendangregg/FlameGraph.git`
`cd FlameGraph/`

2. 采集数据
- 全局
`perf record -F 99 -a -g --sleep 60`
- 单独进程
`perf record -F 99 -p detail_process_id -g --sleep 60`
  注： 如果结果很多Unknown，说明调用栈的符号信息没获取到，把`-g`改成`--call-graph dwarf`

3. 处理数据输出svg
`perf script > out.perf`
`./stackcollapse-perf.pl out.perf > out.folded`
`./flamegraph.pl out.folded > 2.svg`
`sz 2.svg`
