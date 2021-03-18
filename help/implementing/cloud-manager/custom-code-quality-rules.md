---
title: 'Reglas de calidad de código personalizadas: Cloud Services'
description: 'Reglas de calidad de código personalizadas: Cloud Services'
translation-type: tm+mt
source-git-commit: 96aa0ef43613e6ae72bf4c454be46329abb19a0c
workflow-type: tm+mt
source-wordcount: '3278'
ht-degree: 4%

---


# Reglas de calidad de código personalizadas {#custom-code-quality-rules}


En esta página se describen las reglas de calidad de código personalizadas ejecutadas por Cloud Manager, creadas sobre la base de las prácticas recomendadas de ingeniería de AEM.

>[!NOTE]
>Los ejemplos de código que se proporcionan aquí solo tienen fines ilustrativos. Consulte [Conceptos](https://docs.sonarqube.org/7.4/user-guide/concepts/) para conocer los conceptos y las reglas de calidad de SonarQube.

## Reglas de SonarQube {#sonarqube-rules}

La siguiente sección resalta las reglas de SonarQube:

### No utilice funciones potencialmente peligrosas {#do-not-use-potentially-dangerous-functions}

**Clave**: CQRules: CWE-676

**Tipo**: Vulnerabilidad

**Gravedad**: Principal

**Desde**: Versión 2018.4.0

Los métodos ***Thread.stop()*** y ***Thread.interrupt()*** pueden producir problemas difíciles de reproducir y, en algunos casos, vulnerabilidades de seguridad. Su utilización debe ser objeto de un estricto seguimiento y validación. En general, transmitir mensajes es una manera más segura de lograr objetivos similares.

#### Código no compatible {#non-compliant-code}

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

#### Código compatible {#compliant-code}

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

### No utilice cadenas de formato que puedan estar controladas externamente {#do-not-use-format-strings-which-may-be-externally-controlled}

**Clave**: CQRules: CWE-134

**Tipo**: Vulnerabilidad

**Gravedad**: Principal

**Desde**: Versión 2018.4.0

El uso de una cadena de formato de una fuente externa (como un parámetro de solicitud o contenido generado por el usuario) puede producir y exponer una aplicación a ataques de denegación de servicio. Hay circunstancias en las que una cadena de formato puede estar controlada externamente, pero solo se permite desde fuentes de confianza.

#### Código no compatible {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### Las solicitudes HTTP siempre deben tener tiempos de espera de socket y conexión {#http-requests-should-always-have-socket-and-connect-timeouts}

**Clave**: CQRules:ConnectionTimeoutFacility

**Tipo**: Error

**Gravedad**: Importante

**Desde**: Versión 2018.6.0

Al ejecutar solicitudes HTTP desde una aplicación AEM, es fundamental asegurarse de que se han configurado los tiempos de espera adecuados para evitar un consumo de subprocesos innecesario. Desafortunadamente, el comportamiento predeterminado del cliente HTTP predeterminado de Java (java.net.HttpUrlConnection) y del cliente de componentes HTTP Apache que se utiliza comúnmente es no agotar el tiempo de espera, por lo que los tiempos de espera deben establecerse explícitamente. Además, como práctica recomendada, estos tiempos de espera no deben superar los 60 segundos.

#### Código no compatible {#non-compliant-code-2}

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

#### Código compatible {#compliant-code-1}

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

### Los clientes {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers} no deben implementar ni ampliar las API de producto anotadas con @ProviderType

**Clave**: CQBP-84, dependencias CQBP-84

**Tipo**: Error

**Gravedad**: Importante

**Desde**: Versión 2018.7.0

La API de AEM contiene interfaces y clases de Java que solo están pensadas para utilizarse, pero no para implementarse, mediante código personalizado. Por ejemplo, la interfaz *com.day.cq.wcm.api.Page* está diseñada para que la implemente ***solo AEM***.

Cuando se añaden nuevos métodos a estas interfaces, esos métodos adicionales no afectan al código existente que utiliza estas interfaces y, como resultado, la adición de nuevos métodos a estas interfaces se considera compatible con versiones anteriores. Sin embargo, si el código personalizado ***implementa*** una de estas interfaces, dicho código personalizado ha introducido un riesgo de compatibilidad con versiones anteriores para el cliente.

Las interfaces (y clases) que solo se van a implementar mediante AEM están anotadas con *org.osgi.anottation.versioning.ProviderType* (o, en algunos casos, una anotación heredada similar *Qute.bnd.anottation.ProviderType*). Esta regla identifica los casos en los que dicha interfaz se implementa (o una clase se amplía) mediante código personalizado.

#### Código no compatible {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### Los objetos ResourceResolver siempre deben cerrarse {#resourceresolver-objects-should-always-be-closed}

**Clave**: CQRules:CQBP-72

**Tipo**: Huele de código

**Gravedad**: Principal

**Desde**: Versión 2018.4.0

Los objetos ResourceResolver obtenidos de ResourceResolverFactory consumen recursos del sistema. Aunque existen medidas para recuperar estos recursos cuando ResourceResolver ya no se está utilizando, es más eficaz cerrar explícitamente cualquier objeto ResourceResolver abierto llamando al método close() .

Una idea errónea relativamente común es que los objetos ResourceResolver creados usando una sesión de JCR existente no deberían cerrarse explícitamente o que al hacerlo, se cerraría la sesión de JCR subyacente. Este no es el caso, independientemente de cómo se abra un ResourceResolver, debe cerrarse cuando ya no se utilice. Dado que ResourceResolver implementa la interfaz Closeable, también es posible utilizar la sintaxis try-with-resources en lugar de invocar explícitamente close().

#### Código no compatible {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Código compatible {#compliant-code-2}

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

### No utilice rutas de servlet de Sling para registrar servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

**Clave**: CQRules:CQBP-75

**Tipo**: Huele de código

**Gravedad**: Principal

**Desde**: Versión 2018.4.0

Como se describe en la [documentación de Sling](http://sling.apache.org/documentation/the-sling-engine/servlets.html), se desaconsejan los enlaces de servlets por rutas. Los servlets enlazados a rutas no pueden utilizar controles de acceso JCR estándar y, como resultado, requieren un rigor de seguridad adicional. En lugar de utilizar servlets enlazados a rutas, se recomienda crear nodos en el repositorio y registrar servlets por tipo de recurso.

#### Código no compatible {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Las excepciones capturadas deben registrarse o emitirse, pero no {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**Clave**: CQRules:CQBP-44—CatchAndOrLogOrThrow

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

En general, una excepción debe registrarse exactamente una vez. El registro de excepciones varias veces puede causar confusión, ya que no está claro cuántas veces se produjo una excepción. El patrón más común que lleva a esto es registrar y arrojar una excepción capturada.

#### Código no compatible {#non-compliant-code-6}

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

#### Código compatible {#compliant-code-3}

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

### Evite tener una sentencia de registro seguida inmediatamente por una sentencia {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**Clave**: CQRules:CQBP-44—ConsecutiveLogAndThrow

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

Otro patrón común que se debe evitar es registrar un mensaje y luego iniciar inmediatamente una excepción. Esto generalmente indica que el mensaje de excepción terminará duplicado en los archivos de registro.

#### Código no compatible {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Código compatible {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Evite iniciar sesión en INFO al gestionar solicitudes de GET o HEAD {#avoid-logging-at-info-when-handling-get-or-head-requests}

**Clave**: CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**Tipo**: Huele de código

**Gravedad**: Menor

En general, el nivel de registro INFO debe utilizarse para demarcar acciones importantes y, de forma predeterminada, AEM está configurado para registrar a nivel INFO o superior. Los métodos GET y HEAD sólo deben ser operaciones de sólo lectura y, por lo tanto, no constituyen acciones importantes. Es probable que el registro en el nivel INFO como respuesta a solicitudes de GET o HEAD cree un ruido de registro significativo, lo que dificulta la identificación de información útil en los archivos de registro. El registro al gestionar solicitudes de GET o HEAD debe realizarse en los niveles WARN o ERROR cuando algo ha salido mal o en los niveles DEBUG o TRACE si sería útil disponer de información más detallada sobre la solución de problemas.

>[!CAUTION]
>
>Esto no se aplica al registro de tipo access.log para cada solicitud.

#### Código no compatible {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Código compatible {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### No utilice Exception.getMessage() como el primer parámetro de una instrucción de registro {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**Clave**: CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

Como práctica recomendada, los mensajes de registro deben proporcionar información contextual sobre dónde se ha producido una excepción en la aplicación. Aunque el contexto también se puede determinar mediante el uso de trazos de pila, en general el mensaje de registro será más fácil de leer y comprender. Como resultado, al registrar una excepción, es una mala práctica utilizar el mensaje de la excepción como mensaje de registro: el mensaje de excepción contendrá lo que salió mal, mientras que el mensaje de registro debería usarse para decirle a un lector de registro qué estaba haciendo la aplicación cuando se produjo la excepción. El mensaje de excepción se seguirá registrando; al especificar su propio mensaje, los registros serán más fáciles de entender.

#### Código no compatible {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Código compatible {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### El inicio de sesión en bloques catch debe estar en el nivel WARN o ERROR {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**Clave**: CQRules:CQBP-44—ErrorLogLevelInCatchBlock

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

Como su nombre sugiere, las excepciones de Java siempre deben usarse en circunstancias *excepcionales*. Como resultado, cuando se captura una excepción, es importante asegurarse de que los mensajes de registro se registren en el nivel adecuado, ya sea WARN o ERROR. Esto garantiza que esos mensajes aparezcan correctamente en los registros.

#### Código no compatible {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Código compatible {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### No imprima trazos de pila en la consola {#do-not-print-stack-traces-to-the-console}

**Clave**: CQRules:CQBP-44—ExceptionPrintStackTrace

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

Como se ha mencionado, el contexto es fundamental para comprender los mensajes de registro. El uso de Exception.printStackTrace() hace que **only** el seguimiento de pila se envíe al flujo de error estándar, lo que provoca que se pierda todo el contexto. Además, en una aplicación multiproceso como AEM si se imprimen varias excepciones utilizando este método en paralelo, sus trazos de pila pueden superponerse, lo que produce una confusión significativa. Las excepciones solo deben registrarse a través del marco de registro.

#### Código no compatible {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Código compatible {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### No generar la salida estándar o el error estándar {#do-not-output-to-standard-output-or-standard-error}

**Clave**: CQRules:CQBP-44—LogLevelConsolePrinters

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

El inicio de sesión AEM siempre se debe realizar mediante el marco de registro (SLF4J). La salida directa a los flujos de error estándar o de salida estándar pierde la información estructural y contextual proporcionada por el marco de registro y, en algunos casos, puede causar problemas de rendimiento.

#### Código no compatible {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Código compatible {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Evite las rutas /apps y /libs codificadas {#avoid-hardcoded-apps-and-libs-paths}

**Clave**: CQRules:CQBP-71

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2018.4.0

En general, las rutas que comienzan con /libs y /apps no deben codificarse, ya que las rutas a las que se refieren generalmente se almacenan como rutas relativas a la ruta de búsqueda de Sling (que está configurada en /libs,/apps de forma predeterminada). El uso de la ruta absoluta puede introducir defectos sutiles que solo aparecerían más adelante en el ciclo de vida del proyecto.

#### Código no compatible {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Código compatible {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### El planificador de Sling no debe usarse {#sonarqube-sling-scheduler}

**Clave**: CQRules:AMSCORE-554

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

El planificador de Sling no debe utilizarse para tareas que requieran una ejecución garantizada. Los trabajos programados de Sling garantizan la ejecución y son más adecuados para los entornos agrupados y no agrupados.

Consulte [Evento de Apache Sling y Gestión de trabajos](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) para obtener más información sobre cómo se gestionan los trabajos de Sling en entornos agrupados.

### AEM las API obsoletas no deben usarse {#sonarqube-aem-deprecated}

**Clave**: AMSCORE-553

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

La superficie de la API AEM está en constante revisión para identificar las API para las que se desaconseja el uso y que, por lo tanto, se consideran obsoletas.

En muchos casos, estas API quedan obsoletas al utilizar la anotación estándar Java *@Deprecated* y, como tal, tal y como se identifica con `squid:CallToDeprecatedMethod`.

Sin embargo, hay casos en los que una API está en desuso en el contexto de AEM, pero puede que no esté en desuso en otros contextos. Esta regla identifica esta segunda clase.

## Reglas de contenido OakPAL {#oakpal-rules}

A continuación se muestran las comprobaciones OakPAL ejecutadas por Cloud Manager.

>[!NOTE]
>OakPAL es un marco desarrollado por un socio AEM (y ganador de 2019 AEM Rockstar North America) que valida paquetes de contenido usando un repositorio Oak independiente.

### Los Paquetes De Cliente No Deben Crear Ni Modificar Nodos En /libs {#oakpal-customer-package}

**Clave**: BannedPaths

**Tipo**: Error

**Gravedad**: Bloqueador

**Desde**: Versión 2019.6.0

Desde hace mucho tiempo se recomienda que los clientes consideren el árbol de contenido /libs en el repositorio de contenido AEM como de solo lectura. Modificar los nodos y las propiedades en */libs* crea un riesgo significativo para las actualizaciones principales y secundarias. Las modificaciones en */libs* solo deben realizarse por Adobe a través de canales oficiales.

### Los Paquetes No Deben Contener Configuraciones OSGi Duplicadas {#oakpal-package-osgi}

**Clave**: DuplicateOsgiConfigurations

**Tipo**: Error

**Gravedad**: Principal

**Desde**: Versión 2019.6.0

Un problema común que ocurre en proyectos complejos es que el mismo componente OSGi se configura varias veces. Esto crea una ambigüedad sobre la configuración que se puede utilizar. Esta regla es &quot;según el modo de ejecución&quot; ya que solo identificará problemas en los que el mismo componente se haya configurado varias veces en el mismo modo de ejecución (o combinación de modos de ejecución).

>[!NOTE]
>Esta regla producirá problemas en los que la misma configuración, en la misma ruta, se define en varios paquetes, incluidos casos en los que el mismo paquete se duplica en la lista general de paquetes creados. Por ejemplo, si la compilación produce paquetes llamados `com.myco:com.myco.ui.apps` y `com.myco:com.myco.all` donde `com.myco:com.myco.all` incorpora `com.myco:com.myco.ui.apps`, todas las configuraciones dentro de `com.myco:com.myco.ui.apps` se registrarán como duplicados. Este es generalmente un caso en el que no se siguen las [Directrices de estructura del paquete de contenido](/help/implementing/developing/aem-project-content-package-structure.md); en este ejemplo específico, al paquete `com.myco:com.myco.ui.apps` le falta la propiedad `<cloudManagerTarget>none</cloudManagerTarget>`.

#### Código no compatible {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Código compatible {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Las carpetas de configuración e instalación solo deben contener nodos OSGi {#oakpal-config-install}

**Clave**: ConfigAndInstallShouldOnlyContainOsgiNodes

**Tipo**: Error

**Gravedad**: Principal

**Desde**: Versión 2019.6.0

Por motivos de seguridad, las rutas que contienen */config/ y /install/* solo las pueden leer los usuarios administrativos en AEM y solo deben utilizarse para la configuración OSGi y los paquetes OSGi. Colocar otros tipos de contenido en rutas que contienen estos segmentos resulta en un comportamiento de la aplicación que varía involuntariamente entre usuarios administrativos y no administrativos.

Un problema común es el uso de nodos llamados `config` dentro de los cuadros de diálogo de componentes o al especificar la configuración del editor de texto enriquecido para la edición en línea. Para resolver esto, se debe cambiar el nombre del nodo infractor por uno conforme. Para la configuración del editor de texto enriquecido, utilice la propiedad `configPath` del nodo `cq:inplaceEditing` para especificar la nueva ubicación.

#### Código no compatible {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Código compatible {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Los paquetes no deben superponerse {#oakpal-no-overlap}

**Clave**: PackageOverlaps

**Tipo**: Error

**Gravedad**: Principal

**Desde**: Versión 2019.6.0

De forma similar a *Los paquetes no deben contener configuraciones OSGi duplicadas*, este es un problema común en proyectos complejos en los que la misma ruta de nodo se escribe en varios paquetes de contenido separados. Aunque el uso de dependencias de paquetes de contenido se puede utilizar para garantizar un resultado coherente, es mejor evitar las superposiciones por completo.

### El modo de creación predeterminado no debe ser la IU clásica {#oakpal-default-authoring}

**Clave**: ClassicUIAuthoringMode

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

La configuración OSGi `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` define el modo de creación predeterminado dentro de AEM. Como la IU clásica ha quedado obsoleta desde AEM 6.4, ahora se generará un problema cuando el modo de creación predeterminado se configure en la IU clásica.

### Los componentes con cuadros de diálogo deben tener cuadros de diálogo de interfaz de usuario táctil {#oakpal-components-dialogs}

**Clave**: Cuadro de diálogo ComponentWithOnlyClassicUID

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

AEM Los componentes que tienen un cuadro de diálogo de IU clásica siempre deben tener un cuadro de diálogo de IU táctil correspondiente para proporcionar una experiencia de creación óptima y para ser compatibles con el modelo de implementación de Cloud Service, en el que la IU clásica no es compatible. Esta regla verifica los siguientes escenarios:

* Un componente con un cuadro de diálogo de IU clásica (es decir, un nodo secundario de cuadro de diálogo) debe tener un cuadro de diálogo de IU táctil correspondiente (es decir, un nodo secundario `cq:dialog`).
* Un componente con un cuadro de diálogo de diseño de IU clásica (es decir, un nodo design_dialog) debe tener un cuadro de diálogo de diseño de IU táctil correspondiente (es decir, un nodo secundario `cq:design_dialog` ).
* Un componente con un cuadro de diálogo de IU clásica y un cuadro de diálogo de diseño de IU clásica debe tener un cuadro de diálogo de IU táctil correspondiente y un cuadro de diálogo de diseño de IU táctil correspondiente.

La documentación AEM Herramientas de modernización proporciona documentación y herramientas para convertir componentes de la IU clásica a la IU táctil. Consulte [Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) para obtener más información.

### Los paquetes no deben mezclar contenido mutable e inmutable {#oakpal-packages-immutable}

**Clave**: ImmutableMutableMixedPackage

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

Para ser compatible con el modelo de implementación de Cloud Service, los paquetes de contenido individuales deben contener contenido para las áreas inmutables del repositorio (es decir, `/apps and /libs, although /libs` no debe ser modificado por el código del cliente y causará una infracción independiente) o el área mutable (es decir, todo lo demás), pero no ambos. Por ejemplo, un paquete que incluye `/apps/myco/components/text and /etc/clientlibs/myco` no es compatible con el Cloud Service y provocará que se informe de un problema.

Consulte [AEM Estructura del proyecto](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) para obtener más información.

### Los Agentes De Replicación Inversa No Deben Utilizarse {#oakpal-reverse-replication}

**Clave**: ReverseReplication

**Tipo**: Compatibilidad entre huele y Cloud Service de código

**Gravedad**: Menor

**Desde**: Versión 2020.5.0

La compatibilidad con la replicación inversa no está disponible en las implementaciones de Cloud Service, como se describe en las [Notas de la versión: Eliminación de agentes de replicación](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/release-notes/aem-cloud-changes.html#replication-agents).

Los clientes que utilizan la replicación inversa deben ponerse en contacto con el Adobe para obtener soluciones alternativas.

### OakPAL: Los recursos contenidos en bibliotecas de cliente con proxy habilitado deben estar en una carpeta denominada recursos {#oakpal-resources-proxy}

**Clave**: ClientlibProxyResource

**Tipo**: Error

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM bibliotecas cliente pueden contener recursos estáticos como imágenes y fuentes. Como se describe en [Uso de preprocesadores](/help/implementing/developing/introduction/clientlibs.md#using-preprocessors), al utilizar bibliotecas de cliente proxy, estos recursos estáticos deben estar contenidos en una carpeta secundaria denominada resources para que se haga referencia a ellos de forma efectiva en las instancias de publicación.

#### Código no compatible {#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### Código compatible {#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL: Uso de procesos de flujo de trabajo incompatibles con Cloud Service {#oakpal-usage-cloud-service}

**Clave**: CloudServiceIncompatibleWorkflowProcess

**Tipo**: Error

**Gravedad**: Principal

**Desde**: Versión 2021.2.0

Con el paso a los microservicios de recursos para el procesamiento de recursos en AEM Cloud Service, varios procesos de flujo de trabajo que se utilizaban en las versiones locales y AMS de AEM se han vuelto incompatibles o innecesarios. La herramienta de migración en [aem-cloud-migration](https://github.com/adobe/aem-cloud-migration) se puede utilizar para actualizar los modelos de flujo de trabajo durante AEM migración del Cloud Service.

### OakPAL: se desaconseja el uso de plantillas estáticas en favor de plantillas editables {#oakpal-static-template}

**Clave**: StaticTemplateUsage

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

Aunque históricamente el uso de plantillas estáticas ha sido muy común en AEM proyectos, se recomiendan las plantillas editables, ya que proporcionan la mayor flexibilidad y admiten funciones adicionales que no están presentes en las plantillas estáticas. Encontrará más información en [Plantillas de página.](/help/implementing/developing/components/templates.md) La migración de plantillas estáticas a editables se puede automatizar en gran medida mediante las  [AEM Herramientas](https://opensource.adobe.com/aem-modernize-tools/) de modernización.

### OakPAL: se desaconseja el uso de componentes de base heredados {#oakpal-usage-legacy}

**Clave**: LegacyFoundationComponentUsage

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

Los componentes de base heredados (es decir, los componentes de `/libs/foundation`) han quedado obsoletos para varias versiones de AEM en favor de los componentes principales de WCM. El uso de los componentes de base heredados como base para los componentes personalizados (ya sea por superposición o por herencia) se desaconseja y debe convertirse al componente principal correspondiente. Esta conversión se puede facilitar mediante las [AEM Herramientas de modernización](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL: Solo se deben utilizar los nombres y el orden de modo de ejecución compatibles {#oakpal-supported-runmodes}

**Clave**: SupportedRunmode

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service aplica una política de nomenclatura estricta para los nombres de modo de ejecución y un orden estricto para dichos modos de ejecución. La lista de modos de ejecución admitidos se encuentra en [Runmodes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes) y cualquier desviación de esto se identificará como un problema.

### OakPAL: los nodos de definición del índice de búsqueda personalizada deben ser secundarios directos de /oak:index {#oakpal-custom-search}

**Clave**: OakIndexLocation

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo oak:QueryIndexDefinition) sean nodos secundarios directos de `/oak:index`. Los índices de otras ubicaciones deben moverse para que sean compatibles con AEM Cloud Service. Puede encontrar más información sobre los índices de búsqueda en [Búsqueda de contenido e indexación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL: los nodos de definición de índice de búsqueda personalizados deben tener una compatVersion de 2 {#oakpal-custom-search-compatVersion}

**Clave**: IndexCompatVersion

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo oak:QueryIndexDefinition) tengan la propiedad compatVersion establecida en 2. AEM Cloud Service no admite ningún otro valor. Puede encontrar más información sobre los índices de búsqueda en [Búsqueda de contenido e indexación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL: los nodos descendientes de los nodos de definición de índice de búsqueda personalizada deben ser de tipo nt:unstructured {#oakpal-descendent-nodes}

**Clave**: IndexDescendantNodeType

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

Es difícil solucionar problemas cuando se producen cuando un nodo de definición de índice de búsqueda personalizado tiene nodos secundarios sin ordenar. Para evitarlos, se recomienda que todos los nodos descendientes de un nodo `oak:QueryIndexDefinition` sean del tipo nt:unstructured.

### OakPAL: los nodos de definición de índice de búsqueda personalizados deben contener un nodo secundario denominado indexRules que tenga elementos secundarios {#oakpal-custom-search-index}

**Clave**: IndexRulesNode

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

Un nodo de definición de índice de búsqueda personalizado definido correctamente debe contener un nodo secundario llamado indexRules que, a su vez, debe tener al menos un nodo secundario. Puede encontrar más información en [Oak Documentation](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### OakPAL: los nodos de definición del índice de búsqueda personalizada deben seguir las convenciones de nomenclatura {#oakpal-custom-search-definitions}

**Clave**: IndexName

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo `oak:QueryIndexDefinition`) tengan un nombre que siga un patrón específico descrito en [Content Search and Indexing](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL: los nodos de definición del índice de búsqueda personalizada deben utilizar el tipo de índice Lucene {#oakpal-index-type-lucene}

**Clave**: IndexType

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service requiere que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo oak:QueryIndexDefinition) tengan una propiedad type con el valor establecido en **lucene**. La indexación con tipos de índice heredados debe actualizarse antes de la migración a AEM Cloud Service. Consulte [Búsqueda de contenido e indexación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) para obtener más información.

### OakPAL: los nodos de definición del índice de búsqueda personalizada no deben contener una propiedad denominada seed {#oakpal-property-name-seed}

**Clave**: IndexSeedProperty

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service prohíbe que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo `oak:QueryIndexDefinition`) contengan una propiedad denominada seed. La indexación con esta propiedad debe actualizarse antes de la migración a AEM Cloud Service. Consulte [Búsqueda de contenido e indexación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) para obtener más información.

### OakPAL: los nodos de definición del índice de búsqueda personalizada no deben contener una propiedad denominada reindex {#oakpal-reindex-property}

**Clave**: IndexReindexProperty

**Tipo**: Huele de código

**Gravedad**: Menor

**Desde**: Versión 2021.2.0

AEM Cloud Service prohíbe que las definiciones de índice de búsqueda personalizadas (es decir, los nodos de tipo `oak:QueryIndexDefinition`) contengan una propiedad denominada reindex. La indexación con esta propiedad debe actualizarse antes de la migración a AEM Cloud Service. Consulte [Búsqueda de contenido e indexación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) para obtener más información.






