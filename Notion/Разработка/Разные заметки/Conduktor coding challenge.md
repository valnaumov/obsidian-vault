> [!info] conduktor-coding-challenge/kotlin-engineers at main · conduktor/conduktor-coding-challenge  
> Don't hesitate to do the challenges presented here and tell us: jobs@conduktor.  
> [https://github.com/conduktor/conduktor-coding-challenge/tree/main/kotlin-engineers](https://github.com/conduktor/conduktor-coding-challenge/tree/main/kotlin-engineers)  
Что такое partition?
- [ ] Приложение не должно consume messages. Сообщения должны быть переданы другому приложению. Мы — только клиент для просмотра
- [ ] Get-set properties. Admin API. Это на первом View
- [ ] List topics [https://kafka.apache.org/26/javadoc/org/apache/kafka/clients/admin/KafkaAdminClient.html#listTopics-org.apache.kafka.clients.admin.ListTopicsOptions-](https://kafka.apache.org/26/javadoc/org/apache/kafka/clients/admin/KafkaAdminClient.html#listTopics-org.apache.kafka.clients.admin.ListTopicsOptions-)
- [ ] Consume topic data from the beginning `bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092`

> [!info]  
>  
> [https://kafka.apache.org/31/documentation/streams/developer-guide/write-streams.html#testing-a-streams-app](https://kafka.apache.org/31/documentation/streams/developer-guide/write-streams.html#testing-a-streams-app)  
# Concurrency
- [ ] В чём отличие Flow от Channel?