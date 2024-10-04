---
title: Solución de problemas de errores de certificados SSL
description: Obtenga información sobre cómo solucionar errores de certificados SSL identificando causas comunes para que pueda mantener conexiones seguras.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b387fee62500094d712f5e1f6025233c9397f8ec
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 48%

---


# Solucionar errores de certificados SSL {#certificate-errors}

Pueden surgir ciertos errores si un certificado no está instalado correctamente o no cumple los requisitos de Cloud Manager.

+++**Certificado no válido**

Este error se produce porque el cliente utilizó una clave privada cifrada y proporcionó la clave en formato DER.

+++

+++**La clave privada debe tener el formato PKCS 8**

Este error se produce porque el cliente utilizó una clave privada cifrada y proporcionó la clave en formato DER.

+++

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