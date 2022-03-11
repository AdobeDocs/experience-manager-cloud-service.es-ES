---
title: 'Eliminación de un certificado SSL: administración de certificados SSL'
description: 'Eliminación de un certificado SSL: administración de certificados SSL'
exl-id: 43f66871-cca4-4709-95d0-68aa715c0da2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---

# Eliminación de un certificado SSL {#deleting-an-ssl-certificate}

>[!IMPORTANT]
>La eliminación de certificados de Cloud Manager es una acción permanente que no se puede deshacer. Una práctica recomendada es guardar los archivos SSL necesarios localmente antes de eliminarlos en la interfaz de usuario de Cloud Manager.

Un usuario debe estar en la función Propietario empresarial o Administrador de implementación para eliminar un certificado SSL en Cloud Manager. Cloud Manager no le permitirá eliminar un certificado SSL que tenga uno o varios dominios asociados a él.  Todos los dominios asociados deben eliminarse antes de eliminar el certificado SSL. Consulte [Eliminación de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/delete-custom-domain-name.md) para obtener más información.

Siga los pasos a continuación para eliminar un certificado SSL:

1. Vaya a la **Certificados SSL** de la **Entornos** página.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
1. Identifique la fila en la que aparece el nombre del certificado SSL que desea eliminar.
1. Seleccione el **...** del extremo derecho de la fila.
1. Select **Eliminar**.
   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-delete01.png)
1. Confirme el envío desde **Eliminar certificado SSL** para abrir el Navegador.
