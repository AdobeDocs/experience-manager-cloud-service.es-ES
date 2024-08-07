---
title: Introducción a los nombres de dominio personalizados
description: La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1c9924b4477d53d86bb72eda8597a02304450195
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 58%

---


# Introducción a los nombres de dominio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Administrar los nombres de dominio personalizados"
>abstract="La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único."
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Añadir un nombre de dominio personalizado"
>additional-url="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Ver y actualizar nombres de dominio personalizados"

Adobe Experience Manager as a Cloud Service se aprovisiona con un nombre de dominio predeterminado que termina en `*.adobeaemcloud.com`. Con la interfaz de usuario de Cloud Manager puede agregar un dominio personalizado para identificar el sitio con un nombre único de marca en forma de autoservicio. El nombre de dominio predeterminado `*.adobeaemcloud.com` permanece, incluso después de asociar nombres de dominio personalizados al sitio web.

## ¿Qué son los nombres de dominio personalizados? {#what-are-custom-domain-names}

Cada sitio web tiene una dirección numérica única, legible por máquina y asociada a ella, como `184.33.123.64`. El Sistema de nombres de dominio (DNS) es lo que le permite tener dominios personalizados de marca adjuntados a sitios web al traducir direcciones numéricas en direcciones memorables como `wknd.com`.

Se recomienda tener un nombre de dominio para el sitio que sea memorable para los clientes y que refleje la marca.

Puede comprar un nombre de dominio a través de un registrador de nombres de dominio, una empresa u organización que administre y venda nombres de dominio. Los registradores de nombres de dominio administran nombres de dominio en servidores DNS.

>[!IMPORTANT]
>
>Cloud Manager no es un registrador de nombres de dominio y no proporciona servicios DNS.

## Nombres de dominio personalizados y CDN de BYO {#byo-cdn}

AEM as a Cloud Service AEM ofrece un servicio integrado de red de entrega de contenido (CDN), pero también le permite traer su propia CDN (BYO) para utilizarla con los servicios de red de distribución de contenido (CDN) de la red de distribución de contenido (CDN) para usar con los servicios de red de distribución de contenido (CDNs) y de red de distribución de contenido (CDNs) de la red de distribución de contenido (CDNs) para su uso con los servicios de red de. Los dominios personalizados pueden instalarse en la CDN administrada por AEM o en una CDN que administre usted.

* Los nombres de dominio personalizados (y certificados) instalados en la CDN administrada por AEM se administran mediante Cloud Manager.
* Los nombres de dominio personalizados (y certificados) instalados en su propia CDN se administran en esa CDN específica.

No es necesario instalar **dominios administrados en su propia CDN mediante Cloud Manager.AEM**: se ponen a disposición de los usuarios a través de X-Forwarded-Host para que se ajusten a los vhosts definidos en Dispatcher. Consulte la [documentación de CDN.](/help/implementing/dispatcher/cdn.md)

En un entorno puede tener ambos dominios instalados en la CDN administrada por AEM e instalados en su propia CDN.

## Flujo de trabajo {#workflow}

Para agregar un nombre de dominio personalizado es necesaria la interacción entre el servicio DNS y Cloud Manager. Debido a esto, se requieren varios pasos para instalar, configurar y verificar nombres de dominio personalizados. En la tabla siguiente se ofrece una descripción general de los pasos necesarios, incluidos vínculos a recursos de documentación para completar esos pasos.

| Paso | Descripción | Documentación |
|---|---|---|
| 1 | Agregar certificado SSL a Cloud Manager | [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Añadir dominio personalizado a Cloud Manager | [Agregando un nombre de dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | Agregar registro TXT para verificar el dominio | [Agregar un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 4 | Revisar estado de verificación del dominio | [Comprobar el estado del nombre de dominio ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | Configurar la configuración de DNS agregando registros CNAME o APEX DNS que apunten a AEM as a Cloud Service | [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 6 | Comprobar el estado del registro DNS | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>La configuración de nombres de dominio personalizados con AEM as a Cloud Service suele ser un proceso sencillo. Sin embargo, en ocasiones pueden producirse problemas de delegación de dominios que pueden tardar entre 1 y 2 días hábiles en resolverse. Por este motivo, es muy recomendable instalar los dominios mucho antes de la fecha de lanzamiento. Consulte el documento [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

## Limitaciones {#limitations}

El uso de nombres de dominio personalizados con AEMaaCS conlleva varias limitaciones.

* Los nombres de dominio personalizados solo se admiten en Cloud Manager para los servicios de publicación y vista previa de los programas de Sites.
   * No se admiten los dominios personalizados para servicios de autor.
* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.
* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización actual en ejecución asociada a esos entornos.
* No se puede usar el mismo nombre de dominio en más de un entorno.
* Solo se puede agregar un nombre de dominio a la vez.
* AEM as a Cloud Service no admite dominios comodín como `*.example.com`.
* Antes de agregar un nombre de dominio personalizado, debe instalar en el programa un certificado SSL válido que contenga el nombre de dominio personalizado (los certificados comodín son válidos).

## ¡Empiece! {#get-started}

* Empiece a configurar un nuevo nombre de dominio personalizado para su proyecto [agregando un certificado SSL.](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* Administre sus nombres de dominio existentes revisando el documento [Administración de nombres de dominio personalizados.](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
