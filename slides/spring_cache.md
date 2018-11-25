## Spring et le cache

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```
-@@-

### spring-boot-starter-cache

> Annotations de gestion du cache

* @EnableCaching <!-- .element: class="fragment" -->
* @Cacheable <!-- .element: class="fragment" -->
* @CacheConfig <!-- .element: class="fragment" -->
* @CacheEvict<!-- .element: class="fragment" -->
* @CachePut<!-- .element: class="fragment" -->

-@-

### @EnableCaching

Activation du cache au niveau applicatif

```java
@SpringBootApplication
@EnableCaching
public class MainappApplication {

  public static void main(String[] args) {
      SpringApplication.run(MainappApplication.class, args);
  }

}
```
<!-- .element: class="fragment" -->

-@-

### @Cacheable

Permet de chercher dans le cache une valeur lié à la clé

si la valeur est non présente, l'injecte dans le cache

-@@-

### @Cacheable

```java
@Cacheable
Message findByCode(String code);
```

-@@-

### @Cacheable

```java
@Cacheable("messages")
Message findByCode(String code);
```

Mais c'est mieux de preciser le nom du cache

-@@-

### @Cacheable

```java
@Cacheable(value = "messages")
Message findByCode(String code);
```

Mais c'est mieux de preciser le nom du cache

-@@-

### @Cacheable

```java
@Cacheable(value = "messages", unless = "#result == null")
Message findByCode(String code);
```

Aussi de preciser quand cacher ou non

-@@-

### @Cacheable

Que faire quand la clé est un objet "complexe" ?

Et si en plus la méthode a plusieurs paramètres ?

-@@-

### @Cacheable

```java
@Cacheable(
  value = "teams", key = "#p0.name", unless = "#result == null"
)
TeamWithDetails buildTeam(Team team, Locale locale);
```

Utilisation d'expressions `SpEL` 

-@@-

### @Cacheable

Accès concurrentiel

```java
@Cacheable(
  value = "messages", unless = "#result == null", sync = true
)
Message findByCode(String code);
```

sync(true) permet l'injection et l'utilisation du cache par 1 thread


-@@-

### @Cacheable

Accès concurrentiel

```java
@Cacheable(
  value = "messages", unless = "#result == null", sync = true
)
Optional<Message> findByCode(String code);
```

***Ne fonctionne pas !!***<!-- .element: style="color: crimson" -->

*sync ne gere pas les `Optional`*

