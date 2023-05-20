---
title: Fundamentos técnicos de AEM
description: AEM AEM Una visión general de los fundamentos técnicos de la, incluido cómo se estructura la y las tecnologías fundamentales como JCR, Sling y OSGi.
exl-id: ab6e7fe9-a25d-4351-a005-f4466cc0f40e
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 1%

---

# Fundamentos técnicos de AEM {#aem-technical-foundations}

AEM es una plataforma sólida basada en tecnologías probadas, escalables y flexibles. AEM AEM Este documento ofrece una descripción detallada de las distintas partes que componen la y está diseñado como un apéndice técnico para un desarrollador de paquetes de pila completa. No pretende ser una guía de introducción. AEM Si es nuevo en el desarrollo de la, consulte la [Introducción al desarrollo de AEM Sites: Tutorial de WKND](develop-wknd-tutorial.md) como primer paso.

>[!TIP]
>
>AEM Antes de sumergirse en las tecnologías básicas de la, Adobe recomienda completar la [Introducción al desarrollo de AEM Sites: Tutorial de WKND.](develop-wknd-tutorial.md)

## Aspectos básicos {#fundamentals}

AEM Al ser un sistema moderno de gestión de contenidos, se basa en las tecnologías web estándar, que son:

* El ciclo de solicitud-respuesta (XMLHttpRequest / XMLHttpResponse)
* HTML
* CSS
* JavaScript

El repositorio de contenido subyacente y las capas de lógica empresarial se basan en tecnologías Java:

* JCR
* Sling
* OSGi

## Repositorio de contenido Java {#java-content-repository}

El estándar del repositorio de contenido de Java (JCR), [JSR 283](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html), especifica una forma independiente del proveedor y de la implementación de acceder al contenido bidireccionalmente en un nivel granular dentro de un repositorio de contenido. El responsable de la especificación es Adobe Research (Suiza) AG.

El [API JCR 2.0](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) paquete, `javax.jcr.*` se utiliza para el acceso directo y la manipulación del contenido del repositorio.

AEM La se basa en un JCR.

## Apache Jackrabbit Oak {#jackrabbit-oak}

[Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/) es una implementación de un repositorio de contenido jerárquico escalable y de alto rendimiento que se utiliza como base de sitios web modernos de primera clase y otras aplicaciones de contenido exigentes, conforme al estándar JCR.

AEM Jackrabbit Oak (también conocido como Oak) es la implementación del estándar JCR sobre el que se construye el.

## Procesamiento de solicitudes de Sling {#sling-request-processing}

