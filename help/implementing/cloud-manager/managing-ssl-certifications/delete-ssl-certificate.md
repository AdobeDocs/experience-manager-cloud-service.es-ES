---
title: Eliminación de un certificado SSL - Administración de certificados SSL
description: Eliminación de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: 99eb33c3c42094f787d853871aee3a3607856316
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---


# Eliminación de un certificado SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>La eliminación de certificados del Administrador de nube es una acción permanente que no se puede deshacer. Lo mejor es guardar localmente los archivos SSL necesarios antes de eliminarlos en la interfaz de usuario de Cloud Manager.

Un usuario debe estar en la función Propietario de la empresa o Administrador de implementación para eliminar un certificado SSL en Cloud Manager. Cloud Manager no le permitirá eliminar un certificado SSL que tenga uno o varios dominios asociados a él.  Todos los dominios asociados deben eliminarse antes de eliminar el certificado SSL. Consulte [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para obtener más información.

Siga los pasos a continuación para eliminar un certificado SSL:

1. Acceda a la pantalla **Certificados SSL** desde la página **Entornos**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identifique la fila en la que aparece el nombre del certificado SSL que desea eliminar.
1. Seleccione **...** desde el extremo derecho de la fila.
1. Seleccione **Eliminar**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Confirme el envío desde el cuadro de diálogo **Eliminar certificado SSL**.
