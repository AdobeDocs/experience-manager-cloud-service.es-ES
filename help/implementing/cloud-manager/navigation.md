---
title: Navegar por la IU de Cloud Manager
description: Descubra cómo está organizada la IU de Cloud Manager y cómo navegar para administrar sus programas y entornos.
exl-id: 3f3d7631-2bc9-440b-9888-50f6529bcd42
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4c42888af1e846c011242af2c328e553bb811cfd
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 37%

---


# Navegar por la IU de Cloud Manager {#navigation}

Descubra cómo está organizada la IU de Cloud Manager y cómo navegar para administrar sus programas y entornos.


La IU de Cloud Manager está compuesta principalmente por dos interfaces gráficas:

* [La consola Mis programas](#my-programs-console) es donde puede ver y administrar todos los programas.
* [La ventana Información general del programa](#program-overview) es donde puede ver los detalles de un programa individual y administrarlo.

>[!TIP]
>
>Consulte también el [recorrido de documentación de incorporación](/help/journey-onboarding/overview.md) para obtener una descripción general completa de cómo ponerse en marcha con AEM as a Cloud Service mediante Cloud Manager.


## Asistente de IA en AEM

Para los clientes que han [completado criterios de requisitos previos](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), el Asistente de IA en AEM está disponible para los usuarios de su organización. Ver [Asistente de IA en AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).


## Consola Mis programas {#my-programs-console}

Al iniciar sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccionar la organización adecuada, se llega a la consola **Mis programas**.

![Consola Mis programas](assets/my-programs-console.png)

La consola Mis programas proporciona información general de todos los programas a los que tiene acceso en la organización seleccionada. Se compone de partes.

1. [Barras de herramientas](#toolbars-my-programs-toolbars) para la selección de organizaciones, alertas y configuración de la cuenta.
1. Pestañas que permiten alternar la vista actual de los programas.
   * Vista **Inicio** (predeterminada) que selecciona la vista **Mis programas** con información general de todos los programas
   * **Licencia** que accede al [Panel de licencias](/help/implementing/cloud-manager/license-dashboard.md).
   * Tenga en cuenta que las pestañas se cierran de forma predeterminada y se pueden mostrar con ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) en el [encabezado de Cloud Manager](#cloud-manager-header).
1. [Estadísticas y llamada a la acción](#statistics) para obtener una descripción general de su actividad reciente
1. [**Sección Mis programas**](#my-programs-section) con información general de todos sus programas
1. [Vínculos rápidos](#quick-links-section) para acceder fácilmente a recursos relacionados.

>[!TIP]
>
>Consulte el documento [Programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) para obtener más información sobre los programas.

### Barras de herramientas {#my-programs-toolbars}

Hay dos barras de herramientas una encima de la otra.

#### Encabezado de Cloud Manager {#cloud-manager-header}

El primero es el encabezado de Cloud Manager, que es persistente mientras navega por Cloud Manager. Es un anclaje que le permite acceder a la configuración y a la información que se aplican a todos los programas de Cloud Manager.

![El encabezado de Experience Cloud](assets/experience-cloud-header.png)

1. Haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) (mostrar u ocultar menú lateral) para que tenga acceso a una variedad de fichas que pueden llevarlo a partes específicas de un programa individual. O bien, puede cambiar entre el [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md) y la consola **[Mis programas](#my-programs-console)** en función del contexto.
1. Haga clic en el botón Adobe Cloud Manager que le lleva de nuevo a la consola Mis programas de Cloud Manager, independientemente de dónde se encuentre en Cloud Manager.
1. Haga clic en **Comentarios** para proporcionar comentarios a Adobe sobre Cloud Manager.
1. Haga clic en el selector de organización para mostrar la organización en la que está conectado actualmente (en este ejemplo, Foundation Internal). Haga clic para cambiar a otra organización si su Adobe ID está asociado a varias.
1. Haga clic en ![Icono de aplicaciones](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (conmutador de soluciones) para ir rápidamente a otras soluciones de Experience Cloud.
1. Haga clic en ![Icono de ayuda](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Help_18_N.svg) para obtener acceso rápido a los recursos de aprendizaje y asistencia.
1. Haz clic en ![Icono de campana](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) ([Notificaciones](/help/implementing/cloud-manager/notifications.md)) para ver notificaciones y anuncios, entre otras cosas.
1. Haga clic en el icono que representa el acceso del usuario a la configuración de usuario. Si no tiene una imagen de usuario configurada, se le asigna un icono de forma aleatoria.

#### Barra de herramientas del programa {#program-toolbar}

La barra de herramientas del programa proporciona vínculos para cambiar entre los programas de Cloud Manager y las acciones apropiadas para el contexto.

![Barra de herramientas del programa](assets/program-toolbar.png)

1. El selector **Mis programas** abre una lista desplegable donde puede seleccionar otros programas rápidamente o realizar acciones según el contexto, como crear un nuevo programa
1. El vínculo **Introducción** le proporciona acceso al [recorrido de documentación de incorporación](/help/journey-onboarding/overview.md) para que pueda ponerse en marcha con Cloud Manager.
1. El botón de acción ofrece acciones adecuadas al contexto, como agregar un programa.

### Estadísticas y llamadas a la acción {#statistics}

La sección de estadísticas y call-to-action proporciona datos acumulados para su organización. Por ejemplo, si ha configurado correctamente sus programas, pueden mostrarse estadísticas de las actividades de los últimos 90 días, incluidas las siguientes:

* Número de [implementaciones](/help/implementing/cloud-manager/deploy-code.md)
* Número de [problemas de calidad del código](/help/implementing/cloud-manager/code-quality-testing.md) identificados
* Número de compilaciones

O si acaba de comenzar la configuración de su organización, puede haber sugerencias sobre los pasos siguientes o los recursos de documentación.

### Sección Mis programas {#my-programs-section}

El contenido principal de la consola **Mis programas** es la lista de programas de la sección **Mis programas**.

La sección **Mis programas** enumera las tarjetas que representan cada programa. Toque o haga clic en una tarjeta para acceder a la página **información general del programa** para obtener más información sobre el programa.

>[!NOTE]
>
>Según sus privilegios, es posible que no pueda seleccionar determinados programas.


Para encontrar el programa que necesita más fácilmente, utilice las opciones de clasificación.

![Opciones de ordenación](/help/implementing/cloud-manager/assets/my-programs-sorting.png)

* Ordenar por:
   * **Fecha de creación** (predeterminada)
   * **Nombre de programa**
   * **Estado**
* ![Icono de orden descendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderDown_18_N.svg) ascendente (predeterminado) / ![Icono de orden ascendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SortOrderUp_18_N.svg) descendente
* ![Icono de vista de cuadrícula clásica](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ClassicGridView_18_N.svg) Vista de cuadrícula (predeterminado)
* ![Icono de lista de vista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) Vista de lista

#### Tarjetas de programa {#program-cards}

Una tarjeta (o fila en una tabla) representa cada programa, lo que proporciona una descripción general del programa y vínculos rápidos para realizar acciones.

![Tarjeta de programa](assets/program-card.png)

* Imagen asociada al programa, si se ha configurado. La imagen de arriba es &quot;WKND&quot;.
* Nombre asignado al programa. La imagen anterior muestra &quot;Ejemplo de SecurBank&quot; como nombre del programa.
* Tipo de servicio:
   * **Experience Manager Cloud** para programas de AEM as a Cloud Service
   * **Experience Manager** — para [programas de AMS (Adobe Managed Services)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)
* [Tipo de programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md):
   * Zona protegida
   * Producción
* Estado. En la imagen anterior, el estado es Listo con una marca de verificación.
* Soluciones configuradas. En la imagen anterior, Sites y Assets son las soluciones configuradas.
* Fecha de creación.

Un programa de producción puede tener un distintivo para mostrar las funciones adicionales que eligió en el momento en que lo agregó, como las siguientes:

* ![Insignia de HIPAA](assets/hipaa.png) [HIPAA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* ![Insignia WAF-DDOS](assets/waf-ddos-protection.png) [Protección WAF-DDOS](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#security)

* [99,99 % SLA (Service level agreement)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)

El icono de información también permite acceder rápidamente a la información adicional sobre el programa (útil en la vista de listas).

![Información](assets/information-list-view.png)

El icono ![Más](https://spectrum.adobe.com/static/icons/workflow_22/Smock_More_22_N.svg) te da acceso a acciones adicionales que puedes realizar en el programa.

![Botón de puntos suspensivos para programas](assets/program-ellipsis.png)

* Vaya a un ![icono de datos](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Data_22_N.svg) [Entorno](/help/implementing/cloud-manager/manage-environments.md) particular del programa
* Abra el ![icono de información general del programa](/help/implementing/cloud-manager/assets/program-overview.svg) [Información general del programa](#program-overview)
* ![Editar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) [Editar el programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#editing)
* ![Eliminar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)[Eliminar un programa de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#delete-sandbox-program)

>[!TIP]
>
>Para obtener más información acerca de los programas y la adición y administración de programas, vea los temas siguientes:
>
>* [Programas y tipos de programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)
>* [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
>* [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)


### Sección de vínculos rápidos {#quick-links-section}

La sección de vínculos rápidos le permite acceder a recursos utilizados con frecuencia relacionados.

## Página de información general del programa {#program-overview}

Cuando se selecciona un programa en la consola **[Mis programas](#my-programs-console)**, se le redirige a la página **Información general del programa**.

![Información general del programa](assets/program-overview.png)

La descripción general del programa le permite acceder a todos los detalles de un programa de Cloud Manager. Al igual que la consola **Mis programas**, consta de varias partes.

1. [Barras de herramientas](#program-overview-toolbar) para volver rápidamente a la consola Mis programas y navegar por el programa
1. [Pestañas](#program-tabs) para cambiar entre los diferentes aspectos del programa
1. Una [llamada a la acción](#cta) basada en las últimas acciones del programa
1. Una [descripción general de los entornos](#environments) del programa
1. Una [descripción general de las canalizaciones](#pipelines) del programa
1. Una [descripción general del rendimiento](#performance) del programa
1. Vínculos a [recursos útiles](#useful-resources)

### Barras de herramientas {#program-overview-toolbar}

Las barras de herramientas de la descripción general del programa son similares a las barras de herramientas de [Mis programas](#my-programs-toolbars). Aquí solo se ilustran las diferencias.

#### Encabezado de Cloud Manager {#cloud-manager-header-2}

En la esquina superior izquierda de la página se encuentra el encabezado Cloud Manager de Adobe. Puede hacer clic en ![Icono de menú lateral](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar u ocultar el menú lateral de pestañas a otras áreas del software.

![menú lateral de Cloud Manager](assets/cloud-manager-hamburger.png)

Haga clic en Adobe Cloud Manager para volver a Inicio.

#### Barra de herramientas del programa {#program-toolbar-2}

La barra de herramientas de programas le permite cambiar rápidamente a otros programas, pero además le da acceso a acciones apropiadas para el contexto, como agregar y editar el programa.

![Barra de herramientas del programa](assets/cloud-manager-program-toolbar.png)

La barra de herramientas siempre muestra la ficha en la que se encuentra, incluso si ha ocultado las fichas mediante ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg).

### Pestañas del programa {#program-tabs}

Cada programa tiene muchas opciones y datos asociados. Estas opciones y datos se recopilan en pestañas para facilitar la navegación por el programa. Las pestañas le permiten acceder a lo siguiente:

**Programa**

* ![Icono de vista de cuadrícula moderna](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ModernGridView_18_N.svg) Información general: la descripción general del programa tal como se describe en el documento actual
* ![Icono de campana](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bell_18_N.svg) [Actividad](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity): el historial de ejecuciones de canalización del programa
* ![Icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) [Canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines): todas las canalizaciones configuradas para el programa
* ![Icono de carpeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) [Repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md): todos los repositorios configurados para el programa
* ![Icono gráfico circular](https://spectrum.adobe.com/static/icons/workflow_18/Smock_GraphPie_18_N.svg) [Informes](/help/implementing/cloud-manager/sla-reporting.md): métricas como datos de SLA

**Servicios**

* ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) [Entornos](/help/implementing/cloud-manager/manage-environments.md): todos los entornos configurados para el programa
* ![Icono de páginas web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) [Sitios Edge Delivery](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md) - Administrar sitios Edge Delivery
* ![Icono de configuración](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Settings_18_N.svg) [Configuración de dominio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Administrar nombres de dominio personalizados para el programa
* ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md): administre los certificados SSL para el programa
* ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) [Asignaciones de dominio](/help/implementing/cloud-manager/custom-domain-names/introduction.md) - Administrar asignaciones de dominio
* ![Icono de lista de tareas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md): defina listas de permitidos para determinadas direcciones IP
* ![Icono de cuadro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) [Conjuntos de contenido](/help/implementing/developing/tools/content-copy.md) - Conjuntos de contenido creados con fines de copia
* ![Icono de historial](https://spectrum.adobe.com/static/icons/workflow_18/Smock_History_18_N.svg) [Copiar actividad de contenido](/help/implementing/developing/tools/content-copy.md) - Actividades de copia de contenido
* ![Icono de canal](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Channel_18_N.svg) [Infraestructura de red](/help/security/configuring-advanced-networking.md) - Administrar las opciones avanzadas de red para el programa

**Recursos**

* ![Icono de libro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Book_18_N.svg) Rutas de aprendizaje - Recursos de aprendizaje adicionales acerca de Cloud Manager

De forma predeterminada, al abrir un programa, llega a la pestaña **Información general**. La pestaña actual está resaltada. Seleccione otra pestaña para mostrar sus detalles.

En la esquina superior izquierda del [encabezado de Cloud Manager](#cloud-manager-header-2), haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar u ocultar el menú lateral de las pestañas.

### Llamada a la acción {#cta}

La sección de llamada a la acción le proporciona información útil según el estado del programa. Para un programa nuevo, es posible que vea los pasos siguientes dados y un recordatorio de una fecha de lanzamiento, [establecida durante la creación del programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).

![Call-to-action para un nuevo programa](/help/implementing/cloud-manager/assets/info-banner-new-program.png)

Para un programa activo, el estado de la última implementación con vínculos para obtener más información e iniciar una nueva implementación.

![Llamada a la acción](/help/implementing/cloud-manager/assets/info-banner.png)

### Tarjeta Entornos {#environments}

La tarjeta **Entornos** le ofrece una descripción general de sus entornos, así como vínculos para acciones rápidas.

La tarjeta **Entornos** solo enumera tres entornos. Haga clic en ![icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar todo** para ver todos los entornos del programa.

Consulte también [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md).

### Tarjeta de canalizaciones {#pipelines}

La tarjeta de **Canalizaciones** le ofrece una descripción general de sus canalizaciones, así como vínculos para acciones rápidas.

La tarjeta **Canalizaciones** solo enumera tres canalizaciones. Haga clic en ![icono de flujo de trabajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **Mostrar todo** para ver todas las canalizaciones del programa.

Consulte también [Administrar canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para obtener detalles sobre cómo administrar sus canalizaciones.

### Tarjeta de rendimiento {#performance}

La tarjeta **Rendimiento** proporciona información general sobre el **[panel de CDN](/help/implementing/cloud-manager/cdn-performance.md)**.

![Tarjeta de rendimiento](/help/implementing/cloud-manager/assets/cdn-performance-dashboard.png)

### Recursos útiles {#useful-resources}

La sección **Recursos útiles** proporciona vínculos a recursos de aprendizaje adicionales para Cloud Manager.
