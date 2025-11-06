---
title: Administrar los nombres de dominio personalizados
description: Aprenda a utilizar Cloud Manager para ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 21%

---


# Administrar nombres de dominio personalizados {#managing-custom-domain-names}

Cloud Manager permite editar, actualizar, reemplazar, comprobar y eliminar nombres de dominio personalizados.

## Editar una configuración de nombre de dominio personalizada {#view-and-update}

En Adobe Cloud Manager, es posible que desee editar una configuración de nombre de dominio personalizado por los siguientes motivos:

* **Entornos de cambio**: Para aplicar la configuración correcta en función de si está sirviendo contenido a usuarios finales (Publicación) o a usuarios internos (Autor).
* **Actualizaciones de seguridad**: Para actualizar a un certificado SSL más reciente con fines de cumplimiento o seguridad mejorados.
* **Cambiando la estrategia de implementación**: Para asegurarse de que se aplica el certificado SSL correcto a un entorno específico para el cifrado y el acceso al sitio adecuados.

**Para editar una configuración de nombre de dominio personalizado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.

1. Bajo el encabezado **Servicios**, haga clic en ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Asignaciones de dominio**.

1. En la página **Asignaciones de dominio**, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuya CDN desee editar.

1. Haga clic en **Editar**.

1. En el cuadro de diálogo **Editar configuración de dominio**, haga lo siguiente:

   * En la lista desplegable **Nivel**, seleccione el nivel (Publicar o Vista previa) que desee utilizar.
   * En la lista desplegable **certificado SSL**, seleccione el certificado SSL que desee usar.

1. Haga clic en **Actualizar**.


## Actualizar el certificado SSL de un nombre de dominio personalizado {#update-cert}

Siga los mismos pasos anteriores para actualizar el certificado SSL de un nombre de dominio personalizado.

>[!NOTE]
>
>El certificado SSL debe ser válido [ya configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) y contener el nombre de dominio personalizado que está actualizando.


## Comprobar un nombre de dominio personalizado {#verify-custom-domain-name}

Consulte también [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la página **Configuración de dominio** desde la pantalla **Información general**.

1. Identifique la fila del nombre de dominio personalizado que desee comprobar.

1. Haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho de la fila.

1. En el menú desplegable, haga clic en **Verificar**.

1. En el cuadro de diálogo **Verificar dominio**, en **¿Qué tipo de certificado planea usar con este dominio?**, seleccione una de las siguientes opciones:

   | Opción de tipo de certificado | Descripción |
   | --- | --- |
   | Certificado SSL administrado por Adobe (DV) | Seleccione este tipo de certificado si desea utilizar un certificado DV (validación de dominio). Esta opción es ideal para la mayoría de los casos, ya que proporciona una validación básica del dominio. Adobe administra y renueva el certificado automáticamente. |
   | Certificado SSL administrado por el cliente (OV/EV) | Seleccione este tipo de certificado si desea utilizar un certificado SSL EV/OV para proteger el dominio. Esta opción ofrece una seguridad mejorada con OV (validación de organización) o EV (validación extendida). Utilícelo si se requiere una verificación más estricta, niveles de confianza más altos o control personalizado de los certificados. |

1. En el cuadro de diálogo **Verificar dominio**, en función del tipo de certificado seleccionado, realice una de las siguientes acciones:

   | Si seleccionó el tipo de certificado | Descripción |
   | --- | ---  |
   | Certificado administrado por Adobe | a. Complete los [pasos de certificado administrado por Adobe](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps). Cuando complete los pasos del cuadro de diálogo **Verificar dominio**, haga clic en **Verificar**.<ul><li>La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.</li><li>Cloud Manager finalmente verifica la propiedad del nombre de dominio y actualiza el estado en la tabla **Configuración de dominio**. Consulte [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.</li>![Verificar el estado del dominio](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b. Ya está listo para [agregar un certificado SSL administrado por Adobe (DV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert).</li></ul> |
   | Certificado administrado por el cliente | a. Haga clic en **Aceptar**.<br>b. Ya está listo para [agregar un certificado SSL administrado por el cliente (OV/EV)](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert).<br>Después de agregar el certificado, el nombre de dominio se marca como verificado en la tabla **Configuración de dominio**. Consulte [Comprobar el estado del nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.</li></ul><br>![Verificar el dominio de un certificado EV/OV administrado por el cliente](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## Eliminar un nombre de dominio personalizado de todos los entornos asociados {#deleting}

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede usar Cloud Manager para eliminar un nombre de dominio personalizado.

### Eliminar un nombre de dominio personalizado de todos los entornos asociados {#delete-cdn-all}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la página **Configuración de dominio** desde la pantalla **Información general**.

1. Identifique la fila del nombre de dominio personalizado que desee eliminar.

1. Haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho de la fila.

1. Seleccione **Eliminar**.

1. Confirme el envío.


### Eliminar un nombre de dominio personalizado de un entorno específico {#delete-cdn-specific}

>[!WARNING]
>
>Quite los registros DNS del dominio con su proveedor DNS *antes* de eliminar el dominio en Cloud Manager. Las entradas DNS abandonadas (colgadas) pueden secuestrarse y suponer un riesgo para la seguridad.

**Para eliminar un nombre de dominio personalizado de un entorno específico:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. En la página **Entornos**, vaya a una pantalla de detalles del entorno que le interese.

1. En la tabla Asignaciones de dominio, identifique la fila del nombre de dominio personalizado que desee eliminar.

1. Haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho de la fila.

1. Seleccione **Eliminar**.

1. Confirme el envío.
