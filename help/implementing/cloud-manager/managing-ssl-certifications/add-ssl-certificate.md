---
title: Agregar un certificado SSL
description: Aprenda a añadir su propio certificado SSL o certificado DV (validación de dominio) con las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3aec9d13e2eb4bbc9a972e28195a6f43e92c1842
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 22%

---


# Añadir un certificado SSL

Obtenga información sobre cómo agregar un certificado SSL administrado por el cliente o un certificado DV (validación de dominio) administrado y generado por Adobe mediante las herramientas de autoservicio de Cloud Manager.


## Añadir un certificado SSL o DV {#adding-an-ssl-certificate}

Un certificado puede tardar unos días en aprovisionarse. Por ello, el Adobe recomienda que el certificado se aprovisione con bastante antelación a cualquier fecha límite o de lanzamiento.

Asegúrese de revisar **Requisitos de certificado** en [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) para asegurarse de que AEM as a Cloud Service admite el certificado que desea agregar.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

>[!NOTE]
>
>Los clientes no pueden cargar certificados DV (validación de dominio).

**Para agregar un certificado SSL o DV:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Desde la página **Información general**, vaya a la pantalla **Entornos**.

1. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Certificados SSL**. Si no ve el panel de navegación izquierdo como se ve en la siguiente imagen, es posible que tenga que hacer clic en el icono de hamburguesa en la esquina superior izquierda.

   ![Agregando un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Cerca de la esquina superior derecha de la página, haga clic en **Agregar certificado SSL**.

1. En el cuadro de diálogo **Agregar certificado SSL**, en función de [su caso de uso particular](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md), realice una de las siguientes acciones:

   | | Caso de uso | Etapas |
   | --- | --- | --- |
   | 1 | **Agregar un certificado administrado por Adobe (DV)** | **Para agregar un certificado administrado por Adobe (DV):**<br> a. Seleccione el tipo de certificado **administrado por Adobe (DV)**.<br>![Agregar certificado DV](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. En la lista desplegable **Seleccionar dominios**, seleccione uno o varios dominios que desee asociar con el certificado DV.<br>¿No hay dominios que seleccionar? Si es así, significa que debe agregar un dominio personalizado. Consulte [Agregar un dominio personalizado](#add-custom-domain). Cuando termine de agregar un nombre de dominio personalizado, vuelva a este tema y comience de nuevo en el paso 1.<br>d. Continúe con el paso 7. |
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

   Una vez emitido correctamente el certificado, muestra una marca de verificación verde, como se ve en la imagen anterior

   ![Certificado DV emitido](assets/issued-dv-certificate.png)

### Añadir un dominio personalizado {#add-custom-domain}

Para poder agregar un certificado validado por dominio (DV) administrado y generado por Adobe, primero debe agregar un dominio personalizado. El proceso para hacerlo es casi el mismo que se detalla en [Introducción a los nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md) y [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Sin embargo, esa funcionalidad ahora se amplía ligeramente, como se describe a continuación.

1. Al agregar un nombre de dominio personalizado, en el cuadro de diálogo **Verificar dominio**, seleccione un **certificado administrado por Adobe**.

   ![Elegir administrado por el Adobe](assets/verify-domain-dialog.png)

1. En el cuadro de diálogo **Verificar dominio**, agregue un registro de verificación CNAME a su DNS.

   ![Agregar entrada CNAME](assets/verify-domain-dialog-adobe-managed.png)

1. Una vez creado el dominio, haga clic en el botón de puntos suspensivos en la lista de dominios y seleccione **Verificar** para comprobar el dominio.

   ![Verificar dominio](assets/verify-domain.png)

1. Reanudar la tarea [Agregar un certificado DV](#adding-an-ssl-certificate).

### Solución de problemas de errores de certificados {#certificate-errors}

Pueden surgir ciertos errores si un certificado no está instalado correctamente o no cumple los requisitos de Cloud Manager.

+++**Orden de certificado correcto**

El motivo más común para que una implementación de certificado falle es que los certificados intermedios o de cadena no están en el orden correcto.

Los archivos de certificado intermedios deben finalizar con el certificado raíz o el certificado más cercano a la raíz. Deben estar en orden descendente desde el certificado`main/server` a la raíz.

Puede determinar el orden de los archivos intermedios mediante el siguiente comando.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Puede verificar que la clave privada y el certificado `main/server` coincidan mediante los siguientes comandos.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no encuentra una clave privada que coincida con su certificado `main/server`, deberá volver a escribir el certificado y generar un CSR nuevo o solicitar un certificado actualizado a su proveedor SSL.

+++

+++**Quitar certificados de cliente**

Al agregar un certificado, recibe un error similar al siguiente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Es probable que haya incluido el certificado de cliente en la cadena de certificados. Asegúrese de que la cadena no incluya el certificado de cliente e inténtelo de nuevo.

+++

+++**Directiva de certificado**

Si ve el siguiente error, compruebe la directiva de su certificado.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Los valores OID incrustados normalmente identifican directivas de certificado. Si se envía un certificado a texto y se busca el OID, se muestra la directiva del certificado.

Puede incluir los detalles del certificado como texto si usa el siguiente ejemplo como guía.

```text
openssl x509 -in 9178c0f58cb8fccc.pem -text
certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            91:78:c0:f5:8c:b8:fc:cc
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
        Validity
            Not Before: Nov 10 22:55:36 2021 GMT
            Not After : Dec  6 15:35:06 2022 GMT
        Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
        Subject Public Key Info:
...
```

El patrón OID del texto define el tipo de directiva del certificado.

| Patrón | Directiva | Aceptable en Cloud Manager |
|---|---|---|
| `2.23.140.1.1` | EV | Sí |
| `2.23.140.1.2.2` | OV | Sí |
| `2.23.140.1.2.1` | DV | No |

Por `grep` ping para los patrones OID en el texto del certificado de salida, puede confirmar la directiva de certificado.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

+++

+++**Fechas de validez del certificado**

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días desde la fecha actual. Compruebe la validez de la cadena de certificados.

+++

## Pasos siguientes {#next-steps}

Ahora ha agregado un certificado SSL de trabajo para el proyecto. Este paso suele ser el primero en configurar un nombre de dominio personalizado.

* Para configurar un nombre de dominio personalizado, consulte [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Para obtener más información sobre cómo actualizar y administrar los certificados SSL en Cloud Manager, consulte [Administrar certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
