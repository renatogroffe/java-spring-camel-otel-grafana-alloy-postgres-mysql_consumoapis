# java-spring-camel-otel-grafana-alloy-postgres-mysql_consumoapis
Exemplo de aplicação criada com Java + Spring + Apache Camel e utilizando Distributed Tracing com Grafana + OpenTelemetry, com consumo de APIs REST (uma destas depende de bases PostgreSQL + MySQL). Inclui o uso de Docker Compose para a subida de ambiente que faz uso da stack Grafana, incluindo o serviço Grafana Alloy (baseado em OTLP).

APIs REST utilizadas por este projeto:
- [**Contagem de acessos (.NET 9 + ASP.NET Core)**](https://github.com/renatogroffe/aspnetcore9-otel-grafana-alloy-postgres-mysql_apicontagem)
- [**Saudações (Node.js)**](https://github.com/renatogroffe/nodejs-otel-jaeger_apisaudacoes)

Agents Java do Grafana: **https://github.com/grafana/grafana-opentelemetry-java/releases**

Documentação: **https://grafana.com/docs/grafana-cloud/monitor-applications/application-observability/instrument/jvm/**

Variáveis de ambiente a serem configuradas para uso de tracing distribuído com Jaeger:

| Variável                          | Valor                   |
|-----------------------------------|-------------------------|
| OTEL_EXPORTER_OTLP_PROTOCOL       | grpc                    |
| OTEL_EXPORTER_OTLP_TRACES_ENDPOINT| http://localhost:4317   |
| OTEL_LOGS_EXPORTER                | none                    |
| OTEL_METRICS_EXPORTER             | none                    |
| OTEL_SERVICE_NAME                 | consumerspringcamel     |
| OTEL_TRACES_EXPORTER              | otlp                    |

Essas variáveis podem ser configuradas no Eclipse IDE através do menu **Run > Run Configurations... > Environment**:

![Variáveis de ambiente no Eclipse](img/eclipse-env-var-grafana.png)

Já o Agent Java do Grafana foi configurado em **Run > Run Configurations... > Arguments > VM arguments**:

![Configurando uso do Agent Java do OpenTelemetry no Eclipse](img/eclipse-arguments-grafana.png)

Para os testes na minha máquina utilizei o valor:

```
-javaagent:D:/Java/opentelemetry/grafana-opentelemetry-java.jar
```

Visualizando no Grafana os traces gerados durante os testes, com uma interação entre as 3 aplicações aqui mencionadas:

![Traces no Grafana](img/grafana-alloy-trace.png)