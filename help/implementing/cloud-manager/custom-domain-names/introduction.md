---
title: Introducción a los nombres de dominio personalizados
description: La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f3cd1bc761c513ebb85351185e7aa0b6f6eb6f33
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 34%

---


# Introducción a los nombres de dominio personalizados {#introduction}

<!-- Alexandru: contextual help links are broken, temporarily comminting this out until they,re fixed.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Manage Custom Domain Names"
>abstract="Cloud Manager's UI lets you add a custom domain to identify your site with a unique, branded name in a self-service manner."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Adding a Custom Domain Name"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="View & Update Custom Domain Name"

-->

Adobe Experience Manager as a Cloud Service se aprovisiona con un nombre de dominio predeterminado que termina en `*.adobeaemcloud.com`. Con la interfaz de usuario de Cloud Manager puede agregar un dominio personalizado para identificar el sitio con un nombre único de marca en forma de autoservicio. El nombre de dominio predeterminado `*.adobeaemcloud.com` permanece, incluso después de asociar nombres de dominio personalizados al sitio web.

## ¿Qué son los nombres de dominio personalizados? {#what-are-custom-domain-names}

Cada sitio web tiene una dirección numérica única, legible por máquina y asociada a ella, como `184.33.123.64`. El Sistema de nombres de dominio (DNS) es lo que le permite tener dominios personalizados de marca adjuntados a sitios web al traducir direcciones numéricas en direcciones memorables como `wknd.com`.

Se recomienda tener un nombre de dominio para el sitio que sea memorable para los clientes y que refleje la marca.

Puede comprar un nombre de dominio a través de un registrador de nombres de dominio, una empresa u organización que administre y venda nombres de dominio. Los registradores de nombres de dominio administran nombres de dominio en servidores DNS.

>[!IMPORTANT]
>
>Cloud Manager no es un registrador de nombres de dominio y no proporciona servicios DNS.

## Nombres de dominio personalizados y sus propias CDN {#byo-cdn}

AEM as a Cloud Service ofrece un servicio integrado de CDN (red de distribución de contenido), pero también le permite comprar (traer su propia) CDN para utilizarla con AEM. Los dominios personalizados pueden instalarse en la CDN administrada por AEM o en una CDN que administre usted.

* Cloud Manager administra los nombres de dominio personalizados y los certificados instalados en la CDN administrada por AEM.
* Los nombres de dominio personalizados y los certificados instalados en una CDN BYO se administran directamente dentro de esa CDN.

**Los dominios administrados en su propia CDN no requieren instalación a través de Cloud Manager**. Están disponibles para AEM mediante X-Forwarded-Host y coinciden con los vhosts definidos en Dispatcher. Consulte la [Documentación de la CDN](/help/implementing/dispatcher/cdn.md).

En un entorno, puede tener ambos dominios instalados en la CDN administrada por AEM e instalados en una CDN por BYO.

## Flujo de trabajo {#workflow}

Para agregar un nombre de dominio personalizado es necesaria la interacción entre el servicio DNS y Cloud Manager. Debido a este flujo de trabajo, se requieren varios pasos para instalar, configurar y comprobar los nombres de dominio personalizados. En la tabla siguiente se describen los pasos necesarios, con vínculos a los recursos de documentación para completarlos.

>[!WARNING]
>
>Ejecute el paso 4 (Configurar DNS) *solo después de que* el paso 3 (Agregar asignación de dominio) haya finalizado correctamente. Si sigue este orden, registra el dominio con la CDN de Adobe y configura el enrutamiento correcto, lo que protege el sitio de las absorciones de dominios.

| Paso | Descripción |
| --- | --- |
| 1 | [Agregar certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | [Agregar un dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | [Agregar asignación de dominio](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | [Configurar DNS](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#config-dns) |
| 5 | [Comprobar el estado DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>La configuración de nombres de dominio personalizados con AEM as a Cloud Service suele ser un proceso sencillo. Sin embargo, en ocasiones pueden producirse problemas de delegación de dominios que pueden tardar entre 1 y 2 días hábiles en resolverse. Por este motivo, se recomienda instalar los dominios mucho antes de la fecha de lanzamiento. Consulte el documento [Comprobar el estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.

## Notas de uso {#usage-notes}

* Los nombres de dominio personalizados solo se admiten en Cloud Manager para los servicios de publicación y vista previa de los programas de Sites.
   * No se admiten los dominios personalizados para servicios de autor.
* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.
* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.
* No se puede usar el mismo nombre de dominio en más de un entorno.
* Solo se puede agregar un nombre de dominio a la vez.
* AEM as a Cloud Service no admite dominios comodín como `*.example.com`.
* Antes de agregar un nombre de dominio personalizado, debe instalar en el programa un certificado SSL válido que contenga el nombre de dominio personalizado (los certificados comodín son válidos).
* Se requieren pasos de configuración adicionales para usar un nombre de dominio personalizado con [la característica de canalización front-end](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md#custom-domains).

## Introducción {#get-started}

* Empiece a configurar un nuevo nombre de dominio personalizado para su proyecto [agregando un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Administre sus nombres de dominio existentes revisando el documento [Administrar nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
