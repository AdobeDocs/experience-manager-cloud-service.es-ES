---
title: Añadir un certificado SSL
description: Obtenga información sobre cómo agregar su propio certificado SSL o un certificado DV (validación de dominio) administrado por Adobe mediante las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 6%

---


# Añadir un certificado SSL {#add-ssl-cert}

Obtenga información sobre cómo agregar su propio certificado SSL o un certificado DV (validación de dominio) administrado por Adobe mediante Cloud

>[!NOTE]
>
>Si usa un certificado SSL administrado por el cliente (OV/EV) y un proveedor de CDN administrado por el cliente, puede omitir agregar un certificado SSL e ir directamente a [Agregar una asignación de dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) cuando esté listo.

El aprovisionamiento de un certificado puede tardar varios días. Por lo tanto, Adobe recomienda aprovisionar su propio certificado con mucha antelación a cualquier fecha límite o fecha de lanzamiento para evitar retrasos.

Para obtener más información sobre cómo actualizar y administrar los certificados SSL en Cloud Manager, consulte [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

Si tiene problemas para agregar o administrar sus certificados, consulte [Solucionar errores de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).


## Requisitos previos {#prerequisites}

* Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para agregar un certificado SSL.
* Si va a instalar su propio certificado, consulte **Requisitos de certificado** en [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).

## Elección del certificado SSL que se agregará {#which-ssl-to-add}

Después de [agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) en AEM Cloud Manager, el siguiente paso depende de si eligió usar un certificado SSL administrado por Adobe (DV) (recomendado) o un certificado SSL administrado por el cliente (OV/EV).

* **Para un certificado SSL administrado por Adobe (DV):**
   * El proceso de validación del dominio se realiza una vez que el dominio personalizado se agrega y verifica en Cloud Manager.
   * Ahora, debe [agregar un certificado SSL administrado por Adobe (DV)](#add-adobe-managed-ssl-cert).
Una vez agregado a Cloud Manager, espere a que Adobe emita e instale el certificado SSL de DV en su nombre.
   * Cuando el certificado esté activo, el dominio personalizado estará listo para usarse.

* **Para un certificado SSL administrado por el cliente (OV/EV):**

   * Obtenga su certificado SSL OV/EV de una autoridad certificadora. Para obtener más información, revise los [requisitos para los certificados SSL OV/EV administrados por el cliente](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).
   * Después de adquirir el certificado, [agregue los detalles del certificado SSL administrado por el cliente (OV/EV)](#add-customer-managed-ssl-cert) en Cloud Manager.
   * Una vez agregado, el nombre de dominio personalizado se marca como verificado y se aplica el certificado SSL.

En cualquier caso, después de comprobar e instalar el certificado, el dominio personalizado está disponible para su uso seguro en su entorno. Asegúrese de [comprobar el estado del dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) en la interfaz de Cloud Manager con regularidad para confirmar que todo funciona correctamente.

Consulte también [Introducción a los certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md).

## Añadir un certificado SSL administrado por Adobe (DV) {#add-adobe-managed-ssl-cert}

¿Necesita ayuda para elegir entre utilizar un certificado SSL administrado por Adobe (recomendado) o un certificado SSL administrado por el cliente con su dominio? Ver [Elección del certificado SSL que se agregará](#which-ssl-to-add)

**Para agregar un certificado SSL administrado por Adobe (DV):**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.

1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Agregando un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Cerca de la esquina superior derecha de la página Certificados SSL, haga clic en **Agregar certificado SSL**.

1. En el cuadro de diálogo **Agregar certificado SSL**, en función de [su caso de uso particular](#which-ssl-to-add), seleccione **Adobe Administrado (DV)**.

   ![Agregar certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. En el campo **Nombre del certificado**, escriba un nombre que desee asociar con el certificado SSL de DV.

1. En la lista desplegable **Seleccionar dominios**, seleccione uno o varios dominios comprobados que desee asociar con el certificado SSL de DV.
   * ¿No hay dominios que seleccionar? Si es así, primero debe [agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) y asegurarse de que está verificado antes de agregar un certificado SSL administrado por Adobe.
   * Cuando termine de agregar un nombre de dominio personalizado, vuelva a este tema y comience de nuevo en el paso 1.

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Guardar**.

   Una vez emitido correctamente el certificado SSL, se muestra con una marca de verificación válida de color verde en la tabla **Certificados SSL**.

Ahora ha agregado un certificado SSL de DV administrado de Adobe en funcionamiento para su proyecto. Este paso suele ser el primero en configurar un nombre de dominio personalizado.

Ya está listo para agregar una [configuración de CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Añadir un certificado SSL administrado por el cliente (OV/ED) {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

¿Necesita ayuda para elegir entre utilizar un certificado SSL administrado por Adobe (recomendado) o un certificado SSL administrado por el cliente con su dominio? Ver [Elección del certificado SSL que se agregará](#which-ssl-to-add)

>[!IMPORTANT]
>
>Al agregar o actualizar un certificado SSL, no incluya el nuevo certificado en la cadena de certificados. Si se incluye, se evita que la carga se complete correctamente.

**Para agregar un certificado SSL administrado por el cliente (OV/EV):**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú lateral.

1. Bajo el encabezado **Servicios**, haga clic en ![Icono de bloqueo cerrado](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **Certificados SSL**.

   ![Agregando un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Cerca de la esquina superior derecha de la página Certificados SSL, haga clic en **Agregar certificado SSL**.

1. En el cuadro de diálogo **Agregar certificado SSL**, en función de [su caso de uso particular](#which-ssl-to-add), seleccione **Administrado por el cliente (OV/EV)**.

1. En el campo **Nombre del certificado**, escriba un nombre para el certificado.
Este campo es solo informativo y puede ser cualquier nombre que le ayude a hacer referencia al certificado SSL fácilmente.

1. En los campos **Certificado**, **Clave privada** y **Cadena de certificados**, copie los valores requeridos de su certificado SSL OV o EV y péguelos en sus respectivos campos en el cuadro de diálogo.

   Se muestran todos los errores detectados en los valores. Para poder guardar el certificado, debe corregir todos los errores. Consulte [Errores de certificado](#certificate-errors) para obtener más información sobre la solución de problemas de errores comunes.

   ![Agregar cuadro de diálogo de certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Guardar**.

   >[!NOTE]
   >
   >* Si seleccionó **Certificado administrado por el cliente** mientras [agregaba un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), el dominio se verifica ***después de*** de que se agregue y guarde el certificado SSL administrado por el cliente (OV/EV). Vea también [Comprobar el estado de un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

   Una vez emitido correctamente el certificado SSL, se muestra con una marca de verificación verificada en verde en la tabla **Certificados SSL**.

Ahora ha agregado un certificado SSL de trabajo para el proyecto. Este paso suele ser el primero en configurar un nombre de dominio personalizado.

Ya está listo para agregar una [configuración de CDN](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
