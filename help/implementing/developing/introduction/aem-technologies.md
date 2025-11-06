---
title: Fundamentos técnicos de AEM
description: Una visión general de los fundamentos técnicos de AEM, incluido cómo AEM está estructurado y utiliza tecnologías fundamentales como JCR, Sling y OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2129'
ht-degree: 1%

---

# Fundamentos técnicos de AEM {#aem-technical-foundations}

AEM es una plataforma sólida basada en tecnologías probadas, escalables y flexibles. Este documento ofrece información general detallada sobre las distintas partes que componen AEM y está diseñado como apéndice técnico para un desarrollador de AEM de pila completa. No pretende ser una guía de introducción. Si es nuevo en el desarrollo de AEM, consulte [Introducción al desarrollo de AEM Sites - Tutorial de WKND](develop-wknd-tutorial.md) como primer paso.

>[!TIP]
>
>Antes de sumergirse en las tecnologías principales de AEM, Adobe recomienda completar el [Tutorial de WKND de introducción al desarrollo de AEM Sites](develop-wknd-tutorial.md).

## Aspectos básicos {#fundamentals}

Como sistema moderno de administración de contenido, AEM se basa en tecnologías web estándar:

* El ciclo de solicitud-respuesta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

El repositorio de contenido subyacente y las capas de lógica empresarial se basan en las tecnologías Java™:

* JCR
* Sling
* OSGi

## Repositorio de contenido de Java™ {#java-content-repository}

El estándar del repositorio de contenido Java™ (JCR), [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor e independiente de la implementación para acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido. El responsable de la especificación es Adobe Research (Suiza) AG.

El paquete [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html), `javax.jcr.*`, se usa para el acceso directo y la manipulación del contenido del repositorio.

AEM se basa en un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/) es una implementación de un repositorio de contenido jerárquico escalable y de alto rendimiento que se usará como base de sitios web modernos de primera clase y otras aplicaciones de contenido exigentes, de conformidad con el estándar JCR.

Jackrabbit Oak (también denominado simplemente Oak) es la implementación del estándar JCR sobre el que se crea AEM.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

