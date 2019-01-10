<!-- .slide: data-background="./images/redis-logo.png" data-background-size="70%" data-background-position="center center" -->

-@@-

## Redis

> **RE**mote **DI**ctionary **S**erver

*système de gestion de base de données clé-valeur scalable in-memory*<!-- .element class="fragment" -->

notes:
Une des principales caractéristiques de Redis est de conserver l'intégralité des données en RAM. Cela permet d'obtenir d'excellentes performances en évitant les accès disques, particulièrement coûteux sur ce plan. 

-@@-

## Redis

* Système clé-valeur
* in-memory
* scalable (cluster)
* dockerisable
* JSR 107 compliant

-@@-

## Redis - activation

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
Ajout d'une dépendance

-@@-

## Redis - configuration

```yaml
  cache:
    type: redis
    redis:
      time-to-live: 30000 # TTL global en ms
```
application.yaml

-@@-

## Redis - configuration

```
spring.cache.type=redis
spring.cache.redis.time-to-live=30000
```
application.properties

-@@-

## Redis - Time To Live

# ...

-@@-
<!-- .slide: data-background="./images/Wile_E_Coyote_04.png" data-background-size="18%" data-background-position="right bottom" -->
## Redis - Time To Live

# Global

-@@-

## Redis - JSR 107

***full compliant !!!*** <!-- .element class="fragment highlight-red" -->

-@@-

## Redis - JSR 107

```java
public void clearCache(String cacheName) {
  this.cacheManager.getCache(cacheName).clear();
}
```

-@@-

## Redis - monitoring

Facile a monitorer via le CLI

-@@-

# Demo

-@@-

## Redis

* Facile a mettre en place<!-- .element style="color: green" -->
* Facile a monitorer<!-- .element style="color: green" -->
* TTL global<!-- .element style="color: crimson" -->
* Pas de replication locale<!-- .element style="color: crimson" -->

> Use case plus restreint
