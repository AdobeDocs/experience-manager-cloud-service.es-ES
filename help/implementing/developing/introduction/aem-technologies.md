---
title: Fundamentos técnicos AEM
description: Una visión general de los fundamentos técnicos de la AEM, incluyendo cómo AEM está estructurado y las tecnologías fundamentales como JCR, Sling y OSGi.
translation-type: tm+mt
source-git-commit: 750fded1564de2b11f6c104cc70befc4453405b4
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 0%

---


# Fundamentos técnicos AEM {#aem-technical-foundations}

AEM es una plataforma sólida basada en tecnologías probadas, ampliables y flexibles. Este documento ofrece una descripción detallada de las distintas partes que componen AEM y está diseñado como un apéndice técnico para un desarrollador de AEM de pilas completas. No está pensada como guía de introducción. Si es nuevo en AEM desarrollo, consulte el [Tutorial de ](develop-wknd-tutorial.md) Introducción al desarrollo de AEM Sites - WKND como primer paso.

>[!TIP]
>
>Antes de sumergirse en las tecnologías principales de AEM, Adobe recomienda completar el [Tutorial de &lt;a0/>Introducción al desarrollo de AEM Sites - WKND.](develop-wknd-tutorial.md)

## Aspectos básicos {#fundamentals}

Como sistema gestor de contenido moderno, AEM se basa en tecnologías web estándar:

