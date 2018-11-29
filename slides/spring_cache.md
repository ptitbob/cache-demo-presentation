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

* @EnableCaching 
* @Cacheable 
* @CacheConfig 
* @CacheEvict 
* @CachePut 

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

Utilisation d'expressions **`SpEL`**

> (**`Sp`**ring **`E`**xpression **`L`**anguage)

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

-@-

## @CacheConfig

Configuration du cache de manière globale pour une classe

-@@-

## @CacheConfig

```java
@CacheConfig(cacheNames = "messages")
public interface MessageRepository ... {
  ...
}
```

-@@-

## @CacheConfig

```java
@CacheConfig(cacheNames = {"messages"})
public interface MessageRepository ... {
  ...
}
```

> On peut définir plusieurs caches

-@@-

## @CacheConfig

```java
@CacheConfig(cacheNames = {"messages", "cache2"})
public interface MessageRepository ... {
  ...
}
```

> On peut définir plusieurs caches

-@@-

## @CacheConfig

*La déclaration d'une mise en cache devient*

```java
@CacheConfig(cacheNames = "messages")
public interface MessageRepository ... {
  ...
  @Cacheable(unless = "#result == null")
  Optional<Message> findByCode(String code);
  ...
}
```

-@-

## @CacheEvict

Permet la suppression d'une valeur

> rendre le cache consistant

-@@-

## @CacheEvict

```java
@CacheEvict(key = "#p0.code")
void delete(Message message);
```

> Utilisation `SpEL` afin de preciser la clé.

-@@-

## @CacheEvict

*Et suppression de toutes les valeurs*<!-- .element style="color: crimson;" -->

```java
@CacheEvict(allEntries = true)
void deleteAll(List<Message> messageList);
```

-@-

## @CachePut

*Injecter ou mettre à jour une valeur*

> rendre le cache consistant

-@@-

## @CachePut

```java
@CachePut(key = "#result.code", condition = "#result != null")
Message save(Message message);
```

> Dans ce cas, le code fait un `create` et un `update`

-@-

***En conclusion***

* `@Cacheable` : Accès à la donnée en cache
* .............  Permet la mise en cache à l'accès <!-- .element class="fragment" -->
* `@CacheEvict` : Suppression d'une(des) valeur(s)
* `@CachePut` : Mise en cache / MàJ d'une valeur

*`@CacheEvict` & `@CachePut` participe à la cohésion du cache*<!-- .element style="color: #00cc99" -->

-@-

***Au final***

```java
@CacheConfig(cacheNames = "messages")
public interface MessageRepository ... {

  @Cacheable(unless = "#result == null")
  Optional<Message> findByCode(String code);

  @CacheEvict(key = "#p0.code")
  void delete(Message message);

  @CachePut(key = "#result.code", condition = "#result != null")
  Message save(Message message);

}
```

-@-

# Démo
