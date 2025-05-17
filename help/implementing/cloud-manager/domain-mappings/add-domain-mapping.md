---
title: Agregar una asignación de dominio
description: Obtenga información sobre cómo agregar una asignación de dominio para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: c2229d040c8df7c9089d141d57ca59ff2f4ce8a7
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 9%

---


# Agregar una asignación de dominio {#add-domain-mapping}

Para vincular un dominio con un certificado SSL en la CDN administrada por Adobe dentro del programa, debe agregar una configuración de CDN (red de distribución de contenido).

Para CDN administrados por Adobe, al utilizar un certificado SSL DV, solo se permiten sitios con validación ACME.

>[!IMPORTANT]
>
>¿Ha [agregado un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) y [agregado un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md), respectivamente? Si no es así, debe completar estas dos tareas antes de agregar una configuración de CDN.

Consulte también [CDN administrada por Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed).

**Para agregar una asignación de dominio:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Según el caso de uso, realice una de las siguientes acciones:

   | Caso de uso | Etapas |
   | --- | --- |
   | Quiero agregar una configuración de CDN a un *sitio Edge Delivery existente* en Cloud Manager | a. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de páginas web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios Edge Delivery**.<br>b. En la tabla de Edge Delivery, al final de una fila que no tiene un dominio asociado, haga clic en ![Más iconos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).<br>c. Haga clic en **Configurar CDN**. |
   | Quiero añadir una configuración de CDN en Cloud Manager | a. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Asignaciones de dominio**.<br>b. Cerca de la esquina superior derecha de la página Asignaciones de dominio, haga clic en **Agregar**. |

1. En el cuadro de diálogo **Configurar CDN**, en la lista desplegable **Origen**, seleccione una de las siguientes opciones:

   ![Cuadro de diálogo Configurar CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

   | Origen | Descripción |
   | --- | --- |
   | Sites | Seleccione un sitio de Edge Delivery. |
   | Entorno | Seleccione un entorno de Cloud Service específico que desee segmentar en la configuración de AEM.<br>En la lista desplegable **Nivel**, seleccione una de las siguientes opciones:<br>· Seleccione **Publicar** para segmentar un entorno de producción activo en el que el contenido se entregue a los usuarios finales.<br>· Seleccione **Vista previa** para entornos de ensayo o de no producción donde pruebe los cambios antes de que se activen. |

1. Seleccione el tipo de CDN y la configuración asociada seleccionando una de las siguientes opciones:

   | Tipo de CDN | Detalles de configuración |
   | --- | --- |
   | CDN administrada por Adobe | En **Detalles de configuración**, haga lo siguiente:<br>a. En la lista desplegable **Dominio**, seleccione el nombre de dominio que desee usar.<br>No hay dominios comprobados disponibles en la lista desplegable? Consulte [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b. En la lista desplegable **certificado SSL**, seleccione el certificado que desee usar.<br>No hay certificados SSL disponibles en la lista desplegable? Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Otro proveedor de CDN | Seleccione esta opción si está utilizando su propio proveedor de CDN y no la CDN administrada por Adobe que está disponible.<br>En **Detalles de configuración**, en la lista desplegable **Dominio**, seleccione el nombre de dominio que desee usar.<br>No hay dominios comprobados disponibles en la lista desplegable? Consulte [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Haga clic en **Guardar**.
