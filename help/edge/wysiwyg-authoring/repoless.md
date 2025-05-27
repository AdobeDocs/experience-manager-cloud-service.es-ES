---
title: Reutilización del código en varios sitios
description: Si tiene muchos sitios similares, con un aspecto y un comportamiento prácticamente idénticos, pero con contenido diferente, descubra cómo puede compartir código en varios sitios en un modelo sin repositorio.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a6bc0f35-9e76-4b5a-8747-b64e144c08c4
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '1039'
ht-degree: 100%

---

# Reutilización del código en varios sitios {#repoless}

Si tiene muchos sitios similares, con un aspecto y un comportamiento prácticamente idénticos, pero con contenido diferente, descubra cómo puede compartir código en varios sitios en un modelo sin repositorio.

## Un código base para varios sitios {#one-codebase}

De forma predeterminada, AEM está estrechamente enlazado con el repositorio de código, que cumple con la mayoría de los casos de uso. Sin embargo, es posible que tenga varios sitios que difieran principalmente en su contenido, pero que podrían aprovechar la misma base de código.

En lugar de crear varios repositorios de GitHub y ejecutar cada sitio desde un repositorio de GitHub dedicado mientras se mantienen sincronizados, AEM permite ejecutar varios sitios desde el mismo código base.

Esta configuración simplificada, que elimina la necesidad de replicar código, también se conoce como [sin repositorio](https://www.aem.live/docs/repoless), dado que no todos los sitios, excepto el primero, necesitan un repositorio GitHub propio.

Si su proyecto requiere la flexibilidad de la configuración sin repositorio para reutilizar código en distintos sitios, puede activar la función.

Independientemente de cuántos sitios desee crear en última instancia sin repositorio, debe crear el primer sitio, que sirve como sitio base. En este documento se explica cómo crear su primer sitio para el uso del modelo sin repositorio.

## Requisitos previos {#prerequisites}

Para aprovechar esta función, asegúrese de haber hecho lo siguiente.

* Su sitio ya está completamente configurado mediante el documento [Guía de introducción para desarrolladores para la creación WYSIWYG con Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Está ejecutando AEM as a Cloud Service 2024.08 como mínimo.

También deberá solicitar a Adobe que configure los siguientes elementos por usted. Póngase en contacto a través de su canal de Slack o plantee un problema de asistencia para solicitar a Adobe que realice estos cambios:

* Pida que se active el [servicio de configuración aem.live](https://www.aem.live/docs/config-service-setup#prerequisites) para su entorno y que esté configurado como administrador.
* Solicite habilitar la función sin repositorio para su programa mediante Adobe.
* Pida a Adobe que cree la organización por usted.

## Activación de la función sin repositorio {#activate}

Existen varios pasos para activar la funcionalidad sin repositorio de su proyecto.

1. [Recuperar el token de acceso](#access-token)
1. [Configurar el servicio de configuración](#config-service)
1. [Añadir la configuración del sitio y la cuenta técnica](#access-control)
1. [Actualizar la configuración de AEM](#update-aem)
1. [Autenticar el sitio](#authenticate-site)

Estos pasos utilizan el sitio `https://wknd.site` como ejemplo. Sustitúyalo por uno propio si lo considera adecuado.

### Recuperar el token de acceso {#access-token}

Primero necesitará un token de acceso para utilizar el servicio de configuración y configurarlo para el caso de uso sin repositorio.

1. Vaya a `https://admin.hlx.page/login` y utilice la dirección `login_adobe` para iniciar sesión con el proveedor de identidad de Adobe.
1. Se le reenviará a `https://admin.hlx.page/profile`.
1. Con las herramientas para desarrolladores del explorador, copie el valor de `x-auth-token` desde la cookie del token web JSON que establece la página `admin.hlx.page`.

Una vez que tenga el token de acceso, se puede pasar en el encabezado de las solicitudes cURL con el siguiente formato.

```text
--header 'x-auth-token: <your-token>'
```

### Añadir la asignación de ruta para la configuración del sitio y establecer una cuenta técnica {#access-control}

Debe crear una configuración del sitio y añadirla a la asignación de ruta.

1. Cree una nueva página en la raíz del sitio y elija la plantilla [**Configuración**](/help/edge/wysiwyg-authoring/tabular-data.md#other).
   * Puede dejar vacía la configuración con solo las columnas `key` y `value` predefinidas. Solo es necesario crearla.
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

1. Inicie sesión en la instancia de autor de AEM y vaya a **Herramientas** -> **Cloud Services** -> **Configuración de Edge Delivery Services**, seleccione la configuración que se creó automáticamente para su sitio y pulse o haga clic en **Propiedades** en la barra de herramientas.

1. En la ventana **Configuración de Edge Delivery Services**, seleccione la pestaña **Autenticación** y copie el valor del **ID técnico de la cuenta**.

   * Tendrá un aspecto similar a `<tech-account-id>@techacct.adobe.com`
   * La cuenta técnica es la misma para todos los sitios en un solo entorno de creación de AEM.

1. Establezca la cuenta técnica para su configuración sin repositorio con un comando cURL similar al siguiente, utilizando el ID de cuenta técnica que ha copiado.

   * Adapte el bloque `admin` para definir los usuarios que deben tener acceso administrativo completo al sitio.
      * Es una matriz de direcciones de correo electrónico.
      * Se puede usar el comodín `*`.
      * Consulte el documento [Configuración de la autenticación para autores](https://www.aem.live/docs/authentication-setup-authoring#default-roles) para obtener más información.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/<your-aem-project>/access.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
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
   }'
   ```

Dado que ahora utiliza el servicio de configuración, puede quitar `fstab.yaml` y `paths.json` de su repositorio Git.

>[!NOTE]
>
>Al usar el servicio de configuración y exponer la asignación de ruta de acceso mediante `config.json`, se omite el archivo `path.json`.

Una vez configurado AEM para el uso sin repositorio, debe usar el servicio de configuración y proporcionar un `config.json` válido con la asignación de rutas.

### Actualizar la configuración de AEM {#update-aem}

Ahora está listo para realizar los cambios necesarios en Edge Delivery Services en AEM.

1. Inicie sesión en la instancia de autor de AEM y vaya a **Herramientas** -> **Cloud Services** -> **Configuración de Edge Delivery Services**, seleccione la configuración que se creó automáticamente para su sitio y pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la ventana **Configuración de Edge Delivery Services**, cambie el tipo de proyecto a **aem.live con la configuración sin repositorio** y pulse o haga clic en **Guardar y cerrar**.
   ![Configuración de Edge Delivery Services](/help/edge/wysiwyg-authoring/assets/repoless/edge-delivery-services-configuration.png)
1. Vuelva al sitio mediante el editor universal y asegúrese de que sigue procesando correctamente.
1. Modifique parte del contenido y vuelva a publicarlo.
1. Visite el sitio publicado en `https://main--<your-aem-project>--<your-github-org>.aem.page/` y verifique que los cambios se reflejen correctamente.

El proyecto está configurado para el uso sin repositorio.

## Siguientes pasos {#next-steps}

Ahora que el sitio base está configurado para el uso sin repositorio, puede crear sitios adicionales que aprovechen la misma base de código. Consulte la siguiente documentación en función de su caso de uso.

* [Administración de varios sitios sin repositorio](/help/edge/wysiwyg-authoring/repoless-msm.md)
* [Entornos de ensayo y producción sin repositorio](/help/edge/wysiwyg-authoring/repoless-stage-prod.md)
* [Autenticación del sitio para la creación de contenido](/help/edge/wysiwyg-authoring/site-authentication.md)

## Solución de problemas {#troubleshooting}

El problema más común que se ha detectado después de configurar el caso de uso sin repositorio es que las páginas del editor universal ya no se procesan, o que recibe una página en blanco o un mensaje de error genérico de AEM as a Cloud Service. En ambos casos:

* Vea el origen de la página procesada.
   * ¿Se ha procesado realmente algo (encabezado HTML correcto con `scripts.js`, `aem.js` y archivos JSON relacionados con el editor)?
* Compruebe el archivo `error.log` de AEM de la instancia de autor para ver si hay excepciones.
   * El problema más común es que el componente de página falla con el error 404.
   * `config.json or paths.json` no se puede cargar
   * `component-definition.json` etc.  no se puede cargar
