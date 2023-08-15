---
title: Asignación de recursos
description: AEM Obtenga información sobre cómo definir redirecciones, URL de vanidad y hosts virtuales para mediante la asignación de recursos para su.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 1a1bb23c-d1d1-4e2b-811b-753e6a90a01b
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 6%

---

# Asignación de recursos{#resource-mapping}

AEM La asignación de recursos se utiliza para definir redirecciones, URL de vanidad y hosts virtuales para los usuarios de la red de distribución de recursos ().

Por ejemplo, puede utilizar estas asignaciones para lo siguiente:

* Agregue a todas las solicitudes el prefijo `/content` para que la estructura interna se oculte a los visitantes del sitio web.
* Defina una redirección para que todas las solicitudes a `/content/en/gateway` de su sitio web se redirigen a `https://gbiv.com/`.

Una posible asignación HTTP prefija todas las solicitudes a `localhost:4503` con `/content`. Una asignación como esta podría utilizarse para ocultar la estructura interna de los visitantes del sitio web, ya que permite lo siguiente:

`localhost:4503/content/we-retail/en/products.html`

Para acceder a él, utilice:

`localhost:4503/we-retail/en/products.html`

Como la asignación añade automáticamente el prefijo `/content` hasta `/we-retail/en/products.html`.

>[!CAUTION]
>
>Las URL mnemónicas no admiten patrones de regex.

>[!NOTE]
>
>Consulte la documentación de Sling y [Asignaciones para la resolución de recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) y [Recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para obtener más información.

## Visualización de definiciones de asignación {#viewing-mapping-definitions}

Las asignaciones de dos listas que evalúa el JCR Resource Resolver (de arriba a abajo) para encontrar una coincidencia.

Estas listas se pueden ver (junto con la información de configuración) en la **ResourceResolver de JCR** de la consola Felix; por ejemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* Configuración Muestra la configuración actual (tal como se define para la variable [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map)).

* Prueba de configuración Permite introducir una dirección URL o una ruta de recurso. Clic **Resolver** o **Mapa** para confirmar cómo el sistema transforma la entrada.

* **Entradas de mapa de resolución**
La lista de entradas utilizadas por los métodos ResourceResolver.resolve para asignar direcciones URL a recursos.

* **Entradas de mapa de asignación**
La lista de entradas utilizadas por los métodos ResourceResolver.map para asignar rutas de recursos a las direcciones URL.

Las dos listas muestran varias entradas, incluidas las entradas definidas como predeterminadas por las aplicaciones. Estas entradas suelen tener como objetivo simplificar las direcciones URL del usuario.

El par de listas a **Patrón**, una expresión regular coincidente con la solicitud, con un **Sustitución** que define la redirección que se va a imponer.

Por ejemplo, el:

**Patrón** `^[^/]+/[^/]+/welcome$`

Déclencheur el:

**Sustitución** `/libs/cq/core/content/welcome.html`.

Para redirigir una solicitud:

`https://localhost:4503/welcome` ``

A:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Se crean nuevas definiciones de asignación dentro del repositorio.

>[!NOTE]
>
>Hay muchos recursos disponibles para explicar cómo definir las expresiones regulares. Por ejemplo, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### AEM Creación de Definiciones de Asignación en el {#creating-mapping-definitions-in-aem}

AEM En una instalación estándar de la carpeta de carpetas, puede encontrar la siguiente carpeta:

`/etc/map/http`

Esta carpeta es la estructura utilizada al definir asignaciones para el protocolo HTTP. Otras carpetas ( `sling:Folder`) se puede crear en `/etc/map` para cualquier otro protocolo que desee asignar.

#### Configuración de una redirección interna a /content {#configuring-an-internal-redirect-to-content}

Para crear la asignación que prefija cualquier solicitud a https://localhost:4503/ con `/content`:

1. Uso de CRXDE para desplazarse a `/etc/map/http`.

1. Cree un nodo:

   * **Tipo** `sling:Mapping`
Este tipo de nodo está diseñado para este tipo de asignaciones, aunque su uso no es obligatorio.

   * **Nombre** `localhost_any`

1. Haga clic en **Guardar todo**.
1. **Añadir** Agregue las siguientes propiedades a este nodo:

   * **Nombre** `sling:match`

      * **Tipo** `String`

      * **Valor** `localhost.4503/`

   * **Nombre** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor** `/content/`

1. Haga clic en **Guardar todo**.

Esta asignación administra una solicitud como:
`localhost:4503/geometrixx/en/products.html`
como si:
`localhost:4503/content/geometrixx/en/products.html`
se ha solicitado.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) en la Documentación de Sling para obtener más información sobre las propiedades de Sling disponibles y cómo se pueden configurar.
>Por ejemplo, [Interpolación de cadenas](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html#string-interpolation-for-etcmap) es útil porque permite configurar una asignación que obtiene valores por entorno a través de variables de entorno.

>[!NOTE]
>
>Puede utilizar `/etc/map.publish` para guardar las configuraciones del entorno de publicación. Estas configuraciones deben replicarse y la nueva ubicación ( `/etc/map.publish`) configurado para **Ubicación de asignación** de la [Apache Sling Resource Resolver](/help/overview/seo-and-url-management.md#etc-map) del entorno de publicación
