---
title: Uso de recursos conectados para compartir recursos DAM en [!DNL Sites]
description: Usar recursos disponibles en un remoto [!DNL Adobe Experience Manager Assets] implementación al crear sus páginas web en otro [!DNL Adobe Experience Manager Sites] implementación.
contentOwner: AK
mini-toc-levels: 2
feature: Asset Management,Connected Assets,Asset Distribution,User and Groups
role: Admin,User,Architect
exl-id: 2346f72d-a383-4202-849e-c5a91634617a
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '3842'
ht-degree: 13%

---


# Uso de recursos conectados para compartir recursos DAM en [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html) |
| AEM as a Cloud Service | Este artículo |

En las grandes empresas se puede distribuir la infraestructura necesaria para crear sitios web. A veces, las capacidades de creación de sitios web y los recursos digitales utilizados para crear estos sitios web se pueden encontrar en diferentes implementaciones. Una razón puede ser la distribución geográfica de implementaciones existentes que son necesarias para trabajar juntas. Otra razón pueden ser las adquisiciones que conducen a una infraestructura heterogénea, incluidas diferentes [!DNL Experience Manager] versiones, que la compañía principal desea utilizar juntas.

La funcionalidad Recursos conectados admite los casos de uso anteriores mediante la integración de [!DNL Experience Manager Sites] y [!DNL Experience Manager Assets]. Los usuarios pueden crear páginas web en [!DNL Sites] que utilizan los recursos digitales de un [!DNL Assets] implementaciones.

>[!NOTE]
>
>Configure los recursos de red solo cuando necesite utilizar los recursos disponibles en una implementación remota de DAM en una implementación independiente de Sites para crear páginas web.

## Información general sobre los recursos conectados {#overview-of-connected-assets}

Al editar páginas en [!UICONTROL Editor de página] como destino de destino, los creadores pueden buscar, examinar e incrustar recursos sin problemas desde un entorno diferente [!DNL Assets] implementación que actúa como origen de recursos. Los administradores crean una integración única de una implementación de [!DNL Experience Manager] con [!DNL Sites] con otra implementación de [!DNL Experience Manager] con [!DNL Assets] capacidad. También puede utilizar imágenes de Dynamic Media en las páginas web del sitio a través de Recursos conectados y utilizar las funcionalidades de Dynamic Media, como los ajustes preestablecidos de recorte inteligente y de imagen.

Para el [!DNL Sites] Para los creadores, los recursos remotos están disponibles como recursos locales de solo lectura. La funcionalidad admite la búsqueda y el acceso ininterrumpidos a recursos remotos en el Editor del sitio. Para cualquier otro caso de uso que requiera que el cuerpo de recursos completo esté disponible en Sites, considere migrar los recursos de forma masiva en lugar de utilizar Recursos conectados.

### Requisitos previos e implementaciones admitidas {#prerequisites}

Antes de usar o configurar esta capacidad, asegúrese de lo siguiente:

* Los usuarios forman parte de los grupos correspondientes en cada implementación.
* Para [!DNL Adobe Experience Manager] tipos de implementación, se cumple uno de los criterios admitidos. [!DNL Experience Manager] as a Cloud Service [!DNL Assets] funciona con [!DNL Experience Manager] 6.5. Para obtener más información sobre cómo funciona esta funcionalidad en [!DNL Experience Manager] 6.5, véase [Recursos conectados en [!DNL Experience Manager] 6,5 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/use-assets-across-connected-assets-instances.html).

  | | [!DNL Sites] as a [!DNL Cloud Service] | [!DNL Experience Manager] 6,5 [!DNL Sites] en AMS | [!DNL Experience Manager] 6,5 [!DNL Sites] on-premise |
  |---|---|---|---|
  | **[!DNL Experience Manager Assets]as a[!DNL Cloud Service]** | Compatible | Compatible | Compatible  |
  | **[!DNL Experience Manager]6,5 [!DNL Assets] en AMS** | Compatible | Compatible | Compatible  |
  | **[!DNL Experience Manager]6,5 [!DNL Assets] on-premise** | No compatible | No compatible | No compatible |

### Formatos de archivo compatibles {#mimetypes}

