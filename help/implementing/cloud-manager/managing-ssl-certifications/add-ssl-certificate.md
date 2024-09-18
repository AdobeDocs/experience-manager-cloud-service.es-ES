---
title: Agregar un certificado SSL
description: Aprenda a añadir su propio certificado SSL o certificado DV (validación de dominio) con las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 9%

---


# Añadir un certificado SSL {#add-ssl-cert}

Obtenga información sobre cómo agregar un certificado SSL administrado por el cliente o un certificado DV (validación de dominio) administrado y generado por Adobe mediante las herramientas de autoservicio de Cloud Manager.

Consulte también [Solucionar errores de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).

## Añadir un certificado SSL {#adding-an-ssl-certificate}

Un certificado puede tardar unos días en aprovisionarse. Por ello, el Adobe recomienda que el certificado se aprovisione con bastante antelación a cualquier fecha límite o de lanzamiento.

Asegúrese de revisar **Requisitos de certificado** en [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements) para asegurarse de que AEM as a Cloud Service admite el certificado que desea agregar.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

>[!NOTE]
>
>Los clientes no pueden cargar certificados DV (validación de dominio).

**Para agregar un certificado SSL:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Desde la página **Información general**, vaya a la pantalla **Entornos**.

1. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Certificados SSL**. Si no ve el panel de navegación izquierdo como se ve en la siguiente imagen, es posible que tenga que hacer clic en el icono de hamburguesa en la esquina superior izquierda.

   ![Agregando un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Cerca de la esquina superior derecha de la página, haga clic en **Agregar certificado SSL**.

1. En el cuadro de diálogo **Agregar certificado SSL**, en función de [su caso de uso particular](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), realice una de las siguientes acciones:

   | | Caso de uso | Etapas |
   | --- | --- | --- |
   | 1 | **Agregar un certificado administrado por Adobe (DV)** | **Para agregar un certificado administrado por Adobe (DV):**<br> a. Seleccione el tipo de certificado **administrado por Adobe (DV)**.<br>![Agregar certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. En el campo **Nombre del certificado**, escriba un nombre que desee asociar con el certificado.<br>c. En la lista desplegable **Seleccionar dominios**, seleccione uno o varios dominios que desee asociar con el certificado DV.<br>¿No hay dominios que seleccionar? Si es así, significa que debe agregar un dominio personalizado. Consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Cuando termine de agregar un nombre de dominio personalizado, vuelva a este tema y comience de nuevo en el paso 1.<br>d. Continúe con el paso 7. |
   | 2 | **Agregar un certificado administrado por el cliente (OV/EV)** | **Para agregar un certificado administrado por el cliente (OV/EV):**<br> a. Seleccione el tipo de certificado **administrado por el cliente (OV/EV)**.<br>b. En el campo **Nombre del certificado**, escriba un nombre para el certificado. Este campo es solo informativo y puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.<br>c. En los campos **Certificado**, **Clave privada** y **Cadena de certificados**, pegue los valores necesarios en sus respectivos campos.<br>![Cuadro de diálogo Agregar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Se muestran todos los errores detectados en los valores. Para poder guardar el certificado, debe corregir todos los errores. Consulte [Errores de certificado](#certificate-errors) para obtener más información sobre la solución de problemas de errores comunes.<br>d. Continúe con el paso 7. |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Guardar**.

   Una vez emitido correctamente el certificado, muestra una marca de verificación verde en la tabla **Certificados SSL**.

Ahora ha agregado un certificado SSL de trabajo para el proyecto. Este paso suele ser el primero en configurar un nombre de dominio personalizado.

* Para configurar un nombre de dominio personalizado, consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Para obtener más información sobre cómo actualizar y administrar los certificados SSL en Cloud Manager, consulte [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

<!--
### Add a custom domain {#add-custom-domain}

Before you can add an Adobe generated and managed Domain Validated (DV) certificate, you must first add a custom domain. The process for doing so is nearly the same as detailed in [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) and [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). However, that functionality is now slightly expanded, as described below.

1. When adding a custom domain name, in the **Verify domain** dialog box, select an **Adobe managed certificate**.

    ![Choose Adobe-managed](assets/verify-domain-dialog.png)

1. In the **Verify domain** dialog box, add a CNAME verification record to your DNS.

    ![Add CNAME entry](assets/verify-domain-dialog-adobe-managed.png)

1. After the domain is created, click the ellipsis button in the list of domains and select **Verify** to verify the domain.

    ![Verify domain](assets/verify-domain.png) 

1. Resume the task [Add a DV certificate](#adding-an-ssl-certificate). -->


