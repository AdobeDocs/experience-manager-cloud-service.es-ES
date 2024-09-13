---
title: Compatibilidad con Edge Delivery Services en Cloud Manager
description: Obtenga información sobre cómo entregar sus proyectos de Cloud Manager con Edge Delivery Services.
exl-id: f33bd6f0-62fc-4ecc-b8d2-65d1f1c44d82
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bc9aa376a402a55191e153f662262ff65df32f5e
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 5%

---

# Compatibilidad con Edge Delivery Services en Cloud Manager {#edge-delivery-services}

Aprenda a utilizar su licencia de Edge Delivery Services para crear un sitio de Edge Delivery Services.

<!-- RELEASED TO GA SEPTEMBER 5, 2024
>[!NOTE]
>
>This feature is only available to [the early adopter program](/help/implementing/cloud-manager/release-notes/current.md#early-adoption). -->

## Edge Delivery Services en resumen {#edge-overview}

Edge Delivery Services es un conjunto de servicios componibles que permite un alto grado de flexibilidad en la forma en que se crea contenido en su sitio web. Esta capacidad le permite hacer lo siguiente:

* Crea sitios rápidos con una puntuación perfecta en Lighthouse.
* Monitorizar continuamente el rendimiento a través de RUM (Monitoreo de Uso Real).
* Aumente la eficacia de la creación desacoplando las fuentes de contenido.

AEM Puede utilizar tanto la administración de contenido de como la creación WYSIWYG mediante el Editor universal y la creación basada en documentos.

Cloud Manager en AEM as a Cloud Service le permite habilitar el servicio de Edge Delivery para su proyecto.

>[!TIP]
>
>Para obtener más información acerca de los Edge Delivery Services AEM y cómo se pueden usar con los, consulte el documento [Información general de los Edge Delivery Services](/help/edge/overview.md).

## Edge Delivery Services en Cloud Manager {#edge-in-cloud-manager}

Si tiene Edge Delivery Services con licencia como parte de Adobe Experience Manager Sites, puede incorporar su sitio con Edge Delivery Services directamente en Cloud Manager e iniciar [con una experiencia guiada de autoservicio](/help/implementing/cloud-manager/managing-code/private-repositories.md).

AEM Además, puede acceder a una experiencia unificada para administrar todas las propiedades de la y garantizar la coherencia en los flujos de trabajo clave. Estas incluyen administración de nombres de dominio, administración de certificados SSL y asignaciones de CDN.

## Adición de Edge Delivery Services a un programa de producción o de zona protegida

Para agregar o editar programas, debe ser miembro del rol **Propietario del negocio** o tener permiso para hacerlo.
Su organización debe tener una licencia de Edge Delivery Services no utilizada para poder aplicarla a un programa de producción.

>[!NOTE]
>
>Una vez que la licencia de Edge Delivery Services se aplica a un programa o se elimina de él, el cambio entra en vigor inmediatamente sin necesidad de ejecutar una canalización. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

Según el caso de uso, realice una de las siguientes acciones:

| Caso de uso | Descripción |
| --- | --- |
| Deseo agregar Edge Delivery Services a un nuevo programa de producción. | Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).<br>En el asistente, en la ficha **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo agregar Edge Delivery Services a un programa de producción existente. | Ver [Editar programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md).<br>En el cuadro de diálogo **Editar programa**, en la ficha **Soluciones y complementos**, seleccione **Edge Delivery Services**. |
| Deseo agregar Edge Delivery Services a un programa de zona protegida nuevo o existente. | Consulte [Crear programas de zona protegida](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md).<br>Al crear un programa de zona protegida, los Edge Delivery Services se agregan al programa de forma predeterminada; no es necesario seleccionarlo.<br>Los programas de zonas protegidas existentes heredan los Edge Delivery Services automáticamente. |

## Ruta recomendada de Adobe para clientes contratados {#recommended-path-eds}

