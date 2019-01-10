<!-- .slide: data-background="./images/HazelcastLogo-Blue_Dark_800px.png" data-background-size="80%" data-background-position="center center" -->

-@@-

## Hazelcast

Datagrid in-memory scalable

-@@-

## Hazelcast

* Système clé-valeur
* in-memory
* local / synchronisé
* Auto découvrable (sic)

-@@-

## Hazelcast - activation

```xml
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast</artifactId>
</dependency>
<dependency>
    <groupId>com.hazelcast</groupId>
    <artifactId>hazelcast-spring</artifactId>
</dependency>
```

Ajout de 2 dépendances

-@@-

## Hazelcast - activation

Pas JSR107 compliant !<!-- .element style="color: crimson" -->

Suppression de la dépendance JSR107 <!-- .element class="fragment" -->

Pas de gestion des caches <!-- .element class="fragment" style="color: crimson" -->

-@@-

## Hazelcast - configuration

* configuration application
* Fichier de configuration Hazelcast

-@@-

## Hazelcast - configuration

```yaml
spring:
  cache:
    type: hazelcast
  hazelcast:
    config: classpath:hazelcast.xml
```

`application.yml`

-@@-

## Hazelcast - configuration

```
spring.cache.type=hazelcast
spring.hazelcast.config=classpath:hazelcast.xml
```

`application.properties`

-@@-

## Hazelcast - configuration

```xml
<hazelcast
  xsi:schemaLocation="http://www.hazelcast.com/schema/config http://www.hazelcast.com/schema/config/hazelcast-config.xsd"
  xmlns="http://www.hazelcast.com/schema/config"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
...
</hazelcast>
```
`hazelcast.xml`

-@@-

## Hazelcast - configuration

```xml
<hazelcast...>
  <map name="message">
    <max-size>200</max-size>
    <eviction-policy>LFU</eviction-policy>
    <time-to-live-seconds>30</time-to-live-seconds>
  </map>
</hazelcast>
```
`hazelcast.xml`

-@@-

## Hazelcast - Docker

***Obligation pour les noeuds d'être au sein d'un même reseau***<!-- .element style="color:crimson" -->

*Auto découverte des noeuds et synchronisation*

-@@-

# Demo

-@@-

## Hazelcast

* Facile a mettre en place<!-- .element style="color: green" -->
* auto-synchronisation<!-- .element style="color: green" -->
* cache configurable individuellement<!-- .element style="color: green" -->
* pas de monitoring<!-- .element style="color: crimson" -->
* Pas de replication locale<!-- .element style="color: crimson" -->
* JSR 107 non compliant<!-- .element style="color: crimson" -->
* Pas de serveur dédié<!-- .element style="color: green" -->

-@@-

## Hazelcast

* Facile a mettre en place<!-- .element style="color: green" -->
* auto-synchronisation<!-- .element style="color: green" -->
* cache configurable individuellement<!-- .element style="color: green" -->
* pas de monitoring<!-- .element style="color: crimson" -->
* Pas de replication locale<!-- .element style="color: crimson" -->
* JSR 107 non compliant<!-- .element style="color: crimson" -->
* Pas de serveur dédié <-- c'est aussi un défaut<!-- .element style="color: red" -->

