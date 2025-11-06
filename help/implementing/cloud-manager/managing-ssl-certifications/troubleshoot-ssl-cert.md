---
title: Solucionar problemas de certificados SSL
description: Obtenga información sobre cómo solucionar problemas de certificados SSL identificando causas comunes para que pueda mantener conexiones seguras.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 8fb8f708-51a5-46d0-8317-6ce118a70fab
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 31%

---

# Solucionar problemas de certificados SSL {#certificate-problems}

Obtenga información sobre cómo solucionar problemas de certificados SSL identificando causas comunes para que pueda mantener conexiones seguras.

+++**Certificado no válido**

## Certificado no válido {#invalid-certificate}

Este error se produce porque el cliente utilizó una clave privada cifrada y proporcionó la clave en formato DER.

+++

+++**La clave privada debe tener el formato PKCS 8**

## La clave privada debe tener el formato PKCS 8 {#pkcs-8}

Este error se produce porque el cliente utilizó una clave privada cifrada y proporcionó la clave en formato DER.

+++

+++**Orden de certificado correcto**

## Orden de certificados correcto {#certificate-order}

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

## Quitar certificados de cliente {#client-certificates}

Al agregar un certificado, recibe un error similar al siguiente:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Es probable que haya incluido el certificado de cliente en la cadena de certificados. Asegúrese de que la cadena no incluya el certificado de cliente e inténtelo de nuevo.

+++

+++**Directiva de certificado**

## Directiva de certificados {#policy}

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

+++**Validez del certificado

## Validez del certificado {#validity}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días desde la fecha actual. Compruebe la validez de la cadena de certificados.

+++

+++**Se ha aplicado un certificado SAN incorrecto a mi dominio

## Se ha aplicado un certificado SAN incorrecto a mi dominio {#wrong-san-cert}

Supongamos que desea vincular `dev.yoursite.com` y `stage.yoursite.com` a su entorno que no sea de producción y a `prod.yoursite.com` a su entorno de producción.

Para configurar la CDN para estos dominios, necesita instalar un certificado para cada uno, de modo que instale un certificado que cubra `*.yoursite.com` para los dominios que no sean de producción y otro que también cubra `*.yoursite.com` para los dominios de producción.

Esta configuración es válida. Sin embargo, al actualizar uno de los certificados, ya que ambos cubren la misma entrada de SAN, la red de distribución de contenido (CDN) instalará el certificado más reciente en todos los dominios aplicables, lo que podría parecer inesperado.

Aunque esto puede ser inesperado, no se trata de un error y es el comportamiento estándar de la CDN subyacente. Si tiene dos o más certificados SAN que cubren la misma entrada de dominio SAN, si ese dominio está cubierto por un certificado y el otro se actualiza, este último se instalará ahora para el dominio.

+++
