---
title: Añadir una configuración de CDN
description: Obtenga información acerca de cómo añadir una configuración de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 6%

---


# Añadir una configuración de CDN {#add-cdn}

Para vincular un dominio con un certificado SSL en la CDN administrada por Adobe dentro del programa, debe agregar una configuración de CDN (red de distribución de contenido).

En el caso de las CDN administradas por Adobe, al utilizar certificados DV, solo se permiten sitios con validación ACME.

>[!IMPORTANT]
>
>¿Ha [agregado un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) y [agregado un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md), respectivamente? Si no es así, debe completar estas dos tareas antes de agregar una configuración de CDN.

**Para agregar una configuración de CDN:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Según el caso de uso, realice una de las siguientes acciones:

   | Caso de uso | Etapas |
   | --- | --- |
   | Quiero agregar una configuración de CDN a un *sitio Edge Delivery existente* en Cloud Manager | a. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Sitios Edge Delivery**.<br>b. En la tabla de Edge Delivery, al final de una fila que no tiene un dominio asociado, haga clic en los puntos suspensivos.<br>c. Haga clic en **Configurar CDN**.  ![Haga clic en Configurar CDN para un sitio de Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-config-cdn.png) |
   | Quiero añadir una configuración de CDN en Cloud Manager | a. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Configuraciones de CDN**.<br>b. Cerca de la esquina superior derecha de la página Configuraciones de CDN, haga clic en **Agregar**. |

1. En el cuadro de diálogo **Configurar CDN**, en la lista desplegable **Origen**, seleccione una de las siguientes opciones:

   ![Cuadro de diálogo Configurar CDN](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

   | Origen | Descripción |
   | --- | --- |
   | Sites | Seleccione un sitio de Edge Delivery. |
   | Entorno | Seleccione un entorno de Cloud Service AEM específico que desee segmentar en la configuración de la.<br>En la lista desplegable **Nivel**, seleccione una de las siguientes opciones:<br>· Seleccione **Publish** para segmentar un entorno de producción activo en el que el contenido se entregue a los usuarios finales.<br>· Seleccione **Vista previa** para entornos de ensayo o de no producción donde pruebe los cambios antes de que se activen. |

1. Seleccione el tipo de CDN y la configuración asociada seleccionando una de las siguientes opciones:

   | Tipo de CDN | Detalles de configuración |
   | --- | --- |
   | CDN administrada por Adobe | En **Detalles de configuración**, haga lo siguiente:<br>a. En la lista desplegable **Dominio**, seleccione el nombre de dominio que desee usar.<br>No hay dominios comprobados disponibles en la lista desplegable? Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b. En la lista desplegable **certificado SSL**, seleccione el certificado que desee usar.<br>No hay certificados SSL disponibles en la lista desplegable? Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Otro proveedor de CDN | Seleccione esta opción si utiliza su propio proveedor de CDN y no la CDN administrada por Adobe que está disponible.<br>En **Detalles de configuración**, en la lista desplegable **Dominio**, seleccione el nombre de dominio que desee usar.<br>No hay dominios comprobados disponibles en la lista desplegable? Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Haga clic en **Guardar**.
