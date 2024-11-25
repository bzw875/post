---
title: 记一段aws开发运维的工作
date: 2024-07-06 12:00:11
updated: 2024-07-06 12:00:11
tags: [aws, 云计算]
categories:
---

我2024年入职了一家外企做开发运维，大概是美国的代码部署到中国。这个外企全套亚马逊云(aws)。我入职的时候什么是Lambda都不知道，也算是积累了宝贵的经验。


## aws 常见资源和说明

* EC2 Instances（EC2 实例）：Amazon Elastic Compute Cloud (EC2) 提供的虚拟服务器实例。
* S3 Buckets（S3 存储桶）：Amazon Simple Storage Service (S3) 提供的对象存储桶。
* RDS Databases（RDS 数据库）：Amazon Relational Database Service (RDS) 提供的托管关系型数据库实例。
* Lambda Functions（Lambda 函数）：AWS Lambda 提供的无服务器函数。
* LAM Users（IAM 用户）：AWS Identity and Access Management (IAM) 提供的用户实体。
* SQS Queues（SQS 队列）：Amazon Simple Queue Service (SQS) 提供的消息队列。
* SNS Topics（SNS 主题）：Amazon Simple Notification Service (SNS) 提供的通知主题。
* Elastic Load Balancers（ELB 负载均衡器）：Elastic Load Balancing (ELB) 提供的负载均衡器实



## 先看看他们的JD

#### Job description

1、10年的开发经验，精通Node.js、TypeScript和JavaScript，熟悉其他编程语言。
2、熟悉软件设计模式，微服务架构、面向对象编程(OOP)、领域驱动设计(DDD)和GraphQL具备AWS Serverless开发经验，有AWS和Alibaba Cloud相关证书优先考虑。
4、对时间序列数据库、图数据库和DynamoDB数据库有了解，有相关经验佳。
5、有laC经验和CI/CD经验佳
6、熟悉敏捷开发和软件开发生命周期(SDLC)

面试主要提问是基于技术栈，主要问到3个方面，重要性依次递减：
1、大数据处理，最好有ETL经验，有ETL的概念，主要使用的是一整套AWS组件形成的ETL架构，包含组件:AWS Glue ，dynamodb，s3，datalake，redshift，athena稍微了解，他们是用外部开发了一个工具对接athena做前端展示
2、TypeScript，他们使用TypeScript做全套逻辑处理，包括前段react api-gateway，后端主要用cdk，调用aws组件
3、他们使用CircleCI，只需要有标准pipeline经验没问题