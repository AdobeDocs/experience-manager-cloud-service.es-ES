---
title: Prácticas recomendadas para integrar con  [!DNL Adobe Creative Cloud]
description: Las prácticas recomendadas integran una implementación de Experience Manager con Adobe Creative Cloud para optimizar los flujos de trabajo de transferencia de recursos y lograr la máxima eficiencia.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration, Adobe Asset Link, Desktop App
role: User, Developer, Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '3438'
ht-degree: 14%

---

# Prácticas recomendadas de integración de Adobe Experience Manager y Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Adobe Experience Manager Assets es una solución de administración de activos digitales (DAM) que se puede integrar con Adobe Creative Cloud para ayudar a los usuarios de DAM a trabajar junto con equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

Adobe Creative Cloud proporciona a los equipos creativos un ecosistema de soluciones y servicios para ayudarles a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, y mercados como Adobe Stock.

Continúe leyendo para saber qué integraciones elegir entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>El uso compartido de carpetas de Experience Manager a Creative Cloud ha quedado obsoleto y ya no se cubre a continuación. Adobe recomienda funcionalidades más nuevas, como Adobe Asset Link o la aplicación de escritorio de Experience Manager, para proporcionar a los usuarios creativos acceso a los recursos administrados en Experience Manager.

## Necesidad de Collaboration de creativos, especialistas en marketing y usuarios de DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superficies afectadas |
|---|---|---|
| Simplifique la experiencia para creativos en equipos de escritorio | Optimice el acceso al recurso desde un DAM ([!DNL Assets]) para los profesionales creativos o, más en general, para los usuarios de escritorio que trabajan en aplicaciones nativas de creación de recursos. Necesitan una forma fácil y directa de descubrir, utilizar (abrir), editar y guardar cambios en Experience Manager y cargar nuevos archivos. | Windows o Mac para escritorio; aplicaciones de Creative Cloud |
| Proporcionar recursos de alta calidad listos para usar de [!DNL Adobe Stock] | Los especialistas en marketing ayudan a acelerar el proceso de creación de contenido al ayudar con la obtención y el descubrimiento de recursos. Los profesionales de Creative utilizan los recursos aprobados desde sus herramientas creativas. | [!DNL Assets]; mercado [!DNL Adobe Stock]; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/sucursales locales y los socios externos, distribuidores y agencias utilizan los activos aprobados compartidos por la organización matriz. La organización desea compartir de forma segura y sin problemas los recursos creados para una reutilización más amplia. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Generar automáticamente variaciones predefinidas de recursos cargados | Procese recursos automáticamente mediante la tecnología de transformación y gestión de medios única de Adobe para acciones predefinidas. Cree una lógica personalizada para definir sus propias acciones mediante API y microservicios de recursos. | Interfaz de usuario [!DNL Assets] |

