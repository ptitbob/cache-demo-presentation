## Cache spring simple

Exposition d'un `@Bean` pour le cache manager

-@@-

## Les dépendances

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

-@@-

## Cache spring simple

```java
@Configuration
public class CachingConfig {
    @Bean
    public CacheManager cacheManager() {
        return new ConcurrentMapCacheManager("messages");
    }
}
```

-@@-

## Cache spring simple

Pratique pour un POC

Simple

Mais<!-- .element class="fragment" style="font-family: 'Sedgwick Ave', cursive; font-size: 1.5em; color: crimson;" -->

-@@-

## Cache spring simple

Peu ou pas paramétrable à la demande

Pas de gestion de la taille du heap

Pas de durée de vie

notes:
Pas de templating non plus
-@@-
<!-- .slide: data-background="./images/Wile_E_Coyote_06.png" data-background-size="24%" data-background-position="left bottom" -->
*Si aucune délétion*

*Les données reste*

*en permanence dans le cache*

-@@-
<!-- .slide: data-background="./images/nuclear-explosion.jpg" data-background-size="100%" data-background-position="center center" -->
# problème <!-- .element style="color: black; font-family: 'Bangers', cursive;" -->

## Out Of Memory <!-- .element class="fragment" style="color: white; font-family: 'Bangers', cursive;" -->

-@@-

### Solutions ?

* Limite la quantité de donnée cachée
* Durée de vie du cache

-@@-

### Solutions ?

* Limite la quantité de donnée cachée --> heap size
* Durée de vie du cache --> TTL

-@@-

### Solutions ?

> Solution permettant une gestion du cache
> local et/ou distribué

* ehCache
* Redis
* Hazelcast

