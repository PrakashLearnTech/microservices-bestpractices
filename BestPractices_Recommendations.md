# microservices-bestpractices
Microservices: bestpractices and recommendations

## A) Feature flags:

Feature flags (also known as feature toggles or feature switches) are a software development technique that turns certain functionality on and off during runtime, without deploying new code. This allows for better control and more experimentation over the full lifecycle of features.

Also referred to as or release toggles, feature flags are a best practice in DevOps, often occurring within distributed version control systems.

One of the main advantage is, it decouples code deployment and feature release. Incomplete features can be merged into the production codebase but hidden behind feature flags - by controlling who sees what and when.

Few products available in the market - 

- Optimizely (Optimizely Rollouts is a free product)
- CloudBees
- LaunchDarkly
- DevCycle
- Apptimize

The feature flags also helps in scenarios like - A/B Testing and Feature gating.

B) AbstractRoutingDataSource - 

Assuming most of the micro services are going to be developed using spring boot AbstractRoutingDataSource 
api can be used in some commmon scenarios.

When the monolith is broke up in to multiple micro services. In an ideal domain bound scenario, each service will have its own data base. But there will be cross domain common services which may need to interact with multiple data bases.

AbstractRoutingDataSource

https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/datasource/lookup/AbstractRoutingDataSource.html

Based on lookup keys, we can determine which data source need to be invoked can be invoked for which scenarios. 

Also, there are scenarios where read only replica data base access will be sufficient for some use cases. The routing for such criteria can also be controlled with AbstractRoutingDataSource.

C) Functional abstraction:

When developing cloud native micro services, the code we develop inadeverently gets coupled to the 
cloud vendor platform we are hosting it.

Say for example, if I have a file upload service micro service in our application it will gets tied to AWS s3 if the hosting platfrom is AWS or Blob Storage if the hosting platform is Azure.

The approach we suggest should be - to leverage vendor managed service but don't get locked in.

When we develop the code to integrate with vendor managed services, make sure conditional bean creators are in place not only for the current hosting platform but also the promising alternatives available in the makrket. The design approach should be that the implementation's can be quickly swapped in and swapped out.

If the Amazon s3 is used, the conditional beans should be developed for Azure Blob Storage as well. Same applicable for any vendor managed service like messaging(SQS) etc.,

The basic guiding principle is - leverage vendor managed service, but never gets locked in.
