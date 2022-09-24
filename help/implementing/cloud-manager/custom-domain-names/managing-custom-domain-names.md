---
title: Administración de nombres de dominio personalizados
description: Aprenda a utilizar Cloud Manager para ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 955f4bb55434eeb1a429a1972714b71c5370de1e
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 5%

---

# Administración de nombres de dominio personalizados {#managing-custom-domain-names}

Cloud Manager le permite ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.

## Ver y actualizar {#view-and-update}

Utilice la variable **Ver y actualizar** para ver los detalles de cualquiera de sus nombres de dominio personalizados.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Entornos** de la **Información general** página.

1. Identifique la fila del nombre de dominio personalizado que desee ver o actualizar.

1. Haga clic en el botón de puntos suspensivos en el extremo derecho de la fila.

1. Seleccione el **Ver y actualizar** .

## Actualización del certificado SSL del nombre de dominio personalizado {#update-cert}

Puede seguir [los mismos pasos para ver y actualizar un nombre de dominio personalizado](#view-and-update) para actualizar el certificado SSL de un nombre de dominio personalizado.

>[!NOTE]
>
>El certificado SSL debe ser válido, [ya configurado,](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) y contienen el nombre de dominio personalizado que está actualizando.

## Eliminación de un nombre de dominio personalizado {#deleting}

Un usuario con la variable **Propietario empresarial** o **Administrador de implementación** puede usar Cloud Manager para eliminar un nombre de dominio personalizado.

### Eliminación de un nombre de dominio personalizado de todos los entornos asociados {#delete-cdn-all}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a la **Entornos** de la **Información general** página.

1. Vaya a la **Configuración de dominio** desde la página **Entornos** en el Navegador.

1. Identifique la fila del nombre de dominio personalizado que desee eliminar.

1. Haga clic en el botón de puntos suspensivos en el extremo derecho de la fila.

1. Select **Eliminar**.

   ![Eliminación de nombres de dominio personalizados](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Confirme el envío.

### Eliminación de un nombre de dominio personalizado de un entorno específico {#delete-cdn-specific}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.
1. Vaya a la **Entornos** de la **Información general** página.
1. En el **Entornos** , vaya a la pantalla de detalles del entorno de interés.
1. En la tabla de nombres de dominio, identifique la fila del nombre de dominio personalizado que desee eliminar.
1. Haga clic en el botón de puntos suspensivos en el extremo derecho de la fila.
1. Select **Eliminar**.
1. Confirme el envío.
