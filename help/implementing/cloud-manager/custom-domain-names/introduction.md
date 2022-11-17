---
title: Introducción a los nombres de dominio personalizados
description: La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: 42318a42a55134501eb13feca22791bb5db4e83f
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 83%

---


# Introducción a los nombres de dominio personalizados {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Administrar los nombres de dominio personalizados"
>abstract="La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=es" text="Agregar un nombre de dominio personalizado"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html?lang=es" text="Ver y actualizar nombres de dominio personalizados"

La interfaz de usuario de Cloud Manager le permite agregar a usted mismo un dominio personalizado para identificar su sitio con un nombre único. Adobe Experience Manager as a Cloud Service se aprovisiona con un nombre de dominio predeterminado que termina en `*.adobeaemcloud.com`. Este nombre de dominio predeterminado permanece, incluso después de asociar nombres de dominio personalizados al sitio web.

## ¿Qué son los nombres de dominio personalizados? {#what-are-custom-domain-names}

Cada sitio web tiene una dirección numérica única, legible por máquina y asociada a ella, como `184.33.123.64`. El sistema de nombres de dominio (DNS) es lo que le permite tener dominios personalizados de marca adjuntados a sitios web al traducir direcciones numéricas en direcciones memorables como `wknd.com`.

Es recomendable tener un nombre de dominio para el sitio que sea memorable para los clientes y que refleje la marca.

Puede comprar un nombre de dominio a través de un registrador de nombres de dominio, una empresa u organización que administre y venda nombres de dominio. Los registradores de nombres de dominio administran nombres de dominio en servidores DNS.

>[!IMPORTANT]
>
>Cloud Manager no es un registrador de nombres de dominio y no proporciona servicios DNS.

## Restricciones {#limitations}

El uso de nombres de dominio personalizados con AEMaaCS conlleva varias limitaciones.

* Los nombres de dominio personalizados se admiten en Cloud Manager tanto para los servicios de publicación como de vista previa para los programas de Sites. Los dominios personalizados del lado del autor no son compatibles.
* Cada entorno de Cloud Manager puede alojar hasta un máximo de 500 dominios personalizados por entorno.
* AEM as a Cloud Service no admite dominios comodín.
* Antes de agregar un nombre de dominio personalizado, debe instalar en el programa un certificado SSL válido que contenga el nombre de dominio personalizado. Consulte Agregar un certificado SSL para obtener más información.
* Los nombres de dominio no se pueden agregar a entornos mientras haya una canalización en ejecución asociada a esos entornos.
* Solo se puede agregar un nombre de dominio a la vez.
* No se puede usar el mismo nombre de dominio en más de un entorno.

>[!NOTE]
>
>Los dominios personalizados se admiten en Cloud Manager **only** si utiliza la CDN administrada de AEM. Si trae su propia CDN y [diríjala a la CDN administrada de AEM](/help/implementing/dispatcher/cdn.md) tendrá que usar esa CDN específica para administrar dominios, no Cloud Manager.

## Flujo de trabajo {#workflow}

Para agregar un nombre de dominio personalizado es necesaria la interacción entre el servicio DNS y Cloud Manager. Debido a esto, se requieren varios pasos para instalar, configurar y verificar nombres de dominio personalizados. En la siguiente tabla se proporciona una descripción general de los pasos necesarios, lo que incluye qué hacer cuando se producen errores comunes.

| Paso | Descripción | Responsabilidad | Más información |
|--- |--- |--- |---|
| 1 | Añadir certificado SSL a Cloud Manager | Cliente | [Agregar un certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Agregar registro TXT para verificar el dominio | Cliente | [Agregar un registro TXT](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Revisar estado de verificación del dominio | Cliente | [Comprobar el estado del nombre de dominio ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | Si la verificación del dominio falla con el estado `Domain Verification Failure` | Cliente | [Comprobar el estado del nombre de dominio ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Si la verificación del dominio falla con el estado `Verified, Deployment Failed`, póngase en contacto con Adobe | Servicio de atención al cliente de Adobe | [Comprobar el estado del nombre de dominio ](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Configurar la configuración de DNS agregando registros CNAME o APEX DNS que apunten a AEM as a Cloud Service | Cliente | [Configuración de DNS](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Comprobar el estado del registro DNS | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | Si el estado del registro DNS falla con `DNS status not detected` | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Si el estado del registro DNS falla con `DNS resolves incorrectly` | Cliente | [Comprobación del estado de registro DNS](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>La configuración de nombres de dominio personalizados con AEM as a Cloud Service suele ser un proceso sencillo. Sin embargo, en ocasiones pueden producirse problemas de delegación de dominios que pueden tardar entre 1 y 2 días hábiles en resolverse. Por este motivo, es muy recomendable instalar los dominios mucho antes de la fecha de lanzamiento. Consulte el documento [Comprobación del estado del nombre de dominio](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) para obtener más información.
