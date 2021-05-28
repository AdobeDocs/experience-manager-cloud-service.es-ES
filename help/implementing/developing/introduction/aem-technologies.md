---
title: Fundamentos técnicos AEM
description: Una visión general de los fundamentos técnicos de la AEM, incluyendo cómo AEM está estructurada y las tecnologías fundamentales como JCR, Sling y OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 8ba7968ee7f4d3c808740054bf841dbaf9dd4254
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 0%

---

# Fundamentos técnicos AEM {#aem-technical-foundations}

AEM es una plataforma sólida basada en tecnologías comprobadas, ampliables y flexibles. Este documento ofrece una descripción detallada de las distintas partes que componen AEM y está diseñado como un apéndice técnico para un desarrollador de AEM de pila completa. No está pensado como guía de introducción. Si es nuevo en AEM desarrollo, consulte el [Introducción al desarrollo de AEM Sites - Tutorial WKND](develop-wknd-tutorial.md) como primer paso.

>[!TIP]
>
>Antes de sumergirse en las tecnologías principales de AEM, Adobe recomienda completar el [Tutorial de introducción al desarrollo de AEM Sites - WKND.](develop-wknd-tutorial.md)

## Aspectos básicos {#fundamentals}

Como sistema moderno de administración de contenido, AEM se basa en tecnologías web estándar:

* Ciclo de solicitud-respuesta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

Las capas subyacentes del repositorio de contenido y la lógica empresarial se crean en torno a las tecnologías Java:

* JCR
* Sling
* los paquetes

## Repositorio de contenido Java {#java-content-repository}

