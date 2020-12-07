---
title: Obtención de un certificado SSL - Administración de certificados SSL
description: Obtención de un certificado SSL - Administración de certificados SSL
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Obtención de un certificado SSL {#getting-an-ssl-certificate}

Las empresas utilizan certificados SSL para proteger sus sitios web y permitir a sus clientes depositar confianza en ellos. Para utilizar el protocolo SSL, un servidor web requiere el uso de un certificado SSL. Cloud Manager no proporciona certificados SSL ni claves privadas. Estos deben obtenerse de Entidades emisoras de certificados (CA).

Cuando una entidad solicita un certificado de una entidad emisora de certificados, ésta completa un proceso de verificación. Esto puede ir desde la verificación del control de nombres de dominio hasta la recopilación de documentos de registro de compañías y acuerdos de suscriptor. Una vez verificada la información de una entidad, la CA firmará su clave pública utilizando la clave privada de la CA. Dado que todas las autoridades de certificados principales tienen certificados raíz en los exploradores Web, el certificado de la entidad se vinculará a través de una *cadena de confianza* y el explorador Web lo reconocerá como un certificado de confianza.

>[!NOTE]
>AEM como Cloud Service solo aceptará certificados OV (validación de organización) o EV (validación extendida). No se aceptarán los certificados DV (validación de dominio) o autofirmados. Los certificados OV y EV proporcionan a los usuarios información adicional validada por CA que pueden utilizar para decidir si el propietario de un sitio web, el remitente de un mensaje de correo electrónico o el firmante digital de un código ejecutable o documentos PDF son fiables. Los certificados DV son comunes y baratos. Sin embargo, no permiten la verificación de la propiedad.

