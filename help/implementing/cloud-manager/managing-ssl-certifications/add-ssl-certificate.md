---
title: Agregar un certificado SSL
description: Aprenda a agregar su propio certificado SSL con las herramientas de autoservicio de Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 14e0255b3ce2ca44579b9fc3de6c7b7f5d8f34b6
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 100%

---

# Agregar un certificado SSL {#adding-an-ssl-certificate}

Aprenda a agregar su propio certificado SSL con las herramientas de autoservicio de Cloud Manager.

>[!TIP]
>
>Un certificado puede tardar unos días en aprovisionarse. Por lo tanto, Adobe recomienda que el certificado se aprovisione con bastante antelación.

## Formato del certificado {#certificate-format}

Los archivos de certificado SSL deben tener el formato PEM para que se instalen con Cloud Manager. Las extensiones de archivo comunes del formato PEM incluyen `.pem,` .`crt`, `.cer`, y `.cert`.

Los siguientes comandos `openssl` se pueden utilizar para convertir certificados que no sean PEM.

* Convertir PFX a PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* Convertir P7B a PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* Convertir DER a PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## Agregar un certificado {#adding-a-cert}

Siga estos pasos para agregar un certificado mediante Cloud Manager.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Haga clic en **Certificados SSL** en el panel de navegación izquierdo. Se mostrará en la pantalla principal una tabla con detalles de cualquier certificado SSL existente.

   ![Agregar un certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Haga clic en **Agregar certificado SSL** para abrir el cuadro de diálogo **Agregar certificado SSL**.

   * Escriba un nombre para el certificado en **Nombre del certificado**.
      * Esto es solo para fines informativos y puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.
   * Pegue los valores **Certificado**, **Clave privada** y **Cadena de certificados** en sus respectivos campos. Los tres campos son obligatorios.

   ![Cuadro de diálogo Agregar certificado SSL](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Se mostrarán todos los errores detectados.
      * Debe corregir todos los errores antes de guardar el certificado.
      * Consulte la sección [Errores de certificado](#certificate-errors) para obtener más información sobre cómo solucionar errores comunes.


1. Haga clic en **Guardar** para guardar el certificado.

Una vez guardado, verá el certificado como una fila nueva en la tabla.

![Certificado SSL guardado](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>Un usuario debe ser miembro del rol de **Propietario del negocio** o **Administrador de implementación** para instalar un certificado SSL en Cloud Manager.

## Errores de certificado {#certificate-errors}

Pueden surgir ciertos errores si un certificado no está instalado correctamente o si no cumple los requisitos de Cloud Manager.

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
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no puede localizar una clave privada que coincida con su certificado `main/server`, deberá volver a escribir el certificado y generar un CSR nuevo o solicitar un certificado actualizado a su proveedor SSL.

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días desde la fecha actual. Debe comprobar la validez de la cadena de certificados.