* Ciclo request-response (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

El repositorio de contenido subyacente y las capas de lógica empresarial se crean en torno a las tecnologías Java:

* JCR
* Sling
* los paquetes

## Repositorio de contenido Java {#java-content-repository}

El estándar de Java Content Repository (JCR), [JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html), especifica una manera independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido. El responsable de la especificación es Adobe Research (Suiza) AG.

El paquete [JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*`, se utiliza para el acceso directo y la manipulación del contenido del repositorio.

AEM está construido sobre un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit ](https://jackrabbit.apache.org/oak/) Oakis es una implementación de un repositorio de contenido jerárquico escalable y de alto rendimiento para su uso como la base de los sitios web de clase mundial modernos y otras aplicaciones de contenido exigentes, de conformidad con el estándar JCR.

Jackrabbit Oak (también conocido como Oak), es la implementación del estándar JCR sobre el cual se construye AEM.

## Procesamiento de solicitudes Sling {#sling-request-processing}

AEM se crea mediante [Sling](https://sling.apache.org/site/index.html), un marco de Aplicación web basado en los principios REST que proporciona un fácil desarrollo de aplicaciones orientadas al contenido. Sling usa un repositorio JCR, como Apache Jackrabbit Oak, como su almacén de datos. Sling ha sido aportado a la Apache Software Foundation - más información se puede encontrar en Apache.

### Introducción a Sling {#introduction-to-sling}

Con Sling, el tipo de contenido que se va a procesar no es la primera consideración de procesamiento. En su lugar, la principal consideración es si la dirección URL se resuelve en un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la representación. Esto proporciona una excelente compatibilidad a los autores de contenido web para crear páginas que se adapten fácilmente a sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando se necesitan páginas que se puedan personalizar fácilmente. En particular, al implementar un sistema de Gestor de contenido Web como AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución del script Sling: muestra cómo pasar de una solicitud HTTP a un nodo de contenido, de un nodo de contenido a un tipo de recurso, de un tipo de recurso a una secuencia de comandos y qué variables de secuencias de comandos están disponibles.

![Explicación de la resolución de secuencias de comandos de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican todos los parámetros de solicitud ocultos pero potentes que puede utilizar al tratar con `SlingPostServlet`, el controlador predeterminado para todas las solicitudes de POST que le ofrece infinitas opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling está *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destinatario es el recurso (nodo JCR) que contiene el contenido
* En segundo lugar, la representación, o secuencia de comandos, se encuentra desde las propiedades del recurso en combinación con determinadas partes de la solicitud (por ejemplo, selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a su filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, presenta un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* Muy RESTful, no sólo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* Quita uno o varios modelos de datos
   * Otros marcos de gestor de contenido pueden requerir la estructura URL, objetos comerciales y esquema de base de datos para acceder a un recurso.
   * Con Sling, esto se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se controla mediante la dirección URL de la solicitud de usuario. Define el contenido que deben mostrar las secuencias de comandos correspondientes. Para ello, la información se extrae de la dirección URL.

Si analizamos la siguiente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos desglosarlo en sus partes compuestas:

| protocolo | host |  | ruta de contenido | selector(s) | extension |  | sufijo |  | param(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo** - HTTPS
* **host** : dominio del sitio
* **ruta**  de contenido: ruta que especifica el contenido que se va a representar y se utiliza en combinación con la extensión; en este ejemplo, traducen a  `tools/spy.html`
* **selector(s)** - Se utiliza para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4
* **extension** - Formato del contenido; también especifica la secuencia de comandos que se utilizará para la representación
* **sufijo** : se puede utilizar para especificar información adicional
* **param(s)** : cualquier parámetro requerido para contenido dinámico

#### De URL a contenido y secuencias de comandos {#from-url-to-content-and-scripts}

Uso de los principios de descomposición de URL:

* La asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso.
* Cuando se encuentra el recurso adecuado, se extrae el tipo de recurso sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido.

En la siguiente figura se ilustra el mecanismo utilizado, que se analizará con más detalle en las siguientes secciones.

![Mecanismo de asignación de URL](assets/url-mapping.png)

Con Sling, se especifica qué secuencia de comandos procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo oferta más libertad que uno en el que la secuencia de comandos accede a las entidades de datos (como haría una instrucción SQL en una secuencia de comandos PHP) ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca en el repositorio el recurso solicitado (nodo de contenido):

* First Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; p. ej. `../content/corporate/jobs/developer.html`
* Si no se encuentra ningún nodo, se interrumpe la extensión y se repite la búsqueda; p. ej. `../content/corporate/jobs/developer`
* Si no se encuentra ningún nodo, Sling devolverá el código http 404 (no encontrado).

Sling también permite que otros elementos que no sean nodos JCR sean recursos, pero se trata de una característica avanzada.

### Localización de la secuencia de comandos {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae el **tipo de recurso sling**. Se trata de una ruta que localiza la secuencia de comandos que se utilizará para procesar el contenido.

La ruta especificada por `sling:resourceType` puede ser:

* Absoluto
* Relativo a un parámetro de configuración

>[!TIP]
>
>Las rutas relativas se recomiendan por Adobe, ya que aumentan la portabilidad.

Todos los scripts Sling se almacenan en subcarpetas de `/apps` (mutable, scripts de usuario) o `/libs` (inmutables, scripts del sistema), que se buscarán en este orden.

Otros puntos a tener en cuenta son:

* Cuando se requiera el método (GET, POST), se especificará en mayúsculas según la especificación HTTP, por ejemplo: `jobs.POST.esp`
* Se admiten varios motores de secuencias de comandos, pero las secuencias de comandos recomendadas comunes son HTL y JavaScript.

La lista de los motores de secuencias de comandos admitidos por la instancia de AEM dada se muestra en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

Utilizando el ejemplo anterior, si el `sling:resourceType` es `hr/jobs` entonces para:

* Solicitudes de GET/HEAD y direcciones URL que finalizan en `.html` (tipos de solicitud predeterminados, formato predeterminado)
   * La secuencia de comandos será `/apps/hr/jobs/jobs.esp`; la última sección de `sling:resourceType` forma el nombre del archivo.
* Solicitudes de POST (todos los tipos de solicitud, excluyendo GET/HEAD, el nombre del método debe estar en mayúsculas)
   * POST se utilizará en el nombre de la secuencia de comandos.
   * La secuencia de comandos será `/apps/hr/jobs/jobs.POST.esp`.
* Direcciones URL en otros formatos, sin terminar con `.html`
   * Por ejemplo `../content/corporate/jobs/developer.pdf`
   * La secuencia de comandos será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre de la secuencia de comandos.
* Direcciones URL con selectores
   * Los selectores pueden utilizarse para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente RSS o un resumen.
   * Si vemos una versión descriptiva de la impresora donde el selector podría ser `print`; como en `../content/corporate/jobs/developer.print.html`
   * La secuencia de comandos será `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre de la secuencia de comandos.
* Si no se ha definido ningún `sling:resourceType`:
   * La ruta de contenido se utilizará para buscar una secuencia de comandos adecuada (si la ruta basada en `ResourceTypeProvider` está activa).
   * Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.
   * Se utilizará el tipo de nodo principal.
* Si no se encuentra ninguna secuencia de comandos, se utilizará la secuencia de comandos predeterminada.
   * La representación predeterminada se admite actualmente como texto sin formato (`.txt`), HTML (`.html`) y JSON (`.json`), todos los cuales lista las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión `.res`, o solicitudes sin extensión de solicitud, es rastrear el recurso (cuando sea posible).
* Para la gestión de errores http (códigos 403 o 404) Sling buscará una secuencia de comandos en:
   * Ubicación `/apps/sling/servlet/errorhandler` para secuencias de comandos personalizadas
   * O la ubicación de la secuencia de comandos estándar `/libs/sling/servlet/errorhandler/404.jsp`

Si se aplican varias secuencias de comandos para una solicitud determinada, se selecciona la secuencia de comandos con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; en otras palabras, cuanto más selector coincida mejor, independientemente de la coincidencia de la extensión de solicitud o el nombre del método.

Por ejemplo, considere una solicitud de acceso al recurso

* `/content/corporate/jobs/developer.print.a4.html`

de tipo

* `sling:resourceType="hr/jobs"`

Supongamos que tenemos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por la propiedad `sling:resourceType`) también está el supertipo de recurso. Esto se indica generalmente mediante la propiedad `sling:resourceSuperType`. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos en la que el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) es la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que apunta `sling:resourceType`.

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

