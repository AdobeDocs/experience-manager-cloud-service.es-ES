---
title: Administración de certificados SSL
description: Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL y cómo editarlos, reemplazarlos, actualizarlos y eliminarlos.
exl-id: ad6170f4-93bd-4bac-9c54-63c35a0d4f06
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 82%

---


# Administración de certificados SSL {#managing-ssl-certificates}

Obtenga información sobre cómo utilizar Cloud Manager para comprobar el estado de los certificados SSL y cómo editarlos, reemplazarlos, actualizarlos y eliminarlos.

## Comprobar el estado de los certificados SSL {#checking-status-an-ssl-certificate}

El estado de los certificados SSL se puede entender de un vistazo desde la página de certificados SSL.

* **Verde**: Este estado indica que el certificado es válido durante al menos 60 días desde la fecha actual.

* **Naranja**: Este estado indica que el certificado caducará en menos de 60 días.
   * Es hora de asegurarse de que tiene un plan para renovar su certificado y reemplazarlo a través de la interfaz de usuario de Cloud Manager para evitar posibles interrupciones de acceso al sitio.
   * Cloud Manager enviará notificaciones regulares en la interfaz de usuario para avisarle de una caducidad inminente del certificado.

* **Rojo**: Este estado indica que el certificado SSL ha caducado.

## Actualizar un certificado SSL {#update-ssl-certificate}

Cuando un certificado caduca, cualquier dominio que esté en uso con el certificado caducado dejará de funcionar. La actualización de los certificados mediante los siguientes pasos garantiza que el dominio funcionará como se quiere.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta la pantalla **Certificados SSL** de la pantalla **Entornos**.
1. Puede ver una tabla con una fila para cada certificado SSL que se haya instalado correctamente en el programa. Haga clic en el botón de los tres puntos del extremo derecho de la fila del certificado que desea actualizar y seleccione **Ver y actualizar**.
1. Los detalles del certificado se muestran y se pueden actualizar.
1. Ejecute la canalización para implementar el certificado actualizado.

>[!NOTE]
>
>El usuario debe ser miembro de la función **Propietario del negocio** o **Administrador de implementación** para actualizar un certificado SSL en Cloud Manager.

## Reemplazar un certificado SSL {#replace-ssl-certificate}

Un certificado SSL se puede reemplazar si sigue los pasos descritos en la sección [Actualizar un certificado SSL.](#update-ssl-certificate)

## Eliminar un certificado SSL {#deleting-an-ssl-certificate}

La eliminación de certificados de Cloud Manager es una acción permanente que no se puede deshacer. Como práctica recomendada, Adobe recomienda guardar los archivos SSL localmente antes de eliminarlos en Cloud Manager.

Cloud Manager no le permitirá eliminar un certificado SSL que tenga uno o varios dominios asociados a él. Todos los dominios asociados deben eliminarse antes de eliminar el certificado SSL. Consulte [Administración de nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) para obtener más información.

Siga estos pasos para eliminar un certificado SSL.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Navegue hasta la pantalla **Certificados SSL** de la pantalla **Entornos**.
1. Puede ver una tabla con una fila para cada certificado SSL que se haya instalado correctamente en el programa. Haga clic en los puntos suspensivos en el extremo derecho de la fila del certificado que desea eliminar y seleccione **Eliminar**.
1. Confirme la eliminación en el cuadro de diálogo **Eliminar certificado SSL**.
1. Ejecute la canalización para anular la implementación del certificado eliminado.

>[!NOTE]
>
>El usuario debe ser miembro de la función **Propietario del negocio** o **Administrador de implementación** para eliminar un certificado SSL en Cloud Manager.

## Configuraciones de CDN preexistentes {#pre-existing-cdn}

Si tiene una configuración de CDN preexistente para su certificado SSL, habrá un mensaje informativo en la página **Certificados SSL** que le anima a agregar estas configuraciones a través de la interfaz de usuario para que sean visibles y configurables en Cloud Manager.

El mensaje desaparece una vez que se migran todas las configuraciones de entorno preexistentes mediante la interfaz de usuario. El mensaje puede tardar entre 1 y 2 días hábiles en desaparecer.

Consulte [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) para obtener más información.

También se proporciona un mensaje similar en las páginas **Lista de IP permitidas** y **Entornos** para entornos que tienen configuraciones de CDN preexistentes para listas de IP permitidas o nombres de dominio personalizados.
