---
title: Redirecciones de URL sin canalizaciones
description: Aprenda a declarar redirecciones 301 o 302 sin acceso a canalizaciones Git o Cloud Manager.
feature: Dispatcher
role: Admin
source-git-commit: 567c75f456f609dbc254753b439151d0f4100bc0
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Redirecciones de URL sin canalizaciones {#pipeline-free-redirects}

>[!NOTE]
>Esta función aún no se ha lanzado.

Por varios motivos, las organizaciones reescriben las direcciones URL de forma que provocan un redireccionamiento 301 (o 302), lo que significa que el explorador se redirige a una página diferente.

Los escenarios incluyen:

* Se ha eliminado una página del HTML, por lo que se lleva al usuario a una página de reemplazo (a veces la página principal) en lugar de ver un error de `404 Page Not Found`.
* Una página de HTML renombrada.
* Optimización de SEO.

AEM as a Cloud Service ofrece [varios enfoques](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/administration/url-redirection) para implementar redirecciones del lado del cliente, pero la estrategia descrita en este artículo, redirecciones sin canalización, es una buena opción cuando:

* Las personas que mantienen las redirecciones son usuarios empresariales, que no tienen el acceso necesario para confirmar los cambios de archivo en el control de código fuente o la posibilidad de ejecutar una canalización de configuración de nivel web de Cloud Manager.
* El número de redirecciones va de unas pocas a decenas de miles.
* Desea la opción de una interfaz de usuario, ya sea creada como un proyecto personalizado o usando el [Administrador de reescritura de mapas de ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html).

AEM El núcleo de esta función es la capacidad de Apache/Dispatcher para cargar (o volver a cargar) uno o más archivos de asignación de reescritura que se han colocado en una ubicación especificada del repositorio de publicación. Es importante mencionar que la forma en que los archivos llegan a ese punto está fuera del ámbito de esta función, pero puede considerar uno de los siguientes métodos:

* Ingesta de la asignación de reescritura como un recurso en la interfaz de usuario de creación y publicación.
* Instalando [ACS Commons Rewrite Map Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/redirect-map-manager/index.html), que incluye una interfaz de usuario para administrar las asignaciones de URL y también puede publicar el archivo de asignación de reescritura.
* Flexibilidad total al escribir una aplicación personalizada. AEM Por ejemplo, una interfaz de usuario o de línea de comandos para administrar las asignaciones de URL o, alternativamente, un formulario para cargar una asignación de reescritura, que luego utiliza las API de para publicar el archivo de asignación de reescritura.

>[!NOTE]
> AEM Esta característica requiere la versión de la **18311 o superior**.

## El mapa de reescritura {#rewrite-map}

El servidor HTTP Apache vuelve a cargar (si se cambia) el mapa de reescritura cada 300 segundos de forma predeterminada (el valor se puede configurar). El formato de archivo debe seguir el formato de archivo de mapa de clave-valor de texto sin formato RewriteMap descrito en la [documentación de Apache](https://httpd.apache.org/docs/2.4/rewrite/rewritemap.html#txt).

Se debe crear un archivo con el nombre `managed-rewrite-maps.yaml` para especificar la ubicación del archivo de asignación de reescritura y se debe implementar una vez mediante la canalización de pila completa de Cloud Manager o la canalización de nivel web. El archivo debe crearse en la carpeta [src/opt-in](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype/dispatcher.cloud/src/opt-in) de la configuración de Dispatcher. Asegúrese de utilizar la [estructura de archivos de modo flexible](/help/implementing/dispatcher/validation-debug.md#flexible-mode-file-structure).

Puede configurarlo con el siguiente patrón:

```
maps:
- name: my.map
  path: <path-in-publish-repository>/redirectmap.txt
```

AEM Si, por ejemplo, el método elegido para colocar el archivo de asignación de reescritura es introducirlo como un recurso denominado `mysite-redirectmap.txt` y, a continuación, publicarlo, puede especificar una carpeta en `/content/dam`:

```
maps:
- name: my.map
  path: /content/dam/redirectmaps/mysite-redirectmap.txt
```

A continuación, en un archivo de configuración de apache como `rewrites/rewrite.rules` o `<yourfile>.vhost`, debe configurar el archivo de asignación al que hace referencia la propiedad name ( `my.map` en el ejemplo anterior).

La directiva `RewriteMap` debe indicar que los datos están almacenados en un formato de archivo de administrador de base de datos (DBM) utilizando el formato `sdbm` (DBM simple).

El resto de la configuración dependerá del formato de `redirectmap.txt`. El formato más sencillo, que se muestra en el ejemplo siguiente, es una asignación individual entre la dirección URL original y la asignada:

```
# RewriteMap from managed rewrite maps
RewriteMap map.foo dbm=sdbm:/tmp/rewrites/my.map
RewriteCond ${map.foo:$1} !=""
RewriteRule ^(.*)$ ${map.foo:$1|/} [L,R=301]
```


## Consideraciones {#considerations}

Tenga en cuenta lo siguiente:

* De forma predeterminada, al cargar un mapa de reescritura, Apache se iniciará sin esperar a que se carguen los archivos de mapa completos y, por lo tanto, puede haber incoherencias temporales hasta que se carguen los mapas completos. Esta configuración se puede cambiar para que Apache espere a que se cargue todo el contenido del mapa, pero Apache tardará más en iniciarse. Para cambiar este comportamiento para que Apache espere, agregue `wait:true` al archivo `managed-rewrite-maps.yaml`.
* Para cambiar la frecuencia entre cargas, agregue `ttl: <integer>` al archivo `managed-rewrite-maps.yaml`. Por ejemplo, `ttl: 120`.
* Apache tiene un límite de longitud de 1024 para las entradas únicas de RewriteMap.
