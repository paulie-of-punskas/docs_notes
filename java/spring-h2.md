#### Kap padaryt
- sukuriam `resources/db_schema.sql`, kuriame yra DB schema
- `resources/application.properties` irasom:
```java
spring.application.name=track_workout
spring.h2.console.enabled=true
spring.datasource.generate-unique-name=false
spring.datasource.name=db_workouts

logging.level.org.springframework.jdbc=DEBUG
```

#### Paleidziam
turi but paleistas Spring'o aplinkoj. Po to, einam i browser'i: http://localhost:8080/h2-console
ir pakeiciam URL i `jdbc:h2:mem:db_workouts` (pagal `spring.datasource.name`)
