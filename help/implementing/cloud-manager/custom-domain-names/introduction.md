---
title: Introducción a los nombres de dominio personalizados
description: La interfaz de usuario de Cloud Manager le permite agregar un dominio personalizado para identificar su sitio con un nombre único con marca de una manera autoservicio.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: cc1b0d653706150c616ceafd002dc7594b6c7072
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 9%

---


# Introducción a los nombres de dominio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Administrar nombres de dominio personalizados"
>abstract="La interfaz de usuario de Cloud Manager le permite agregar un dominio personalizado para identificar su sitio con un nombre único con marca de una manera autoservicio."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="Adición de un nombre de dominio personalizado"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="Ver y actualizar nombre de dominio personalizado"

La interfaz de usuario de Cloud Manager le permite agregar un dominio personalizado para identificar su sitio con un nombre único con marca de una manera autoservicio. Adobe Experience Manager as a Cloud Service se aprovisiona con un nombre de dominio predeterminado que termina en `*.adobeaemcloud.com`. Este nombre de dominio predeterminado permanece, incluso después de asociar nombres de dominio personalizados al sitio web.

## ¿Qué son los nombres de dominio personalizados? {#what-are-custom-domain-names}

Cada sitio web tiene una dirección numérica única, legible por máquina y asociada a ella, como `184.33.123.64`. El Sistema de nombres de dominio (DNS) es lo que le permite tener dominios personalizados con marca adjuntados a sitios web traduciendo direcciones numéricas en direcciones memorables como `wknd.com`.

Es recomendable tener un nombre de dominio para el sitio que sea memorable para los clientes y que refleje la marca.

Puede comprar un nombre de dominio a través de un registrador de nombres de dominio, una empresa u organización que administre y venda nombres de dominio. Los registradores de nombres de dominio administran nombres de dominio en servidores DNS.

>[!IMPORTANT]
>
>Cloud Manager no es un registrador de nombres de dominio y no proporciona servicios DNS.

## Restricciones     {#limitations}

El uso de nombres de dominio personalizados con AEMaaCS conlleva varias limitaciones.

* Los nombres de dominio personalizados se admiten en Cloud Manager tanto para los servicios de publicación como de vista previa para los programas de Sites. Los dominios personalizados del lado del autor no son compatibles.
* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.
* AEM as a Cloud Service no admite dominios comodín.
* Antes de agregar un nombre de dominio personalizado, debe instalar en el programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte Adición de un certificado SSL para obtener más información.
* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.
* Solo se puede agregar un nombre de dominio a la vez.
* No se puede usar el mismo nombre de dominio en más de un entorno.

## Flujo de trabajo {#workflow}

Para agregar un nombre de dominio personalizado es necesario interactuar entre el servicio DNS y Cloud Manager. Debido a esto, se requieren varios pasos para instalar, configurar y verificar nombres de dominio personalizados. En la tabla siguiente se proporciona una descripción general de los pasos necesarios, lo que incluye qué hacer cuando se producen errores comunes.

| Etapa | Descripción | Responsabilidad | Más información |
|--- |--- |--- |---|
| 1 | Añadir certificado SLL a Cloud Manager | Cliente | [Adición de un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Añadir registro TXT para verificar el dominio | Cliente | [Adición de un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Revisar estado de verificación del dominio | Cliente | [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3 bis | Si la verificación del dominio falla con el estado `Domain Verification Failure` | Cliente | [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Si la verificación del dominio falla con el estado `Verified, Deployment Failed`, Adobe de contacto | Servicio de atención al cliente de Adobe | [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Configurar la configuración de DNS agregando registros CNAME o APEX DNS que apunten a AEM as a Cloud Service | Cliente | [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Comprobar el estado del registro DNS | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | Si el estado del registro DNS falla con `DNS status not detected` | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Si el estado del registro DNS falla con `DNS resolves incorrectly` | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
