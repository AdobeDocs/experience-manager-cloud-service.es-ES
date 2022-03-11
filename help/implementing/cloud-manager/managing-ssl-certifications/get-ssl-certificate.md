---
title: 'Obtención de un certificado SSL: administración de certificados SSL'
description: 'Obtención de un certificado SSL: administración de certificados SSL'
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Obtención de un certificado SSL {#getting-an-ssl-certificate}

Las empresas utilizan certificados SSL para proteger sus sitios web y permitir a sus clientes depositar confianza en ellos. Para utilizar el protocolo SSL, un servidor web requiere el uso de un certificado SSL. Cloud Manager no proporciona certificados SSL ni claves privadas. Deben obtenerse de Entidades de certificación (CA).

Cuando una entidad solicita un certificado de una entidad emisora de certificados, esta completa un proceso de verificación. Esto puede abarcar desde verificar el control de nombres de dominio hasta recopilar documentos de registro de empresas y acuerdos de suscriptores. Una vez verificada la información de una entidad, la entidad emisora de certificados firmará su clave pública utilizando la clave privada de la entidad emisora de certificados. Dado que todas las autoridades de certificados principales tienen certificados raíz en los exploradores web, el certificado de la entidad se vinculará a través de un *cadena de confianza* y el explorador web lo reconocerá como un certificado de confianza.

>[!NOTE]
>AEM as a Cloud Service solo aceptará certificados OV(Organization Validation) o EV(Extended Validation). No se aceptarán los certificados DV (validación de dominio) o autofirmados. Los certificados OV y EV proporcionan a los usuarios información adicional y validada por CA que pueden utilizar para decidir si el propietario de un sitio web, el remitente de un correo electrónico o la firma digital de un código ejecutable o de documentos PDF es fiable. Los certificados DV son comunes y baratos. Sin embargo, no permiten la verificación de la propiedad.
>Además, cualquier certificado debe ser un certificado X.509 TLS de una entidad de certificación (CA) de confianza con una clave privada RSA de 2048 bits que coincida.
