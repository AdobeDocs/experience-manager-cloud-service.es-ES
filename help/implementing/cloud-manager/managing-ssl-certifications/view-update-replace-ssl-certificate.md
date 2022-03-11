---
title: 'Visualización de la actualización y sustitución de un certificado SSL - Administración de SSL '
description: Visualización de la actualización y sustitución de un certificado SSL - Administración de certificados SSL
exl-id: 662494b1-a710-4822-97ef-057043ef89ba
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# Visualización, actualización y sustitución de un certificado SSL  {#view-update-replace-ssl-certificate}

## Visualización y actualización de un certificado SSL {#view-update}

Cuándo utilizar estas opciones en la interfaz de usuario de Cloud Manager:

* Un certificado existente está a punto de caducar. El usuario ha renovado el certificado con el proveedor de certificados y desea reemplazar el certificado existente que está a punto de caducar. Nota Solo los usuarios con los permisos adecuados pueden realizar actualizaciones.
* Utilice la variable **Ver y actualizar** para ver los detalles del certificado SSL.
* También puede cambiar el nombre que se ha utilizado para hacer referencia a un certificado desde esta pantalla.
* Solo los usuarios con los permisos adecuados pueden realizar actualizaciones.


## Actualización de un certificado SSL a punto de caducar {#update-ssl-certificate}

Cuando un certificado caduca, cualquier dominio que esté en uso con el certificado caducado dejará de funcionar. Para actualizar un certificado caducado, se deben seguir los pasos que se indican a continuación. Esto garantizará que su dominio siga funcionando como desee. Para agregar un nuevo certificado, será necesario actualizar el nombre de dominio personalizado con el nuevo certificado antes de que los dominios funcionen como desee. Consulte [Visualización, actualización y reemplazo de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md) para obtener más información.

Siga los pasos a continuación para actualizar un certificado SSL:

>[!NOTE]
>Un usuario debe estar en la función Propietario empresarial o Administrador de implementación para actualizar un certificado SSL en Cloud Manager.

1. Vaya a la pantalla Certificados SSL desde la página **Entornos** página.
1. Verá una tabla con una fila para cada certificado SSL que se haya instalado correctamente en su programa.
1. Se puede acceder a las opciones de menú de cada fila seleccionando los tres botones situados en el extremo derecho de la fila de interés.
1. Select **Ver y actualizar**. Los detalles del certificado se pueden ver desde aquí.

## Sustitución de un certificado SSL {#replace-ssl-certificate}

Siga los pasos a continuación para reemplazar un certificado SSL:

1. Vaya a la pantalla Certificados SSL desde la página **Entornos** página.
1. Verá una tabla con una fila para cada certificado SSL que se haya instalado correctamente en su programa.
1. Se puede acceder a las opciones de menú de cada fila seleccionando los tres botones situados en el extremo derecho de la fila de interés.
1. Select **Ver y actualizar**.
1. Para reemplazar el certificado, pegue el nuevo contenido en los campos de entrada correspondientes y haga clic en **Guardar**. Deberá corregir cualquier error que pueda surgir.

   Consulte [Errores de certificado](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) para solucionar los problemas más comunes.