Como cliente contratado, asegúrese de maximizar sus beneficios del Adobe accediendo y consumiendo su licencia de Edge Delivery Services a través de Cloud Manager. Este enfoque le permite usar [CDN administrada por Adobe](/help/implementing/dispatcher/cdn.md#aem-managed-cdn) y aprovechar ventajas clave como la administración de CDN de autoservicio, incluida la configuración y adición de certificados DV. Además, después de crear un certificado DV, Adobe lo renueva automáticamente cada tres meses, a menos que se elimine. Si no tiene una licencia de Edge Delivery Services con Adobe y decide omitir estos beneficios, solo puede utilizar una CDN administrada por el cliente. Esta configuración debe estar en la plataforma `aem.live`.

Si tiene una licencia de Edge Delivery Services de AEM as a Cloud Service Sites contratada, inicie sesión en Cloud Manager para asegurarse de que puede hacer lo siguiente:

* Consuma la licencia en el programa elegido.
* Aproveche los beneficios de [API-first](https://developer.adobe.com/experience-cloud/experience-manager-apis/) para realizar operaciones CRUD (crear, leer, actualizar, eliminar).
<!-- REMOVED AS PER https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+Self-service+access+to+Edge+Delivery+Services+and+Adobe+Managed+CDN * Access to license dashboard and reporting -->
* Acceso a los informes de SLA (*próximamente*) <!-- ADD LINK TO IT WHEN FINALLY ADDED -->
* Obtener soporte de Adobe. Asegúrese de que los sitios de Edge Delivery Services estén registrados a través de un programa de producción en Cloud Manager para que el Adobe los reconozca y admita correctamente.

## Añadir un sitio de Edge Delivery {#eds-add-site}

Después de agregar Edge Delivery Services a un programa de producción, se le aplica la licencia de Edge Delivery Services.

Se ve una ficha en la que se puede hacer clic llamada **Edge Delivery** en la página Información general. Al hacer clic en la pestaña, se muestra una tabla que enumera todos los sitios de Edge Delivery que ha agregado. En el panel de navegación izquierdo, en la agrupación **Servicios**, observe la opción de menú denominada **Sitios Edge Delivery**.

![Página de información general que muestra Edge Delivery Sites en el panel de navegación izquierdo y la pestaña Edge Delivery a la derecha de la pestaña Publish Delivery](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Para agregar un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurados, donde desee agregar un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:
   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. A continuación, cerca de la esquina inferior derecha de la página, haga clic en **Agregar sitio de Edge Delivery**.

     ![Agregar sitio Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     La **lista de tareas pendientes de Edge Delivery**, tal como se ve en la imagen anterior, es una guía de lista de comprobación de incorporación opcional diseñada para ayudarle a empezar a usar Edge Delivery. Ver [Acerca de la lista de tareas pendientes de Edge Delivery](#ed-todo-list).

   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**. Cerca de la esquina superior derecha de la página, haga clic en **Agregar sitio**.

     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. En el cuadro de diálogo **Agregar sitio Edge Delivery**, haga lo siguiente:

   | Campo de texto | Qué hacer |
   | --- | --- |
   | Nombre del sitio | Escriba el nombre del sitio de Edge Delivery que está agregando. El nombre sirve como identificador único del sitio en Cloud Manager. |
   | URL del repositorio | Este campo hace referencia al repositorio de Git donde se almacena el código del sitio web.<br>Introduzca la URL del repositorio de Git que contiene los archivos y recursos necesarios (como HTML, CSS, JavaScript y otros recursos web) para su sitio de Edge Delivery. Esta disposición permite a Cloud Manager extraer el código de ese repositorio durante el proceso de implementación. |
   | Descripción del sitio (opcional) | Escriba una breve descripción del sitio de Edge Delivery que está agregando.<br>Esta descripción ayuda a identificar y diferenciar el sitio, lo que facilita la administración y el reconocimiento, entre otros sitios que ha agregado. Es posible que desee incluir detalles sobre el propósito, el contenido o cualquier otra información relevante que pueda ayudar a aclarar su función o alcance. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Agregar**.

1. En el cuadro de diálogo **Verificar propiedad del repositorio**, realice cada una de las siguientes acciones:

   | Paso | Descripción |
   | --- | --- |
   | 1 | Agregue un archivo con la ruta de ubicación a la rama `main` del repositorio Git que aparece en el campo **URL del repositorio**. Si es necesario, haga clic en el icono Copiar para copiar la ruta de acceso en el portapapeles.<br> La ruta de acceso de la ubicación es:<br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>No *agregue un punto al inicio de la ruta de acceso de la ubicación, está en:<br>`.well-known/adobe/cloudmanager-challenge.txt`* |
   | 2 | Agregue el código generado al archivo que creó en el paso 1. Si es necesario, haga clic en el icono Copiar para copiar el código en el portapapeles. |
   | 3 | En el repositorio Git, cree una solicitud de extracción y, a continuación, fusiónela para validar el código. |

1. Haga clic en **Verificar**. Una vez verificado el repositorio, su estado en la tabla Edge Deliver Sites cambia a un círculo verde con una marca de verificación blanca dentro de él.

## Acerca de la lista de tareas pendientes de Edge Delivery {#ed-todo-list}

La **lista de tareas pendientes de Edge Delivery** es una lista de comprobación de tareas de incorporación diseñada para guiarle a través de la incorporación, y administrar su sitio de Edge Delivery hasta [Go-Live](/help/journey-onboarding/go-live-checklist.md).

|  | Tarea | Descripción |
| --- | --- | --- |
| 1 | Únase al canal de colaboración de productos | Al hacer clic en **Enviar solicitud ahora** se envía una solicitud al Adobe para crear un canal para su compañía. Si el canal ya existe, se le reenviará al canal de la empresa. |
| 2 | Complete los requisitos previos | Al hacer clic en **Ver tutorial de introducción**, accederá al [Tutorial de introducción para desarrolladores](https://www.aem.live/developer/tutorial). |
| 3 | Agregar sitio de Edge Delivery | Consulte [Agregar un sitio Edge Delivery](#eds-add-site). |
| 4 | Añadir dominio | Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |
| 5 | Añadir certificado SSL | Consulte [Agregar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
| 6 | Configuración de la CDN del sitio de Edge Delivery | Consulte [Agregar una configuración de CDN](#add-cdn). |

>[!VIDEO](https://video.tv.adobe.com/v/3428020?learn=on)

## Añada una configuración de CDN al sitio de Edge Delivery {#add-cdn}

Consulte [Agregar una configuración de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Eliminación de un sitio de Edge Delivery {#eds-site-delete}

>[!IMPORTANT]
>
>Si elimina un sitio de Edge Delivery Services, también se eliminarán todas las configuraciones de CDN asociadas. Esta acción interrumpe la conexión entre los dominios personalizados y el sitio. Para obtener más información, consulte Configuraciones de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para eliminar un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurados, donde desee agregar un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:
   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee quitar. Haga clic en **Eliminar** y, a continuación, haga clic en **Eliminar** de nuevo para confirmar la eliminación del sitio.

     ![Agregar sitio Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee quitar. Haga clic en **Eliminar** y, a continuación, haga clic en **Eliminar** de nuevo para confirmar la eliminación del sitio.


     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)


<!--
Edge Delivery Services can be enabled when adding a new production program or editing an existing one.

![Add production program with Edge Delivery Services](assets/add-production-program-with-edge.png)

For more information about adding programs, see the following:

* [Create Production programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* [Create Sandbox programs](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) -->
