---
title: 'Adición de un certificado SSL: administración de certificados SSL'
description: 'Adición de un certificado SSL: administración de certificados SSL'
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 1%

---

# Adición de un certificado SSL {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as a Cloud Service solo aceptará certificados que se ajusten a la directiva OV (validación de organización) o EV (validación extendida). No se aceptará la directiva DV (validación de dominio). Además, cualquier certificado debe ser un certificado X.509 TLS de una entidad de certificación (CA) de confianza con una clave privada RSA de 2048 bits que coincida. AEM as a Cloud Service aceptará certificados SSL comodín para un dominio.

Un certificado tarda unos días en proporcionarse y se recomienda que se aprovisione el certificado incluso con meses de antelación. Consulte [Obtención de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) para obtener más información.

## Formato del certificado {#certificate-format}

Los archivos SSL deben tener formato PEM para poder instalarse en Cloud Manager. Las extensiones de archivo comunes que están dentro del formato PEM incluyen `.pem,` .`crt`, `.cer`, y `.cert`.

Siga los pasos a continuación para convertir el formato de sus archivos SSL a PEM:

* Convertir PFX a PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Convertir P7B a PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Convertir DER a PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Consideraciones importantes {#important-considerations}

* Un usuario debe tener la función Propietario empresarial o Administrador de implementación para poder instalar un certificado SSL en Cloud Manager.

* En cualquier momento dado, Cloud Manager permitirá un máximo de 10 certificados SSL que se pueden asociar con uno o más entornos en todo el programa, incluso si un certificado ha caducado. Sin embargo, la interfaz de usuario de Cloud Manager permitirá instalar hasta 50 certificados SSL en el programa con esta restricción. Normalmente, un certificado puede abarcar varios dominios (hasta 100 SANs), por lo que puede considerar la posibilidad de agrupar varios dominios en el mismo certificado para permanecer dentro de este límite.


## Adición de un certificado {#adding-a-cert}

Siga los pasos a continuación para añadir un certificado:

1. Inicie sesión en Cloud Manager.
1. Vaya a **Entornos** pantalla de **Información general** página.
1. Haga clic en **Certificados SSL** en el menú de navegación de la izquierda. En esta pantalla se mostrará una tabla con detalles de cualquier certificado SSL existente.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Haga clic en **Añadir certificado SSL** para abrir **Añadir certificado SSL** para abrir el Navegador.

   * Escriba un nombre para el certificado en **Nombre del certificado**. Puede ser cualquier nombre que le ayude a hacer referencia al certificado fácilmente.
   * Pegue el **Certificado**, **Clave privada** y **Cadena de certificados** en sus respectivos campos. Utilice el icono de pegado a la derecha del cuadro de entrada.
Los tres campos no son opcionales y deben incluirse.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Se mostrarán todos los errores detectados. Debe corregir todos los errores antes de guardar el certificado. Consulte la [Errores de certificado](#certificate-errors) para obtener más información sobre cómo solucionar errores comunes.

1. Haga clic en **Guardar** para enviar el certificado. Verá que se muestra como una fila nueva en la tabla.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Errores de certificado {#certificate-errors}

### Política de certificados {#certificate-policy}

Si ve el error &quot;La directiva de certificado debe ajustarse a EV u OV, y no a la directiva de DV&quot;, compruebe la directiva del certificado.

Normalmente, los tipos de certificados se identifican mediante los valores OID incrustados en las políticas. Estos OID son únicos y, por lo tanto, convertir un certificado en un formulario de texto y buscar el OID confirmará que el certificado tiene una coincidencia.

Puede ver los detalles del certificado como se indica a continuación.

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

En esta tabla se indican los patrones de identificación.

| Patrón | Tipo de certificado | Aceptable |
|---|---|---|
| `2.23.140.1.2.1` | DV | No |
| `2.23.140.1.2.2` | OV | Sí |
| `2.23.140.1.2.3` y `TLS Web Server Authentication` | Certificado IV con permiso de uso para https | Sí |

`grep`para ver los patrones, puede confirmar el tipo de certificado.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Orden de certificados correcto {#correct-certificate-order}

El motivo más común para que una implementación de certificado falle es que los certificados intermedios o de cadena no están en el orden correcto. En concreto, los archivos de certificado intermedios deben finalizar con el certificado raíz o el certificado más cercano a la raíz y estar en orden descendente desde el `main/server` certificado a la raíz.

Puede determinar el orden de los archivos intermedios mediante el siguiente comando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Puede verificar que la clave privada y `main/server` coincidencia de certificado mediante los siguientes comandos:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>El resultado de estos dos comandos debe ser exactamente el mismo. Si no encuentra ninguna clave privada que coincida con su `main/server` , deberá volver a escribir el certificado generando un CSR nuevo o solicitando un certificado actualizado a su proveedor SSL.

### Fechas de validez del certificado {#certificate-validity-dates}

Cloud Manager espera que el certificado SSL sea válido durante al menos 90 días en el futuro. Debe comprobar la validez de la cadena de certificados.