AEM se creó con [Sling](https://sling.apache.org/index.html), un módulo de aplicaciones web basado en los principios de REST que facilita el desarrollo de aplicaciones orientadas a contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit Oak, como almacén de datos. Sling ha sido colaborador de Apache Software Foundation; puede encontrar más información en Apache.

### Introducción a Sling {#introduction-to-sling}

Con Sling, el tipo de contenido que se procesará no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL se resuelve en un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Este proceso proporciona un soporte excelente para que los autores de contenido web creen páginas que se personalicen fácilmente según sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando necesita páginas que se puedan personalizar fácilmente. En concreto, al implementar un sistema de administración de contenido web como AEM.

Consulte [Discover Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

El diagrama siguiente explica la resolución de scripts de Sling. Muestra cómo pasar de una solicitud HTTP al nodo de contenido, de un nodo de contenido al tipo de recurso, de un tipo de recurso al script y qué variables de script están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el diagrama siguiente se explican los parámetros de solicitud ocultos pero eficaces que se pueden usar con `SlingPostServlet`, el controlador predeterminado para todas las solicitudes POST. El controlador le ofrece un sinfín de opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Usando SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling está *centrado en contenido*. Significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido
* En segundo lugar, la representación o script se encuentra en las propiedades del recurso con determinadas partes de la solicitud (por ejemplo, los selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a su filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* RESTful, no solo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* Quita uno o más modelos de datos
   * Otros marcos de gestión de contenido pueden requerir una estructura URL, objetos empresariales o un esquema de base de datos para acceder a un recurso.
   * El uso de Sling lo reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se basa en la dirección URL de la solicitud del usuario. Define el contenido que se muestra mediante los scripts adecuados y la información se extrae de la dirección URL.

Análisis de la siguiente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Puede dividirlo en sus partes compuestas:

| protocolo | host |  | ruta de contenido | selectores | extensión |  | sufijo |  | parámetros |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo** - HTTPS
* **host** - Dominio del sitio
* **ruta de contenido**: ruta que especifica el contenido que se procesará y que se utilizará con la extensión. En este ejemplo, se traduce como `tools/spy.html`
* **selectores**: se utilizan para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4
* **extensión** - Formato de contenido; también especifica el script que se utilizará para la representación
* **sufijo** - Se puede usar para especificar información adicional
* **params**: cualquier parámetro necesario para el contenido dinámico

#### De la URL al contenido y los scripts {#from-url-to-content-and-scripts}

Uso de los principios de descomposición de URL:

* La asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso.
* Cuando se encuentra el recurso adecuado, se extrae el tipo de recurso de sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido.

La siguiente figura ilustra el mecanismo utilizado, que se analiza con más detalle en las secciones siguientes.

![Mecanismo de asignación de URL](assets/url-mapping.png)

Con Sling, puede especificar qué script procesa una entidad determinada (estableciendo la propiedad `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como lo haría una instrucción SQL en un script PHP), ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca el recurso solicitado en el repositorio (nodo de contenido):

* Primer Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; por ejemplo, `../content/corporate/jobs/developer.html`
* Si no se encuentra ningún nodo, se quitará la extensión y se repetirá la búsqueda; por ejemplo, `../content/corporate/jobs/developer`
* Si no se encuentra ningún nodo, Sling devuelve el código http 404 (no encontrado).

Sling también permite que otros nodos que no sean nodos JCR sean recursos, pero esta funcionalidad es avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso apropiado (nodo de contenido), se extrae **sling resource type**. Esta ruta localiza el script que se utilizará para procesar el contenido.

La ruta especificada por `sling:resourceType` puede ser:

* Absoluto
* Relativo a un parámetro de configuración

>[!TIP]
>
>Adobe recomienda las rutas relativas a medida que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` (scripts mutables, de usuario) o `/libs` (scripts inmutables, del sistema), en las que se busca en este orden.

Otros puntos que hay que tener en cuenta son:

* Cuando se requiere el método (GET, POST), se especifica en mayúsculas según la especificación HTTP, por ejemplo, `jobs.POST.esp`
* Se admiten varios motores de scripts, pero los scripts comunes recomendados son HTL y JavaScript.

La lista de motores de scripts admitidos por la instancia determinada de AEM se enumera en la Consola de administración Felix ( `http://<host>:<port>/system/console/slingscripting`).

En el ejemplo anterior, si `sling:resourceType` es `hr/jobs`, para:

* Solicitudes y direcciones URL de GET/HEAD que terminan en `.html` (tipos de solicitud predeterminados, formato predeterminado)
   * El script es `/apps/hr/jobs/jobs.esp`; la última sección de `sling:resourceType` forma el nombre del archivo.
* Solicitudes POST (todos los tipos de solicitud excepto GET/HEAD, el nombre del método debe estar en mayúsculas)
   * POST se utiliza en el nombre del script.
   * El script es `/apps/hr/jobs/jobs.POST.esp`.
* Direcciones URL en otros formatos, que no terminan con `.html`
   * Por ejemplo, `../content/corporate/jobs/developer.pdf`
   * El script es `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre del script.
* URL con selectores
   * Los selectores se pueden utilizar para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con una impresora, una fuente RSS o un resumen.
   * Si observa una versión compatible con la impresora donde el selector podría ser `print`; como en `../content/corporate/jobs/developer.print.html`
   * El script es `/apps/hr/jobs/jobs.print.esp`; el selector se agrega al nombre del script.
* Si no, se define `sling:resourceType`, entonces:
   * La ruta de contenido se usa para buscar un script apropiado (si está activo el script basado en rutas `ResourceTypeProvider`).
   * Por ejemplo, el script de `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.
   * Se utiliza el tipo de nodo principal.
* Si no se encuentra ninguna secuencia de comandos, se utiliza la predeterminada.
   * La representación predeterminada se admite como texto sin formato (`.txt`), HTML (`.html`) y JSON (`.json`), todos los cuales enumeran las propiedades del nodo (con el formato adecuado). La representación predeterminada para la extensión `.res`, o solicitudes sin una extensión de solicitud, es poner en cola el recurso (cuando sea posible).
* Para la administración de errores de http (códigos 403 o 404), Sling busca una secuencia de comandos en:
   * La ubicación `/apps/sling/servlet/errorhandler` para los scripts personalizados
   * O la ubicación del script estándar `/libs/sling/servlet/errorhandler/404.jsp`

Si se aplican varios scripts a una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; es decir, cuanto más coincida el selector, mejor, independientemente de la coincidencia de cualquier extensión de solicitud o nombre de método.

Por ejemplo, considere una solicitud de acceso al recurso

* `/content/corporate/jobs/developer.print.a4.html`

Del tipo

* `sling:resourceType="hr/jobs"`

Suponiendo que tiene la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por la propiedad `sling:resourceType`), también está el supertipo de recursos. Este tipo se indica mediante la propiedad `sling:resourceSuperType`. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos en la que el tipo de recurso predeterminado `sling/servlet/default` (utilizado por los servlets predeterminados) sea en realidad la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por la propiedad `sling:resourceSuperType` del recurso.
* por la propiedad `sling:resourceSuperType` del nodo al que señala `sling:resourceType`.

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
   * Es `[ c, b, a, <default>]`
* Mientras que para `/y`
   * La jerarquía es `[ c, a, <default>]`

El motivo se debe a que `/y` tiene la propiedad `sling:resourceSuperType`, mientras que `/x` no la tiene y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### Los scripts de Sling no se pueden llamar directamente {#sling-scripts-cannot-be-called-directly}

En Sling, no se puede llamar directamente a los scripts porque rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculta el recurso dentro de la secuencia de comandos, por lo que el marco de trabajo (Sling) ya no sabe nada de él. Por lo tanto, se pierden ciertas funciones:

* Gestión automática de métodos http distintos de GET, incluidos:
   * POST, PUT, DELETE que se gestiona con una implementación predeterminada de sling
   * El script `POST.jsp` en su ubicación `sling:resourceType`
* Su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; es de suma importancia para el desarrollo a gran escala

### API de Sling {#sling-api}

Utiliza el paquete de API de Sling, `org.apache.sling.*` y las bibliotecas de etiquetas.

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los guiones.

Los scripts más complejos (agregar scripts) tienen acceso a varios recursos (por ejemplo, navegación, barra lateral, pie de página y elementos de una lista) y lo hacen incluyendo el *recurso*.

En este caso, puede utilizar el comando `sling:include("/<path>/<resource>")`. Incluye efectivamente la definición del recurso al que se hace referencia.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) define una arquitectura para desarrollar e implementar aplicaciones y bibliotecas modulares (también se conoce como Dynamic Module System for Java™). Los contenedores OSGi le permiten dividir la aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en la terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* Servicios implementados dentro del contenedor
* Un contrato entre el contenedor y la aplicación

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse dinámicamente entre sí para colaborar.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciarlos.

>[!NOTE]
>
>Encontrará información completa sobre la tecnología OSGi en el [sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. Sling y, por lo tanto, AEM, utilizan la implementación [Apache Felix](https://felix.apache.org/documentation/index.html) de OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esta funcionalidad permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* Instalar
* Iniciar
* Detener
* Actualizar
* Desinstalar
* Ver estado más reciente
* Acceda a información más detallada sobre paquetes específicos, por ejemplo, nombre simbólico, versión y ubicación

Consulte [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información.

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece información general sobre la estructura que se ve dentro del repositorio.

* `/apps` - Relacionado con la aplicación; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/core/wcm/components`.
* `/content`: contenido creado para su sitio web.
* `/etc`
* `/home` - Información de usuario y grupo.
* `/libs`: bibliotecas y definiciones que pertenecen al núcleo de AEM. Las subcarpetas de `/libs` representan las características de AEM listas para usar. No se puede modificar el contenido de `/libs`. Las características específicas del sitio web deben realizarse en `/apps`.
* `/tmp` - Área de trabajo temporal.
* `/var`: archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y control de eventos.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado. Asegúrese de comprender completamente las implicaciones de cualquier cambio que realice.
>
>No cambie nada en la ruta de acceso `/libs`. Para cambios de configuración y de otro tipo, copie el elemento de `/libs` a `/apps` y realice los cambios que desee en `/apps`.
