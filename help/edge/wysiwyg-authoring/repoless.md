---
title: Reutilización del código en varios sitios
description: Si tiene muchos sitios similares que en su mayoría tienen el mismo aspecto y comportamiento, pero tienen contenido diferente, descubra cómo puede compartir código en varios sitios en un modelo sin respuestas.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
source-git-commit: 7b37f3d387f0200531fe12cde649b978f98d5d49
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 2%

---

# Reutilización del código en varios sitios {#repoless}

Si tiene muchos sitios similares que en su mayoría tienen el mismo aspecto y comportamiento, pero tienen contenido diferente, descubra cómo puede compartir código en varios sitios en un modelo sin respuestas.

## Un código base para varios sitios {#one-codebase}

AEM De forma predeterminada, la está estrechamente ligada al repositorio de código, que cumple con la mayoría de los casos de uso. Sin embargo, puede tener varios sitios que difieren principalmente en su contenido, pero que podrían aprovechar la misma base de código.

AEM En lugar de crear varios repositorios de GitHub y ejecutar cada sitio desde un repositorio de GitHub dedicado mientras se mantienen sincronizados, admite la ejecución de varios sitios desde el mismo código base.

Esta configuración simplificada, que elimina la necesidad de replicación de código, también se conoce como [&quot;repoless&quot;,](https://www.aem.live/docs/repoless) porque todos los sitios, excepto el primero, no necesitan un repositorio propio de GitHub.

Si el proyecto requiere la flexibilidad de reutilización de código entre sitios, puede activar la función.

Independientemente de cuántos sitios desee crear en última instancia de forma independiente, debe crear el primer sitio, que sirve como sitio base. En este documento se explica cómo crear su primer sitio para el uso de las réplicas.

## Requisitos previos {#prerequisites}

Para aprovechar esta función, asegúrese de haber hecho lo siguiente.

* Su sitio ya está completamente configurado al seguir el documento [Guía de introducción para desarrolladores de WYSIWYG Authoring con Edge Delivery Services.](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md)
* Está ejecutando AEM as a Cloud Service 2024.08 como mínimo.

También deberá pedir al Adobe que configure dos elementos por usted. Póngase en contacto con el Adobe a través del canal del Slack o plantee un problema de asistencia para realizar estas solicitudes.

* El [servicio de configuración aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) está activo para su entorno y usted se ha configurado como administrador.
* La función de reutilización debe habilitarse para su programa por Adobe.

## Activar función de reutilización {#activate}

Existen varios pasos para activar la funcionalidad de reutilización en su proyecto.

1. [Recuperar token de acceso](#access-token)
1. [Configurar el servicio de configuración](#config-service)
1. [Agregar configuración de sitio y cuenta técnica](#access-control)
1. [AEM Actualizar configuración de la](#update-aem)
1. [Autenticar sitio](#authenticate-site)

Estos pasos utilizan el sitio `https://wknd.site` como ejemplo. Sustituye a los tuyos adecuadamente.

### Recuperar token de acceso {#access-token}

Primero necesitará un token de acceso para utilizar el servicio de configuración y configurarlo para el caso de uso de reinicios.

1. Vaya a `https://admin.hlx.page/login` y use la dirección `login_adobe` para iniciar sesión con el proveedor de identidad de Adobe.
1. Se le reenviará a `https://admin.hlx.page/profile`.
1. Con las herramientas para desarrolladores del explorador, copie el valor de `x-auth-token` desde la cookie de token web JSON que establece la página `admin.hlx.page`.

Una vez que tenga el token de acceso, se puede pasar en el encabezado de las solicitudes cURL con el siguiente formato.

```text
--header 'x-auth-token: <your-token>'
```

### Configurar el servicio de configuración {#config-service}

Como se menciona en los [requisitos previos,](#prerequisites) el servicio de configuración debe estar habilitado para su entorno. Puede comprobar la configuración del servicio de configuración con este comando cURL.

```text
curl  --location 'https://admin.hlx.page/config/<your-github-org>.json' \
--header 'x-auth-token: <your-token>'
```

Si el servicio de configuración está configurado correctamente, se devolverá un archivo JSON similar al siguiente.

```json
{
  "title": "<your-github-org>",
  "description": "Your GitHub Org",
  "lastModified": "2024-11-14T12:14:04.230Z",
  "created": "2024-11-14T12:13:37.032Z",
  "version": 1,
  "users": [
    {
      "email": "justthisguyyouknow@adobe.com",
      "roles": [
        "admin"
      ],
      "id": "<your-id>"
    }
  ]
}
```

Póngase en contacto con el Adobe a través del canal del Slack del proyecto o genere un problema de asistencia si el servicio de configuración no está habilitado. Una vez que tenga el token y haya comprobado que el servicio de configuración está habilitado, puede continuar con la configuración.

1. Compruebe que el origen de contenido esté configurado correctamente.

   ```text
   curl --request GET \
   --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>.json \
   --header 'x-auth-token: <your-token>'
   ```

1. Agregue una asignación de ruta a la configuración pública.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```

Una vez creada la configuración pública, puede acceder a ella a través de una dirección URL similar a `https://main--<your-aem-project>--<your-github-org>.aem.page/config.json` para verificarla.

### Agregar asignación de ruta para configuración de sitio y establecer cuenta técnica {#access-control}

Debe crear una configuración de sitio y agregarla a la asignación de ruta.

1. Cree una nueva página en la raíz del sitio y elija la plantilla [**Configuración**.](/help/edge/wysiwyg-authoring/tabular-data.md#other)
   * Puede dejar vacía la configuración con solo las columnas predefinidas `key` y `value`. Solo es necesario crearlo.
1. Cree una asignación en la configuración pública a la configuración del sitio mediante un comando cURL similar al siguiente.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/public.json \
     --header 'x-auth-token: <your-token>' \
     --header 'Content-Type: application/json' \
     --data '{
       "paths": {
           "mappings": [
               "/content/<your-site-content>/:/",
               "/content/<your-site-content>/configuration:/.helix/config.json"
      ],
           "includes": [
               "/content/<your-site-content>/"
           ]
       }
   }'
   ```
1. Compruebe que la configuración pública se haya establecido y que esté disponible con un comando cURL similar al siguiente.

   ```text
   curl 'https://main--<your-aem-project>--<your-github-org>.aem.live/config.json'
   ```

Una vez asignada la configuración del sitio, puede configurar el control de acceso definiendo la cuenta técnica para que tenga privilegios de publicación.

1. En su explorador, recupere la cuenta técnica en la respuesta del siguiente vínculo.

   ```text
   https://author-p<programID>-e<envionmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/<your-aem-project>/main/.helix/config.json
   ```

1. La respuesta será similar a la siguiente.

   ```json
   {
     "total": 1,
     "offset": 0,
     "limit": 1,
     "data": [
       {
         "key": "admin.role.publish",
         "value": "<tech-account-id>@techacct.adobe.com"
       }
     ],
     ":type": "sheet"
   }
   ```

1. Establezca la cuenta técnica en la configuración con un comando cURL similar al siguiente.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "admin": {
           "role": {
               "admin": [
                   "*@adobe.com"
               ],
               "config_admin": [
                   "<tech-account-id>@techacct.adobe.com"
               ]
           },
           "requireAuth": "auto"
       }
   }'
   ```

Dado que ahora utiliza el servicio de configuración, puede quitar `fstab.yaml` y `paths.json` de su repositorio Git.

>[!NOTE]
>
>Al usar el servicio de configuración y exponer la asignación de ruta de acceso mediante `config.json`, se omite el archivo `path.json`.

AEM Una vez configurado el servicio de configuración para el uso de repoless, debe usar y proporcionar un `config.json` válido con la asignación de rutas de acceso.

### AEM Actualizar configuración de la {#update-aem}

Ahora está listo para realizar los cambios necesarios en los Edge Delivery Services AEM de la aplicación en la.

1. AEM Inicie sesión en la instancia de autor de la y vaya a **Herramientas** -> **Cloud Service** -> **Configuración de Edge Delivery Services**, seleccione la configuración que se creó automáticamente para su sitio y toque o haga clic en **Propiedades** en la barra de herramientas.
1. En la ventana **Configuración de Edge Delivery Services**, cambie el tipo de proyecto a **aem.live con la configuración de repoless** y toque o haga clic en **Guardar y cerrar**.
   ![Configuración de Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Vuelva al sitio mediante el Editor universal y asegúrese de que aún se procesa correctamente.
1. Modifique parte del contenido y vuelva a publicarlo.
1. Visite el sitio publicado en `https://main--<your-aem-project>--<your-github-org>.aem.page/` y verifique que los cambios se reflejen correctamente.

El proyecto está configurado para su uso sin reposo.

## Siguientes pasos {#next-steps}

Ahora que el sitio base está configurado para el uso de reinicios, puede crear sitios adicionales que aprovechen la misma base de código. Consulte la siguiente documentación en función de su caso de uso.

* [Administración de varios sitios sin repositorio](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Entornos de ensayo y producción sin repositorio](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)

## Solución de problemas {#troubleshooting}

El problema más común que se ha encontrado después de configurar el caso de uso de las réplicas es que las páginas del editor universal ya no se representan, o que recibe una página en blanco o un mensaje de error genérico de AEM as a Cloud Service. En tales casos:

* Ver el origen de la página representada.
   * ¿Se ha procesado realmente algo (encabezado de HTML correcto con `scripts.js`, `aem.js` y archivos JSON relacionados con el editor)?
* AEM Compruebe las excepciones en el recurso `error.log` de la instancia de autor.
   * El problema más común es que el componente de página falla con errores 404.
   * `config.json or paths.json` no se puede cargar
   * `component-definition.json`, etc. no se puede cargar
