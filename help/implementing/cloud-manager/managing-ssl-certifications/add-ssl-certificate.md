---
title: Añadir un certificado SSL
description: Obtenga información sobre cómo agregar su propio certificado SSL o un certificado DV (validación de dominio) administrado por Adobe mediante las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 493c5729c3107f151685a243006b17196b74c1bd
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---


# Añadir un certificado SSL {#add-ssl-cert}

Obtenga información sobre cómo agregar su propio certificado SSL o un certificado DV (validación de dominio) administrado por Adobe mediante Cloud

>[!TIP]
>
>Un certificado puede tardar unos días en aprovisionarse. Como tal, Adobe recomienda que, si proporciona su propio certificado, se aprovisione con mucha antelación a cualquier fecha límite o fecha de lanzamiento.

## Requisitos previos {#prerequisites}

* Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para agregar un certificado.
* Si va a instalar su propio certificado, asegúrese de revisar **Requisitos de certificado** en [Introducción a la administración de certificados SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)

## Adición de un certificado SSL {#add-certificate}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.
1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Agregando un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Cerca de la esquina superior derecha de la página Certificados SSL, haga clic en **Agregar certificado SSL**.

1. En el cuadro de diálogo **Agregar certificado SSL**, en función de [su caso de uso particular](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), realice una de las siguientes acciones:

   | | Caso de uso | Etapas |
   | --- | --- | --- |
   | 1 | **Agregar un certificado administrado por Adobe (DV)** | **Para agregar un certificado administrado por Adobe (DV):**<br> a. En el cuadro de diálogo **Agregar certificado SSL**, seleccione el tipo de certificado **Administrado por Adobe (DV)**.<br>![Agregar certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. En el campo **Nombre del certificado**, escriba un nombre que desee asociar con el certificado.<br>c. En la lista desplegable **Seleccionar dominios**, seleccione uno o varios dominios que desee asociar con el certificado DV.<br>¿No hay dominios que seleccionar? Si es así, significa que debe agregar un dominio personalizado. Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Cuando termine de agregar un nombre de dominio personalizado, vuelva a este tema y comience de nuevo en el paso 1.<br>d. Continúe con el paso 7. |
   | 2 | **Agregar un certificado administrado por el cliente (OV/EV)** | **Para agregar un certificado administrado por el cliente (OV/EV):**<br> a. En el cuadro de diálogo **Agregar certificado SSL**, seleccione el tipo de certificado **Administrado por el cliente (OV/EV)**.<br>b. En el campo **Nombre del certificado**, escriba un nombre para el certificado. Este campo es solo informativo y puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.<br>c. En los campos **Certificado**, **Clave privada** y **Cadena de certificados**, pegue los valores necesarios en sus respectivos campos.<br>![Cuadro de diálogo Agregar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Se muestran todos los errores detectados en los valores. Para poder guardar el certificado, debe corregir todos los errores. Consulte [Errores de certificado](#certificate-errors) para obtener más información sobre la solución de problemas de errores comunes.<br>d. Continúe con el paso 7. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Guardar**.

Una vez emitido correctamente el certificado, se mostrará con una marca de verificación verde en la tabla **Certificados SSL**.

Ahora ha agregado un certificado SSL de trabajo para el proyecto. Este paso suele ser el primero en configurar un nombre de dominio personalizado.

* Para configurar un nombre de dominio personalizado, consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Para obtener más información sobre cómo actualizar y administrar los certificados SSL en Cloud Manager, consulte [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

>[!TIP]
>
>Si tiene problemas para agregar o administrar sus certificados, consulte el documento [Solucionar errores de certificados SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)
