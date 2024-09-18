---
title: Administrar los nombres de dominio personalizados
description: Aprenda a utilizar Cloud Manager para ver, actualizar, reemplazar y eliminar nombres de dominio personalizados.
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 34%

---


# Administrar nombres de dominio personalizados {#managing-custom-domain-names}

Cloud Manager permite editar, actualizar, reemplazar y eliminar nombres de dominio personalizados.

## Editar una configuración de nombre de dominio personalizada {#view-and-update}

En Adobe Cloud Manager, es posible que desee editar una configuración de nombre de dominio personalizado por los siguientes motivos:

* **Cambiar entornos**: Para aplicar la configuración correcta en función de si va a ofrecer contenido a los usuarios finales (Publish) o a los usuarios internos (Author).
* **Actualizaciones de seguridad**: Para actualizar a un certificado SSL más reciente con fines de cumplimiento o seguridad mejorados.
* **Cambiando la estrategia de implementación**: Para asegurarse de que se aplica el certificado SSL correcto a un entorno específico para un cifrado y acceso al sitio adecuados.

**Para editar una configuración de nombre de dominio personalizado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo.
1. Bajo el encabezado **Servicios**, haga clic en **Configuraciones de CDN**.
1. En la página **Configuraciones de CDN**, haga clic en los puntos suspensivos al final de una fila cuya CDN desee editar.
1. Haga clic en **Editar**.
1. En el cuadro de diálogo **Editar configuración de CDN**, haga lo siguiente:
   * En la lista desplegable **Nivel**, seleccione el nivel (Autor o Publish) que desee usar.
   * En la lista desplegable **certificado SSL**, seleccione el certificado SSL que desee usar.
1. Haga clic en **Actualizar**.


## Actualizar el certificado SSL de un nombre de dominio personalizado {#update-cert}

Puede seguir [los mismos pasos para ver y actualizar un nombre de dominio personalizado](#view-and-update) para actualizar el certificado SSL de un nombre de dominio personalizado.

>[!NOTE]
>
>El certificado SSL debe ser válido [ya configurado](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md) y contener el nombre de dominio personalizado que está actualizando.


## Eliminar un nombre de dominio personalizado {#deleting}

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede usar Cloud Manager para eliminar un nombre de dominio personalizado.

### Eliminar un nombre de dominio personalizado de todos los entornos asociados {#delete-cdn-all}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la página **Configuración de dominio** desde la pantalla **Información general**.

1. Identifique la fila del nombre de dominio personalizado que desee eliminar.

1. Haga clic en el botón de los tres puntos del extremo derecho de la fila.

1. Seleccione **Eliminar**.

1. Confirme el envío.


### Eliminar un nombre de dominio personalizado de un entorno específico {#delete-cdn-specific}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. En la página **Entornos**, vaya a una pantalla de detalles del entorno que le interese.
1. En la tabla de nombres de dominio, identifique la fila del nombre de dominio personalizado que desee eliminar.
1. Haga clic en el botón de los tres puntos del extremo derecho de la fila.
1. Seleccione **Eliminar**.
1. Confirme el envío.
