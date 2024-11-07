---
title: Notas de la versión para Cloud Manager 2024.11.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2024.11.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 29%

---

# Notas de la versión para Cloud Manager 2024.11.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

Obtenga información acerca del lanzamiento de Cloud Manager AEM 2024.11.0 en el as a Cloud Service de (Adobe Experience Manager) en la.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2024.11.0 en AEM as a Cloud Service es el 7 de noviembre de 2024.

La próxima versión planificada es el 5 de diciembre de 2024.

## Novedades {#what-is-new}

* Experimente la última innovación en Edge Delivery Services con AEM Cloud Service, ahora disponible para explorar en su programa de zona protegida. [Más información](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* La página Configuración de dominio de AEM Cloud Manager ahora incluye una función de búsqueda que permite localizar rápidamente dominios por nombre. Puede introducir palabras clave en el campo de búsqueda para filtrar y mostrar los dominios coincidentes, lo que facilita la administración eficaz de varios dominios. Además, la página ofrece filtros de estado, como **Verificado** y **No verificado**, para restringir aún más los resultados de búsqueda. <!-- (CMGR-62615) -->

![Campo de búsqueda en la configuración de dominio](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## Programa para primeros usuarios {#early-adoption}

Participe en nuestro programa para primeros usuarios de Cloud Manager y tenga la oportunidad de probar algunas de las próximas funciones.

### AEM Página de inicio {#aem-home}

AEM La página de inicio es un nuevo punto de partida centralizado para administrar el contenido, los recursos y los sitios en Adobe Experience Manager. AEM AEM Diseñado para proporcionar una experiencia personalizada, el Hogar de la aplicación ayuda a los usuarios a navegar sin problemas por el ecosistema en función de sus roles y objetivos. Está diseñado para servir de guía y ofrece perspectivas clave y acciones recomendadas para lograr los resultados deseados de forma eficaz. AEM AEM Al presentar una hoja de ruta clara y basada en el perfil del usuario, el Hogar de los usuarios garantiza que estos encuentren rápidamente lo que necesitan para lograr sus objetivos, lo que permite una experiencia más ágil y eficaz en todas las capacidades de la.

AEM Disponible para los clientes que la adoptaron por primera vez, el Hogar de la ofrece una primera mirada a una experiencia mejorada que optimiza los flujos de trabajo, prioriza los objetivos e impulsa los resultados. AEM AEM Al optar por participar, tiene la oportunidad de dar forma al desarrollo de la página de inicio de la comunidad, proporcionando comentarios que influyen en su evolución para servir mejor a la comunidad de la.

Si está interesado en probar esta nueva funcionalidad y compartir sus comentarios, envíe un correo electrónico a [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir la siguiente información:

* La función que mejor se adapta a su perfil: Autor de contenido, Desarrollador, Propietario empresarial, Administrador u Otro (proporcione una descripción).
* AEM Su superficie de acceso principal al: AEM Sites, AEM Assets, AEM Forms, Cloud Manager u Otros (proporcione una descripción).

### Usar su propio Git: ahora se admiten GitLab y Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

La función **Usar su propio Git** se ha ampliado para incluir compatibilidad con repositorios externos como GitLab y Bitbucket. Esta nueva compatibilidad se suma a la compatibilidad ya existente con repositorios de GitHub privados y de empresa. Al añadir estos nuevos repositorios, también puede vincularlos directamente a sus canalizaciones. Puede alojar estos repositorios en plataformas públicas en la nube o dentro de su infraestructura o nube privada. Esta integración también elimina la necesidad de sincronización constante del código con el repositorio de Adobe y proporciona la capacidad de validar las solicitudes de extracción antes de combinarlas en una rama principal.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>Actualmente, las comprobaciones de calidad del código de las solicitudes de extracción listas para usar son exclusivas de los repositorios alojados en GitHub, pero se está trabajando en una actualización para ampliar esta funcionalidad a otros proveedores de Git.

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privada/pública o empresarial. —>


## Corrección de errores

* Una actualización reciente solucionó un problema en SonarQube en el que las contraseñas codificadas no se detectaban en determinados casos. La corrección ahora incluye una comprobación de patrones ampliada y se alinea con los estándares de detección predeterminados en SonarQube. <!-- CMGR-62682 -->
* Al intentar actualizar un certificado SSL en Cloud Manager, aparecería un error desconocido después de hacer clic en **[!UICONTROL Actualizar]** en el cuadro de diálogo **[!UICONTROL Ver y actualizar el certificado SSL]**. <!-- CMGR-62848 -->
* En Cloud Manager, las actualizaciones de certificados SSL fallaban con el error &quot;El nuevo certificado no coincide con los dominios existentes&quot;, incluso cuando los dominios eran idénticos pero tenían diferencias en mayúsculas y minúsculas. La actualización ahora reconoce los dominios como que no distinguen entre mayúsculas y minúsculas, alineándose con los estándares RFC. <!-- CMGR-62844 -->
* En Cloud Manager, los enlaces de Lista de permitidos IP permanecían atascados en un estado de ejecución porque faltaban vínculos de clave externa a configuraciones de dominio. La corrección ahora garantiza que los enlaces de Lista de permitidos IP se vinculen correctamente a las configuraciones de dominio asociadas. <!-- CMGR-62838 -->
* Cloud Manager valida el estado de OCSP (Online Certificate Status Protocol) de un certificado SSL. El Adobe recomienda validar también la integridad del certificado localmente mediante una herramienta como `openssl verify -untrusted intermediate.pem certificate.pem` antes de instalarlo mediante Cloud Manager. Para obtener más información, consulte la [documentación sobre los requisitos de certificado SSL](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements). <!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->