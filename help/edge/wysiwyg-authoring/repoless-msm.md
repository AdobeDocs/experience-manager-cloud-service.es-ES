---
title: Administración de varios sitios sin repositorio
description: Conozca las recomendaciones de prácticas para configurar un proyecto sin repositorio con sitios localizados que aprovechen una sola base de código, cada uno servido por Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1260'
ht-degree: 100%

---

# Administración de varios sitios sin repositorio {#repoless-msm}

Conozca las recomendaciones de prácticas para configurar un proyecto sin repositorio con sitios localizados que aprovechen una sola base de código, cada uno servido por Edge Delivery Services.

## Información general {#overview}

El [Administrador de varios sitios (MSM)](/help/sites-cloud/administering/msm/overview.md) y sus funciones de Live Copy le permiten utilizar el mismo contenido del sitio en varias ubicaciones, a la vez que permiten variaciones. Puede crear contenido una vez y crear copias Live Copy. MSM mantiene relaciones activas entre su contenido de origen y sus copias Live Copy para que, al cambiar el contenido de origen, se puedan sincronizar el origen y las copias Live Copy.

Puede utilizar MSM para crear una estructura de contenido completa para su marca en diferentes configuraciones regionales e idiomas, creando el contenido de forma centralizada. A continuación, los sitios localizados se pueden enviar mediante Edge Delivery Services, aprovechando una base de código central.

## Requisitos  {#requirements}

Para configurar MSM en un caso de uso sin repositorio, primero debe completar las siguientes tareas:

