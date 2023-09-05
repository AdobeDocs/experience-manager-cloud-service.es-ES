---
title: Reglas de calidad del código personalizadas
description: Esta página describe las reglas de calidad del código personalizadas ejecutadas por Cloud Manager como parte de las pruebas de calidad del código. Se basan en las prácticas recomendadas de ingeniería de Adobe Experience Manager.
exl-id: f40e5774-c76b-4c84-9d14-8e40ee6b775b
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: ht
source-wordcount: '3502'
ht-degree: 100%

---

# Reglas de calidad de código personalizadas {#custom-code-quality-rules}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_customcodequalityrules"
>title="Reglas de calidad del código personalizadas"
>abstract="Esta página describe las reglas de calidad del código personalizadas ejecutadas por Cloud Manager como parte de las pruebas de calidad del código. Se basan en las prácticas recomendadas de ingeniería de Adobe Experience Manager."

Esta página describe las reglas de calidad del código personalizadas ejecutadas por Cloud Manager como parte de las [pruebas de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md). Se basan en las prácticas recomendadas de ingeniería de Experience Manager.

>[!NOTE]
>
>Las reglas completas de SonarQube no están disponibles para su descarga debido a la información de Adobe registrada. Puede descargar la lista completa de reglas [mediante este vínculo](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx). Continúe leyendo este documento para obtener descripciones y ejemplos de las reglas.