AEM se crea usando el [Sling](https://sling.apache.org/site/index.html), un marco de trabajo de aplicaciones web basado en principios REST que proporciona un fácil desarrollo de aplicaciones orientadas a contenido. Sling utiliza un repositorio JCR, como Apache Jackrabbit Oak, como almacén de datos. Sling ha sido colaborador de Apache Software Foundation; puede encontrar más información en Apache.

### Introducción a Sling {#introduction-to-sling}

Con Sling, el tipo de contenido que se procesará no es la primera consideración de procesamiento. En su lugar, la consideración principal es si la URL responde a un objeto de contenido para el que se puede encontrar una secuencia de comandos para realizar la renderización. Esto proporciona una excelente compatibilidad para que los autores de contenido web creen páginas que se personalicen fácilmente según sus necesidades.

Las ventajas de esta flexibilidad son evidentes en aplicaciones con una amplia gama de elementos de contenido diferentes o cuando necesita páginas que se puedan personalizar fácilmente. AEM En concreto, al implementar un sistema de administración de contenido web como, por ejemplo, la administración de contenido web, se puede hacer lo siguiente

Consulte [Descubra Sling en 15 minutos](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) para conocer los primeros pasos para desarrollar con Sling.

En el diagrama siguiente se explica la resolución de scripts de Sling: se muestra cómo ir de una solicitud HTTP al nodo de contenido, de un nodo de contenido al tipo de recurso, de un tipo de recurso al script y qué variables de scripts están disponibles.

![Explicación de la resolución de scripts de Apache Sling](assets/sling-cheatsheet-01.png)

En el siguiente diagrama se explican todos los parámetros de solicitud ocultos, pero útiles, que puede utilizar al tratar con el `SlingPostServlet`, el controlador predeterminado para todas las solicitudes de POST que le ofrece un sinfín de opciones para crear, modificar, eliminar, copiar y mover nodos en el repositorio.

![Uso de SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling se centra en el contenido {#sling-is-content-centric}

Sling es *centrado en el contenido*. Esto significa que el procesamiento se centra en el contenido, ya que cada solicitud (HTTP) se asigna al contenido en forma de recurso JCR (un nodo de repositorio):

* El primer destino es el recurso (nodo JCR) que contiene el contenido
* En segundo lugar, la representación o script se encuentra en las propiedades del recurso en combinación con ciertas partes de la solicitud (por ejemplo, los selectores o la extensión)

### RESTful Sling {#restful-sling}

Debido a su filosofía centrada en el contenido, Sling implementa un servidor orientado a REST y, por lo tanto, incluye un nuevo concepto en los marcos de aplicaciones web. Las ventajas son:

* Muy RESTful, no solo en la superficie; los recursos y las representaciones se modelan correctamente dentro del servidor
* Quita uno o más modelos de datos
   * Otros marcos de gestión de contenido pueden requerir una estructura URL, objetos empresariales o un esquema de base de datos para acceder a un recurso.
   * Con Sling, esto se reduce a: URL = recurso = estructura JCR

### Descomposición de URL {#url-decomposition}

En Sling, el procesamiento se basa en la dirección URL de la solicitud del usuario. Esto define el contenido que deben mostrar los scripts adecuados. Para ello, se extrae información de la dirección URL.

Si analizamos la siguiente URL:

```text
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

Podemos dividirlo en sus partes compuestas:

| protocolo | host |  | ruta de contenido | selector(es) | extensión |  | sufijo |  | parámetro(s) |
|---|---|---|---|---|---|---|---|---|---|
| `https://` | `myhost` | `/` | `tools/spy` | `.printable.a4.` | `html` | `/` | `a/b` | `?` | `x=12` |

* **protocolo** - HTTPS
* **host** - Dominio del sitio
* **ruta de contenido** - Ruta que especifica el contenido que se va a procesar y que se utiliza en combinación con la extensión; en este ejemplo se traducen en `tools/spy.html`
* **selector(es)** - Se utiliza para métodos alternativos de representación del contenido; en este ejemplo, una versión compatible con la impresora en formato A4
* **extensión** - Formato del contenido; también especifica el script que se utilizará para el procesamiento
* **sufijo** - Se puede utilizar para especificar información adicional
* **parámetro(s)** - Cualquier parámetro necesario para el contenido dinámico.

#### De la URL al contenido y los scripts {#from-url-to-content-and-scripts}

Uso de los principios de descomposición de URL:

* La asignación utiliza la ruta de contenido extraída de la solicitud para localizar el recurso.
* Cuando se encuentra el recurso adecuado, se extrae el tipo de recurso de sling y se utiliza para localizar la secuencia de comandos que se utilizará para procesar el contenido.

La siguiente figura ilustra el mecanismo utilizado, que se analizará con más detalle en las secciones siguientes.

![Mecanismo de asignación de URL](assets/url-mapping.png)

Con Sling, puede especificar qué secuencia de comandos procesa una entidad determinada (configurando la variable `sling:resourceType` en el nodo JCR). Este mecanismo ofrece más libertad que una en la que el script accede a las entidades de datos (como lo haría una instrucción SQL en un script PHP), ya que un recurso puede tener varias representaciones.

#### Asignación de solicitudes a los recursos {#mapping-requests-to-resources}

La solicitud se desglosa y se extrae la información necesaria. Se busca el recurso solicitado en el repositorio (nodo de contenido):

* Primer Sling comprueba si existe un nodo en la ubicación especificada en la solicitud; por ejemplo, `../content/corporate/jobs/developer.html`
* Si no se encuentra ningún nodo, la extensión se suelta y la búsqueda se repite; por ejemplo, `../content/corporate/jobs/developer`
* Si no se encuentra ningún nodo, Sling devolverá el código http 404 (no encontrado).

Sling también permite que otras cosas que no sean nodos JCR sean recursos, pero esta es una función avanzada.

### Localización del script {#locating-the-script}

Cuando se encuentra el recurso adecuado (nodo de contenido), la variable **tipo de recurso de sling** se ha extraído. Esta es una ruta que localiza el script que se utilizará para procesar el contenido.

La ruta especificada por el `sling:resourceType` puede ser:

* Absoluto
* Relativo a un parámetro de configuración

>[!TIP]
>
>El Adobe recomienda las rutas relativas a medida que aumentan la portabilidad.

Todos los scripts de Sling se almacenan en subcarpetas de `/apps` (mutable, scripts de usuario) o `/libs` (inmutable, scripts del sistema), que se buscarán en este orden.

Otros puntos que hay que tener en cuenta son:

* Cuando se requiere el método (GET, POST), se especifica en mayúsculas como según la especificación HTTP, por ejemplo, `jobs.POST.esp`
* Se admiten varios motores de scripts, pero los scripts comunes recomendados son HTL y JavaScript.

AEM La lista de motores de scripts admitidos por la instancia determinada de se enumera en la consola de administración de Felix ( ). `http://<host>:<port>/system/console/slingscripting`).

En el ejemplo anterior, si la variable `sling:resourceType` es `hr/jobs` y luego para:

* Solicitudes y direcciones URL de GET/HEAD que terminan en `.html` (tipos de solicitud predeterminados, formato predeterminado)
   * El script será `/apps/hr/jobs/jobs.esp`; la última sección de la `sling:resourceType` forma el nombre del archivo.
* Solicitudes de POST (todos los tipos de solicitud excepto GET/HEAD, el nombre del método debe estar en mayúsculas)
   * Se utilizará el POST en el nombre del script.
   * El script será `/apps/hr/jobs/jobs.POST.esp`.
* URL con otros formatos que no terminan con `.html`
   * Por ejemplo `../content/corporate/jobs/developer.pdf`
   * El script será `/apps/hr/jobs/jobs.pdf.esp`; el sufijo se agrega al nombre del script.
* URL con selectores
   * Los selectores se pueden utilizar para mostrar el mismo contenido en un formato alternativo. Por ejemplo, una versión compatible con la impresora, una fuente RSS o un resumen.
   * Si miramos una versión compatible con la impresora donde el selector podría ser `print`; como en `../content/corporate/jobs/developer.print.html`
   * El script será `/apps/hr/jobs/jobs.print.esp`; el selector se añade al nombre del script.
* Si no `sling:resourceType` se ha definido a continuación:
   * La ruta de contenido se utilizará para buscar un script adecuado (si la ruta está basada en `ResourceTypeProvider` está activo).
   * Por ejemplo, la secuencia de comandos para `../content/corporate/jobs/developer.html` generaría una búsqueda en `/apps/content/corporate/jobs/`.
   * Se utilizará el tipo de nodo principal.
* Si no se encuentra ninguna secuencia de comandos, se utilizará la predeterminada.
   * La representación predeterminada se admite actualmente como texto sin formato (`.txt`), HTML (`.html`) y JSON (`.json`), todas las cuales enumerarán las propiedades del nodo (con el formato adecuado). Representación predeterminada de la extensión. `.res`, o solicitudes sin una extensión de solicitud, es para poner en cola el recurso (cuando sea posible).
* Para la gestión de errores http (códigos 403 o 404), Sling buscará un script en:
   * La ubicación. `/apps/sling/servlet/errorhandler` para scripts personalizados
   * O la ubicación del script estándar `/libs/sling/servlet/errorhandler/404.jsp`

Si se aplican varios scripts a una solicitud determinada, se selecciona el script con la mejor coincidencia. Cuanto más específica sea una coincidencia, mejor será; es decir, cuanto más coincida el selector, mejor, independientemente de la coincidencia de cualquier extensión de solicitud o nombre de método.

Por ejemplo, considere una solicitud de acceso al recurso

* `/content/corporate/jobs/developer.print.a4.html`

de tipo

* `sling:resourceType="hr/jobs"`

Suponiendo que tenemos la siguiente lista de scripts en la ubicación correcta:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

Entonces el orden de preferencia sería (8) - (7) - (6) - (5) - (4) - (3) - (2) - (1).

Además de los tipos de recursos (definidos principalmente por el `sling:resourceType` propiedad) también está el supertipo de recurso. Esto generalmente se indica mediante la variable `sling:resourceSuperType` propiedad. Estos supertipos también se tienen en cuenta al intentar encontrar una secuencia de comandos. La ventaja de los supertipos de recursos es que pueden formar una jerarquía de recursos donde el tipo de recurso predeterminado es `sling/servlet/default` (utilizado por los servlets predeterminados) es en realidad la raíz.

El supertipo de recurso de un recurso se puede definir de dos maneras:

* por el `sling:resourceSuperType` propiedad del recurso.
* por el `sling:resourceSuperType` propiedad del nodo al que se va a `sling:resourceType` puntos.

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

Esto se debe a `/y` tiene el `sling:resourceSuperType` propiedad mientras que `/x` no y, por lo tanto, su supertipo se toma de su tipo de recurso.

#### Los scripts de Sling no se pueden llamar directamente {#sling-scripts-cannot-be-called-directly}

En Sling, no se puede llamar directamente a los scripts, ya que esto rompería el concepto estricto de un servidor REST; mezclaría recursos y representaciones.

Si llama a la representación (la secuencia de comandos) directamente, oculta el recurso dentro de la secuencia de comandos, por lo que el marco de trabajo (Sling) ya no sabe nada de él. Por lo tanto, se pierden ciertas funciones:

* Gestión automática de métodos http distintos de la GET, incluidos:
   * POST, PUT y DELETE que se gestionan con una implementación predeterminada de sling
   * El `POST.jsp` script en su `sling:resourceType` ubicación
* Su arquitectura de código ya no es tan limpia ni está tan claramente estructurada como debería ser; es de suma importancia para el desarrollo a gran escala

### API Sling {#sling-api}

Utiliza el paquete de API de Sling, `org.apache.sling.*`, y bibliotecas de etiquetas.

### Hacer referencia a elementos existentes mediante sling:include {#referencing-existing-elements-using-sling-include}

Una consideración final es la necesidad de hacer referencia a los elementos existentes dentro de los guiones.

Es posible que los scripts más complejos (agregar scripts) necesiten acceder a varios recursos (por ejemplo, navegación, barra lateral, pie de página, elementos de una lista) y hacerlo incluyendo la variable *resource*.

Para ello, puede utilizar el `sling:include("/<path>/<resource>")` comando. Esto incluirá de forma efectiva la definición del recurso al que se hace referencia.

## OSGi {#osgi}

OSGi (Open Services Gateway Initiative) define una arquitectura para el desarrollo e implementación de aplicaciones y bibliotecas modulares (también se conoce como Dynamic Module System for Java). Los contenedores OSGi le permiten dividir la aplicación en módulos individuales (son archivos jar con información meta adicional y llamados paquetes en la terminología OSGi) y administrar las dependencias cruzadas entre ellos con:

* Servicios implementados dentro del contenedor
* Un contrato entre el contenedor y la aplicación

Estos servicios y contratos proporcionan una arquitectura que permite a los elementos individuales descubrirse dinámicamente entre sí para colaborar.

A continuación, un marco OSGi le ofrece carga/descarga dinámica, configuración y control de estos paquetes, sin necesidad de reiniciar.

>[!NOTE]
>
>Puede encontrar información completa sobre la tecnología OSGi en el [Sitio web de OSGi](https://www.osgi.org).
>
>En particular, su página de Educación Básica contiene una colección de presentaciones y tutoriales.

Esta arquitectura le permite ampliar Sling con módulos específicos de la aplicación. AEM Sling y, por lo tanto, el uso de la función de la interfaz de usuario de, [Apache Felix](https://felix.apache.org/) implementación de OSGi. Ambas son colecciones de paquetes OSGi que se ejecutan dentro de un marco OSGi.

Esto le permite realizar las siguientes acciones en cualquiera de los paquetes de la instalación:

* Instalar
* Inicial
* Detener
* Actualizar
* Desinstalar
* Ver el estado actual
* Acceda a información más detallada (por ejemplo, nombre simbólico, versión, ubicación, etc.) sobre los paquetes específicos

Consulte [AEM Configuración de OSGi para la as a Cloud Service](/help/implementing/deploying/configuring-osgi.md) para obtener más información.

## Estructura dentro del repositorio {#structure-within-the-repository}

La siguiente lista ofrece una descripción general de la estructura que verá dentro del repositorio.

* `/apps` - Relacionado con la aplicación; incluye definiciones de componentes específicas del sitio web. Los componentes que desarrolle se pueden basar en los componentes predeterminados disponibles en `/libs/core/wcm/components`.
* `/content` : contenido creado para su sitio web.
* `/etc`
* `/home` : información de usuario y grupo.
* `/libs` AEM - Bibliotecas y definiciones que pertenecen al núcleo de la. Las subcarpetas de `/libs` AEM representan las funciones de la aplicación listas para usar de la serie de la aplicación de la aplicación de la. El contenido de `/libs` no se puede modificar. Las funciones específicas del sitio web deben realizarse en `/apps`.
* `/tmp` - Zona de trabajo temporal.
* `/var` : archivos que cambian y son actualizados por el sistema; como registros de auditoría, estadísticas y administración de eventos.

>[!CAUTION]
>
>Los cambios en esta estructura, o en los archivos que contiene, deben realizarse con cuidado. Asegúrese de comprender completamente las implicaciones de cualquier cambio que realice.
>
>No debe cambiar nada en el `/libs` ruta. Para cambios de configuración y de otro tipo, copie el elemento de `/libs` hasta `/apps` y realice cualquier cambio en `/apps`.