* Este documento supone que ya ha creado un sitio para su proyecto basado en la [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Tiene que haber [habilitado la función sin repositorio para su proyecto](/help/edge/wysiwyg-authoring/repoless.md).

## Caso práctico {#use-case}

Este documento supone que ya ha creado una estructura de sitio localizada básica para su proyecto. Utiliza la siguiente estructura para la marca wknd, con presencia en Suiza y Alemania como ejemplo.

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

El contenido de `language-masters` es el origen de las copias Live Copy para los sitios localizados: Alemania (`de`) y Suiza (`ch`). El objetivo de este documento es crear sitios de Edge Delivery Services que utilicen la misma base de código para cada sitio localizado.

## Configuración {#configuration}

Deben realizarse varios pasos para configurar el caso de uso sin repositorio de MSM.

1. [Actualizar las configuraciones del sitio de AEM](#update-aem-configurations).
1. [Crear nuevos sitios de Edge Delivery Services para las páginas localizadas](#create-edge-sites).
1. [Actualizar la configuración de la nube en AEM para los sitios localizados](#update-cloud-configurations).

### Actualizar las configuraciones del sitio de AEM {#update-aem-configurations}

Las [configuraciones](/help/implementing/developing/introduction/configurations.md) se pueden considerar como espacios de trabajo que se pueden usar para recopilar grupos de configuraciones y su contenido asociado con fines organizativos. Al crear un sitio en AEM, se crea automáticamente una configuración para él.

Por lo general, desea compartir determinado contenido entre sitios, como, por ejemplo:

* Plantillas creadas a partir del contenido del modelo
* Modelos de fragmento de contenido, persistentes, consultas, etc.

Puede crear configuraciones adicionales para facilitar este uso compartido. En el caso de uso de wknd, se necesitan configuraciones para las siguientes rutas.

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

Es decir, tendrá una configuración para la raíz del contenido de la marca wknd (`/content/wknd`) utilizada por los modelos y una configuración utilizada por cada sitio localizado (Suiza y Alemania).

1. Inicie sesión en la instancia de creación de AEM.
1. Vaya a **Explorador de configuración** accediendo a **Herramientas** -> **General** -> **Explorador de configuración**.
1. Seleccione la configuración que se creó automáticamente para su proyecto (en este caso, wknd) y, a continuación, pulse o haga clic en **Crear** en la barra de herramientas.
1. En el cuadro de diálogo **Crear configuración**, proporcione un **Nombre** descriptivo para su sitio localizado (como `Switzerland`) y para el **Título** use el mismo título del tamaño localizado (en este caso `ch`).
1. Seleccione la función **Configuración de nube** y cualquier función adicional que pueda necesitar para su proyecto, como **Plantillas editables**.
1. Haga clic o pulse en **Crear**.

Cree configuraciones para cada sitio localizado que necesite. En el caso de wknd, necesitaría crear una configuración para `de` además de la configuración `ch`.

Una vez creadas las configuraciones, debe asegurarse de que los sitios localizados las utilicen.

1. Inicie sesión en la instancia de creación de AEM.
1. Vaya a la **Consola Sites** en **Navegación** -> **Sites**.
1. Seleccione el sitio localizado como `Switzerland`.
1. Pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la ventana de propiedades de la página, seleccione la pestaña **Avanzado** y, bajo el encabezado **Configuración**, anule la selección de la opción **Heredado de /content/wknd**, donde `wknd` es la raíz del sitio.
1. En el campo **Configuración de nube**, use el explorador de rutas para seleccionar la configuración que creó para su sitio localizado, como `Switzerland` en `/conf/wknd/ch`.
1. Haga clic o pulse en **Guardar y cerrar**.

Asigne las configuraciones respectivas a los sitios localizados adicionales. En el caso de wknd, también debería asignar la configuración `/conf/wknd/de` al sitio de Alemania.

### Crear nuevos sitios de Edge Delivery Services para las páginas localizadas {#create-edge-sites}

Para conectar más sitios a Edge Delivery Services para una configuración del sitio en varias regiones y varios idiomas, debe configurar un nuevo sitio aem.live para cada uno de los sitios MSM de AEM. Existe una relación 1:1 entre los sitios MSM de AEM y los sitios de aem.live con un repositorio de Git compartido y una base de código.

Para este ejemplo, crearemos el sitio `wknd-ch` para la presencia de Suiza de wknd, cuyo contenido localizado se encuentra en la ruta de AEM `/content/wknd/ch`.

1. Recupere el token de autenticación y la cuenta técnica para su programa.
   * Consulte el documento **Reutilización del código en varios sitios** para obtener más información sobre cómo [obtener el token de acceso](/help/edge/wysiwyg-authoring/repoless.md#access-token) y la [cuenta técnica](/help/edge/wysiwyg-authoring/repoless.md#access-control) para su programa.
1. Cree un nuevo sitio realizando la siguiente llamada al servicio de configuración. Tenga en cuenta lo siguiente:
   * El nombre del proyecto en la URL de POST debe ser el nuevo nombre del sitio que está creando. En este ejemplo, es `wknd-ch`.
   * La configuración `code` debe ser la misma que utilizó para la creación inicial del proyecto.
   * `content` > `source` > `url` debe adaptarse al nombre del nuevo sitio que está creando. En este ejemplo, es `wknd-ch`.
   * Es decir, el nombre del sitio en la URL de POST y `content` > `source` > `url` deben ser iguales.
   * Adapte el bloque `admin` para definir los usuarios que deben tener acceso administrativo completo al sitio.
      * Es una matriz de direcciones de correo electrónico.
      * Se puede usar el comodín `*`.
      * Consulte el documento [Configuración de la autenticación para autores](https://www.aem.live/docs/authentication-setup-authoring#default-roles) para obtener más información.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
           "admin": {
               "role": {
                   "admin": [
                       "<email>@<domain>.<tld>"
                   ],
                   "config_admin": [
                       "<tech-account-id>@techacct.adobe.com"
                   ]
               },
               "requireAuth": "auto"
           }
       }
   }'
   ```

1. Añada la asignación de ruta para el nuevo sitio realizando la siguiente llamada al servicio de configuración.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. Compruebe que la configuración pública del nuevo sitio funcione llamando a `https://main--wknd-ch--<your-github-org>.aem.page/config.json` y verificando el contenido del JSON devuelto.

Repita los pasos para crear sitios localizados adicionales. En el caso de wknd, también debería crear un sitio `wknd-de` para la presencia de Alemania.

### Actualización de las configuraciones de la nube en AEM para las páginas localizadas {#update-cloud-configurations}

Sus páginas de AEM deben configurarse para que utilicen los nuevos sitios de Edge Delivery que creó en la sección anterior para su presencia localizada. En este ejemplo, el contenido bajo `/content/wknd/ch` necesita saber cómo usar el sitio `wknd-ch` que creó. Del mismo modo, el contenido de `/content/wknd/de` debe utilizar el sitio `wknd-de`.

1. Inicie sesión en la instancia de autor de AEM y vaya a **Herramientas** -> **Cloud Services** -> **Configuración de Edge Delivery Services**.
1. Seleccione la configuración que se creó automáticamente para el proyecto y, a continuación, la carpeta que se creó para la página localizada. En este caso, sería Suiza (`ch`).
1. Pulse o haga clic en **Crear** > **Configuración** en la barra de herramientas.
1. En la ventana **Configuración de Edge Delivery Services**, haga lo siguiente:
   * Proporcione su organización de GitHub en el campo **Organización**.
   * Cambie el nombre del sitio por el nombre del sitio que creó en la sección anterior. En este caso, sería `wknd-ch`.
   * Cambie el tipo de proyecto a **aem.live con la configuración sin repositorio**.
1. Haga clic o pulse en **Guardar y cerrar**.

## Verifique su configuración {#verify}

Ahora que ha realizado todos los cambios de configuración necesarios, compruebe que todo funciona según lo esperado.

1. Inicie sesión en la instancia de creación de AEM.
1. Vaya a la **Consola Sites** accediendo a **Navegación** -> **Sites**.
1. Seleccione el sitio localizado como `Switzerland`.
1. Pulse o haga clic en **Editar** en la barra de herramientas.
1. Asegúrese de que la página se procese correctamente en el editor universal y utilice el mismo código que la raíz del sitio.
1. Realice un cambio en la página y vuelva a publicarla.
1. Visite su nuevo sitio de Edge Delivery Services para esa página localizada en `https://main--wknd-ch--<your-github-org>.aem.page`.

Si ve los cambios que ha realizado, es que la configuración de MSM funciona correctamente.
