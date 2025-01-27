## Learn_Druid
## 学习德鲁伊笔记

Druid的部署环境：

1.JAVA开发，目前支持JDK7以上版本，以后将会支持JDK8以上版本，建议直接从JDK8以上开始。
2.在操作系统方面，支持主流Linux 和Mac OS，不支持Windows 操作系统。

Druid的基本概念：

1.数据格式：Druid 在数据摄入之前，首先需要定义一个数据源（DataSource），这个DataSource 有些类似数据库中表的概念。每个数据集合包括三个部分：时间列（TimeStamp）、维度列（Dimension）和指标列（Metric）。

（1）时间列：每个数据集合都必须有时间列，这个列是数据聚合的重要维度，Druid 会将时间很近的一些数据行聚合在一起。另外，所有的查询都需要指定查询时间范围。

（2）维度列：维度来自于OLAP 的概念，用来标识一些事件（Event），这些标识主要用于过滤或者切片数据，维度列的字段为字符串类型。例如，对于一次广告展现，我们可以将“哪个广告”、“哪个广告位置”、“计费的类型”、“广告主的类型”等作为广告展现的描述信息。随着业务分析的精细化，增加维度列也是一个常见的需求。

（3）指标列：指标对应于OLAP 概念中的Fact，即用于聚合和计算的列。指标列字段通常为数值类型，计算操作通常包括Count、Sum 和Mean 等。指标通常是业务的关键量化指标，包括收入、使用时长等核心可度量和比较的指标。数据格式样例如图1-2 所示。

<img src="https://github.com/jiaming9844/learn_druid/blob/master/image/2017022015123066.jpg"/>
 

2.数据摄入：Druid 提供两种数据摄入方式，如图1-3 所示，其中一种是实时数据摄入；另一种是批处理数据摄入。

<img src="https://github.com/jiaming9844/learn_druid/blob/master/image/2017022015123158.jpg"/>

3.数据查询：在数据查询方面，Druid原生采用的JSON格式，通过HTTP传送。Druid不支持标准的SQL语言查询，因为有些SQL语言查询并不适用Druid现在的设计。随着Druid应用越来越广泛，支持标准SQL的需求越来越重要，一些开源生态项目正在向这个方向努力，例如：Imply.io的PlyQL等。

对于Druid 的查询访问，除了原生Java 客户端支持外，也出现了很多支持不同语言客户端访问的开源项目，例如Python、R、JavaScript 和Ruby 等。

下面是一个用JSON 表达的查询例子，该查询中指定了时间范围、聚合粒度、数据源等。
````
{
“queryType”: “timeseries”,
“dataSource”: “sample_datasource”,
“granularity”: “day”,
“aggregations”: [
{ “type”: “longSum”, “name”: “result_name”, “fieldName”: “field_name” }
],
“intervals”: [“2012-01-01T00:00:00.000/2012-01-04T00:00:00.000”],
“context” : {“skipEmptyBuckets”: “true”}
}
````
https://www.afenxi.com/41702.html

ffffffff
