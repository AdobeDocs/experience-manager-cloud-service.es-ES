---
title: Notas de la versión 2023.8.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service
description: Estas son las notas de la versión 2023.8.0 para Cloud Manager en AEM as a Cloud Service.
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: 99772a1a3faa454a9b07dd92c9e7622ddb37ce2d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 37%

---


# Notas de la versión 2023.8.0 para Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

Esta página documenta las notas de la versión 2023.8.0 para Cloud Manager en AEM as a Cloud Service.

>[!NOTE]
>
>Consulte [esta página](/help/release-notes/release-notes-cloud/release-notes-current.md) para ver las notas de la versión actuales de Adobe Experience Manager as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2023.8.0 en AEM as a Cloud Service es el 10 de agosto de 2023. El próximo lanzamiento está programado para el 7 de septiembre de 2023.

## Novedades {#what-is-new}

* Al configurar un conjunto de contenido como [copiar contenido,](/help/implementing/developing/tools/content-copy.md) [configuraciones según el contexto](/help/implementing/developing/introduction/configurations.md) ahora se permiten en los conjuntos de contenido de la interfaz de usuario.
* Se han realizado mejoras para la comprensión y la aparición de mensajes de error en la IU de Cloud Manager.

## Programa de adopción temprana {#early-adoption}

Forme parte de nuestro programa de adopción anticipada y tenga la oportunidad de probar algunas de las próximas funciones.

### Restauración de contenido de autoservicio {#content-restore}

[Una nueva función de restauración de contenido de autoservicio](/help/operations/restore.md) ahora proporciona una restauración de copia de seguridad durante un máximo de siete días y está disponible para los usuarios que la adoptaron por primera vez con fines de evaluación, que incluye:

* Restauración de la copia de seguridad puntual de las 24 horas anteriores
* Restauraciones a tiempo fijo de hasta siete días

Si está interesado en probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a `aemcs-restorefrombackup-adopter@adobe.com` de su correo electrónico asociado a su Adobe ID. Importante:

* El programa de los primeros en adoptarlo se limita únicamente a los entornos de desarrollo.
* La disponibilidad del programa de adopción anticipada de esta función es limitada.
* Esta función se utiliza para recuperar contenido eliminado accidentalmente y no está pensada para la recuperación ante desastres.

### Tablero de auditoría de experiencias {#experience-audit-dashboard}

[El panel de auditoría de experiencias de Cloud Manager](/help/implementing/cloud-manager/experience-audit-dashboard.md) incluye una vista de tendencias de las puntuaciones de rendimiento de la página, junto con perspectivas y recomendaciones para ayudarle a mejorarlas. La auditoría de experiencias se incluye como paso en la canalización de producción de Cloud Manager.

El tablero aprovecha Google Lighthouse, una herramienta automatizada de código abierto para mejorar la calidad de sus aplicaciones web. Puede ejecutarlo en cualquier página web, pública o que requiera autenticación. Tiene auditorías de rendimiento, accesibilidad, aplicaciones web progresivas, SEO y más.

¿Interesado en probar a conducir el nuevo tablero? Envíe un correo electrónico a `aem-lighthouse-pilot@adobe.com` a partir de su correo electrónico asociado con su Adobe ID y podemos ayudarle a empezar.

## Correcciones de errores {#bug-fixes}

* El menú **Entornos** ahora se cierra después de activar **[Copiar contenido](/help/implementing/developing/tools/content-copy.md)** modal.
* [La nueva ejecución de una canalización](/help/implementing/cloud-manager/deploy-code.md#reexecute-deployment) ya no se permite si la ejecución anterior no tiene un `commitId` establecido en el estado de fase de compilación.
* Ahora se muestra un mensaje más comprensible para los errores poco frecuentes cuando un usuario hace clic en una canalización en las pantallas **Actividad** o **Canalización**.
* El `contentSetName` ya no falta en los registros y ahora se proporciona en las entradas al iniciar una [copia de contenido](/help/implementing/developing/tools/content-copy.md) operación.
* En determinadas circunstancias excepcionales, ya no es posible iniciar dos ejecuciones desde la misma canalización que conducen a un estado &quot;atascado&quot;.
* Cuando caduca un certificado, los nombres de dominio y las listas de IP permitidas asociadas con el certificado ya no se eliminarán de la CDN.
   * En tales casos, el sitio continuará siendo accesible.
   * [](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)La IU de Cloud Manager proporcionará advertencias avanzadas más visibles de que el certificado SSL está a punto de caducar.
* AEM Se corrigió un problema con la pérdida de acceso de los usuarios a un punto final de publicación en situaciones en las que Sites se agrega como solución a un programa solo de Assets.
