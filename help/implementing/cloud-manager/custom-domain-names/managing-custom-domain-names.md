---
title: Administrar los nombres de dominio personalizados
description: Aprenda a utilizar Cloud Manager para ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
source-git-commit: 955f4bb55434eeb1a429a1972714b71c5370de1e
workflow-type: ht
source-wordcount: '338'
ht-degree: 100%

---

# Administrar los nombres de dominio personalizados {#managing-custom-domain-names}

Cloud Manager le permite ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.

## Ver y actualizar {#view-and-update}

Utilice el menú **Ver y actualizar** para ver los detalles de cualquiera de sus nombres de dominio personalizados.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Identifique la fila del nombre de dominio personalizado que desee ver o actualizar.

1. Haga clic en el botón de los tres puntos del extremo derecho de la fila.

1. Seleccione la opción **Ver y actualizar**.

## Actualizar el certificado SSL de un nombre de dominio personalizado {#update-cert}

Puede seguir [los mismos pasos para ver y actualizar un nombre de dominio personalizado](#view-and-update) para actualizar el certificado SSL de un nombre de dominio personalizado.

>[!NOTE]
>
>El certificado SSL debe ser válido, [ya debe estar configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) y debe contener el nombre de dominio personalizado que está actualizando.

## Eliminación de un nombre de dominio personalizado {#deleting}

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede usar Cloud Manager para eliminar un nombre de dominio personalizado.

### Eliminar un nombre de dominio personalizado de todos los entornos asociados {#delete-cdn-all}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Navegue hasta la pantalla **Entornos** de la página **Información general**.

1. Navegue hasta la página **Configuración de dominio** desde la pantalla **Entornos**.

1. Identifique la fila del nombre de dominio personalizado que desee eliminar.

1. Haga clic en el botón de los tres puntos del extremo derecho de la fila.

1. Seleccione **Eliminar**.

   ![Eliminar nombres de dominio personalizados](/help/implementing/cloud-manager/assets/cdn/cdn-delete.png)

1. Confirme el envío.

### Eliminar un nombre de dominio personalizado de un entorno específico {#delete-cdn-specific}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. En la página **Entornos**, navegue hasta la pantalla de detalles del entorno que le interese.
1. En la tabla de nombres de dominio, identifique la fila del nombre de dominio personalizado que desee eliminar.
1. Haga clic en el botón de los tres puntos del extremo derecho de la fila.
1. Seleccione **Eliminar**.
1. Confirme el envío.
