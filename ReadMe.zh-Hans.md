# ASP.NET Core开发者指南


> 2024年 [ASP.NET Core](https://docs.microsoft.com/zh-cn/aspnet/core/) 开发人员指南：

## 学习资源

1. 通用开发技能

   - 学习 [Git](https://git-scm.com/doc)，在 [GitHub](https://docs.github.com/en/get-started/quickstart) 上创建几个仓库，与你的代码分享给其他人。
   - 了解 [HTTP(S) 协议](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)、请求方法（[GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET)、[POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)、[PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT)、[PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH)、[DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE)、[OPTIONS](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) 等）。
   - 什么是 [TLS](https://www.cloudflare.com/learning/ssl/transport-layer-security-tls/)？
   - 什么是 [SSL](https://www.cloudflare.com/learning/ssl/what-is-ssl/)？
   - 不要害怕使用 Google，[Google 强力搜索](http://www.powersearchingwithgoogle.com)。
   - 开始使用 [ChatGPT](https://chat.openai.com/chat)。
   - 读几本关于算法和数据结构的书](https://www.interviewbit.com/blog/data-structures-and-algorithms-books)。

2. C#

   - [C# 12](https://www.pluralsight.com/paths/c-12)
   - [.NET 8](https://devblogs.microsoft.com/dotnet/announcing-dotnet-8)
   - [.NET CLI](https://docs.microsoft.com/dotnet/core/tools)
   - [StyleCop 规则](https://github.com/DotNetAnalyzers/StyleCopAnalyzers/blob/master/DOCUMENTATION.md)

3. SQL 基础知识

   - 教程 📚
     - [Pluralsight 学习路径：使用 T-SQL 查询 SQL Server 数据](https://www.pluralsight.com/paths/querying-data-with-t-sql-from-sql-server)

4. ASP.NET Core 基础

   - [MVC](https://docs.microsoft.com/en-us/aspnet/core/mvc/overview)
   - [Minimal APIs](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis)
   - [REST](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api)
   - [Application Settings & Configurations](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration)
   - [Middlewares](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware)
   - [Filters & Attributes](https://docs.microsoft.com/en-us/aspnet/core/mvc/controllers/filters)
   - [Authentication](https://docs.microsoft.com/en-us/aspnet/core/security/authentication)
   - [Authorization](https://docs.microsoft.com/en-us/aspnet/core/security/authorization/introduction)
   - [IdentityServer](https://identityserver4.readthedocs.io/en/latest)
   - [Duende IdentityServer](https://duendesoftware.com)
   - [OpenIddict](https://github.com/openiddict/openiddict-core)
   - [Auth0](https://auth0.com/docs)
   - [OIDC](https://openid.net/connect)
   - [Razor Pages](https://docs.microsoft.com/en-us/aspnet/core/razor-pages)
   - [Razor Components](https://docs.microsoft.com/en-us/aspnet/core/blazor/components)
   - 教程 📚
     - [From Zero to Hero: REST APIs in .NET](https://dometrain.com/course/from-zero-to-hero-rest-apis-in-asp-net-core/?affcode=1115529_alq6yoqt)
     - [From Zero to Hero: Minimal APIs in .NET with C#](https://dometrain.com/course/from-zero-to-hero-minimal-apis-in-net-with-c/?affcode=1115529_alq6yoqt)

5. 五个面向对象设计原则（SOLID）：

   - [Single Responsibility Principle (SRP)](https://www.dotnetcurry.com/software-gardening/1148/solid-single-responsibility-principle)
   - [Open-Closed Principle (OCP)](https://www.dotnetcurry.com/software-gardening/1176/solid-open-closed-principle)
   - [Liskov Substitution Principle (LSP)](https://www.dotnetcurry.com/software-gardening/1235/liskov-substitution-principle-lsp-solid-patterns)
   - [Interface Segregation Principle (ISP)](https://www.dotnetcurry.com/software-gardening/1257/interface-segregation-principle-isp-solid-principle)
   - [Dependency Inversion Principle (DIP)](https://www.dotnetcurry.com/software-gardening/1284/dependency-injection-solid-principles)

6. 面向对象关系映射（ORM）

   - [Entity Framework Core](https://learn.microsoft.com/en-us/ef/core)
     - 教程 📚
       - [From Zero to Hero: Entity Framework Core in .NET](https://dometrain.com/course/from-zero-to-hero-entity-framework-core-in-dotnet/?affcode=1115529_alq6yoqt)
   - [Dapper](https://github.com/StackExchange/Dapper)

7. 依赖注入（Dependency Injection）

   1. 依赖注入容器（DI Containers）
      - [Microsoft.Extensions.DependencyInjection](https://docs.microsoft.com/aspnet/core/fundamentals/dependency-injection)
      - [AutoFac](https://autofaccn.readthedocs.io/en/latest/integration/aspnetcore.html)
   2. 依赖注入开源库：[Scrutor](https://github.com/khellang/Scrutor)

   - 教程📚
     - [From Zero to Hero: Dependency Injection in .NET](https://dometrain.com/course/from-zero-to-hero-dependency-injection-in-net/?affcode=1115529_alq6yoqt) 

8. 数据库（Databases）

   1. 关系数据库（Relational）
      - [SQL Server](https://www.microsoft.com/sql-server/sql-server-2019)
      - [PostgreSQL](https://www.postgresql.org)
      - [MariaDB](https://mariadb.org)
      - [MySQL](https://www.mysql.com)
   2. 搜索引擎（Search Engines）
      - [ElasticSearch](https://www.elastic.co)
      - [Meilisearch](https://github.com/meilisearch/meilisearch)
      - [ManticoreSearch](https://github.com/manticoresoftware/manticoresearch)
      - [OpenSearch](https://github.com/opensearch-project/OpenSearch)
   3. NoSQL
      - 本地部署（On-Premises）
        - [Redis](https://redis.io)
        - [MongoDB](https://docs.microsoft.com/aspnet/core/tutorials/first-mongo-app)
        - [Apache Cassandra](http://cassandra.apache.org)
        - [LiteDB](https://github.com/mbdavid/LiteDB)
        - [RavenDB](https://github.com/ravendb/ravendb)
        - [CouchDB](http://couchdb.apache.org)
      - 云部署（Cloud）
        - [CosmosDB](https://docs.microsoft.com/azure/cosmos-db)
        - [DynamoDB](https://aws.amazon.com/dynamodb)

9. 缓存（Caching）

   - 内存缓存 [（Memory Cache）](https://docs.microsoft.com/aspnet/core/performance/caching/memory)
   - 分布式缓存 [（Distributed Cache）](https://docs.microsoft.com/aspnet/core/performance/caching/distributed)
     1. [Redis](https://redis.io/)
        1. [StackExchange.Redis](https://stackexchange.github.io/StackExchange.Redis)
        2. [EasyCaching](https://github.com/dotnetcore/EasyCaching)
     2. [Memcached](https://memcached.org)
   - 应用程序级缓存 （Application-Level）
     - 响应缓存（Response Caching）
       1. [Built in](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/response)
       2. [Marvin.Cache.Headers](https://github.com/KevinDockx/HttpCacheHeaders)
     - 输出缓存[（Output Caching）](https://learn.microsoft.com/en-us/aspnet/core/performance/caching/output?source=recommendations)
     - Entity Framework 二级缓存[（Entity Framework 2nd Level Cache）](https://github.com/VahidN/EFCoreSecondLevelCacheInterceptor)

10. 日志框架（Log Frameworks）

  - [Serilog](https://github.com/serilog/serilog)
  - [NLog](https://github.com/NLog/NLog)
  - 教程 📚
    - [From Zero to Hero: Logging in .NET](https://dometrain.com/course/from-zero-to-hero-logging-in-dotnet/?affcode=1115529_alq6yoqt)

11. API 客户端与通信（API Clients & Communications）

    1. REST
       - [Gridify](https://github.com/alirezanet/Gridify)
       - [OData](https://learn.microsoft.com/en-us/odata/webapi/first-odata-api) 
       - REPR 模式（[REPR Pattern](https://ardalis.com/mvc-controllers-are-dinosaurs-embrace-api-endpoints/)）
         - [Minimal APIs](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/overview)
         - [Ardalis.Endpoints](https://github.com/ardalis/ApiEndpoints)
         - [Fast Endpoints](https://github.com/FastEndpoints/FastEndpoints)
    2. [gRPC](https://docs.microsoft.com/en-us/aspnet/core/grpc)
    3. GraphQL
       - [HotChocolate](https://github.com/ChilliCream/hotchocolate)
       - [GraphQL-dotnet](https://github.com/graphql-dotnet/graphql-dotnet)

    - 教程 📚
      - [From Zero to Hero: REST APIs in .NET](https://dometrain.com/course/from-zero-to-hero-rest-apis-in-asp-net-core/?affcode=1115529_alq6yoqt)
      - [From Zero to Hero: Minimal APIs in .NET with C#](https://dometrain.com/course/from-zero-to-hero-minimal-apis-in-net-with-c/?affcode=1115529_alq6yoqt)
      - [From Zero to Hero: gRPC in .NET](https://dometrain.com/course/from-zero-to-hero-grpc-in-dotnet/?affcode=1115529_alq6yoqt)

12. 实时通信（Real-Time Communication）

    - [SignalR](https://docs.microsoft.com/aspnet/core/signalr)
    - [WebSockets](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/websockets)

13. 对象映射（Object Mapping）

    - [Manual mapping!](https://www.youtube.com/watch?v=U8gSdQN2jWI)
    - [Mapperly](https://github.com/riok/mapperly)
    - [AutoMapper](https://github.com/AutoMapper/AutoMapper)

14. 后台任务调度器（Background Task Scheduler）

    - [Native BackgroundService](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services)
    - [HangFire](https://github.com/HangfireIO/Hangfire)
    - [Quartz](https://github.com/quartznet/quartznet)
    - [Coravel](https://github.com/jamesmh/coravel)    

15. 测试（Testing）

    1. 单元测试（Unit Testing）
       - 框架（Frameworks）
         - [xUnit](https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-dotnet-test)
         - [NUnit](https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-nunit)
         - [MSTest](https://docs.microsoft.com/dotnet/core/testing/unit-testing-with-mstest)
       - 模拟（Mocking）
         - [Moq](https://github.com/moq/moq4)
         - [NSubstitute](https://github.com/nsubstitute/NSubstitute)
         - [FakeItEasy](https://github.com/FakeItEasy/FakeItEasy)
       - 断言（Assertion）
         - [FluentAssertion](https://github.com/fluentassertions/fluentassertions)
       - 假数据生成器（Fake Data Generators）
         - [Bogus](https://github.com/bchavez/Bogus)
         - [AutoFixture](https://github.com/AutoFixture/AutoFixture)
    2. 集成测试（Integration Testing）
       - [WebApplicationFactory](https://docs.microsoft.com/aspnet/core/test/integration-tests)
       - [.NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire)
       - [Test Containers](https://github.com/testcontainers/testcontainers-dotnet)
       - [Respwan](https://github.com/jbogard/Respawn)
    3. 快照测试（Snapshot Testing）
       - [Verify](https://github.com/VerifyTests/Verify)
    4. 行为测试（Behavior Testing）
       - [SpecFlow](https://github.com/techtalk/SpecFlow/tree/DotNetCore)
    5. 端到端测试（E2E Testing）
       - [Selenium](https://www.hanselman.com/blog/real-browser-integration-testing-with-selenium-standalone-chrome-and-aspnet-core-21)
       - [Puppeteer-Sharp](https://github.com/kblok/puppeteer-sharp)
    6. 性能测试（Performance Testing）
       - [K6](https://github.com/grafana/k6)
       - [JMeter](https://github.com/apache/jmeter)
       - [Crank](https://github.com/dotnet/crank)
       - [Bombardier](https://github.com/codesenberg/bombardier)
    7. 架构测试（Architecture Testing）
       - [ArchUnitNET](https://github.com/TNG/ArchUnitNET)
       - [NetArchTest](https://github.com/BenMorris/NetArchTest)   

    - 教程 📚
      - [From Zero to Hero: Unit testing in C#](https://dometrain.com/course/from-zero-to-hero-unit-testing-in-c/?affcode=1115529_alq6yoqt)
      - [From Zero to Hero: Integration testing in ASP.NET Core](https://dometrain.com/course/from-zero-to-hero-integration-testing-in-asp-net-core/?affcode=1115529_alq6yoqt)
      - [From Zero to Hero: Test-Driven Development in C#](https://dometrain.com/course/from-zero-to-hero-test-driven-development-tdd-csharp/?affcode=1115529_alq6yoqt)

16. 微服务（Microservices）

    1. 消息代理（Message-Broker）
       - [RabbitMQ](https://www.rabbitmq.com/tutorials/tutorial-one-dotnet.html)
       - [Apache Kafka](https://github.com/confluentinc/confluent-kafka-dotnet)
       - [Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging)
       - [Amazon SQS](https://aws.amazon.com/sqs)
       - [NetMQ](https://github.com/zeromq/netmq)
    2. 消息总线（Message-Bus）
       - [MassTransit](https://github.com/MassTransit/MassTransit)
       - [NServiceBus](https://github.com/Particular/NServiceBus)
       - [EasyNetQ](https://github.com/EasyNetQ/EasyNetQ)
    3. API 网关（API Gateway）
       - [Ocelot](https://github.com/ThreeMammals/Ocelot)
       - [YARP](https://github.com/microsoft/reverse-proxy)
    4. 容器化（Containerization）
       - [Docker](https://www.docker.com)
       - [Podman](https://podman.io)
    5. 编排（Orchestration）
       - [Kubernetes](https://kubernetes.io)
         - [Rancher](https://github.com/rancher/rancher)
         - [Kubectl](https://kubernetes.io/docs/reference/kubectl)
         - [K9s](https://github.com/derailed/k9s)
    6. 其他（Other）
       - [.NET Aspire](https://learn.microsoft.com/en-us/dotnet/aspire)
       - [Orleans](https://github.com/dotnet/orleans)
       - [Proto.Actor](https://github.com/asynkron/protoactor-dotnet)
       - [Dapr](https://github.com/dapr/dapr)

    - 教程 📚
      - [Getting Started: Microservices Architecture](https://dometrain.com/course/getting-started-microservices-architecture/?affcode=1115529_alq6yoqt)
      - [Getting Started: Solution Architecture](https://dometrain.com/course/getting-started-solution-architecture/?affcode=1115529_alq6yoqt)
      - [From Zero to Hero: Docker for Developers](https://dometrain.com/course/from-zero-to-hero-docker/?affcode=1115529_alq6yoqt)

17. 持续集成与交付（自动化）

    - [GitHub Actions](https://github.com/features/actions)
    - [Azure Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines)
    - [GitLab CI/CD](https://docs.gitlab.com/ee/ci)
    - [TeamCity CI/CD](https://www.jetbrains.com/teamcity)

18. 设计模式（Design Patterns）

    - 分类
      - [创建型（Creational）](https://refactoring.guru/design-patterns/creational-patterns)
      - [结构型（Structural）](https://refactoring.guru/design-patterns/structural-patterns)
      - [行为型（Behavioral）](https://refactoring.guru/design-patterns/behavioral-patterns)
    - 教程 📚
      - [Pluralsight Learning Path: Design Patterns in C#](https://www.pluralsight.com/paths/design-patterns-in-c)

19. 监控/日志记录/追踪/告警（Monitoring/Logging/Tracing/Alerting）

    - 监控（Monitoring）
      - 本地部署（On-Premises）
        - [Prometheus](https://github.com/prometheus/prometheus)
        - [Grafana](https://github.com/grafana/grafana)
      - 云部署（Cloud）
        - [Datadog](https://www.datadoghq.com)
    - 日志记录（Logging）
      - 本地部署（On-Premises）
        - [ELK Stack](https://www.elastic.co/what-is/elk-stack)
        - [Seq](https://datalust.co/seq)
        - [Sentry.io](https://sentry.io/welcome/)
      - 云部署（Cloud）
        - [Datadog](https://docs.datadoghq.com/logs)
        - [Sentry.io](https://sentry.io/welcome/)
      - 教程 📚
        - [From Zero to Hero: Logging in .NET](https://dometrain.com/course/from-zero-to-hero-logging-in-dotnet/?affcode=1115529_alq6yoqt)
    - 追踪（Tracing）
      - 本地部署（On-Premises）
        - [OpenTelemetry](https://github.com/open-telemetry/opentelemetry-dotnet)
          - [Jaeger](https://github.com/jaegertracing/jaeger)
          - [Zipkin](https://github.com/openzipkin/zipkin)
          - [Sentry.io](https://sentry.io/welcome/)
      - 云部署（Cloud）
        - [Datadog](https://docs.datadoghq.com/tracing)
        - [Sentry.io](https://sentry.io/welcome/)
    - 告警（Alerting）
      - 本地部署（On-Premises）
        - [Zabbix](https://www.zabbix.com)
        - [Alertmanager](https://github.com/prometheus/alertmanager)
      - 云部署（Cloud）
        - [Datadog](https://docs.datadoghq.com/monitors)

20. 客户端 .NET（Client-Side .NET）

    - 模板引擎（Template Engines）
      - [Razor](https://docs.microsoft.com/aspnet/core/mvc/views/razor)
      - [Scriban](https://github.com/lunet-io/scriban)
      - [Fluid](https://github.com/sebastienros/fluid)
    - 框架（Frameworks）
      - [Blazor](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
      - [.NET MAUI](https://github.com/dotnet/maui)

21. 实用库

    - [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore)
    - [MediatR](https://github.com/jbogard/MediatR)
    - [Fluent Validation](https://github.com/JeremySkinner/FluentValidation)
    - [Polly](https://github.com/App-vNext/Polly)
    - [Benchmark.NET](https://github.com/dotnet/BenchmarkDotNet)
    - [Distributed Lock](https://github.com/madelson/DistributedLock)
    - [EF Core Bulk Extensions](https://github.com/borisdj/EFCore.BulkExtensions)
    - [Nuke Build](https://github.com/nuke-build/nuke)
    - [Marten](https://github.com/JasperFx/marten)

## 总结

如果您认为本指南可以改进，请提交包含任何更新的PR或提交任何Issue。此外，我将会持续改进这个存放库，因此您可以按下 star 这个存放库以便于重新访问。

灵感来源： [React Developer RoadMap](https://github.com/adam-golab/react-developer-roadmap)