El estándar del repositorio de contenido Java (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido. El responsable de la especificación es Adobe Research (Suiza) AG.

El paquete [JCR API 2.0](https://docs.adobe.com/content/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*` se utiliza para el acceso directo y la manipulación del contenido del repositorio.

AEM se basa en un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit ](https://jackrabbit.apache.org/oak/) Oakis es una implementación de un repositorio de contenido jerárquico escalable y de alto rendimiento para su uso como la base de los sitios web modernos de nivel mundial y otras aplicaciones de contenido exigentes, de conformidad con el estándar JCR.

Jackrabbit Oak (también conocido como simplemente Oak), es la implementación del estándar JCR en el que AEM está construido.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

AEM se crea utilizando [Sling](https://sling.apache.org/site/index.html), un marco de aplicaciones web basado en los principios de REST que proporciona un fácil desarrollo de aplicaciones orientadas al contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit Oak, como su almacén de datos. Sling ha sido contribuido a la Apache Software Foundation - puede encontrar más información en Apache.

### Introducción a Sling {#introduction-to-sling}

Con Sling, el tipo de contenido que se va a procesar no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL se resuelve en un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Esto proporciona una excelente compatibilidad a los autores de contenido web para crear páginas que se adapten fácilmente a sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes, o cuando necesita páginas que se puedan personalizar fácilmente. En concreto, al implementar un sistema de administración de contenido web como AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución del script Sling: muestra cómo pasar de una solicitud HTTP al nodo de contenido, de un nodo de contenido a un tipo de recurso, de un tipo de recurso a un script y qué variables de secuencias de comandos están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos pero poderosos que puede utilizar al tratar con `SlingPostServlet`, el controlador predeterminado para todas las solicitudes de POST que le ofrece infinitas opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling es centrado en el contenido {#sling-is-content-centric}

Sling es *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido
* En segundo lugar, la representación, o la secuencia de comandos, se encuentra desde las propiedades del recurso en combinación con ciertas partes de la solicitud (por ejemplo, selectores o la extensión)

### Sling RESTful {#restful-sling}

Debido a su filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* Muy RESTful, no sólo en la superficie; los recursos y las representaciones están modelados correctamente dentro del servidor
* Elimina uno o varios modelos de datos
   * Otros marcos de administración de contenido pueden requerir estructura de URL, objetos empresariales y esquema de base de datos para acceder a un recurso.
   * Con Sling, esto se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se controla mediante la dirección URL de la solicitud del usuario. Define el contenido que se mostrará en las secuencias de comandos correspondientes. Para ello, la información se extrae de la dirección URL.

Si analizamos la siguiente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividirla en sus partes compuestas:

| protocol | host |  | ruta de contenido | selector(s) | Extensión |  | sufijo |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo**  - HTTPS
* **host** : dominio del sitio
* **ruta de contenido** : ruta que especifica el contenido que se va a procesar y se utiliza en combinación con la extensión; en este ejemplo traducen a  `tools/spy.html`
* **selector(s)** : se utiliza para métodos alternativos de renderización del contenido; en este ejemplo, una versión compatible con impresora en formato A4
* **extensión** : formato de contenido; también especifica la secuencia de comandos que se utilizará para la renderización
* **sufijo** : se puede utilizar para especificar información adicional
* **param(s)** : cualquier parámetro necesario para el contenido dinámico

#### De URL a contenido y scripts {#from-url-to-content-and-scripts}

Uso de los principios de descomposición de URL:

* La asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso.
* Cuando se encuentra el recurso adecuado, se extrae el tipo de recurso de sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido.

En la siguiente figura se ilustra el mecanismo utilizado, que se debatirá más detalladamente en las secciones siguientes.

![Mecanismo de asignación de URL](assets/url-mapping.png)

Con Sling, se especifica qué secuencia de comandos procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como haría una instrucción SQL en un script PHP) ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca en el repositorio el recurso solicitado (nodo de contenido):

* El primer Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; p. ej. `../content/corporate/jobs/developer.html`
* Si no se encuentra ningún nodo, se interrumpe la extensión y se repite la búsqueda; p. ej. `../content/corporate/jobs/developer`
* Si no se encuentra ningún nodo, Sling devolverá el código http 404 (No encontrado).

Sling también permite que otras cosas que no sean nodos JCR sean recursos, pero esta es una característica avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae el **tipo de recurso de sling**. Esta es una ruta, que localiza la secuencia de comandos que se utilizará para procesar el contenido.

La ruta especificada por el `sling:resourceType` puede ser:

* Absoluto
* Relativo a un parámetro de configuración

>[!TIP]
>
>Las rutas relativas se recomiendan por Adobe, ya que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` (mutable, scripts de usuario) o `/libs` (inmutable, scripts del sistema), que se buscarán en este orden.

Otros puntos a tener en cuenta son:

* Cuando el método (GET, POST) es obligatorio, se especifica en mayúsculas según la especificación HTTP, por ejemplo `jobs.POST.esp`
* Se admiten varios motores de secuencias de comandos, pero los scripts recomendados y comunes son HTL y JavaScript.

La lista de motores de secuencia de comandos admitidos por la instancia dada de AEM se muestra en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizando el ejemplo anterior, si `sling:resourceType` es `hr/jobs` entonces para:

* Solicitudes de GET/HEAD y direcciones URL que terminan en `.html` (tipos de solicitud predeterminados, formato predeterminado)
   * El script será `/apps/hr/jobs/jobs.esp`; la última sección de `sling:resourceType` forma el nombre del archivo.
* solicitudes del POST (todos los tipos de solicitud, excepto el GET/HEAD, el nombre del método debe estar en mayúsculas)
   * se utilizará el POST en el nombre de la secuencia de comandos.
   * El script será `/apps/hr/jobs/jobs.POST.esp`.
* URL en otros formatos, sin finalizar con `.html`
   * Por ejemplo `../content/corporate/jobs/developer.pdf`
   * El script será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre de la secuencia de comandos.
* Direcciones URL con selectores
   * Los selectores pueden utilizarse para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente rss o un resumen.
   * Si miramos una versión fácil de imprimir donde el selector podría ser `print`; como en `../content/corporate/jobs/developer.print.html`
   * El script será `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre de la secuencia de comandos.
* Si no se ha definido ningún `sling:resourceType`, entonces:
   * La ruta de contenido se utilizará para buscar una secuencia de comandos adecuada (si la ruta basada en `ResourceTypeProvider` está activa).
   * Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.
   * Se utilizará el tipo de nodo principal.
* Si no se encuentra ningún script, se utilizará el script predeterminado.
   * Actualmente, la representación predeterminada se admite como texto sin formato (`.txt`), HTML (`.html`) y JSON (`.json`), todos los cuales enumerarán las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión `.res`, o solicitudes sin extensión de solicitud, es agrupar el recurso (siempre que sea posible).
* Para la gestión de errores http (códigos 403 o 404) Sling buscará un script en:
   * La ubicación `/apps/sling/servlet/errorhandler` para scripts personalizados
   * O la ubicación del script estándar `/libs/sling/servlet/errorhandler/404.jsp`

Si se aplican varios scripts para una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; en otras palabras, cuanto más selector coincida, mejor, independientemente de cualquier extensión de solicitud o coincidencia de nombre de método.

Por ejemplo, considere una solicitud para acceder al recurso

* `/content/corporate/jobs/developer.print.a4.html`

de tipo

* `sling:resourceType="hr/jobs"`

Suponiendo que tengamos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recurso (definidos principalmente por la propiedad `sling:resourceType` ), también está el supertipo de recurso. Esto se indica generalmente con la propiedad `sling:resourceSuperType` . Estos supertipos también se tienen en cuenta al intentar encontrar un script. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos donde el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) es efectivamente la raíz.

El supertipo de recurso de un recurso se puede definir de dos formas:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que apunta el `sling:resourceType`.

Por ejemplo:

* `/`
   * `a`
   * `b`
      * `sling:resourceSuperType = a`
   * `c`
      * `sling:resourceSuperType = b`
   * `x`
      * `sling:resourceType = c`
   * `y`
      * `sling:resourceType = c`
      * `sling:resourceSuperType = a`

La jerarquía de tipo de:

* `/x`
   * Is `[ c, b, a, <default>]`
* Mientras que para `/y`
   * La jerarquía es `[ c, a, <default>]`

Esto se debe a que `/y` tiene la propiedad `sling:resourceSuperType` mientras que `/x` no lo tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### No se puede llamar directamente a los scripts de Sling {#sling-scripts-cannot-be-called-directly}

Dentro de Sling, no se pueden llamar directamente a los scripts, ya que esto rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculte el recurso dentro de la secuencia de comandos, de modo que la estructura (Sling) ya no lo sepa. Por lo tanto, se pierden algunas funciones:

* Gestión automática de métodos http distintos de la GET, que incluyen:
   * POST, PUT y DELETE que se administran con una implementación predeterminada de sling
   * El script `POST.jsp` en la ubicación `sling:resourceType`
* Su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; de gran importancia para el desarrollo a gran escala

### API de Sling {#sling-api}

Utiliza el paquete de la API de Sling, `org.apache.sling.*` y las bibliotecas de etiquetas.

### Referencia a elementos existentes utilizando sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los scripts.

Es posible que las secuencias de comandos más complejas (agregación de secuencias de comandos) necesiten acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página y elementos de una lista) y hacerlo incluyendo el *recurso*.

Para ello, puede utilizar el comando `sling:include("/<path>/<resource>")`. Esto incluirá efectivamente la definición del recurso al que se hace referencia.

## los paquetes {#osgi}

OSGi (Open Services Gateway Initiative) define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también conocida como Sistema de módulos dinámicos para Java). Los contenedores OSGi le permiten dividir su aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* Servicios implementados dentro del contenedor
* Un contrato entre el contenedor y su aplicación

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse entre sí de forma dinámica para la colaboración.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de aplicaciones. Sling, y por lo tanto AEM, utiliza la implementación [Apache Felix](https://felix.apache.org/) de OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* Instalar
* Inicial
* Detener
* Actualizar
* Desinstalar
* Ver el estado actual
* Acceda a información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [Configuración de OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información.

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece una descripción general de la estructura que verá dentro del repositorio.

* `/apps` - Relacionadas con las solicitudes; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/core/wcm/components`.
* `/content` - Contenido creado para su sitio web.
* `/etc`
* `/home` - Información de usuarios y grupos.
* `/libs` - Bibliotecas y definiciones que pertenecen al núcleo del AEM. Las subcarpetas de `/libs` representan las funciones de AEM listas para usar. El contenido de `/libs` no se puede modificar. Las funciones específicas de su sitio web deben realizarse en `/apps`.
* `/tmp` - Zona de trabajo temporal.
* `/var` - Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y gestión de eventos.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado. Asegúrese de comprender completamente las implicaciones de cualquier cambio que realice.
>
>No debe cambiar nada en la ruta `/libs`. Para cambios de configuración y otros cambios, copie el elemento de `/libs` a `/apps` y realice cualquier cambio dentro de `/apps`.
