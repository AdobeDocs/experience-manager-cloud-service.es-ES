---
title: Administrar certificados SSL
description: Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL y cómo editarlos, reemplazarlos, actualizarlos y eliminarlos.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 16%

---


# Administrar certificados SSL {#managing-ssl-certificates}

Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL administrados por el Adobe y por el cliente, y cómo eliminarlos. Para los certificados administrados por el cliente, también puede editarlos y actualizarlos (reemplazarlos).

## Comprobar el estado de los certificados SSL {#checking-status-an-ssl-certificate}

El estado de sus certificados SSL se puede entender de un vistazo desde la página **Certificados SSL**.

| Estado del certificado SSL | Descripción |
| --- | --- |
| Verde | El certificado es válido durante al menos 14 días desde la fecha actual. |
| Naranja | El certificado caducará en menos de 14 días.<br>· Asegúrese de que tiene un plan para renovar su certificado y reemplazarlo mediante la interfaz de usuario de Cloud Manager para evitar posibles interrupciones o accesos al sitio.<br>· Cloud Manager envía notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado. |
| Rojo | El certificado SSL ha caducado.<br>Consulte [Actualizar un certificado SSL administrado por el cliente y caducado](#update-ssl-certificate) o [Eliminar un certificado SSL](#deleting-an-ssl-certificate). |

## Actualizar un certificado SSL caducado y administrado por el cliente {#update-ssl-certificate}

Cuando un certificado administrado por el cliente caduca, cualquier dominio que esté en uso con el certificado caducado ya no funciona. La actualización de los certificados garantiza que el dominio funcionará como se desea.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para actualizar un certificado SSL caducado administrado por el cliente:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Desde la página **Información general**, vaya a la pantalla **Entornos**.
1. Desde la pantalla **Entornos**, vaya a la pantalla **Certificados SSL**.
1. En la fila del certificado administrado por el cliente caducado que desea actualizar, haga clic en los puntos suspensivos en el extremo derecho y, a continuación, seleccione **Ver y actualizar**.

   ![Actualizar una certificación SSL caducada administrada por el cliente](/help/implementing/cloud-manager/assets/ssl/ssl-cert-update.png)

1. En el cuadro de diálogo **Ver y actualizar certificado SSL**, haga lo siguiente:

   * (Opcional) En el campo **Nombre del certificado**, escriba un nombre nuevo.
   * En el campo **Certificado**, pegue la nueva clave de contenido del certificado.
   * En el campo **Clave privada**, actualice este campo solo si ha realizado cambios en el certificado.
   * En el campo **Cadena de certificados** (o cadena de confianza), pegue la cadena de certificados.

1. Haga clic en **Actualizar** para guardar los cambios y que se apliquen automáticamente.

## Reemplazar un certificado SSL caducado y administrado por el cliente {#replace-ssl-certificate}

Siga los mismos pasos que se describen en [Actualizar un certificado SSL caducado](#update-ssl-certificate) para reemplazar un certificado SSL caducado administrado por el cliente.

## Eliminar un certificado SSL {#deleting-an-ssl-certificate}

La eliminación de los certificados SSL administrados por el Adobe o por el cliente de Cloud Manager es una acción permanente que no se puede deshacer. Como práctica recomendada, Adobe recomienda guardar los archivos SSL localmente antes de eliminarlos en Cloud Manager.

>[!NOTE]
>
>No puede eliminar un certificado SSL administrado por Adobe que tenga uno o más dominios activos asociados a él. Todos los dominios activos asociados deben eliminarse antes de eliminar el certificado SSL. Consulte [Administrar nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para eliminar un certificado SSL:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Desde la página **Información general**, vaya a la pantalla **Entornos**.
1. Desde la pantalla **Entornos**, vaya a la pantalla **Certificados SSL**.
1. En la fila del certificado que desea eliminar, haga clic en los puntos suspensivos en el extremo derecho y, a continuación, seleccione **Eliminar**.
Si el botón Eliminar tiene un icono de información como se ve en la siguiente imagen, consulte la Nota anterior.

   ![Botón Eliminar con icono de información](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete-infoicon.png)

1. En el cuadro de diálogo **Eliminar certificado SSL**, haga clic en **Eliminar** para confirmar la eliminación.
1. Ejecute la canalización para anular la implementación del certificado eliminado.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si ya tiene una configuración de CDN para su certificado SSL, la página **Certificados SSL** muestra un mensaje informativo. Le anima a añadir estas configuraciones a través de la interfaz de usuario para que sean visibles y manejables en Cloud Manager.

El mensaje desaparece después de migrar todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

También se proporciona un mensaje similar en las páginas **Lista de IP permitidas** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para listas de IP permitidas o nombres de dominio personalizados.
