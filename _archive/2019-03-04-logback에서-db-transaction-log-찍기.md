logback에서 db transaction log 찍기
===

### 설정 추가하기

```xml
  <logger name="org.mybatis.spring.transaction.SpringManagedTransaction" level="${LEVEL}" additivity="false">
    <appender-ref ref="console"/>
  </logger>

  <logger name="org.springframework.jdbc.DataSourceTransactionManager" level="${LEVEL}" additivity="true">
    <appender-ref ref="console"/>
  </logger>

  <logger name="org.springframework.jdbc.datasource.DataSourceTransactionManager" level="${LEVEL}" additivity="false">
    <appender-ref ref="console"/>
  </logger>
```