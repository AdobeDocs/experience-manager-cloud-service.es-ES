---
title: Edición de programas
description: Obtenga información sobre cómo editar los programas de producción y de zonas protegidas para ajustar sus opciones después de crearlas.
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: d5c87853bcc10587c97710e69b350bb9ebe509ae
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---


# Editar programas {#editing-programs}

Para administrar y editar programas, empieza en la consola [**Mis programas**](/help/implementing/cloud-manager/navigation.md). La página **Mis programas** proporciona una descripción general de todos los programas a los que tiene acceso. Al seleccionar un programa individual, la página **Resumen del programa** proporciona una descripción general de los detalles del programa.

Desde la **Descripción general del programa**, los usuarios con los permisos necesarios pueden editar [programas de producción creados en su organización](creating-production-programs.md) y [programas de zonas protegidas creados en su organización](creating-sandbox-programs.md). Al editar un programa, puede hacer lo siguiente:


* Habilite o deshabilite la protección **WAF-DDOS** en la ficha **Seguridad**.
* Agregue la solución Sites a un programa existente con Assets y agregue Assets a un programa existente con Sites.
* Eliminar Sites o Assets de un programa existente que tenga ambos y Assets.
* Agregar un derecho de solución no utilizado a un programa existente o crear un nuevo programa.
* Marcar programas de producción para su eliminación.
* Eliminar programas de zona protegida.

## Permisos {#permissions}

Debe tener la función **Propietario del negocio** para editar programas, eliminar programas de zona protegida, marcar programas de producción para su eliminación y acceder al tablero de licencias.

## Editar un programa {#editing}

Cada vez que se edita un programa, incluida la adición o eliminación de una solución o complemento, esos cambios surten efecto después de la siguiente implementación.

**Para editar un programa:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización adecuada.
1. En la página **Mis programas**, haga clic en el programa que desee editar.
1. Cerca de la esquina superior izquierda de la página, haga clic en el nombre del programa y, a continuación, seleccione **Editar programa**.

   ![Editar opción de programa en el menú desplegable Programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program.png)

