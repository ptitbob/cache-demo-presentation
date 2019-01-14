<!-- .slide: data-background="./images/ehcache-logo.png" data-background-size="80%" data-background-position="center center" -->


-@@-

## ehCache

lib OSS

A inspiré la JSR 107

Porté par Terracotta

Element (un des) par défaut SpringBoot

-@@-

## ehCache

Gestion de la taille

Gestion TTL

Via @Bean<!-- .element class="fragment fade-out" -->

Via configuration

Templating

-@@-

## dependance

`pom.xml`

```xml
<dependency>
    <groupId>org.ehcache</groupId>
    <artifactId>ehcache</artifactId>
</dependency>
```
ou<!-- .element class="fragment" -->
```xml
<dependency>
    <groupId>org.ehcache</groupId>
    <artifactId>ehcache</artifactId>
    <scope>runtime</scope>
</dependency>
```
<!-- .element class="fragment" -->

-@@-

## initialisation

`application.yaml`

```yaml
spring:
  cache:
    jcache:
      config: ehcache.xml
```

-@@-

## initialisation

`application.properties`

```
spring.cache.jcache.config=ehcache.xml
```

-@@-

## `ehcache.xml`

```xml
<config xmlns="http://www.ehcache.org/v3"
  xmlns:jsr107="http://www.ehcache.org/v3/jsr107">
    
</config>
```
*la base*

-@@-

## `ehcache.xml`

```xml
<config xmlns="http://www.ehcache.org/v3"
  xmlns:jsr107="http://www.ehcache.org/v3/jsr107">
    <cache alias="messages">
        <heap unit="entries">10</heap>
    </cache>
</config>
```

-@@-

## `ehcache.xml`

```xml
<cache alias="messages">
    <heap unit="entries">10</heap>
</cache>
```

*Taille du heap*

Entries(défaut), B, kB, MB, GB, TB, PB

-@@-

## `ehcache.xml`

```xml
<cache alias="messages">
    <expiry>
        <ttl unit="hours">6</ttl>
    </expiry>
</cache>
```
> `T`ime `T`o `L`ive

nanos, micros, millis, seconds(défaut), minutes, hours, days

notes:
Autant pour la taille ils ont vu grand, pour ttl c'est plus raisonnable

-@@-

## `ehcache.xml`

```xml
<cache alias="messages">
    <expiry>
        <ttl unit="hours">6</ttl>
    </expiry>
</cache>
```
> `T`ime `T`o `L`ive

Temps max de presence d'un élément dans le cache, sans se soucier du nombre d'accès

-@@-

## `ehcache.xml`

```xml
<cache alias="messages">
    <expiry>
        <tti unit="minutes">30</tti>
    </expiry>
</cache>
```
> `T`ime `T`o `I`dle

Temps de presence d'un élément sans accès

-@@-

## `ehcache.xml`

```xml
<cache alias="messages">
    <expiry>
        <ttl unit="hours">6</ttl>
    </expiry>
    <heap unit="entries">10</heap>
</cache>
```

> Combinaison !

*Astuce : Expiration avant la taille*<!-- .element class="fragment" -->

