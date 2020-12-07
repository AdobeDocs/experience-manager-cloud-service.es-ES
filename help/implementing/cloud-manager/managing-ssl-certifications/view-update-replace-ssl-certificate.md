---
title: 'Visualización de la actualización y sustitución de un certificado SSL - Administración de SSL '
description: Visualización de la actualización y sustitución de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: e5305efad061ae0b06ecb16433fccd5e97f978f3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Visualización de la actualización y reemplazo de un certificado SSL {#view-update-replace-ssl-certificate}

## Visualización y actualización de un certificado SSL {#view-update}

Cuándo utilizar esta opción en la interfaz de usuario del Administrador de nube:

* Un certificado existente está a punto de caducar. El usuario ha renovado el certificado con el proveedor de certificados y desea reemplazar el certificado existente que está a punto de caducar. Nota Solo los usuarios con los permisos adecuados pueden realizar actualizaciones.
* Utilice el menú Vista y actualización para simplemente vista los detalles del certificado SSL.
* También puede cambiar el nombre que se ha utilizado para hacer referencia a un certificado desde esta pantalla.
   >[!NOTE]
   >Solo los usuarios con los permisos adecuados pueden realizar actualizaciones.


## Actualizando un certificado SSL a punto de caducar {#update-ssl-certificate}


>[!NOTE]
>Cuando un certificado caduca, ya no funcionará ningún dominio que esté en uso con el certificado caducado. Para actualizar un certificado caducado, debe seguir los pasos que se indican a continuación. Esto garantizará que su dominio siga funcionando como desee. Para añadir un nuevo certificado, será necesario actualizar el nombre de dominio personalizado con el nuevo certificado antes de que los dominios funcionen como se desee. Consulte Vista y actualización del nombre de dominio personalizado para obtener más información

Siga los pasos a continuación para actualizar un certificado SSL:

>[!NOTE]
>Un usuario debe estar en la función Propietario de la empresa o Administrador de implementación para actualizar un certificado SSL en Cloud Manager.

1. Acceda a la pantalla Certificados SSL desde la página **Entornos**.
1. Verá una tabla con una fila para cada certificado SSL que se haya instalado correctamente en el programa.
1. Se puede acceder a las opciones de menú de cada fila seleccionando los tres botones situados en el extremo derecho de la fila de interés. Desde aquí, seleccione Vista y actualización. Los detalles del certificado se pueden ver desde aquí, como se ilustra en el ejemplo siguiente.
1. Para reemplazar el certificado, pegue el nuevo contenido en los campos de entrada correspondientes y guárdelo. Tendrá que solucionar cualquier error que pueda surgir. Consulte la sección Errores de certificado para solucionar los problemas más comunes.