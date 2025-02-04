---
title: Spring Boot ATNA support
layout: single
permalink: /docs/boot-atna/
classes: wide
---

`ipf-atna-spring-boot-starter` sets up the infrastructure for ATNA auditing.
 
The dependency on the IPF [Spring Boot] ATNA starter module is:

```xml
    <dependency>
        <groupId>org.openehealth.ipf.boot</groupId>
        <artifactId>ipf-atna-spring-boot-starter</artifactId>
    </dependency>
```

All IHE-related Spring boot starter modules depend on this starter module, so if you use one of those you do not have to
explicitly depend on `ipf-atna-spring-boot-starter`.
{: .notice--info}

In case want to explicitly depend on `ipf-atna-spring-boot-starter` without using Apache Camel (e.g. without using any
of the provided IHE components) or other IPF features, you can exclude the transitive dependency on 
`ipf-spring-boot-starter`:

```xml
    <dependency>
        <groupId>org.openehealth.ipf.boot</groupId>
        <artifactId>ipf-atna-spring-boot-starter</artifactId>
        <exclusions>
           <exclusion>
              <groupId>org.openehealth.ipf.boot</groupId>
              <artifactId>ipf-spring-boot-starter</artifactId>          
           </exclusion>
        </exclusions>
    </dependency>
```


`ipf-atna-spring-boot-starter` auto-configures by default:

* a configurable [`AuditContext`](../apidocs/org/openehealth/ipf/commons/audit/DefaultAuditContext.html) bean
* a basic listeners that write ATNA audit events upon application startup and shutdown 
  ([`ApplicationStartEventListener`](../apidocs/org/openehealth/ipf/boot/atna/ApplicationStartEventListener.html) 
  and [`ApplicationStopEventListener`](../apidocs/org/openehealth/ipf/boot/atna/ApplicationStopEventListener.html))
* a basic listener for login events if Spring Security is on the classpath ([`AuthenticationListener`](../apidocs/org/openehealth/ipf/boot/atna/AuthenticationListener.html)) 

You can define your own beans of this type in order to override the defaults.

`ipf-atna-spring-boot-starter` provides the following application properties that configures the `AuditContext`
as described [here]({{ site.baseurl }}{% link _pages/ihe/atna.md %}).

| Property (`ipf.atna.`)         | Default               | Description                                         |
|--------------------------------|-----------------------|-----------------------------------------------------|
| `audit-enabled`                | false                 | Whether auditing is enabled |
| `audit-repository-host`        | localhost             | Host of the ATNA repository to send the events to |
| `audit-repository-port`        | 514                   | Port of the ATNA repository to send the events to |
| `audit-repository-transport`   | UDP                   | Wire transport format (UDP, TLS) |
| `audit-source-id`              | `${spring.application.name}` | Source ID for ATNA events |
| `audit-enterprise-site-id`     |                       | Enterprise Site ID for ATNA events |
| `include-participants-from-response`| false            | Whether to include (patient) participants from responses as well |
| `audit-source-type`            | 4 (ApplicationServerProcess) | Type of Audit Source |
| `audit-queue-class`            | `org.openehealth.ipf.commons.audit.queue.SynchronousAuditMessageQueue` | Queue implementation for auditing |
| `audit-sender-class`           | as indicated by `audit-repository-transport` | ATNA sender implementation |
| `audit-exception-handler-class`| `org.openehealth.ipf.commons.audit.handler.LoggingAuditExceptionHandler`| Exception handler impleemntation |
| `audit-value-if-missing`       | `UNKNOWN`             | Value used for mandatory audit attributes that are not set |


[Spring Boot]: https://projects.spring.io/spring-boot/