Los autores buscan imágenes y los siguientes tipos de documentos en el buscador de contenido y arrastran los recursos buscados en el editor de páginas. Los documentos se agregan a `Download` componentes e imágenes a `Image` componente. Los creadores también pueden agregar recursos remotos en cualquier [!DNL Experience Manager] componente que amplía el valor predeterminado `Download` o `Image` componentes. Los formatos admitidos son:

* **Formatos de imagen**: Los formatos que el [Componente de imagen](file-format-support.md#image-formats) admite.
* **Formatos de documento**: Consulte la [formatos de documento admitidos](file-format-support.md#document-formats).

### Usuarios y grupos implicados {#users-and-groups-involved}

A continuación se describen las distintas funciones que se deben configurar, la capacidad y sus grupos de usuarios correspondientes. El ámbito local se utiliza para el caso de uso en el que un autor crea una página web. El ámbito remoto se utiliza para la implementación de DAM que aloja los recursos necesarios. El [!DNL Sites] El creador recupera estos recursos remotos.

| Función | Ámbito | Grupo de usuarios | Descripciones |
|------|--------|-----------|----------|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | Configuración de [!DNL Experience Manager] y configurar la integración con el remoto [!DNL Assets] implementación. |
| Usuario DAM | Local | `Authors` | Se utiliza para ver y duplicar los recursos recuperados en `/content/DAM/connectedassets/`. |
| [!DNL Sites] autor | Local | <ul><li>`Authors` (con acceso de lectura en el DAM remoto y acceso de autor en el local) [!DNL Sites]) </li> <li>`dam-users` en local [!DNL Sites]</li></ul> | Los usuarios finales son [!DNL Sites] autores que utilizan esta integración para mejorar la velocidad de contenido. Los creadores pueden buscar y examinar recursos en el DAM remoto mediante [!UICONTROL Buscador de contenido] y utilizando las imágenes necesarias en las páginas web locales. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | Configurar el intercambio de recursos de origen cruzado (CORS). |
| Usuario DAM | Remoto | `Authors` | Función de autor en el remoto [!DNL Experience Manager] implementación. Busque y examine recursos en recursos conectados utilizando [!UICONTROL Buscador de contenido]. |
| Distribuidor DAM (usuario técnico) | Remoto | <ul> <li> [!DNL Sites] `Authors`</li> <li> `connectedassets-assets-techaccts` </li> </ul> | Este usuario presente en la implementación remota lo utiliza [!DNL Experience Manager] servidor local (no el [!DNL Sites] función de autor) para recuperar los recursos remotos, en nombre de [!DNL Sites] autor. |
| [!DNL Sites] usuario técnico | Local | `connectedassets-sites-techaccts` | Permite [!DNL Assets] implementación para buscar referencias a recursos en [!DNL Sites] páginas web. |

### Arquitectura de recursos conectados {#connected-assets-architecture}

Experience Manager permite conectar una implementación remota de DAM como origen a varios Experience Manager [!DNL Sites] implementaciones. Sin embargo, puede conectar un [!DNL Sites] implementación con solo una implementación remota de DAM.

Evalúe la cantidad óptima de instancias de Sites para conectarse a una implementación remota de DAM. El Adobe recomienda conectar gradualmente las instancias de Sites a la implementación y probar que no hay ningún impacto en el rendimiento en el DAM remoto, ya que cada instancia de Sites conectada contribuye al tráfico de datos en el DAM remoto.

Los siguientes diagramas ilustran los escenarios admitidos:

![Arquitectura de recursos conectados](assets/connected-assets-architecture.png)

El diagrama siguiente ilustra un escenario no compatible:

![Arquitectura de recursos conectados](assets/connected-assets-architecture-unsupported.png)

## Configuración de una conexión entre [!DNL Sites] y [!DNL Assets] implementaciones {#configure-a-connection-between-sites-and-assets-deployments}

Un [!DNL Experience Manager] El administrador puede crear esta integración. Una vez creada, los permisos necesarios para utilizarla se establecen mediante grupos de usuarios. Los grupos de usuarios se definen en la [!DNL Sites] y en la implementación de DAM.

Para configurar los recursos de red y locales [!DNL Sites] conectividad, siga estos pasos:

1. Acceder a un existente [!DNL Sites] implementación. Esta [!DNL Sites] La implementación de se utiliza para la creación de páginas web, por ejemplo, en `https://<sites_server_fqdn>:[port]`. A medida que la creación de páginas se produce en [!DNL Sites] implementación, llamemos a la [!DNL Sites] implementación como local desde la perspectiva de creación de páginas.

1. Acceder a un existente [!DNL Assets] implementación. Esta [!DNL Assets] la implementación se utiliza para administrar recursos digitales, como en `https://[assets_servername]:port`.

1. Asegúrese de que los usuarios y las funciones con el ámbito adecuado existan en la [!DNL Sites] implementación de y en [!DNL Assets] implementación en AMS. Creación de un usuario técnico en [!DNL Assets] implementación y adición al grupo de usuarios mencionado en [usuarios y grupos implicados](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acceso al local [!DNL Sites] implementación en `https://[sites_servername]:port`. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Configuración de recursos conectados]** y proporcione los siguientes valores:

   1. A **[!UICONTROL Título]** de la configuración.
   1. **[!UICONTROL URL de DAM remoto]** es la dirección URL del [!DNL Assets] ubicación con el formato `https://[assets_servername]:[port]`.
   1. Credenciales de un distribuidor DAM (usuario técnico).
   1. En el **[!UICONTROL Punto de montaje]** , introduzca el local [!DNL Experience Manager] ruta donde [!DNL Experience Manager] recupera los recursos. Por ejemplo, `connectedassets` carpeta. Los recursos que se recuperan de DAM se almacenan en esta carpeta en el [!DNL Sites] implementación.
   1. **[!UICONTROL URL de sitios locales]** es la ubicación del [!DNL Sites] implementación. [!DNL Assets] la implementación utiliza este valor para mantener las referencias a los recursos digitales recuperados por esta [!DNL Sites] implementación.
   1. Credenciales de [!DNL Sites] usuario técnico.
   1. El valor de **[!UICONTROL Umbral de optimización de la transferencia binaria original]** el campo especifica si los recursos originales (incluidas las representaciones) se transfieren sincrónicamente o no. Los recursos con un tamaño de archivo más pequeño se pueden recuperar fácilmente, mientras que los recursos con un tamaño de archivo relativamente mayor se sincronizan mejor de forma asíncrona. El valor depende de las capacidades de red.
   1. Seleccionar **[!UICONTROL Almacén de datos compartido con recursos conectados]**, si utiliza un almacén de datos para almacenar los recursos y este se comparte entre ambas implementaciones. En este caso, el límite de umbral no importa, ya que los binarios de recursos reales están disponibles en el almacén de datos y no se transfieren.

   ![Una configuración típica para la funcionalidad Recursos conectados](assets/connected-assets-typical-config.png)

   *Imagen: una configuración típica para la funcionalidad Recursos conectados.*

1. Los recursos digitales existentes en [!DNL Assets] Las implementaciones de ya se han procesado y se han generado las representaciones. Estas representaciones se recuperan mediante esta funcionalidad, por lo que no es necesario regenerarlas. Deshabilite los iniciadores del flujo de trabajo para evitar la regeneración de representaciones. Ajuste las configuraciones del lanzador en ([!DNL Sites]) implementación para excluir el `connectedassets` carpeta (los recursos se recuperan en esta carpeta).

   1. Activado [!DNL Sites] implementación, haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Lanzadores]**.

   1. Busque iniciadores con flujos de trabajo como **[!UICONTROL Recurso de actualización DAM]** y **[!UICONTROL Reescritura de metadatos DAM]**.

   1. Seleccione el lanzador del flujo de trabajo y haga clic en **[!UICONTROL Propiedades]** en la barra de acciones.

   1. En el [!UICONTROL Propiedades] asistente, cambie el **[!UICONTROL Ruta]** como las asignaciones siguientes para actualizar sus expresiones regulares y excluir el punto de montaje **[!UICONTROL connectedassets]**.

   | Antes | Después |
   | ------ | ------------ |
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas las representaciones disponibles en la implementación remota se recuperan cuando los autores recuperan un recurso. Si desea crear más representaciones de un recurso recuperado, omita este paso de configuración. El [!UICONTROL Recurso de actualización DAM] el flujo de trabajo se activa y crea más representaciones. Estas representaciones solo están disponibles en la versión local de [!DNL Sites] y no en la implementación remota de DAM.

