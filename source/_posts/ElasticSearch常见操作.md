---
title: ElasticSearch常见操作
date: 2018-01-31 10:19:26
tags:
      - ElasticSearch
      - 数据处理
categories: 深耕码农
mathjax: false
---


## 几个基本概念
* 索引——库
* 类型——表
* 文档——表记录
* 字段——字段

##　带来的好处
* 海量数据检索秒级返回，具备结构化、全文、多字段、相关度及模糊匹配搜索能力
* 海量数据量准实时分析，包括按时间统计、过滤、排序、求和、百分位计算等各类聚合操作、关联关系的建模
* NoSql的弹性，无须提前设计表结构

## 如何交互
* JAVA/PYTHON.. API
* Restful 接口
  * CURL
  * 可以使用任何语言
* Sense控制台
  * 参见[Sense UI指南](https://www.elastic.co/guide/en/sense/current/sense-ui.html)

## 如何快速入门
  * 开源开源！—— [官网](https://www.elastic.co)
  * 《Elasticsearch 权威指南》中文版，参考[电子版](https://es.xiaoleilu.com/)

## 简单操作示例
### 增(index)
```python
##PUT-GET谓词
PUT stockfactor_2018.01.30/airr_mapping
{
  "stockname": "招商银行",
  "open":  "32.90",
  "close": "32.57"
}
GET stockfactor_2018.01.30/airr_mapping/600036

##POST谓词
POST stockfactor_2018.01.30/airr_mapping
{
  "stockname": "招商银行",
  "open":  "32.90",
  "close": "32.57"
}
GET stockfactor_2018.01.30/airr_mapping/_search
```
正常的话返回确认响应体，以上代表两种方式，一种是“你严格按照我说的去办”PUT-GET方法，一种是“请帮我处理这条请求”的POST方法，可以注意到，POST方法无须指定_id,ElasticSearch会帮助你生成一条。

### 删
### 改
### 查
```python
##取回部分字段
GET stockfactor_2018.01.30/airr_mapping/600036?_source=stockname,open
GET stockfactor_2018.01.30/airr_mapping/_search
##使用通配符来搜索多索引、多类型
GET */airr_mapping/_search?_source=astr_intro,double_pb,double_pe_ttm?size=5&from=10
```
