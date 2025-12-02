---
title: Añadir una asignación de dominio
description: Obtenga información sobre cómo agregar una asignación de dominio para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 4935fbf5f0eb10f2f17280fb32f07d99f69eb875
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 5%

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

1. En el cuadro de diálogo **Asignar dominio a CDN**, seleccione uno de los siguientes tipos de CDN:

   * **CDN administrado por Adobe (recomendado)**: se usa una CDN administrada por Adobe para esta configuración. Incluye configuración y administración automatizadas, así como funciones de seguridad integradas.
   * **Otro proveedor de CDN** - Se utiliza una red de proveedor de CDN autoadministrada para esta configuración.

1. En función del tipo de CDN seleccionado en el paso anterior, haga lo siguiente:

   * **CDN administrado por Adobe**

     ![Asignar dominio a CDN (cuadro de diálogo) con el botón de opción CDN administrado por Adobe seleccionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-adobe-managed.png)

      1. En la lista desplegable **Origen**, seleccione una de las siguientes opciones:

         | Lista desplegable Origen | Descripción |
         | --- | --- |
         | Sites | Seleccione un sitio de Edge Delivery. |
         | Entorno | Seleccione un entorno de Cloud Service específico que desee segmentar en la configuración de AEM.<br>En la lista desplegable **Nivel**, seleccione una de las siguientes opciones:<br>· Seleccione **Publicar** para segmentar un entorno de producción activo en el que el contenido se entregue a los usuarios finales.<br>· Seleccione **Vista previa** para entornos de ensayo o de no producción donde pruebe los cambios antes de que se activen. |

      1. En la lista desplegable **Dominio**, seleccione el nombre de dominio que desee usar.<br>No hay dominios comprobados disponibles en la lista desplegable? Consulte [Añadir un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

      1. En la lista desplegable **certificado SSL**, seleccione el certificado que desee usar.<br>No hay certificados SSL disponibles en la lista desplegable? Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

      1. Haga clic en **Guardar**.

   * **Otro proveedor de CDN**

     ![Asignar dominio a CDN (cuadro de diálogo) con el botón de opción CDN administrado por Adobe seleccionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-other-provider.png)

     Siga los pasos de configuración enumerados para aplicar la configuración necesaria en la CDN y confirmar la asignación. Consulte también [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

      1. Haga clic en **He configurado mi CDN**.

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

   <!-- In the **Domain** field, enter the customer-facing hostname you want to serve (for example, `www.example.com`) -->

1. Adobe recomienda probar la asignación de dominio.

## Prueba de la asignación de dominio {#test-domain-mapping}

Puede comprobar que una nueva asignación de dominio está activa en la CDN administrada por Adobe sin esperar la propagación pública de DNS.

Ejecute un comando **curl** que anule la resolución de DNS y que apunte directamente al perímetro de CDN:

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* Reemplace `www.example.com` por su dominio.
* La dirección IP `151.101.3.10` es una de las IP que se pueden usar para acceder a AEM Cloud Service. Consulte también [registro APEX](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record).

El indicador `--resolve` fuerza la solicitud a la IP especificada y devuelve el resultado correcto solo después de que el certificado y el enrutamiento para su dominio se hayan instalado correctamente.