>[!NOTE]
>
>Los ejemplos de código que se proporcionan aquí solo tienen fines ilustrativos. Consulte la [Documentación de conceptos](https://docs.sonarqube.org/latest/) de SonarQube para conocer los conceptos y las reglas de calidad de SonarQube.

## Reglas de SonarQube {#sonarqube-rules}

La siguiente sección detalla las reglas de SonarQube ejecutadas por Cloud Manager.

### No utilizar funciones potencialmente peligrosas {#do-not-use-potentially-dangerous-functions}

* **Clave**: CQRules: CWE-676
* **Tipo**: Vulnerabilidad
* **Gravedad**: Principal
* **Desde**: Versión 2018.4.0

Los métodos `Thread.stop()` y `Thread.interrupt()` pueden ocasionar problemas difíciles de reproducir y, a veces, vulnerabilidades de seguridad. Su utilización debe ser objeto de un estricto seguimiento y validación. En general, transmitir mensajes es una manera más segura de lograr objetivos similares.

#### Código no conforme {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### Código conforme {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### No usar cadenas de formato que puedan estar controladas externamente {#do-not-use-format-strings-which-may-be-externally-controlled}

* **Clave**: CQRules: CWE-134
* **Tipo**: Vulnerabilidad
* **Gravedad**: Principal
* **Desde**: Versión 2018.4.0

El uso de una cadena de formato de una fuente externa (como un parámetro de solicitud o contenido generado por el usuario) puede producir y exponer una aplicación a ataques de denegación de servicio. Hay circunstancias en las que una cadena de formato puede estar controlada externamente, pero solo se permite desde fuentes de confianza.

#### Código no conforme {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### Las solicitudes HTTP siempre deben tener tiempos de espera de conexión y socket {#http-requests-should-always-have-socket-and-connect-timeouts}

* **Clave**: CQRules:ConnectionTimeoutMechanism
* **Tipo**: Error
* **Gravedad**: Crítico
* **Desde**: Versión 2018.6.0

Al ejecutar solicitudes HTTP desde la aplicación de Experience Manager, es esencial asegurarse de que se hayan configurado los tiempos de espera adecuados para evitar un consumo de hilos innecesario. Lamentablemente, el comportamiento predeterminado de ambos clientes HTTP predeterminados de Java™ (`java.net.HttpUrlConnection`) y el cliente de componentes HTTP de Apache que se utiliza con frecuencia es nunca emplear el tiempo de espera, por lo que se debe establecer explícitamente. Además, como práctica recomendada, estos tiempos de espera no deben superar los 60 segundos.

#### Código no conforme {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### Código conforme {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### Cerrar siempre objetos ResourceResolver {#resourceresolver-objects-should-always-be-closed}

* **Clave**: CQRules:CQBP-72
* **Tipo**: Code Smell
* **Gravedad**: Principal
* **Desde**: Versión 2018.4.0

Objetos `ResourceResolver` obtenidos de recursos del sistema de consumo `ResourceResolverFactory`. Aunque existen medidas para recuperar estos recursos cuando `ResourceResolver` ya no está en uso, es más eficiente cerrar explícitamente cualquier objeto `ResourceResolver` llamando al método `close()`.

Una idea errónea relativamente frecuente es que los objetos `ResourceResolver` creados con una sesión de JCR existente no deben cerrarse explícitamente o que, de hacerlo, cerrarán la sesión de JCR subyacente. No suele ser el caso. Independientemente de cómo se abra `ResourceResolver`, debe cerrarse cuando ya no se utiliza. Dado que `ResourceResolver` implementa la interfaz `Closeable`, también es posible utilizar la sintaxis `try-with-resources` en lugar de invocar explícitamente `close()`.

#### Código no conforme {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Código conforme {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### No utilizar las rutas del servlet de Sling para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

* **Clave**: CQRules:CQBP-75
* **Tipo**: Code Smell
* **Gravedad**: Principal
* **Desde**: Versión 2018.4.0

Como se describe en la sección [Documentación de Sling](https://sling.apache.org/documentation/the-sling-engine/servlets.html), se desaconsejan los servlets de enlace por rutas. Los servlets enlazados a rutas no pueden utilizar controles de acceso JCR estándar y, como resultado, requieren un rigor de seguridad adicional. En lugar de utilizar servlets enlazados a rutas, se recomienda crear nodos en el repositorio y registrar servlets por tipo de recurso.

#### Código no conforme {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Las excepciones capturadas deben registrarse o activarse, no ambas {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **Clave**: CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

En general, una excepción debe registrarse exactamente una vez. El registro de excepciones varias veces puede causar confusión, ya que no está claro cuántas veces se produjo una excepción. El patrón más común que lleva a esto es registrar y arrojar una excepción capturada.

#### Código no conforme {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### Código conforme {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### Evitar las instrucciones de registro seguidas inmediatamente por las sentencias de lanzamiento {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **Clave**: CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

Otro patrón común que se debe evitar es registrar un mensaje y luego iniciar inmediatamente una excepción. Esta práctica generalmente indica que el mensaje de excepción termina duplicado en los archivos de registro.

#### Código no conforme {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Código conforme {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Evitar iniciar sesión en la información al gestionar solicitudes GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **Clave**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests
* **Tipo**: Code Smell
* **Gravedad**: Menor

En general, el nivel de registro INFO debe utilizarse para demarcar acciones importantes y, de forma predeterminada, Experience Manager está configurado para registrar a nivel INFO o superior. Los métodos GET y HEAD solo deben ser operaciones de solo lectura y, por lo tanto, no constituyen acciones importantes. Es probable que el registro en el nivel INFO como respuesta a solicitudes de GET o HEAD cree un ruido de registro significativo, lo que dificulta la identificación de información útil en los archivos de registro. El registro al administrar solicitudes de GET o HEAD debe realizarse en los niveles WARN o ERROR cuando algo ha salido mal o en los niveles DEBUG o TRACE si sería útil disponer de información más detallada sobre la solución de problemas.

>[!NOTE]
>
>Esto no se aplica al registro de tipo `access.log` para cada solicitud.

#### Código no conforme {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Código conforme {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### No usar Exception.getMessage() como primer parámetro de un enunciado de registro {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **Clave**: CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

Como práctica recomendada, los mensajes de registro deben proporcionar información contextual sobre dónde se ha producido una excepción en la aplicación. Aunque el contexto también se puede determinar mediante el uso de trazos de pila, en general, el mensaje de registro será más fácil de leer y comprender. Como resultado, al registrar una excepción, es una mala práctica utilizar el mensaje de la excepción como mensaje de registro. El mensaje de excepción contiene lo que ha salido mal, mientras que el mensaje de registro debe utilizarse para indicar a un lector de registro qué estaba haciendo la aplicación cuando se produjo la excepción. El mensaje de excepción se sigue registrando. Al especificar su propio mensaje, los registros son más fáciles de entender.

#### Código no conforme {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Código conforme {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### El registro en bloques de captura debe estar en el nivel WARN o ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **Clave**: CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

Como sugiere el nombre, las excepciones de Java™ siempre deben usarse en circunstancias excepcionales. Como resultado, cuando se captura una excepción, es importante asegurarse de que los mensajes de registro se registren en el nivel adecuado, WARN o ERROR. Esto garantiza que esos mensajes aparezcan correctamente en los registros.

#### Código no conforme {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Código conforme {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### No imprimir trazos de pila en la consola {#do-not-print-stack-traces-to-the-console}

* **Clave**: CQRules:CQBP-44---ExceptionPrintStackTrace
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

Como se ha mencionado, el contexto es fundamental para comprender los mensajes de registro. El uso de `Exception.printStackTrace()` hace que solo el trazo de pila se envíe al flujo de error estándar, lo que provoca que se pierda todo el contexto. Además, en una aplicación multiproceso como Experience Manager, si se imprimen varias excepciones mediante este método en paralelo, sus trazos de pila pueden superponerse, lo que produce una confusión significativa. Las excepciones solo deben registrarse en el marco de registro.

#### Código no conforme {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Código conforme {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### No enviar a salida estándar o error estándar {#do-not-output-to-standard-output-or-standard-error}

* **Clave**: CQRules:CQBP-44—LogLevelConsolePrinters
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

El inicio de sesión de Experience Manager siempre se debe realizar mediante el marco de trabajo de registro (SLF4J). La salida directa a los flujos de error estándar o de salida estándar pierde la información estructural y contextual proporcionada por el marco de trabajo de registro. A veces, puede causar problemas de rendimiento.

#### Código no conforme {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Código conforme {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Evitar las rutas /apps y /libs codificadas {#avoid-hardcoded-apps-and-libs-paths}

* **Clave**: CQRules:CQBP-71
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2018.4.0

En general, las rutas que comienzan por `/libs` y `/apps` no deben estar codificadas, ya que las rutas a las que se refieren generalmente se almacenan como rutas relativas a la ruta de búsqueda de Sling, que está configurada como `/libs,/apps` de forma predeterminada. El uso de la ruta absoluta puede introducir defectos sutiles que solo aparecerían más adelante en el ciclo de vida del proyecto.

#### Código no conforme {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Código conforme {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### El planificador de Sling no debe utilizarse {#sonarqube-sling-scheduler}

* **Clave**: CQRules:AMSCORE-554
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

El planificador de Sling no debe utilizarse para tareas que requieren una ejecución garantizada. Los trabajos programados de Sling garantizan la ejecución y son más adecuados para los entornos agrupados y no agrupados.

Consulte la [Documentación sobre eventos de Apache Sling y gestión de trabajos](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) para obtener más información acerca de cómo se administran los trabajos de Sling en entornos agrupados.

### Las API en desuso de Experience Manager no deben usarse {#sonarqube-aem-deprecated}

* **Clave**: AMSCORE-553
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

La superficie de la API de Experience Manager está en constante revisión para identificar las API para las que se desaconseja el uso y que, por lo tanto, se consideran en desuso.

A menudo, estas API están en desuso al utilizar la anotación `@Deprecated` de Java™ estándar y, como tal, identificada por `squid:CallToDeprecatedMethod`.

Sin embargo, hay casos en los que una API está en desuso en el contexto de Experience Manager, pero puede que no en otros contextos. Esta regla identifica esta segunda clase.


## Reglas de contenido OakPAL {#oakpal-rules}

La siguiente sección detalla las comprobaciones OakPAL ejecutadas por Cloud Manager.

>[!NOTE]
>
>OakPAL es un marco de trabajo, que valida paquetes de contenido usando un repositorio Oak independiente. Fue desarrollado por un socio de Experience Manager y ganador del premio de 2019 Experience Manager Rockstar Norteamérica.

### Los clientes no deben implementar ni ampliar las API de producto anotadas con @ProviderType {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **Clave**: CQBP-84
* **Tipo**: Error
* **Gravedad**: Crítico
* **Desde**: Versión 2018.7.0

La API de Experience Manager contiene interfaces y clases de Java™ que solo están pensadas para utilizarse, pero no para implementarse, mediante código personalizado. Por ejemplo, la interfaz `com.day.cq.wcm.api.Page` está diseñada para que la implemente solo Experience Manager.

Cuando se agregan nuevos métodos a estas interfaces, esos métodos adicionales no afectan al código existente que emplea estas interfaces. Como resultado, la adición de nuevos métodos a estas interfaces se considera compatible con versiones anteriores. Sin embargo, si el código personalizado implementa una de estas interfaces, dicho código personalizado ha introducido un riesgo de compatibilidad con versiones anteriores para el cliente.

Las interfaces y clases, implementadas por Experience Manager, están anotadas con `org.osgi.annotation.versioning.ProviderType` o, a veces, una anotación heredada similar `aQute.bnd.annotation.ProviderType`. Esta regla identifica los casos en los que se implementa una interfaz de este tipo o en los que una clase se amplía mediante código personalizado.

#### Código no conforme {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Los índices personalizados de Lucene Oak deben tener una configuración de Tika {#oakpal-indextikanode}

* **Clave**: IndexTikaNode
* **Tipo**: Error
* **Gravedad**: Bloqueador
* **Desde**: 2021.8.0

Múltiples índices de Oak de Experience Manager listos para usar incluyen una configuración de Tika y las personalizaciones de estos índices deben incluirla. Esta regla comprueba las personalizaciones de los índices `damAssetLucene`, `lucene` y `graphqlConfig` generan un problema si el nodo `tika` falta o el nodo `tika` no tiene un nodo secundario llamado `config.xml`.

Consulte la [documentación de indexación](/help/operations/indexing.md#preparing-the-new-index-definition) para obtener más información sobre la personalización de definiciones de índice.

#### Código no conforme {#non-compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
```

#### Código conforme {#compliant-code-indextikanode}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Los índices personalizados de Lucene Oak no deben ser sincrónicos {#oakpal-indexasync}

* **Clave**: IndexAsyncProperty
* **Tipo**: Error
* **Gravedad**: Bloqueador
* **Desde**: 2021.8.0

Los índices Oak del tipo `lucene` siempre deben estar indexado asincrónicamente. Si no es así, puede causar inestabilidad en el sistema. Puede encontrar más información sobre la estructura de los índices de Lucene en la [Documentación de Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html#index-definition)

#### Código no conforme {#non-compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

#### Código conforme {#compliant-code-indexasync}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Los índices personalizados de recursos DAM de Lucene Oak están correctamente estructurados  {#oakpal-damAssetLucene-sanity-check}

* **Clave**: IndexDamAssetLucene
* **Tipo**: Error
* **Gravedad**: Bloqueador
* **Desde**: 2021.6.0

Para que la búsqueda de recursos funcione correctamente en Experience Manager Assets, las personalizaciones del índice Oak `damAssetLucene` deben seguir un conjunto de directrices específicas de este índice. Esta regla comprueba que la definición del índice debe tener una propiedad de varios valores denominada `tags` que contiene el valor `visualSimilaritySearch`.

#### Código no conforme {#non-compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - type: lucene
      + tika
        + config.xml
```

#### Código conforme {#compliant-code-damAssetLucene}

```text
+ oak:index
    + damAssetLucene-1-custom-2
      - async: [async, nrt]
      - evaluatePathRestrictions: true
      - includedPaths: /content/dam
      - reindex: false
      - tags: [visualSimilaritySearch]
      - type: lucene
      + tika
        + config.xml
```

### Los paquetes de clientes no deben crear ni modificar nodos en /libs {#oakpal-customer-package}

* **Clave**: BannedPath
* **Tipo**: Error
* **Gravedad**: Crítico
* **Desde**: Versión 2019.6.0

Una práctica recomendada clásica es que el árbol de contenido `/libs` en el repositorio de contenido de Experience Manager debe considerarse de solo lectura por los clientes. Modificar nodos y propiedades en `/libs` crea un riesgo significativo para las actualizaciones principales y secundarias. Las modificaciones a `/libs` debe hacerlas Adobe a través de canales oficiales.

### Los paquetes no deben contener configuraciones OSGi duplicadas {#oakpal-package-osgi}

* **Clave**: DuplicateOsgiConfigurations
* **Tipo**: Error
* **Gravedad**: Principal
* **Desde**: Versión 2019.6.0

Un problema común que ocurre en proyectos complejos es que el mismo componente OSGi se configura varias veces. Este problema crea una ambigüedad sobre la configuración que se aplicará. Esta regla es “según el modo de ejecución”, ya que solo identifica problemas en los que el mismo componente se haya configurado varias veces en el mismo modo de ejecución o combinación de modos de ejecución.

>[!NOTE]
>
>Esta regla produce problemas en los que la misma configuración, en la misma ruta, se define en varios paquetes, incluso casos en los que el mismo paquete se duplica en la lista general de paquetes creados.
>
>Por ejemplo, si la generación produce paquetes llamados `com.myco:com.myco.ui.apps` y `com.myco:com.myco.all` donde `com.myco:com.myco.all` incrusta `com.myco:com.myco.ui.apps`, entonces todas las configuraciones dentro de `com.myco:com.myco.ui.apps` se registrarán como duplicadas.
>
>Esto suele ser un caso en el que no se siguen las [Directrices de estructura del paquete de contenido](/help/implementing/developing/introduction/aem-project-content-package-structure.md). En este ejemplo específico, el paquete `com.myco:com.myco.ui.apps` no tiene la propiedad `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Código no conforme {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Código conforme {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Las carpetas de configuración e instalación solo deben contener nodos OSGi {#oakpal-config-install}

* **Clave**: ConfigAndInstallShouldOnlyContainOsgiNodes
* **Tipo**: Error
* **Gravedad**: Principal
* **Desde**: Versión 2019.6.0

Por motivos de seguridad, las rutas que contienen `/config/` y `/install/` solo pueden leerlas los usuarios administrativos de Experience Manager y solo deben utilizarse para la configuración OSGi y los paquetes OSGi. Colocar otros tipos de contenido en rutas que contienen estos segmentos resulta en un comportamiento de la aplicación que varía involuntariamente entre usuarios administrativos y no administrativos.

Un problema común es el uso de nodos llamados `config` en los cuadros de diálogo de componentes o al especificar la configuración del editor de texto enriquecido para la edición en línea. Para resolver este problema, se debe cambiar el nombre del nodo infractor por uno conforme. Para la configuración del editor de texto enriquecido, utilice la propiedad `configPath` en el nodo `cq:inplaceEditing` para especificar la nueva ubicación.

#### Código no conforme {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Código conforme {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Los paquetes no deben superponerse {#oakpal-no-overlap}

* **Clave**: PackageOverlaps
* **Tipo**: Error
* **Gravedad**: Principal
* **Desde**: Versión 2019.6.0

Similar a la regla [Los paquetes no deben contener configuraciones OSGi duplicada,](#oakpal-package-osgi), este es un problema común en proyectos complejos en los que la misma ruta de nodo se escribe en varios paquetes de contenido independientes. Aunque el uso de dependencias de paquetes de contenido se puede utilizar para garantizar un resultado coherente, es mejor evitar las superposiciones por completo.

### El modo de creación predeterminado no debe ser la IU clásica {#oakpal-default-authoring}

* **Clave**: ClassicUIAuthoringMode
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

La configuración OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` define el modo de creación predeterminado en Experience Manager. Dado que la IU clásica ha quedado en desuso desde Experience Manager 6.4, ahora se genera un problema cuando el modo de creación predeterminado esté configurado en la IU clásica.

### Los componentes con cuadros de diálogo deben tener cuadros de diálogo de IU táctil {#oakpal-components-dialogs}

* **Clave**: ComponentWithOnlyClassicUIDialog
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

Los componentes de Experience Manager que tengan un cuadro de diálogo de IU clásica siempre deben tener un cuadro de diálogo correspondiente de IU táctil. Ambas ofrecen una experiencia de creación óptima y son compatibles con el modelo de implementación de Cloud Service, con el que la IU clásica no es compatible. Esta regla verifica los siguientes escenarios:

* Un componente con un cuadro de diálogo de IU clásica (es decir, un nodo `dialog` secundario) debe tener un cuadro de diálogo correspondiente de la interfaz de usuario táctil (es decir, un nodo `cq:dialog` secundario).
* Un componente con un cuadro de diálogo de diseño de IU clásica (es decir, un nodo `design_dialog`) debe tener un cuadro de diálogo de diseño de IU táctil correspondiente (es decir, un nodo secundario `cq:design_dialog`).
* Un componente con un cuadro de diálogo y de diseño de IU clásica debe tener un cuadro de diálogo de IU táctil y un cuadro de diálogo de diseño de IU táctil correspondiente.

La documentación de Herramientas de modernización de Experience Manager proporciona documentación y herramientas para convertir componentes de la IU clásica a la IU táctil. Consulte la [documentación de Herramientas de modernización de Experience Manager](https://opensource.adobe.com/aem-modernize-tools/) para obtener más información.

### Los paquetes no deben mezclar contenido mutable e inmutable {#oakpal-packages-immutable}

* **Clave**: ImmutableMutableMixedPackage
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

Para que sean compatibles con el modelo de implementación de Cloud Service, los paquetes de contenido individuales deben incluir contenido para las áreas inmutables del repositorio (`/apps` y `/libs`) o el área modificable (todo lo que no está en `/apps` o `/libs`), pero no ambas. Por ejemplo, un paquete que incluye `/apps/myco/components/text` y `/etc/clientlibs/myco`, no es compatible con Cloud Service y provoca que se notifique un problema.

>[!NOTE]
>
>La regla [Los paquetes de clientes no deben crear ni modificar nodos en /libs](#oakpal-customer-package) siempre se aplica.

Consulte [Documentación de la estructura del proyecto de Experience Manager](/help/implementing/developing/introduction/aem-project-content-package-structure.md) para obtener más información.

### No utilizar agentes de replicación inversa {#oakpal-reverse-replication}

* **Clave**: ReverseReplication
* **Tipo**: Compatibilidad de Code Smell/Cloud Service
* **Gravedad**: Menor
* **Desde**: Versión 2020.5.0

El soporte para la replicación inversa no está disponible en las implementaciones de Cloud Service, tal como se describe como parte de las [notas de la versión de Experience Manager as a Cloud Service](/help/release-notes/aem-cloud-changes.md#replication-agents).

Los clientes que utilizan la replicación inversa deben ponerse en contacto con Adobe para obtener soluciones alternativas.

### Los recursos contenidos en las bibliotecas cliente habilitadas para proxy deben estar en una carpeta denominada Recursos {#oakpal-resources-proxy}

* **Clave**: ClientlibProxyResource
* **Tipo**: Error
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Las bibliotecas de cliente de Experience Manager pueden contener recursos estáticos como imágenes y fuentes. Como se describe en el documento [Uso de preprocesadores,](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors) al utilizar bibliotecas cliente proxy, estos recursos estáticos deben estar contenidos en una carpeta secundaria denominada `resources` para que se pueda consultar en las instancias de publicación.

#### Código no conforme {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Código conforme {#compliant-proxy-enabled}

```tet
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### Uso de procesos de flujo de trabajo incompatibles con Cloud Service {#oakpal-usage-cloud-service}

* **Clave**: CloudServiceIncompatibleWorkflowProcess
* **Tipo**: Error
* **Gravedad**: Principal
* **Desde**: Versión 2021.2.0

Con el cambio a los microservicios de recursos para el procesamiento de recursos en Experience Manager as a Cloud Service, varios procesos de flujo de trabajo que se utilizaron en las versiones On-Premise y AMS de Experience Manager han dejado de ser compatibles o son innecesarios.

La herramienta de migración en el [Repositorio de GitHub de Experience Manager as a Cloud Service Assets](https://github.com/adobe/aem-cloud-migration) se puede utilizar para actualizar modelos de flujo de trabajo durante la migración a Experience Manager as a Cloud Service.

### No se recomienda el uso de plantillas estáticas en lugar de plantillas editables {#oakpal-static-template}

* **Clave**: StaticTemplateUsage
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Si bien el uso de plantillas estáticas siempre ha sido muy común en proyectos de Experience Manager, Adobe recomienda el uso de plantillas editables, ya que proporcionan la mayor flexibilidad y admiten funciones adicionales que no están presentes en las estáticas. Encontrará más información en el documento [Plantillas de páginas](/help/implementing/developing/components/templates.md).

La migración de plantillas estáticas a editables se puede automatizar en gran medida mediante las [Herramientas de modernización de Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### Se desaconseja el uso de componentes de base heredados {#oakpal-usage-legacy}

* **Clave**: LegacyFoundationComponentUsage
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Los componentes de base heredados (es decir, los componentes de `/libs/foundation`) se han quedado obsoletos para varias versiones de Experience Manager en favor de los componentes principales. Se desaconseja el uso de los componentes de base como base para los componentes personalizados (ya sea por superposición o por herencia) y se debe convertir a los componentes principales correspondientes.

Esta conversión se puede facilitar mediante las [Herramientas de modernización de Experience Manager.](https://opensource.adobe.com/aem-modernize-tools/)

### Usar solo nombres y órdenes de modo de ejecución admitidos {#oakpal-supported-runmodes}

* **Clave**: SupportedRunmode
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service aplica una estricta directiva de nomenclatura para los nombres de los modos de ejecución y un orden estricto para ellos. La lista de modos de ejecución admitidos se encuentra en el documento [Implementación en Experience Manager as a Cloud Service](/help/implementing/deploying/overview.md#runmodes) y cualquier desviación de esto se identificará como un problema.

### Los nodos de definición de índice de búsqueda personalizada deben ser tareas secundarias directas de /oak:index {#oakpal-custom-search}

* **Clave**: OakIndexLocation
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, nodos de tipo `oak:QueryIndexDefinition`) sean nodos secundarios directos de `/oak:index`. Los índices de otras ubicaciones deben moverse para que sean compatibles con Experience Manager as a Cloud Service. Encontrará más información sobre los índices de búsqueda en el documento [Búsqueda de contenido e indexación](/help/operations/indexing.md).

### Los nodos de definición de índice de búsqueda personalizada deben tener una compatVersion de 2 {#oakpal-custom-search-compatVersion}

* **Clave**: IndexCompatVersion
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (como nodos de tipo `oak:QueryIndexDefinition`) tengan la propiedad `compatVersion` establecida en `2`. Experience Manager as a Cloud Service no admite ningún otro valor. Encontrará más información sobre los índices de búsqueda en [Búsqueda de contenido e indexación](/help/operations/indexing.md).

### Los nodos descendientes de los nodos de definición de índice de búsqueda personalizada deben ser del tipo nt:unstructured {#oakpal-descendent-nodes}

* **Clave**: IndexDescendantNodeType
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Pueden producirse problemas difíciles de solucionar cuando un nodo de definición de índice de búsqueda personalizada tiene nodos secundarios sin ordenar. Para evitar esta situación, se recomienda que todos los nodos descendientes de un nodo `oak:QueryIndexDefinition` sean de tipo `nt:unstructured`.

### Los nodos de definición de índice de búsqueda personalizada deben contener un nodo secundario denominado indexRules que tenga tareas secundarias. {#oakpal-custom-search-index}

* **Clave**: IndexRulesNode
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Un nodo de definición de índice de búsqueda personalizada definido correctamente debe contener un nodo secundario denominado `indexRules` que, a su vez, debe tener al menos un secundario. Puede encontrar más información en la [documentación de Oak.](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### Los nodos de definición de índices de búsqueda personalizada deben seguir las convenciones de nombres {#oakpal-custom-search-definitions}

* **Clave**: IndexName
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, nodos de tipo `oak:QueryIndexDefinition`) tengan un nombre que siga un patrón específico descrito en el documento [Búsqueda e indexación de contenido](/help/operations/indexing.md).

### Los nodos de definición de índice de búsqueda personalizada deben utilizar el tipo de índice Lucene  {#oakpal-index-type-lucene}

* **Clave**: IndexType
* **Tipo**: Error
* **Gravedad**: Bloqueador
* **Desde**: Versión 2021.2.0 (tipo y gravedad modificados en 2021.8.0)

Experience Manager as a Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, nodos de tipo `oak:QueryIndexDefinition`) tengan una propiedad `type` con el valor establecido en `lucene`. La indexación con tipos de índice heredados debe actualizarse antes de la migración a Experience Manager as a Cloud Service. Consulte la [Documentación de búsqueda de contenido e indexación](/help/operations/indexing.md#how-to-use) para obtener más información.

### Los nodos de definición de índice de búsqueda personalizada no deben contener una propiedad denominada Semilla {#oakpal-property-name-seed}

* **Clave**: IndexSeedProperty
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service prohíbe que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo `oak:QueryIndexDefinition`) contengan una propiedad denominada `seed`. La indexación que utiliza esta propiedad debe actualizarse antes de la migración a Experience Manager as a Cloud Service. Consulte el documento [Búsqueda de contenido e indexación](/help/operations/indexing.md#how-to-use) para obtener más información.

### Los nodos de definición de índice de búsqueda personalizada no deben contener una propiedad denominada “reindex” {#oakpal-reindex-property}

* **Clave**: IndexReindexProperty
* **Tipo**: Code Smell
* **Gravedad**: Menor
* **Desde**: Versión 2021.2.0

Experience Manager as a Cloud Service prohíbe que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo `oak:QueryIndexDefinition`) contengan una propiedad denominada `reindex`. La indexación que utiliza esta propiedad debe actualizarse antes de la migración a Experience Manager as a Cloud Service. Consulte el documento [Búsqueda de contenido e indexación](/help/operations/indexing.md#how-to-use) para obtener más información.
