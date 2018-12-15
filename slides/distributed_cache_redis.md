
![](images/redis-logo.png)

-@@-

## dépendance

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

-@@-

## dépendance

```xml
<dependency>
    <groupId>javax.cache</groupId>
    <artifactId>cache-api</artifactId>
</dependency>
```

*Ne pas oublier*

-@@-

## Configuration

```yaml
spring:
  cache:
    type: redis
  redis:
    host: [HOST]
    port: 6379
```
-@@-

## Configuration

```
spring.cache.type=redis
spring.redis.host=[HOST]
spring.redis.port=6379
```