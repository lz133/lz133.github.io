---
title: Python命名规则
date: 2026-09-29 11:24:28
categories:
  - 学习笔记
tags:
  - Python
  - 学习笔记
---

## bool值命名

- is_xxx
- has_xxx
- allow_xxx

## int/float类型命名

- 释义为数字，如port、age、radius等
- 以_id结尾或者以length_/count_开头
- 最好别拿一个名词的复数形式来作为int类型的变量名，比如apples、trips等，因为这类名字容易与那些装着Apple和Trip的普通容器对象（List[Apple]、List[Trip]）混淆，建议用number_of_apples或trips_count这类复合词来作为int类型的名字。
