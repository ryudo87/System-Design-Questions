# Building a real-time user action counting system for ads 
https://medium.com/pinterest-engineering/building-a-real-time-user-action-counting-system-for-ads-88a60d9c9a

搜索，我们采用Solr+Lucene这套框架

**Aperture**, an in-house data storage and online events tracking service
## user action counts
the count for a Pinner’s past clicks, impressions and other actions on ads
## frequency control 
which sets a maximum number of times an ad is shown to a Pinner

## Fatigue model
Fatigue happens when a Pinner becomes tired of viewing the same ad. This usually has negative impact on CTR (click-through rate). Our ads system has a training pipeline for the fatigue model for pCTR (predictive CTR). 
At the request time, several user counting features are fetched for the user fatigue model. A Pinner’s fatigue is measured at different campaign levels. Our campaign structure has four levels:
Advertisers: the account
Campaigns: houses of ad groups
Ad groups: container of Promoted Pins
Promoted Pins: ads
The required actions are impressions and clicks. First, our ads serving system fetches a Pinner’s past engagement counts over a time range for a list of ads candidates at four campaign levels. Then, the counting features are fed to fatigue models for CTR prediction.

跟后端的连接是用的lukeeper来连接的。我们使用的推特开元的东西去减少整个过程产生的问题。Pinterest是一家图片网站，所以我们有大量的图片。我们暂时存在空间里，这个存储非常贵，我们的图片非常大，所以我们正在做一套自己图片存储的东西。我们一些应用使用ribits，其他的应用使用HBase。我们用的startD的性能比较简单。

　　这是我们智能算法的都是，我们数据处理的一套东西。最上面是API，它会写到KQ里头，分两层，一层是拷到S-street上面去，利用一些软件计算，当年的职能算法是在这上面来算，处理这些。还有一套准实时的东西，我们有一些lesser，去监听整个Kafka的状态，如果产生任何事件以后，会交给实时处理的简单的服务，这个服务会形成实时的推荐和搜索，写入实时推荐和搜索引擎。

　　这是我们非实时数据处理的，我们选择的Hive、Redshift和Casoading，Hive非常简单，但是很慢。Redshift比Hive快，我们正在向这方面改。我们非常复杂的计算采用Casoading，采用JAVA的语言。这大概只是搜索和推荐每天要运行的所有的数据，大概一百多个，我们用Azkaban来做。Azkaban有一些问题我们也内部做了改进。

　　我们的实时处理大概用了Kafka和listeners，我前面讲过了。我们这里实时讲的是分钟级别的，而不是秒的级别。
