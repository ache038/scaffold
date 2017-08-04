# 题目

## Objective

1. 使用Java语言在Spring Boot中开发一个Restful Web Service
2. 使用JUnit测试该Restful Web Service

## Required

1. 这个Restful Web Service需要运行在Docker容器中（Docker容器自选），该Docker镜像在Maven打包过程中构建；
2. 数据库使用Postgre SQL的Docker模式（下载地址：[https://registry.hub.docker.com/\_/postgres/](https://registry.hub.docker.com/_/postgres/)），数据表可在启动过程中自动创建，也可手工创建；
3. 整个项目使用传统分层架构，包括：Resource -&gt; Service -&gt; Dao
4. 针对所有的类书写测试用例，基本要求：
   1. 所有依赖项使用Mock方式（Mockito）
   2. 使用Jococo检查测试覆盖率（&gt;65%）
5. 开发完成后使用Markdown书写相关文档，设计思路、架构、编码规范等；

## Interface

### 1. 创建记录

POST接口创建记录

```json
{
            "businessId": "业务主键（需要检查不重复）",
            "type": "只支持A，B，C三个值",
            "standardItemIdentification": "随意",
            "sellersItemIdentification": "随意",
            "itemName": "随意（不重复）",
            "period": "时间格式，输入格式为201703类似",
            "unitCode": "EA",
            "currencyID": "CNY",
            "receiptID": "随意",
            "comment": "大文本",
            "department": "随意",
            "priceWithTax": "金钱格式",
            "quantity": "数量",
            "amount": "总金额"
}
```

* 在数据库中创建主键，主键使用UUID格式；
* type类型使用PostgreSQL中的enum；
* 


