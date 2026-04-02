---
title: Administración de sitios de Edge Delivery en Cloud Manager
description: Obtenga información sobre cómo añadir una configuración de CDN a un sitio de Edge Delivery o eliminar un sitio de Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: fc9f7f10d1797bda5f31d82005b0afbb6ea1e644
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 64%

---

# Administración de un sitio de Edge Delivery en Cloud Manager {#manage-edge-delivery-sites}

Obtenga información sobre cómo administrar sitios de Edge Delivery en Cloud Manager añadiendo una configuración de CDN a un sitio existente. O bien, elimine un sitio de Edge Delivery.

## Añadir una asignación de dominio a un sitio de Edge Delivery existente {#add-cdn-to-edge-delivery-site}

Consulte [Añadir una asignación de dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Cambiar el nombre de un sitio de Edge Delivery (#rename-edge-delivery-site)

En Adobe Cloud Manager, puede cambiar el nombre de un sitio de Edge Delivery por varios motivos:

* **Claridad y organización**: para describir mejor el propósito del sitio o su entorno asociado (por ejemplo, producción o ensayo).
* **Evitar confusiones**: si se usan varios sitios, cambiar el nombre puede ayudar a diferenciarlos fácilmente, lo que reduce la posibilidad de aplicar configuraciones o actualizaciones al sitio incorrecto.
* **Estandarización**: seguir una convención de nomenclatura coherente que se ajuste a las directrices de su organización para facilitar la administración y la auditoría.

**Para cambiar el nombre de un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado donde desee añadir un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee cambiar de nombre.
Haga clic en **Cambiar nombre**.
   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda. Bajo el encabezado **Servicios**, haga clic en el ![icono de páginas web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) de **Sitios de Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee cambiar de nombre. Haga clic en **Cambiar nombre**.

1. En el cuadro de diálogo **Editar sitio de Edge Delivery**, en el campo de texto **Nombre del sitio**, escriba el nuevo nombre del sitio.
1. Haga clic en **Editar**.


## Activación del nivel de publicación para un sitio de Edge Delivery (Beta) {#activate-publish-tier-for-eds}

>[!NOTE]
>
>La función de publicación que se describe aquí está en Beta. Para unirte a Beta, envía un correo electrónico a [grp-beta_xwalk-publish_config@adobe.com](mailto:grp-beta_xwalk-publish_config@adobe.com) con tu ID de organización de Adobe y tu ID de programa.

Esta capacidad se aplica solamente a los sitios de Edge Delivery creados con la opción **AEM Authoring** en Programas en los que la característica de nivel de publicación flexible está habilitada.

Si el sitio de Edge Delivery utiliza la creación de AEM, el nivel de publicación no se aprovisiona de forma predeterminada porque Edge Delivery administra la entrega de contenido. Sin embargo, puede activar el nivel de publicación en cualquier momento si el sitio lo requiere. Por ejemplo, si necesita admitir la publicación tradicional de AEM junto con Edge Delivery.

Una vez creado el sitio de Edge Delivery y que su estado muestre **Comprobado** en Cloud Manager, podrá crear y publicar contenido con el Editor universal de AEM.

**Para tener acceso al Editor universal desde Cloud Manager:**

1. En la ficha Edge Delivery, en la lista Sitios de Edge Delivery, busque el sitio.

   ![Publicando contenido de AEM Author en Edge Delivery.](/help/implementing/cloud-manager/edge-delivery/assets/eds-content-source-link.png)

1. Haga clic en el vínculo **Source de contenido** en la fila del sitio. El vínculo abre la página Editor universal de AEM, desde la cual puede crear y editar contenido para el sitio.—>

**Para activar el nivel de publicación para un sitio de Edge Delivery:**

1. En la página **Información general del programa**, en la ficha **Publicar entrega**, en la tarjeta **Entorno**, haga clic en el icono Información.

1. En la ventana emergente informativa, en **URL de publicación**, seleccione **Haga clic para activar** y habilitar el aprovisionamiento del nivel de publicación en la interfaz de usuario de Cloud Manager.

   ![Haga clic para activar el aprovisionamiento del nivel de publicación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/click-to-activate-publish-tier-capabilities.png)

1. En el cuadro de diálogo Activar nivel de publicación, haga clic en **Activar**.

   ![Activar cuadro de diálogo Publicar nivel](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/activate-publish-tier.png)

   Una vez activado, el nivel de publicación se aprovisiona automáticamente. Como alternativa, el nivel de publicación se puede aprovisionar automáticamente si el autor intenta publicar contenido directamente desde la interfaz de usuario de AEM.

   Una vez que el nivel de publicación se ha activado y aprovisionado correctamente, el vínculo **Haga clic para activar** se atenúa o no está disponible.

* **De AEM Author**: en la interfaz de creación de AEM, haga clic en **Publicación rápida** para publicar contenido directamente en el sitio de Edge Delivery. El nivel de publicación no es necesario para esta operación cuando Edge Delivery administra la entrega.

Después de la publicación, obtiene una vista previa del contenido en la dirección URL `.page` del sitio o visualícelo en directo en la dirección URL `.live`.—>

>[!NOTE]
>
>Al activar el nivel de publicación, se añade la infraestructura de publicación al entorno. Esta funcionalidad puede afectar al consumo de recursos del programa. Para saber si el nivel de publicación es necesario en el nivel de programa, consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).


## Eliminar un sitio de Edge Delivery {#delete-edge-delivery-site}

Si elimina un sitio de Edge Delivery Services, también se eliminarán todas las configuraciones de CDN asociadas. Esta acción interrumpe la conexión entre los dominios personalizados y el sitio. Para obtener más información, consulte Configuraciones de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para eliminar un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado donde desee añadir un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en el icono ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee quitar. Haga clic en el ![icono Eliminar sitio Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Eliminar** y, a continuación, vuelva a hacer clic en **Eliminar** para confirmar la eliminación del sitio.

     ![Añadir sitio de Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda. Bajo el encabezado **Servicios**, haga clic en el icono ![Página web de los sitios de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios de Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en el icono ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee quitar. Haga clic en el ![icono Eliminar sitio de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Eliminar** y, a continuación, vuelva a hacer clic en **Eliminar** para confirmar la eliminación del sitio.

     ![Añadir el sitio de Edge Delivery desde el botón Sitios de Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Administración de un sitio de Edge Delivery entre Helix 4 y Helix 5

Utilice el punto final de la API `/program/{programId}/site/{siteId}` para migrar un sitio de Edge Delivery entre Helix 4 y Helix 5.

>[!IMPORTANT]
>
>Las configuraciones de CDN para sitios web Helix 4 no se pueden migrar a Helix 5 automáticamente. Esta limitación existe porque los sitios de producción de clientes pueden seguir ejecutándose en Helix 4, mientras que sus versiones de Helix 5 aún están en desarrollo.

**Requisitos previos**

* El `sitename` debe existir previamente.
* Conocer los valores apropiados de `branchName`, Helix `version` y `repo`.
* La migración solo modifica `branchName`, Helix `version` y `repo`. El campo Contraseña no se puede cambiar.

**Formato de API**

```http
PUT /api/program/{programId}/site/{siteId}
```

**Parámetros del cuerpo de solicitud**
Crea una anulación para un sitio de Edge Delivery para aplicar el origen especificado en el cuerpo de la solicitud.

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### Ejemplo 1: Migrar a Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**Resultado de URL de origen**
Devuelve un sitio de Edge Delivery con la siguiente dirección URL de origen:

`"origin": "branch--my-website–Teo48.aem.live"`


### Ejemplo 2: Migrar a Helix 4

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**Resultado de URL de origen**
Devuelve un sitio de Edge Delivery con la siguiente dirección URL de origen:

`"origin": "branch--my-website--Teo48.hlx.live"`

### Ejemplo 3: Migrar el sitio sin repositorio a Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**Resultado de URL de origen**
Devuelve un sitio de Edge Delivery con la siguiente dirección URL de origen:

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## Registro de un vale de asistencia {#eds-support-ticket}

{{support-ticket}}