1. Añada el [!DNL Sites] implementación como origen permitido en la configuración CORS en la [!DNL Assets] implementación. Para obtener más información, consulte [comprender CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html).

1. Configurar [compatibilidad con cookies del mismo sitio](/help/security/same-site-cookie-support.md).

Puede comprobar la conectividad entre los [!DNL Sites] implementaciones y [!DNL Assets] implementación.

![Prueba de conexión de los recursos de red configurados [!DNL Sites]](assets/connected-assets-multiple-config.png)
*Figura: Prueba de conexión de los recursos conectados configurados [!DNL Sites].*

<!-- TBD: Check if Launchers are to be disabled on CS instances. Is this option even available to the users on CS? -->

## Uso de recursos de Dynamic Media {#dynamic-media-assets}


Con Recursos conectados, puede utilizar recursos de imagen procesados por [!DNL Dynamic Media] desde la implementación remota de DAM en páginas de Sites y utilice las funcionalidades de Dynamic Media, como los ajustes preestablecidos de recorte inteligente y de imagen.

Para usar [!DNL Dynamic Media] con recursos conectados:

1. Configurar [!DNL Dynamic Media] en la implementación remota de DAM con el modo de sincronización habilitado.
1. Configurar [Recursos conectados](#configure-a-connection-between-sites-and-assets-deployments).
1. Configurar [!DNL Dynamic Media] en la instancia de Sites con el mismo nombre de empresa que se configuró en el DAM remoto. La implementación de Sites debe tener acceso de solo lectura a la cuenta de Dynamic Media para trabajar con recursos conectados. Por lo tanto, asegúrese de deshabilitar el modo de sincronización en la configuración de Dynamic Media en la instancia de Sites.

>[!CAUTION]
>
>Con recursos conectados y [!DNL Dynamic Media] , no puede utilizar [!DNL Dynamic Media] para procesar los recursos locales disponibles en [!DNL Sites] implementación.

## Configuración de [!DNL Dynamic Media] {#configure-dynamic-media}

Para configurar [!DNL Dynamic Media] el [!DNL Assets] y [!DNL Sites] implementaciones:

1. Cree la configuración de Recursos conectados como se ha descrito anteriormente, excepto cuando configure la funcionalidad, seleccione **[!UICONTROL Recuperar la representación original de los recursos conectados de Dynamic Media]** opción.

1. Configurar [!DNL Dynamic Media] en local [!DNL Sites] y remoto [!DNL Assets] implementaciones. Siga las instrucciones de [configurar [!DNL Dynamic Media]](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).

   * Utilice el mismo nombre de empresa en todas las configuraciones.
   * En local [!DNL Sites], en [!UICONTROL Modo de sincronización de Dynamic Media], seleccione **[!UICONTROL Deshabilitado de forma predeterminada]**. El [!DNL Sites] la implementación debe tener acceso de solo lectura a [!DNL Dynamic Media] cuenta.
   * En local [!DNL Sites], en el **[!UICONTROL Publicar recursos]** , seleccione **[!UICONTROL Publicación selectiva]**. No seleccionar **[!UICONTROL Sincronizar todo el contenido]**.
   * En remoto [!DNL Assets] implementación, en [!UICONTROL Modo de sincronización de Dynamic Media], seleccione **[!UICONTROL Habilitado de forma predeterminada]**.

1. Activar [[!DNL Dynamic Media] compatibilidad en el componente principal de imagen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/image.html#dynamic-media). Esta función habilita el valor predeterminado [Componente de imagen](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/image.html) para mostrar [!DNL Dynamic Media] imágenes cuando [!DNL Dynamic Media] los autores utilizan las imágenes en páginas web en [!DNL Sites] implementación.

## Usar recursos remotos {#use-remote-assets}

Los creadores del sitio web utilizan el buscador de contenido para conectarse a la implementación de DAM. Los autores pueden examinar, buscar y arrastrar los recursos remotos de un componente. Para autenticarse en el DAM remoto, conserve las credenciales proporcionadas por el administrador (si las hay).

Los creadores pueden utilizar los recursos disponibles en la implementación local de DAM y la implementación remota de DAM en una sola página web. Utilice el buscador de contenido para decidir si buscar en el DAM local o en el DAM remoto.

Solo se buscan las etiquetas de recursos remotos que tienen una etiqueta correspondiente exacta junto con la misma jerarquía de taxonomía, disponibles en el [!DNL Sites] implementación. Todas las demás etiquetas se descartan. Los creadores pueden buscar recursos remotos utilizando todas las etiquetas presentes en el recurso remoto [!DNL Experience Manager] , ya que ofrece una búsqueda de texto completo.

### Introducción al uso {#walk-through-of-usage}

Utilice la configuración anterior para probar la experiencia de creación y comprender cómo se utiliza la funcionalidad. Utilice documentos o imágenes de su elección en la implementación remota de DAM.

1. Vaya a [!DNL Assets] en la implementación remota accediendo a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]** de [!DNL Experience Manager] workspace. También puede acceder a `https://[assets_servername_ams]:[port]/assets.html/content/dam` en un explorador. Cargue los recursos que desee.

1. En el [!DNL Sites] implementación, en el activador de perfil en la esquina superior derecha, haga clic en **[!UICONTROL Suplantar como]**. Especifique el nombre de usuario, seleccione la opción proporcionada y haga clic en **[!UICONTROL OK]**.

1. Abra un [!DNL Sites] y editar la página.

   Haga clic en **[!UICONTROL Alternar panel lateral]** en la esquina superior izquierda de la página.

1. Abra el [!UICONTROL Assets] (Buscador de contenido remoto) y haga clic en **[!UICONTROL Inicie sesión en los recursos de red]**.

1. Especifique las credenciales para iniciar sesión en los recursos de red. Este usuario tiene permisos de creación en ambos [!DNL Experience Manager] implementaciones.

1. Busque el recurso que agregó a DAM. Los recursos remotos se muestran en el panel izquierdo. Filtre por imágenes o documentos y por tipos de documentos compatibles. Arrastre las imágenes a un componente `Image` y los documentos a un componente `Download`.

   Los recursos recuperados son de solo lectura en el [!DNL Sites] implementación. Puede seguir utilizando las opciones proporcionadas por su [!DNL Sites] componentes para editar el recurso recuperado. La edición por componentes no es destructiva.

   ![Opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Imagen: opciones para filtrar tipos de documentos e imágenes al buscar recursos en DAM remoto.*

1. Se notifica al creador del sitio si el original de un recurso se recupera de forma asíncrona y si falla alguna tarea de recuperación. Durante la creación o incluso después de esta, los autores pueden ver información detallada sobre las tareas de recuperación y los errores en la [trabajos asincrónicos](/help/operations/asynchronous-jobs.md) interfaz de usuario.

   ![Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: Notificación sobre la captura asincrónica de recursos que se produce en segundo plano.*

1. Al publicar una página, [!DNL Experience Manager] muestra una lista completa de los recursos que se utilizan en la página. Asegúrese de que los recursos remotos se recuperan correctamente en el momento de la publicación. Para comprobar el estado de cada recurso recuperado, consulte [trabajos asincrónicos](/help/operations/asynchronous-jobs.md) interfaz de usuario.

   >[!NOTE]
   >
   >Aunque uno o varios recursos remotos no se recuperen completamente, la página se publicará. El [!DNL Experience Manager] el área de notificación muestra una notificación de los errores que se muestran en la página trabajos asincrónicos.

>[!CAUTION]
>
>Una vez que se utilizan en una página web, cualquier persona que tenga permiso para acceder a la carpeta local puede acceder y utilizar los recursos remotos recuperados. Los recursos recuperados se almacenan en la carpeta local (`connectedassets` en el recorrido anterior). Los recursos también se pueden buscar y ver en el repositorio local mediante [!UICONTROL Buscador de contenido].

Los recursos recuperados se pueden usar como cualquier otro recurso local, pero los metadatos asociados no se pueden editar.

### Comprobar el uso de un recurso en todas las páginas web {#asset-usage-references}

[!DNL Experience Manager] permite a los usuarios de DAM comprobar todas las referencias a un recurso. Ayuda a comprender y administrar el uso de un recurso en remoto [!DNL Sites] y en activos compuestos. Muchos autores de páginas web en [!DNL Experience Manager Sites] la implementación puede utilizar un recurso en un DAM remoto en diferentes páginas web. Para simplificar la administración de recursos y no provocar referencias rotas, es importante que los usuarios de DAM comprueben el uso de un recurso en páginas web locales y remotas. El [!UICONTROL Referencias] pestaña en la carpeta de un recurso [!UICONTROL Propiedades] Esta página enumera las referencias locales y remotas del recurso.

Para ver y administrar referencias en [!DNL Assets] implementación, siga estos pasos:

1. Seleccione un recurso en [!DNL Assets] Consola y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. Clic **[!UICONTROL Referencias]** pestaña. Consulte **[!UICONTROL Referencias locales]** para el uso del recurso en [!DNL Assets] implementación. Consulte **[!UICONTROL Referencias remotas] para el uso del recurso en [!DNL Sites] implementación en la que se recuperó el recurso mediante la funcionalidad Recursos conectados.

   ![Referencias remotas en la página Propiedades del recurso](assets/connected-assets-remote-reference.png)

1. Las referencias para [!DNL Sites] las páginas muestran el recuento total de referencias para cada local [!DNL Sites]. Puede llevar algún tiempo encontrar todas las referencias y mostrar el número total de referencias.
1. La lista de referencias es interactiva y los usuarios de DAM pueden hacer clic en una referencia para abrir la página de referencia. Si por algún motivo no se pueden recuperar las referencias remotas, se muestra una notificación que informa al usuario del error.
1. Los usuarios pueden mover o eliminar el recurso. Al mover o eliminar un recurso, el número total de referencias de todos los recursos o carpetas seleccionados se muestra en un cuadro de diálogo de advertencia. Al eliminar un recurso para el que aún no se han recuperado las referencias, se muestra un cuadro de diálogo de advertencia.

   ![forzar advertencia de eliminación](assets/delete-referenced-asset.png)

### Administrar actualizaciones de recursos en DAM remoto {#handling-updates-to-remote-assets}

Después [configuración de una conexión](#configure-a-connection-between-sites-and-assets-deployments) entre implementaciones remotas de DAM y Sites, los recursos en DAM remoto están disponibles en la implementación de Sites. A continuación, puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites. Además, si se utiliza un recurso en DAM remoto en una página local de Experience Manager Sites, las actualizaciones del recurso en DAM remoto se muestran en la página Sites.

Al mover un recurso de una ubicación a otra, asegúrese de lo siguiente [ajustar referencias](manage-digital-assets.md) para que el recurso se muestre en la página Sitios. Si mueve un recurso a una ubicación a la que no se puede acceder desde la implementación local de Sites, el recurso no se mostrará en la implementación de Sites.

También puede actualizar las propiedades de metadatos de un recurso en DAM remoto y los cambios están disponibles en la implementación local de Sites.

AEM Los creadores de Sites pueden obtener una vista previa de las actualizaciones disponibles en la implementación de Sites y, a continuación, volver a publicar los cambios para que estén disponibles en la instancia de publicación de la.

El Experience Manager muestra un `expired` Indicador visual de estado de los recursos en el Buscador de contenido de recursos remotos para impedir que los creadores del sitio utilicen el recurso en una página de Sites. Si utiliza un recurso con un `expired` estado en una página de Sites, el recurso no se muestra en la instancia de publicación del Experience Manager.

## Preguntas frecuentes {#frequently-asked-questions}

+++**Debe configurar los recursos de red si necesita utilizar los recursos disponibles en su [!DNL Sites] ¿implementación?**

No es necesario configurar los recursos de red en ese caso. Puede utilizar los recursos disponibles en la [!DNL Sites] implementación.

+++

+++**¿Cuándo se debe configurar la función Recursos conectados?**

Configure la función Recursos conectados solo cuando necesite utilizar los recursos disponibles en una implementación remota de DAM en un [!DNL Sites] implementación.

+++

+++**¿Puede conectar varias [!DNL Sites] implementaciones en una implementación remota de DAM después de configurar los recursos conectados**

Sí, puede conectar varias [!DNL Sites] implementaciones en una implementación remota de DAM después de configurar los recursos de red. Para obtener más información, consulte [Arquitectura de recursos conectados](#connected-assets-architecture).

+++

+++**¿Cuántas implementaciones remotas de DAM puede conectar a un [!DNL Sites] implementación después de configurar los recursos conectados**

Puede conectar una implementación remota de DAM a una [!DNL Sites] después de configurar los recursos de red. Para obtener más información, consulte [Arquitectura de recursos conectados](#connected-assets-architecture).

+++

+++**¿Puede utilizar los recursos de Dynamic Media de su [!DNL Sites] implementación después de configurar los recursos conectados**

Después de configurar los recursos conectados, [!DNL Dynamic Media] Los recursos de están disponibles en [!DNL Sites] implementación en modo de solo lectura. Como resultado, no puede utilizar [!DNL Dynamic Media] para procesar recursos en [!DNL Sites] implementación. Para obtener más información, consulte [Configuración de una conexión entre las implementaciones de Sites y Dynamic Media](#dynamic-media-assets).

+++

+++**¿Puede utilizar recursos de los tipos de formato Imagen y Documento desde la implementación remota de DAM en la [!DNL Sites] implementación después de configurar los recursos conectados**

Sí, puede utilizar recursos de los tipos de formato Imagen y Documento desde la implementación remota de DAM en [!DNL Sites] después de configurar los recursos de red.

+++

+++**¿Puede utilizar fragmentos de contenido y recursos de vídeo de la implementación remota de DAM en? [!DNL Sites] implementación después de configurar los recursos conectados**

No, no puede utilizar fragmentos de contenido y recursos de vídeo de la implementación remota de DAM en [!DNL Sites] después de configurar los recursos de red.

+++

+++**¿Puede utilizar los recursos de Dynamic Media desde la implementación remota de DAM en la [!DNL Sites] implementación después de configurar los recursos conectados**

Sí, puede configurar y utilizar recursos de imagen de Dynamic Media desde la implementación remota de DAM en [!DNL Sites] después de configurar los recursos de red. Para obtener más información, consulte [Configuración de una conexión entre las implementaciones de Sites y Dynamic Media](#dynamic-media-assets).

+++

+++**Después de configurar los recursos conectados, ¿puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos?**

Sí, después de configurar Recursos conectados, puede realizar las operaciones de actualización, eliminación, cambio de nombre y movimiento en los recursos o carpetas DAM remotos. Las actualizaciones, con algún retraso, están disponibles automáticamente en la implementación de Sites. Para obtener más información, consulte [Administrar actualizaciones de recursos en DAM remoto](#handling-updates-to-remote-assets).

+++

+++**Después de configurar los recursos de red, puede agregar o modificar recursos en su [!DNL Sites] y ponerlos a disposición en la implementación remota de DAM?**

Puede agregar recursos a [!DNL Sites] sin embargo, estos recursos no se pueden poner a disposición de la implementación remota de DAM.

+++


## Limitaciones y prácticas recomendadas {#tip-and-limitations}

* Para obtener información sobre el uso de los recursos, configure las [Assets Insight](/help/assets/assets-insights.md) funcionalidad en la [!DNL Sites] ejemplo.
* El uso del explorador de rutas en componentes de creación no se admite en recursos conectados.

* No puede arrastrar el recurso remoto al [Cuadro de diálogo Configurar componente de imagen](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html?lang=en#configure-dialog). Sin embargo, puede arrastrar el recurso remoto directamente al componente de imagen en la página de Sites sin hacer clic en **[!UICONTROL Configurar]**.

### Permisos y administración de recursos {#permissions-and-managing-assets}

* Los recursos locales son copias de solo lectura. [!DNL Experience Manager] los componentes realizan ediciones no destructivas en los recursos. No se permiten otras ediciones.
* Los recursos recuperados localmente solo están disponibles para la creación. Los flujos de trabajo de actualización de recursos no se pueden aplicar y los metadatos no se pueden editar.
* Al utilizar [!DNL Dynamic Media] in [!DNL Sites] páginas en las que no se recuperó el recurso original y no se almacenó en la implementación local. El `dam:Asset` , los metadatos y las representaciones generados por [!DNL Assets] todas las implementaciones se recuperan en la [!DNL Sites] implementación.
* Solo se admiten las imágenes y los formatos de documento enumerados. [!DNL Content Fragments] y [!DNL Experience Fragments] no son compatibles.
* [!DNL Experience Manager] no obtiene los esquemas de metadatos. Significa que es posible que no se muestren todos los metadatos recuperados. Si los esquemas se actualizan por separado en la [!DNL Sites] implementación, se muestran todas las propiedades de metadatos.
* Todo [!DNL Sites] Los autores tienen permisos de lectura en las copias recuperadas, incluso si no pueden acceder a la implementación remota de DAM.
* No se admiten las API para personalizar la integración.
* La funcionalidad admite la búsqueda y el uso ininterrumpidos de recursos remotos. Para que varios recursos remotos estén disponibles en la implementación local, considere migrar los recursos.
* No es posible utilizar un recurso remoto como miniatura de página en [!UICONTROL Propiedades de página] interfaz de usuario. Puede establecer una miniatura de una página web en [!UICONTROL Propiedades de página] interfaz de usuario de [!UICONTROL Miniatura] haciendo clic en [!UICONTROL Seleccionar imagen].

### Configuración y licencia {#setup-licensing}

* [!DNL Assets] implementación en [!DNL Adobe Managed Services] es compatible.
* [!DNL Sites] puede conectarse a un único [!DNL Assets] implementación a la vez.
* Una licencia de [!DNL Assets] es necesario trabajar como repositorio remoto.
* Una o más licencias de [!DNL Sites] se requiere trabajar como implementación de creación local.

### Uso {#usage}

* Los usuarios pueden buscar recursos remotos y arrastrarlos a la página local durante la creación. No se admite ninguna otra funcionalidad.
* La operación de recuperación expira al cabo de 5 segundos. Los autores pueden tener problemas para recuperar recursos, por ejemplo, si hay problemas de red. Los autores pueden volver a intentarlo arrastrando el recurso remoto desde [!UICONTROL Buscador de contenido] hasta [!UICONTROL Editor de página].
* Ediciones simples que no son destructivas y que se admiten mediante la variable `Image` componente, se puede hacer en los recursos recuperados. Los recursos son de solo lectura.
* El único método para recuperar el recurso es arrastrarlo a una página. No hay compatibilidad con API ni otros métodos para recuperar un recurso y actualizarlo.
* Si los recursos se retiran del DAM, se seguirán utilizando en [!DNL Sites] páginas.
* Las entradas de referencia remota de un recurso se recuperan de forma asincrónica. Las referencias y el recuento total no se encuentran en tiempo real y puede haber alguna diferencia si [!DNL Sites] El autor utiliza el recurso mientras un usuario de DAM está viendo la referencia. Los usuarios de DAM pueden actualizar la página e intentarlo de nuevo en unos minutos para obtener el recuento total.

## Solucionar problemas {#troubleshoot}

Para solucionar errores comunes, siga estos pasos:

* Si no puede buscar recursos remotos desde el [!UICONTROL Buscador de contenido], y asegúrese de que las funciones y los permisos necesarios estén establecidos.

* Es posible que un recurso recuperado del DAM remoto no se publique en una página web por uno o más motivos. No existe en el servidor remoto, la falta de permisos adecuados para recuperarla o un error de red pueden ser las razones. Asegúrese de que el recurso no se elimine del DAM remoto. Asegúrese de que los permisos adecuados estén establecidos y de que se cumplan los requisitos previos. Vuelva a intentar agregar el recurso a la página y vuelva a publicar. Compruebe la [lista de trabajos asincrónicos](/help/operations/asynchronous-jobs.md) si hay errores en la recuperación de recursos.

* Si no puede acceder a la implementación remota de DAM desde el [!DNL Sites] implementación, asegúrese de que las cookies entre sitios estén permitidas y [compatibilidad con cookies del mismo sitio](/help/security/same-site-cookie-support.md) está configurado. Si las cookies entre sitios están bloqueadas, las implementaciones de [!DNL Experience Manager] no se puede autenticar. Por ejemplo, [!DNL Google Chrome] en el modo incógnito puede bloquear cookies de terceros. Para permitir cookies en [!DNL Chrome] explorador, haga clic en el icono &quot;ojo&quot; en la barra de direcciones y vaya a **El sitio no funciona** > **Bloqueado**, seleccione la URL del sitio remoto DAM y permita la cookie del token de inicio de sesión. Como alternativa, consulte [cómo habilitar cookies de terceros](https://support.google.com/chrome/answer/95647).

  ![Error de cookie en el explorador Chrome en modo de incógnito](assets/chrome-cookies-incognito-dialog.png)

* Si no se recuperan las referencias remotas y el resultado es un mensaje de error, compruebe si [!DNL Sites] la implementación está disponible y compruebe si hay problemas de conectividad de red. Vuelva a intentarlo más tarde para comprobarlo. [!DNL Assets] la implementación intenta establecer conexión dos veces con [!DNL Sites] y, a continuación, informa de un error.

  ![error al recuperar las referencias remotas del recurso](assets/reference-report-failure.png)

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