La jerarquía de tipos de:

* `/x`
   * Es `[ c, b, a, <default>]`
* Mientras que para `/y`
   * La jerarquía es `[ c, a, <default>]`

Esto se debe a que `/y` tiene la propiedad `sling:resourceSuperType`, mientras que `/x` no la tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### No se puede llamar directamente a los scripts de Sling {#sling-scripts-cannot-be-called-directly}

Dentro de Sling, no se pueden llamar directamente a las secuencias de comandos, ya que esto rompería el concepto estricto de un servidor REST; combinaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculte el recurso dentro de la secuencia de comandos, de modo que la estructura (Sling) ya no lo sepa. Por lo tanto, se pierden ciertas funciones:

* Gestión automática de métodos http distintos de la GET, incluidos:
   * POST, PUT y DELETE que se administran con una implementación predeterminada de sling
   * La secuencia de comandos `POST.jsp` de la ubicación `sling:resourceType`
* La arquitectura del código ya no es tan limpia ni tan claramente estructurada como debería ser; de importancia primordial para el desarrollo a gran escala

### Sling API {#sling-api}

Utiliza el paquete de la API de Sling, `org.apache.sling.*` y las bibliotecas de etiquetas.

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los scripts.

Las secuencias de comandos más complejas (agregación de secuencias de comandos) pueden necesitar acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página, elementos de una lista) y hacerlo incluyendo el *recurso*.

Para ello, puede utilizar el comando `sling:include("/<path>/<resource>")`. Esto incluirá efectivamente la definición del recurso al que se hace referencia.

## los paquetes {#osgi}

OSGi (Open Services Gateway Initiative) define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se conoce como Dynamic Module System for Java). Los contenedores OSGi permiten dividir la aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en terminología OSGi) y administrar las interdependencias entre ellos con:

* Servicios implementados dentro del contenedor
* Un contrato entre el contenedor y su solicitud

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrir entre sí dinámicamente para colaboración.

Una estructura OSGi le oferta la carga/descarga dinámica, la configuración y el control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [sitio Web OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. Sling, y por lo tanto AEM, utiliza la implementación [Apache Felix](https://felix.apache.org/) de OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* Instalar
* Inicial
* Detener
* Actualizar
* Desinstalar
* Ver el estado actual
* Obtener información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [Configuración de OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información.

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista proporciona una visión general de la estructura que verá dentro del repositorio.

* `/apps` - Relacionado con la solicitud; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes listos para usar disponibles en `/libs/core/wcm/components`.
* `/content` - Contenido creado para su sitio web.
* `/etc`
* `/home` - Información de usuarios y grupos.
* `/libs` - Bibliotecas y definiciones que pertenecen al núcleo del AEM. Las subcarpetas de `/libs` representan las funciones de AEM listas para usar. No se puede modificar el contenido de `/libs`. Las funciones específicas de su sitio web deben realizarse en `/apps`.
* `/tmp` - Zona de trabajo temporal.
* `/var` - Archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y gestión de eventos.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben hacerse con cuidado. Asegúrese de comprender completamente las implicaciones de cualquier cambio que realice.
>
>No debe cambiar nada en la ruta `/libs`. Para configuración y otros cambios, copie el elemento de `/libs` a `/apps` y realice cualquier cambio dentro de `/apps`.