## Ofertas de Adobe para satisfacer las necesidades de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas involucradas | oferta de Adobe | Superficies afectadas |
|---|---|---|
| Los usuarios de Creative descubren recursos de [!DNL Experience Manager], los abren y utilizan, editan y cargan cambios en [!DNL Experience Manager] y cargan nuevos archivos en [!DNL Experience Manager], sin salir de su aplicación [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html?lang=es) | Photoshop, Illustrator y InDesign. |
| Los usuarios empresariales simplifican la apertura y el uso de los recursos, la edición y carga de cambios en [!DNL Experience Manager] y la carga de nuevos archivos en [!DNL Experience Manager] desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no son de Adobe. | Aplicación de escritorio de [[!DNL Experience Manager]  &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Aplicación de escritorio de Experience Manager en Win y Mac para escritorio |
| Los especialistas en marketing y los usuarios empresariales pueden ver, previsualizar, obtener licencias y guardar y administrar los recursos de Adobe Stock desde Experience Manager. Los recursos con licencia y guardados proporcionan metadatos de Adobe Stock seleccionados para mejorar el control. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | Interfaz web de [!DNL Experience Manager] |
| Mejore la colaboración entre los diseñadores de productos digitales y los especialistas en marketing. Permita que los diseñadores utilicen los recursos digitales en los modelos de diseño y de malla metálica en lienzo Adobe XD. | [[!DNL Adobe Asset Link] para [!DNL Adobe XD]](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Los especialistas en marketing pueden crear automáticamente variaciones y derivados basados en recursos cargados y acciones predefinidas creadas mediante la personalización. Utilice esta automatización para mejorar la velocidad del contenido y reducir el esfuerzo manual. | [Automatización de contenido](/help/assets/cc-api-integration.md) | Interfaz web de [!DNL Experience Manager Assets] |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas como [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), las soluciones que se pueden crear en función de los componentes de [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/), [Link Share](share-assets.md), mediante la [interfaz de usuario web de Experience Manager Assets](/help/assets/manage-digital-assets.md) deben revisarse según los requisitos específicos.

![Conexiones Creative Cloud para Experience Manager: Decidir qué capacidad utilizar](assets/creative-connections-aem.png)

Decidir qué capacidad utilizar

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | aplicación de escritorio de Experience Manager | Observaciones o métodos alternativos |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Descubrir: examinar carpetas | Sí | IU web de Experience Manager + acciones del escritorio | Al examinar el recurso compartido de red, desactive las miniaturas para evitar la descarga de archivos binarios de recursos. |
| Discover: acceso a colecciones | Sí | IU web de Experience Manager + acciones del escritorio |  |
| Discover: buscar recursos | Sí | IU web de Experience Manager + acciones del escritorio |  |
| Uso: Abrir recurso | Sí | Sí, para cualquier aplicación | [Abrir desde la interfaz web](/help/assets/manage-digital-assets.md#previewing-assets) o desde el Finder |
| Uso: coloque un recurso de Experience Manager en un documento | Sí: incrustación | Sí: vinculación o incrustación | La aplicación de escritorio de Experience Manager proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para editar | Sí: acción de salida | Sí: Abrir acción (en el recurso compartido de red) | [Al desprotegerlo en AAL](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html), se guarda el recurso en la cuenta de almacenamiento de Creative Cloud del usuario (sincronizada por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de Experience Manager | Sí, el recurso está disponible en la cuenta de almacenamiento de Creative Cloud del usuario sincronizada con el equipo de escritorio. | Sí |  |
| Editar: cambios de carga | Sí: [acción de protección](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí |  |
| Cargar: un solo archivo | Sí: carga el documento activo actual | Sí | [Cargar mediante interfaz web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Cargar: varios archivos/estructuras de carpetas jerárquicas | No | Sí | [Cargar mediante interfaz web](/help/assets/manage-digital-assets.md#uploading-assets); herramienta o script personalizado |
| Varios: usuario e inicio de sesión | Se reconoce el inicio de sesión único (SSO) de un usuario de Creative Cloud que haya iniciado sesión en la aplicación de escritorio de Creative Cloud | Usuario/inicio de sesión de Experience Manager | Los usuarios de ambas soluciones cuentan con la cuota de usuarios de Experience Manager. |
| Varios: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación de Experience Manager a través de la red | Requiere acceso desde el escritorio del usuario a la implementación de Experience Manager a través de la red | Adobe Asset Link no comparte el entorno de proxy de red. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Para admitir casos de uso de distribución de recursos, tenga en cuenta las siguientes opciones:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para un complemento configurable de Assets para publicar recursos.

* Se crean soluciones personalizadas basadas en el código base [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/).
* Experience Manager [vínculo compartido](/help/assets/share-assets.md) para compartir recursos bajo demanda mediante vínculos.
* [Interfaz web de Assets](/help/assets/manage-digital-assets.md) con áreas para terceros externos protegidos por la configuración de Control de acceso de Experience Manager y con los ajustes de configuración de red/TI necesarios, lo que proporciona a estos usuarios externos acceso a Experience Manager.

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **Trabajo en curso o trabajo en curso creativo (WIP):** Fase del ciclo vital de los recursos en la que sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **Recursos listos para el proceso creativo:** Recursos que están listos para compartirse con un equipo más amplio o que han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.

* **Aprobaciones de recursos:** Proceso de aprobación que se ejecuta para los recursos ya cargados en DAM, que generalmente incluye aprobaciones de marca, aprobaciones legales, etc.
* **Recurso final:** Recurso que ha pasado por todas las aprobaciones/etiquetado de metadatos y está listo para que lo utilice el equipo superior. Este recurso se almacena en DAM y se pone a disposición de todos los usuarios (o de todos los interesados). Se puede utilizar en canales de marketing o en equipos creativos para crear diseños.

* **Cambio o actualización menor de recursos:** Un cambio rápido y pequeño en un recurso digital. A menudo se realiza como respuesta a una solicitud de edición, revisión o aprobación de recursos (por ejemplo, cambiar la posición, el tamaño del texto, ajustar la saturación/brillo, el color, etc.).
* **Cambio o actualización de recursos principales:** Un cambio en un recurso digital que requiere un trabajo considerable y que a veces debe hacerse durante un período de tiempo más largo. Generalmente incluye varios cambios. El recurso debe guardarse varias veces mientras se actualiza. Las principales actualizaciones de recursos suelen hacer que el recurso entre en una etapa de trabajo en curso.
* **DAM**: Administración de recursos digitales. En este documento, es sinónimo de Experience Manager Assets, a menos que se mencione específicamente lo contrario.
* **Usuario creativo:** Un profesional creativo que crea recursos digitales mediante las aplicaciones y los servicios de Creative Cloud. En algunos casos, un usuario creativo puede ser miembro de un equipo creativo que puede utilizar Creative Cloud, pero no crea recursos digitales (como un director creativo o un administrador de equipo creativo).
* **Usuario de DAM:** Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo, un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al utilizar la integración de Experience Manager y Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Este es un breve resumen de las prácticas recomendadas para la integración de Experience Manager y Creative Cloud. Lea el resto de este documento para comprender en detalle estos aspectos.

* **Para usuarios creativos que trabajan en Photoshop, InDesign o Illustrator:** Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la administración del trabajo en curso en los recursos desprotegidos de Experience Manager
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** use la aplicación de escritorio de Experience Manager
* **Comprender por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a los recursos de Adobe Stock desde Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

[Integración de Experience Manager y Adobe Stock](/help/assets/aem-assets-adobe-stock.md) permite a los usuarios de Experience Manager buscar, previsualizar, obtener licencias y guardar recursos de Adobe Stock en Experience Manager. Los recursos de Adobe Stock con licencia y guardados tienen seleccionados metadatos de Stock, que se pueden utilizar para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de Adobe Stock se guardan en Experience Manager, pasan a ser una Experience Manager Assets normal, con archivo binario guardado en el repositorio de Experience Manager. Algunos metadatos relacionados con Adobe Stock se guardan para el recurso en Experience Manager; de lo contrario, el proceso de ingesta tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, estas se añaden a estos recursos al guardarlas.
* El recurso guardado en Experience Manager es una copia, no un vínculo de vuelta a Adobe Stock.

**Trabajando con recursos guardados desde Adobe Stock en Experience Manager en Creative Cloud**. Esta integración es independiente de Adobe Asset Link, pero Adobe Asset Link reconoce estos recursos guardados de Stock de esa manera y muestra metadatos adicionales e iconos de Stock en estos recursos en la interfaz de usuario de la extensión Adobe Asset Link en Photoshop, Illustrator o InDesign. Los archivos están disponibles para explorarlos, abrirlos, etc., ya que son recursos normales de Experience Manager cuando se guardan en Experience Manager.
Los usuarios de Creative que trabajan en aplicaciones de Creative Cloud con la extensión Adobe Asset Link presente, además de tener acceso a recursos con licencia de Adobe Stock en Experience Manager, también pueden utilizar el panel Creative Cloud Libraries para buscar, previsualizar y obtener licencias de recursos de Adobe Stock.
Assets de Adobe Stock con licencia y guardado en Experience Manager está disponible para los equipos que acceden a la implementación de Experience Manager Assets, mientras que los creativos que otorgan licencias a recursos de Adobe Stock a través del panel Creative Cloud Libraries solo las ponen a su disposición de forma predeterminada en su cuenta de Creative Cloud.

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y de marketing/línea de negocios (LOB) y elegir las mejores capacidades de soporte, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué se almacenan los recursos en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM los hace fácilmente accesibles y localizables. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan utilizar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones eligen almacenar únicamente los recursos relevantes para los procesos de marketing descendente/LOB (publicación en canales como el canal web a través de Experience Manager Sites u otros canales ofrecidos por Adobe Experience Cloud: Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan recursos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De este modo, DAM almacena principalmente recursos que tienen altas probabilidades de utilizarse y evita almacenar recursos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de recursos. DAM proporciona servicios adicionales relacionados con los recursos almacenados, como la extracción de metadatos, el control de versiones, la generación de previsualizaciones/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen tiempo y recursos de infraestructura adicionales.

A menudo, no es deseable almacenar todos los recursos y las actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos (y las organizaciones) de Creative generalmente no están interesados en almacenar recursos en cada fase del ciclo de vida del recurso. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Assets que aún no se han finalizado o que están sujetos a experimentación
* Assets que no superan el ciclo de revisión del equipo creativo/interno
* En comparación con el recurso en cuestión, el equipo tiene mejores candidatos para representar su trabajo ante equipos externos

Normalmente, los siguientes recursos de clases se almacenan en DAM:

* Assets que ha alcanzado un cierto grado de madurez y que se considera que está listo para compartirse
* Assets que fueron preseleccionados por el equipo creativo
* Formatos de recurso específicos que el marketing puede utilizar o solicitar, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos de archivos RAW, archivos TIFF/imágenes de PSD originales)

#### Cuando se almacenan actualizaciones de recursos en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla general, solo las actualizaciones de los recursos relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la cronología de recursos de DAM.

Normalmente, los cambios están relacionados con los hitos principales del ciclo vital del recurso. Por ejemplo, el recurso inicial listo para el marketing o una actualización oficial basada en la solicitud/revisión proporcionada por el equipo creativo debe almacenarse y tener versiones en DAM.

La actualización del equipo creativo para que la revise el equipo de marketing después de una solicitud de cambio en el recurso existente en DAM es un ejemplo de actualización relevante. Se debe almacenar y crear versiones en DAM para obtener más información o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que generalmente no son relevantes:

* Versiones tempranas de los recursos cargados antes de que estén listos para la revisión de marketing
* Realice cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso del usuario a DAM {#user-access-to-dam}

Experience Manager Assets admite dos tipos de usuarios en función de su acceso a la implementación de Experience Manager Assets. Normalmente, los usuarios dentro de la red empresarial (cortafuegos) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios de Creative con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Normalmente, los equipos creativos internos o las agencias/los profesionales creativos incorporados a la red interna tienen acceso a la instancia de DAM, incluido el inicio de sesión de Experience Manager. Experience Manager y las infraestructuras de red se pueden configurar para permitir el acceso directo a terceros externos (por lo general, organizaciones de confianza como agencias que trabajan para un cliente) y tener acceso a Experience Manager a través de la red, por ejemplo, mediante una lista de permitidos VPN o IP.

En estos casos, Adobe Asset Link o la aplicación de escritorio de Experience Manager proporcionan un acceso fácil a los recursos finales/aprobados y le permiten guardar recursos listos para la creatividad en DAM.

#### Usuarios de Creative sin acceso a DAM {#creative-users-without-access-to-dam}

Las agencias externas y los autónomos sin acceso directo a la instancia de DAM pueden requerir acceso a recursos aprobados o querer agregar sus nuevos diseños a DAM.

Utilice las siguientes estrategias para proporcionar acceso a los recursos finales/aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Use [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir recursos de forma segura a socios externos
* Use una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice la configuración de Control de acceso de Experience Manager y la infraestructura de red necesaria (por ejemplo, lista de VPN e IP permitidas) para que las partes externas tengan acceso a un área de contenido dedicada en su DAM. Pueden utilizar la interfaz de usuario web de Experience Manager para obtener recursos y cargar contenido nuevo en el DAM.

#### Trabajo en curso en los recursos de Experience Manager {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda realizar actualizaciones importantes en los recursos, a veces denominadas trabajo en curso, sin que todas las ediciones guardadas en el archivo local también se carguen en Experience Manager como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de la red utilizado y mantiene la cronología de los recursos limpia y centrada en actualizaciones importantes y controladas.

Adobe Asset Link ofrece una buena compatibilidad con este caso de uso:

* Cuando los usuarios de Photoshop, InDesign o Illustrator intentan editar un archivo, ejecutan una operación de desprotección en el recurso dado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud de los usuarios sincronizada con el disco mediante la aplicación de escritorio de Creative Cloud y el indicador de cierre de compra se activa en Experience Manager para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo almacenado localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios en cualquier frecuencia requerida
* Además, como el recurso se encuentra en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, se puede abrir o editar en una aplicación móvil de Creative Cloud dedicada) y se puede compartir con otros usuarios de Creative Cloud para colaborar.
* Cuando el usuario creativo haya terminado con los cambios, puede ejecutar una operación de protección en ese archivo en su aplicación de Creative Cloud, con un comentario opcional. El recurso correspondiente en Experience Manager tiene una versión y se actualiza a con el nuevo binario. Los usuarios de Experience Manager, como los especialistas en marketing o los usuarios de LOB, tienen acceso a los cambios de recursos importantes o a los hitos a través de la IU de cronología de recursos de Experience Manager.

La aplicación de escritorio de Experience Manager proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan automáticamente en Experience Manager después de un breve tiempo. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en Experience Manager y se versionarían, lo que crearía una gran cantidad de tráfico de red y posibles desafíos de escalabilidad, sin mencionar las versiones innecesarias en Experience Manager.

El método recomendado aquí es utilizar una opción en la aplicación de escritorio de Experience Manager para desactivar las actualizaciones automatizadas y cargar cambios en los recursos en Experience Manager manualmente, mediante la acción cargar cambios en la IU de estado de los recursos de la aplicación.

#### Carga masiva en DAM {#bulk-upload-to-dam}

Es posible que deba cargar simultáneamente un número mayor de archivos en DAM en algunos casos, por ejemplo:

* Cargar resultados de sesiones de fotos o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Cargar los recursos seleccionados de un conjunto mayor si la selección se realiza fuera de DAM

Esta descripción hace referencia a la carga de archivos de forma operativa (por ejemplo, cada semana o con cada sesión fotográfica ), como parte normal del flujo de trabajo del usuario de escritorio. Las migraciones de recursos grandes no están cubiertas aquí.

Puede utilizar las siguientes capacidades de carga:

* Para cargar carpetas grandes y jerárquicas de forma masiva, utiliza la aplicación de escritorio de Experience Manager que proporciona la funcionalidad [folder upload](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets). También puede cargar estructuras de carpetas jerárquicas. Assets se carga en segundo plano y, por lo tanto, no está vinculado a una sesión del explorador web
* Para cargar algunos archivos desde una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web de Experience Manager Assets.
* Según sus necesidades comerciales, también puede utilizar un cargador personalizado.

#### Administración de recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Recursos compartidos de archivos de red para administrar recursos digitales, el simple uso del recurso compartido de red asignado por la aplicación de escritorio de Experience Manager podría considerarse como un sustituto conveniente. Al realizar la transición desde recursos compartidos de archivos de red, la interfaz web de Experience Manager proporciona un completo conjunto de funciones de administración de recursos digitales que van mucho más allá de las posibles en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, previsualizaciones, etc.). La aplicación de escritorio de Experience Manager proporciona un práctico vínculo para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar la aplicación de escritorio de Experience Manager para administrar recursos directamente en el recurso compartido de red de Experience Manager Assets. Por ejemplo, evite utilizar la aplicación de escritorio de Experience Manager para mover o copiar varios archivos. En su lugar, utilice la interfaz de usuario web de Experience Manager Assets para arrastrar carpetas desde el Finder/Explorer al recurso compartido de red o utilice la función de carga de carpetas de Experience Manager Assets.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con recursos](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos de red](use-assets-across-connected-assets-instances.md)
* [Informes de recurso](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
* [Publicación de recursos en AEM y Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