1. En el cuadro de diálogo **Editar programa**, utilice las fichas para establecer las distintas opciones que desee.

   ![Pestaña General](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/edit-program-dialog-box.png)

   Las opciones disponibles para editar el programa son las mismas para la creación de programas.

   * Puede configurar si un nivel de publicación está aprovisionado para nuevos entornos (Beta). Consulte [Nivel de publicación flexible (Beta)](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#flexible-publish-tier).
   * Consulte [Crear programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) y [Crear programas de espacio aislado](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) para obtener más información sobre las opciones individuales.
   * Para habilitar o deshabilitar el firewall de aplicaciones web (WAF) en cualquier momento, seleccione la ficha **Seguridad** y, a continuación, active o desactive la casilla de verificación **Protección WAF-DDOS**. Si las reglas de WAF tienen licencia pero esta casilla de verificación no está marcada, la función no está activa y no se aplican sus protecciones. Para obtener más información, consulte [Reglas de filtro de tráfico, incluidas las reglas de WAF](/help/security/traffic-filter-rules-including-waf.md).

     >[!NOTE]
     >Para confirmar que la función está activa, revise los [registros de CDN](//help/security/traffic-filter-rules-including-waf.md#cdn-logs) una vez que el tráfico fluya al sitio. Busque entradas de registro que incluyan una propiedad `rules` que contenga un atributo `waf`. Por ejemplo,
     >
     >`"rules": "waf=SQLI"`
     >
     >Este atributo aparece una vez que WAF está activo, incluso antes de que se implementen las reglas de WAF.

     ![Cuadro de diálogo Editar programa que muestra las opciones de la ficha Seguridad](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cmk-edit-programs.png)

   * En la misma ficha **Seguridad**, puede habilitar **Claves administradas por el cliente** para un programa existente.

     CMK no se puede deshabilitar después de la activación. Después de habilitar CMK, configure las claves de cifrado en Experience Hub. Consulte [Configurar CMK en Experience Hub](#configure-cmk-experience-hub).

   * [Hay opciones adicionales](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) disponibles para su programa de producción en función de los derechos de su organización.

1. Haga clic en **Actualizar** para guardar los cambios.

## Configuración de CMK en Experience Hub {#configure-cmk-experience-hub}

Una vez habilitado CMK para un programa, Cloud Manager proporciona un vínculo directo a la página de configuración de CMK en Experience Hub para que pueda configurar su
claves de cifrado sin salir del programa.

Una vez que CMK se ha configurado correctamente para un entorno, la página Detalles del entorno muestra un distintivo de estado **Configuración de CMK**. Si CMK está habilitado para el programa pero aún no se ha configurado para un entorno específico, el distintivo no aparece en la página de detalles de ese entorno.

**Para configurar CMK en Experience Hub:**

1. En la página **Mis programas**, busque la tarjeta de programa con CMK habilitado.
2. Haga clic en ![Puntos suspensivos - icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haga clic en **Configurar CMK**.

   ![Tarjeta de programa que muestra el icono CMK para indicar que está habilitado y luego la opción Configurar CMK del menú de los tres puntos](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cmk-configure-edit-program-dlg.png)

   Experience Hub abre la página de configuración de CMK, donde puede proporcionar los detalles de Azure Key Vault y la información de clave de cifrado.

   Para ver los pasos de configuración completos, consulte [Configuración de claves administradas por el cliente para AEM as a Cloud Service](/help/security/customer-managed-keys.md).

## Marcar un programa de producción para su eliminación {#delete-production-program}

La eliminación de un programa de producción es un proceso de dos fases. Un Propietario del negocio marca el programa para su eliminación, lo que déclencheur un periodo de validación y retirada. A continuación, el programa se elimina permanentemente después de que haya transcurrido el período de eliminación.

Cuando se marca un programa de producción para su eliminación, ocurre lo siguiente:

* El crédito asociado con el programa de producción se devuelve al cliente.
* Se eliminan todos los entornos que pertenecen al programa de producción.

Antes de iniciar la marcación para eliminación, el sistema valida si el programa de producción es apto para eliminación. Si el marcado falla, el programa de producción pasa a un estado `Failed to mark for deletion` en su lugar.

>[!NOTE]
>
>Los programas de zona protegida no se ven afectados por este proceso. Para eliminar un programa de zona protegida, consulte [Eliminar un programa de zona protegida](#delete-sandbox-program).

**Para marcar un programa de producción para su eliminación:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización adecuada.
1. En la página **Mis programas**, para el programa de producción que desea marcar para su eliminación, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haga clic en **Eliminar programa**.

   ![Seleccionar Eliminar programa de la lista desplegable de un programa de producción ](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete1.png)*Ejemplo de programa de producción visto arriba es solo con fines ilustrativos.*

1. En el cuadro de diálogo **Marcar programa de producción para eliminación**, revise la advertencia que enumera los recursos conectados al programa, incluidos los entornos de producción, fase y desarrollo.

   ![Eliminar cuadro de diálogo del programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2.png)


   >[!NOTE]
   >
   >Si el programa de producción tiene recursos de bloqueo, como entornos que se están actualizando en este momento, el botón **Marcar para eliminación** está deshabilitado. Espere a que se desbloqueen todos los recursos del programa para poder marcar el programa para su eliminación.
   >
   >![El cuadro de diálogo Marcar programa de producción para eliminación que muestra que el programa no se puede eliminar porque tiene recursos de bloqueo](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete2b.png)


1. Para confirmar, escriba el nombre del programa tal como se muestra en el cuadro de diálogo y, a continuación, haga clic en **Marcar para eliminación**.

   Después de la confirmación, el programa de producción muestra el estado **Marcando para eliminación** mientras se ejecuta el proceso.

   ![Marcando el estado de eliminación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete3.png)

   Cuando se complete, la tarjeta del programa de producción se actualizará a **Marcado para eliminación** con un distintivo de alerta asociado.

   ![Marcado para eliminación con distintivo de alerta asociado](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete4.png)

1. Haga clic en el distintivo Alerta en la tarjeta del programa de producción para mostrar la fecha de eliminación permanente programada.

   ![Visualización de la fecha de eliminación permanente programada del programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-markfordelete5.png)

   Una vez transcurrido el período de eliminación, el programa se elimina de forma permanente y no se puede restaurar.

### Desmarcar un programa de producción de la eliminación {#unmark-from-deletion}

Puede restaurar un programa de producción que se haya *marcado* para su eliminación, siempre y cuando la eliminación permanente aún no se haya producido.

>[!IMPORTANT]
>
>La restauración de un programa de producción marcado para su eliminación requiere que el cliente tenga créditos disponibles.

**Para quitar la marca de eliminación de un programa de producción:**

1. En la página **Mis programas**, busque la tarjeta del programa de producción que muestra **Marcado para eliminación**.

1. En la tarjeta del programa de producción, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y, a continuación, haga clic en **Desmarcar para eliminación**.

   ![Desmarcando la fecha de eliminación permanente programada del programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/production-program-unmarkfordelete6.png)

   El programa de producción no está marcado para su eliminación.

## Eliminar un programa de zona protegida {#delete-sandbox-program}

Al eliminar un programa de zona protegida se eliminan todos los entornos y canalizaciones asociados a él.

>[!TIP]
>
>Los usuarios con el rol de **Propietario del negocio** o **Administrador de implementación** pueden eliminar sus entornos de producción y ensayo en lugar de todo el programa de zona protegida.

**Para eliminar un programa de zona protegida:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización adecuada.

1. En la página **[Mis programas](#my-programs)**, haga clic en el programa de zona protegida que desee editar para mostrar sus detalles.

1. Haga clic en el nombre del programa de zona protegida en la parte superior izquierda de la página y seleccione **Eliminar programa**.

   ![Opción Eliminar programa](assets/delete-sandbox1.png)

También puede hacer clic en el ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) de la tarjeta del programa de zona protegida en la página de información general de Cloud Manager y seleccionar **Eliminar programa**.

![Eliminar zona protegida de la tarjeta de programa](assets/delete-sandbox2.png)
