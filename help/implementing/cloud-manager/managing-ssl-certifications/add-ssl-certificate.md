---
title: Agregar un certificado SSL
description: Aprenda a agregar su propio certificado SSL con las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 65%

---


# Agregar un certificado SSL {#adding-an-ssl-certificate}

Aprenda a agregar su propio certificado SSL con las herramientas de autoservicio de Cloud Manager.

>[!TIP]
>
>Un certificado puede tardar unos días en aprovisionarse. Por lo tanto, el Adobe recomienda que el certificado se aprovisione con mucha antelación a cualquier fecha límite o fecha de lanzamiento.

## Requisitos de certificado {#certificate-requirements}

Revise la sección **Requisitos de certificado** del documento [Introducción a la administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) para asegurarse de que el certificado que desea agregar sea compatible con AEM as a Cloud Service.

## Agregar un certificado {#adding-a-cert}

Siga estos pasos para agregar un certificado mediante Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en **Certificados SSL** en el panel de navegación izquierdo. Se muestra en la pantalla principal una tabla con detalles de cualquier certificado SSL existente.

   ![Agregar un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Haga clic en **Agregar certificado SSL** para abrir el cuadro de diálogo **Agregar certificado SSL**.

   * Escriba un nombre para el certificado en **Nombre del certificado**.
      * Esto es solo para fines informativos y puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.
   * Pegue los valores de **Certificado**, **Clave privada** y **Cadena de certificados** en sus respectivos campos.
      * Los tres campos son obligatorios.

   ![Cuadro de diálogo Agregar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Se muestran todos los errores detectados.
      * Debe corregir todos los errores antes de guardar el certificado.
      * Consulte la sección [Errores de certificado](#certificate-errors) para obtener más información sobre cómo solucionar errores comunes.

1. Haga clic en **Guardar** para guardar el certificado.

Una vez guardado, verá el certificado como una fila nueva en la tabla.

![Certificado SSL guardado](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>El usuario debe ser miembro de la función **Propietario del negocio** o **Administrador de implementación** para instalar un certificado SSL en Cloud Manager.

## Errores de certificado {#certificate-errors}

Pueden surgir ciertos errores si un certificado no está instalado correctamente o si no cumple los requisitos de Cloud Manager.

### Orden de certificados correcto {#correct-certificate-order}

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

### Quitar certificados de cliente {#client-certificates}

Al agregar un certificado, recibe un error similar al siguiente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Es probable que haya incluido el certificado de cliente en la cadena de certificados. Asegúrese de que la cadena no incluya el certificado de cliente e inténtelo de nuevo.

### Directiva de certificados {#certificate-policy}

Si ve el siguiente error, compruebe la directiva de su certificado.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Normalmente, las directivas de certificados se identifican mediante valores OID incrustados. Si se envía un certificado a texto y se busca el OID, se revelará la directiva del certificado.

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

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días desde la fecha actual. Debe comprobar la validez de la cadena de certificados.

## Siguientes pasos {#next-steps}

Enhorabuena. Ahora tiene un certificado SSL en funcionamiento para el proyecto. A menudo, este es un primer paso para configurar un nombre de dominio personalizado.

* Consulte el documento [Agregar un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) para seguir configurando un nombre de dominio personalizado.
* Consulte el documento [Administración de certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) para obtener información sobre cómo actualizar y administrar los certificados SSL en Cloud Manager.
