---
title: Administrar certificados SSL
description: Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL y cómo editarlos, reemplazarlos, actualizarlos y eliminarlos.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: bf903736e256bb9275bad6c0271b31b8dbdec625
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 13%

---


# Administrar certificados SSL {#managing-ssl-certificates}

Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL y cómo editarlos, reemplazarlos, actualizarlos y eliminarlos.

## Comprobar el estado de los certificados SSL {#checking-status-an-ssl-certificate}

Cloud Manager ofrece una descripción general del estado de todos los certificados del programa.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.
1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

La página **Certificados SSL** proporciona el estado de sus certificados SSL.

| Estado del certificado SSL | Descripción |
| --- | --- |
| Verde | El certificado es válido durante al menos 14 días desde la fecha actual. |
| Naranja | El certificado caducará en menos de 14 días.<br>· Asegúrese de que tiene un plan para renovar su certificado y reemplazarlo mediante la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio.<br>· Cloud Manager envía notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado. |
| Rojo | El certificado SSL ha caducado.<br>Ver [Actualizar un certificado SSL administrado por un cliente caducado](#update-ssl-certificate) o [Eliminar un certificado SSL](#deleting-an-ssl-certificate). |

## Actualizar un certificado SSL administrado por el cliente caducado {#update-ssl-certificate}

Cuando un certificado administrado por el cliente caduca, cualquier dominio que esté en uso con el certificado caducado ya no funciona. La actualización de los certificados garantiza que el dominio funcionará como se desea.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

>[!IMPORTANT]
>
>Al agregar o actualizar un certificado SSL, no incluya el nuevo certificado en la cadena de certificados. Si se incluye, se evita que la carga se complete correctamente.

**Para actualizar un certificado SSL administrado por el cliente caducado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.
1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.
1. En la fila del certificado administrado por el cliente caducado que desea actualizar, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho y, a continuación, haga clic en **Ver y actualizar**.

   ![Actualizar una certificación SSL administrada por el cliente caducada](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. En el cuadro de diálogo **Ver y actualizar certificado SSL**, haga lo siguiente:

   * (Opcional) En el campo **Nombre del certificado**, escriba un nombre nuevo.
   * En el campo **Certificado**, pegue la nueva clave de contenido del certificado.
   * En el campo **Clave privada**, actualice este campo solo si ha realizado cambios en el certificado.
   * En el campo **Cadena de certificados** (o cadena de confianza), pegue la cadena de certificados.

1. Haga clic en **Actualizar** para guardar los cambios y que se apliquen automáticamente.


>[!NOTE]
>
>Si dos o más certificados SAN cubren la misma entrada de dominio SAN y uno de ellos se actualiza, el sistema instala el certificado actualizado para el dominio.
>
>Consulte [Solucionar problemas de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md#wrong-san-cert) para obtener más información.

## Reemplazar un certificado SSL administrado por el cliente caducado {#replace-ssl-certificate}

Siga los mismos pasos que se describen en [Actualizar un certificado SSL caducado](#update-ssl-certificate) para reemplazar un certificado SSL caducado administrado por el cliente.

## Cambiar el nombre de un certificado SSL administrado por Adobe (#rename-an-ssl-certificate)

A continuación se indican algunas razones por las que puede que desee cambiar el nombre de un certificado SSL:

* **Organización mejorada**: Cambiar el nombre del certificado puede ayudar a aclarar su propósito, como identificar para qué entorno (por ejemplo, ensayo, producción) o dominio es.
* **Evitar confusiones**: si administra varios certificados, un nombre descriptivo y claro puede ayudar a evitar errores, como aplicar el certificado incorrecto al dominio incorrecto.
* **Cumplimiento y auditoría**: Puede que sea más fácil realizar el seguimiento de los certificados con nombres correctos por motivos de seguridad y auditoría.

**Para cambiar el nombre de un certificado SSL administrado por Adobe:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.

1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

1. En la página **Certificados SSL**, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuyo certificado SSL **administrado por Adobe** desea cambiar de nombre.

1. En el menú desplegable, haga clic en **Cambiar nombre**.

1. En el cuadro de diálogo **Cambiar nombre de certificado DV**, en el campo de texto **Nombre del certificado**, escriba el nuevo nombre del certificado.

1. Haga clic en **Cambiar nombre**.


## Eliminar un certificado SSL {#deleting-an-ssl-certificate}

La eliminación de certificados SSL administrados por Adobe o por el cliente de Cloud Manager es una acción permanente que no se puede deshacer. Como práctica recomendada, Adobe recomienda guardar los archivos SSL localmente antes de eliminarlos en Cloud Manager.

>[!NOTE]
>
>No puede eliminar un certificado SSL administrado por Adobe que tenga uno o varios dominios activos asociados a él. Todos los dominios activos asociados deben eliminarse antes de eliminar el certificado SSL. Consulte [Administrar nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para eliminar un certificado SSL:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.

1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

1. En la página Certificados SSL, en la fila de la tabla del certificado que desea eliminar, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) en el extremo derecho y, a continuación, haga clic en **Eliminar**.

   Si **Delete** tiene un icono de información como se ve en la siguiente imagen, consulta la nota anterior.

   ![Botón Eliminar con icono de información](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. En el cuadro de diálogo **Eliminar certificado SSL**, haga clic en **Eliminar** para confirmar la eliminación.

1. Ejecute la canalización para anular la implementación del certificado eliminado.


## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si ya tiene una configuración de CDN para su certificado SSL, la página **Certificados SSL** muestra un mensaje informativo. Le anima a añadir estas configuraciones a través de la interfaz de usuario para que sean visibles y manejables en Cloud Manager.

El mensaje desaparece después de migrar todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre uno y dos días hábiles en desaparecer.

Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

También se ha proporcionado un mensaje similar en las páginas **Lista de permitidos IP** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para Listas de permitidos IP o nombres de dominio personalizados.
