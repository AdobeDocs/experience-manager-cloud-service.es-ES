---
title: Notas de la versión 2025.4.0 de Cloud Manager
description: Obtenga información acerca de la versión de Cloud Manager 2025.4.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6d6e3e452b7910148e22d95a222c1a3b674ea83b
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 60%

---

# Notas de la versión para Cloud Manager 2025.4.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.4.0 en AEM (Adobe Experience Manager) as a Cloud Service.


Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.4.0 en AEM as a Cloud Service es el viernes, 10 de abril de 2025.

La próxima versión planificada es para el viernes, 08 de mayo de 2025.

## Novedades {#what-is-new}

* **(IU): visibilidad de implementación mejorada**

  La página de detalles de ejecución de la canalización en Cloud Manager ahora muestra un mensaje de estado (&quot;*En espera - otra actualización en curso*&quot;) cuando una implementación está esperando a que finalice otra implementación. Este flujo de trabajo facilita la comprensión de la secuenciación durante la implementación del entorno.  <!-- CMGR-66890 -->

  ![Cuadro de diálogo de implementación de desarrollo que muestra detalles y desglose](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(IU) Mejora de validación de dominio**

  Al agregar un dominio, Cloud Manager muestra ahora un error si el dominio ya está instalado en una cuenta de Fastly: &quot;*El dominio ya está instalado en una cuenta de Fastly. Elimínelo primero desde allí antes de agregarlo a Cloud Service.*&quot;

## Programa para primeros usuarios {#early-adoption}

Participe en el programa de adopción anticipada de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades de adopción temprana:

### Usar su propio Git: ahora se admiten GitLab y Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La función **Bring Your Own Git** se ha ampliado para incluir compatibilidad con repositorios externos, como GitLab y Bitbucket. Esta nueva compatibilidad se suma a la compatibilidad ya existente con repositorios de GitHub privados y de empresa. Al añadir estos nuevos repositorios, también puede vincularlos directamente a sus canalizaciones. Puede alojar estos repositorios en plataformas públicas en la nube o dentro de su infraestructura o nube privada. Esta integración también elimina la necesidad de sincronización constante del código con el repositorio de Adobe y proporciona la capacidad de validar las solicitudes de extracción antes de combinarlas en una rama principal.

Las canalizaciones que usan repositorios externos (excepto las alojadas en GitHub) y el **Activador de la implementación** establecido en **Cambios en Git** ahora se inician automáticamente.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Actualmente, las comprobaciones de calidad del código de las solicitudes de extracción listas para usar son exclusivas de los repositorios alojados en GitHub, pero se está trabajando en una actualización para ampliar esta funcionalidad a otros proveedores de Git.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privado/público o de empresa.

### Inicio de AEM {#aem-home}

El inicio de AEM presenta un punto de partida centralizado para administrar contenido, recursos y sitios en Adobe Experience Manager. Diseñado para ofrecer una experiencia personalizada, el inicio de AEM le permite navegar por el ecosistema de forma fluida según sus roles y objetivos. Como guía, proporciona perspectivas clave y acciones recomendadas para ayudarle a lograr sus objetivos de forma eficaz. Con un diseño claro y dirigido por el usuario, el inicio de AEM garantiza un acceso rápido a las herramientas esenciales, lo que permite una experiencia ágil y eficaz en todas las funciones de AEM.

Disponible para los primeros usuarios, el inicio de AEM ofrece una experiencia optimizada centrada en mejorar los flujos de trabajo, priorizar los objetivos y lograr resultados. La inclusión le permite influir en el desarrollo del inicio de AEM al proporcionar comentarios que ayudan a dar forma a su futuro y mejorar su valor para toda la comunidad de AEM.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) desde la dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir la siguiente información:

* La función que mejor se adapta a su perfil: Autor de contenido, Desarrollador, Propietario empresarial, Administrador u Otro (proporcione una descripción).
* Su superficie de acceso principal a AEM: AEM Sites, AEM Assets, AEM Forms, Cloud Manager u Otro (proporcione una descripción).

## Correcciones de errores

* **Problema con los certificados que carecen del campo de nombre común (CN)**

  Cloud Manager ya no emite una NullPointerException (NPE) y una respuesta HTTP 500 al procesar certificados EV/OV que no incluyen un nombre común (CN) en el campo Asunto. Los certificados modernos suelen omitir CN y, en su lugar, utilizan un nombre alternativo del sujeto (SAN). Esta corrección garantiza que la ausencia de CN ya no cause un error durante el proceso de compilación de la configuración cuando SAN está presente. <!-- CMGR-67548 -->

* **Problema de verificación de dominio con coincidencia de certificado incorrecta**

  Cloud Manager ya no verifica incorrectamente los dominios con los certificados incorrectos. Anteriormente, la lógica de validación utilizaba la coincidencia basada en patrones en lugar de la coincidencia exacta, lo que provocaba que dominios como `should-not-be-verified.example.com` aparecieran como verificados debido a la superposición con certificados válidos para `example.com`. Esta corrección garantiza que la validación del dominio ahora compruebe coincidencias exactas, lo que evita asociaciones de certificado erróneas. <!-- CMGR-67225 -->

* **Única forzada para nombres de reenvío de puerto de red avanzada**

  Cloud Manager ahora aplica un nombre único para los reenvíos de puertos de red avanzados. Anteriormente, se permitían nombres duplicados, lo que podía provocar conflictos. Esta corrección garantiza que cada entrada de reenvío de puerto tenga un nombre distinto, de acuerdo con las prácticas recomendadas para la integridad de la configuración de red. <!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

