---
title: Prácticas recomendadas para la integración con [!DNL Adobe Creative Cloud]
description: Las prácticas recomendadas integran una implementación Experience Manager con Adobe Creative Cloud para optimizar los flujos de trabajo de transferencia de recursos y lograr la máxima eficacia.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: eaf08018fbbf1cf1e71db2edce9ea673d546073a
workflow-type: tm+mt
source-wordcount: '3294'
ht-degree: 18%

---


# Prácticas recomendadas para la integración de AEM y Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager (AEM) Assets es una solución de administración de recursos digitales (DAM) que se puede integrar con Adobe Creative Cloud para ayudar a los usuarios de DAM a trabajar con equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

Adobe Creative Cloud ofrece a los equipos creativos un ecosistema de soluciones y servicios para ayudarles a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, así como mercados como Adobe Stock.

Siga leyendo para saber qué integraciones elegir entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>El uso compartido de AEM a carpetas de Creative Cloud ya no está en desuso y ya no se trata a continuación. Adobe recomienda nuevas funciones como el vínculo de recursos de Adobe o AEM aplicación de escritorio para proporcionar a los usuarios creativos acceso a los recursos gestionados en AEM.

## Necesidad de colaboración de creativos, especialistas en mercadotecnia y usuarios de DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superficies involucradas |
|---|---|---|
| Simplifique la experiencia para creativos en equipos de escritorio | Racionalice el acceso a los recursos desde un DAM (AEM Assets) para los profesionales creativos o, en términos más generales, para los usuarios de escritorio que trabajan en aplicaciones nativas de creación de recursos. Necesitan una forma sencilla y sencilla de descubrir, utilizar (abrir), editar y guardar los cambios en AEM, así como cargar nuevos archivos. | Win o Mac Desktop; Aplicaciones Creative Cloud |
| Proporcionar recursos listos para usar y de alta calidad de Adobe Stock | Los especialistas en mercadotecnia ayudan a acelerar el proceso de creación de contenido mediante la ayuda en el descubrimiento y el abastecimiento de recursos. Los profesionales creativos utilizan los recursos aprobados directamente desde sus herramientas creativas. | AEM Assets; Adobe Stock Marketplace; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/sucursales locales y los socios, distribuidores y agencias externos utilizan los recursos aprobados compartidos por la organización principal. La organización desea compartir de forma segura y transparente los recursos creados para una reutilización más amplia. | Brand Portal, Asset Share Commons |

## Las ofertas de Adobe para soportar la necesidad de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas involucradas | Oferta de Adobe | Superficies involucradas |
|---|---|---|
| Los usuarios creativos descubren recursos de AEM, los abren y utilizan, editan y cargan cambios en AEM, así como cargan nuevos archivos en AEM sin salir de las aplicaciones Creative Cloud. | [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator y InDesign |
| Los usuarios empresariales simplifican la apertura y el uso de recursos, la edición y la carga de cambios en AEM y la carga de nuevos archivos en AEM desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no son de Adobe. | [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en) | AEM aplicación de escritorio en el escritorio de Windows y Mac |
| Los especialistas en marketing y los usuarios empresariales descubren, previsualización, otorgan licencias y guardan y gestionan los recursos de Adobe Stock desde AEM. Los recursos con licencia y guardados proporcionan metadatos de Adobe Stock seleccionados para una mejor gestión. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | AEM interfaz web |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas como [AEM Assets Brand Portal](https://helpx.adobe.com/es/experience-manager/brand-portal/user-guide.html), las soluciones que se pueden crear en función de los componentes de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](share-assets.md), mediante la interfaz de usuario [web de Recursos](/help/assets/manage-digital-assets.md) AEM deben revisarse en función de requisitos específicos.

![Conexiones de Creative Cloud para AEM: Decidir qué capacidad utilizar](assets/creative-connections-aem.png)

Decidir qué capacidad utilizar

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | Aplicación de escritorio de AEM | Observaciones o métodos alternativos |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Discover: examinar carpetas AEM | Sí | AEM IU web + acciones de escritorio | Al explorar el recurso compartido de red, desactive las miniaturas para evitar la descarga de archivos binarios de recursos. |
| Discover: acceso a AEM colecciones | Sí | AEM IU web + acciones de escritorio |  |
| Discover: buscar recursos de AEM | Sí | AEM IU web + acciones de escritorio |  |
| Usar - abrir recurso | Sí | Sí - para cualquier aplicación | [Abrir desde ](/help/assets/manage-digital-assets.md#previewing-assets) interfaz web o desde Finder |
| Usar - colocar recurso de AEM en un documento | Sí: incrustación | Sí: vinculación o incrustación | AEM aplicación de escritorio proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para editar | Sí: acción de cierre de compra | Sí: acción abierta (en el recurso compartido de red) | [Desproteger en ](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) AALguarda el recurso en la cuenta de almacenamiento de Creative Cloud del usuario (sincronizado por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de AEM | Sí: recurso disponible en la cuenta de almacenamiento del Creative Cloud del usuario sincronizada con el escritorio. | Sí |  |
| Editar - cargar cambios | Sí: [acción de ingreso](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí |  |
| Cargar: archivo único | Sí: carga el documento activo actual | Sí | [Carga mediante interfaz web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Cargar: varios archivos / estructuras de carpetas jerárquicas | No | Sí | [Carga mediante interfaz](/help/assets/manage-digital-assets.md#uploading-assets) web; Herramienta o secuencia de comandos personalizada |
| Misc: usuario e inicio de sesión | Se reconoce al usuario Creative Cloud que ha iniciado sesión en la aplicación de escritorio Creative Cloud (SSO) | AEM usuario / inicio de sesión | Los usuarios de ambas soluciones cuentan con la cuota de usuario AEM. |
| Misc: red y acceso | Requiere acceso desde el escritorio del usuario a AEM implementación a través de la red | Requiere acceso desde el escritorio del usuario a AEM implementación a través de la red | Adobe Asset Link no comparte el entorno de proxy de red. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Para admitir casos de uso de distribución de recursos, se deben considerar otras soluciones:

* [AEM Assets Brand ](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) Portal para un complemento configurable de Recursos para publicar recursos.

* Las soluciones personalizadas se crean en base al código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* AEM [link share](/help/assets/share-assets.md) para compartir recursos ad hoc mediante vínculos.
* [La ](/help/assets/manage-digital-assets.md) interfaz web de AEM Assets con áreas para partes externas garantizadas por AEM configuración de Control de acceso y con los ajustes de configuración de red/TI necesarios, lo que permite a estos usuarios externos acceder a AEM.

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **Trabajo en curso o trabajo en curso creativo (WIP):** Fase del ciclo vital de los recursos en la que sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **Recursos listos para el proceso creativo:** Recursos que están listos para compartirse con un equipo más amplio o que han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.

* **Aprobaciones de recursos:** Proceso de aprobación que se ejecuta para los recursos ya cargados en DAM, que generalmente incluye aprobaciones de marca, aprobaciones legales, etc.
* **Recurso final:** Recurso que ha pasado por todas las aprobaciones/etiquetado de metadatos y está listo para que lo utilice el equipo superior. Este recurso se almacena en DAM y se pone a disposición de todos los usuarios (o de todos los interesados). Se puede utilizar en canales de marketing o en equipos creativos para crear diseños.

* **Cambio o actualización menor de recursos:** Un cambio rápido y pequeño en un recurso digital. A menudo se realiza como respuesta a una solicitud de edición, revisión o aprobación de recursos (por ejemplo, cambiar la posición, el tamaño del texto, ajustar la saturación/brillo, el color, etc.).
* **Cambio o actualización de recursos principales:** Un cambio en un recurso digital que requiere un trabajo considerable y que a veces debe hacerse durante un período de tiempo más largo. Generalmente incluye varios cambios. El recurso debe guardarse varias veces mientras se actualiza. Las principales actualizaciones de recursos suelen hacer que el recurso entre en una etapa de trabajo en curso.
* **DAM**: Administración de recursos digitales. En este documento, es sinónimo de AEM Experience Manager Assets, a menos que se mencione específicamente lo contrario.
* **Usuario creativo:** Un profesional creativo que crea recursos digitales mediante las aplicaciones y los servicios de Creative Cloud. En algunos casos, un usuario creativo puede ser miembro de un equipo creativo que puede utilizar Creative Cloud, pero no crea recursos digitales (como un director creativo o un administrador de equipo creativo).
* **Usuario de DAM:** Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al utilizar la integración de AEM y Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Este es un breve resumen de las prácticas recomendadas para la integración de AEM y Creative Cloud. Lea el resto de este documento para obtener una comprensión detallada de estos.

* **Para usuarios creativos que trabajan con en Photoshop, InDesign o Illustrator:** Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la gestión del trabajo en curso en los recursos extraídos de AEM
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** Use la aplicación de escritorio de AEM
* **Comprender por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a los recursos de Adobe Stock desde AEM Assets {#access-to-adobe-stock-assets-from-aem-assets}

[La ](/help/assets/aem-assets-adobe-stock.md) integración de AEM y Adobe Stock ofrece a los usuarios AEM la capacidad de buscar, previsualización, obtener licencias y guardar recursos de Adobe Stock en AEM. Los recursos de Adobe Stock con licencia y guardados han seleccionado metadatos de almacenamiento, que pueden utilizarse para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de Adobe se guardan en AEM, se convierten en un AEM Assets normal, con el binario guardado en el repositorio de AEM. Algunos metadatos relacionados con Adobe Stock se guardan para el recurso en AEM; de lo contrario, el proceso de inserción tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, las etiquetas se agregan a estos recursos al guardarlos.
* El recurso guardado en AEM es una copia, no un vínculo de vuelta a Adobe Stock.

**Trabajar con recursos guardados de Adobe Stock en AEM en Creative Cloud**. Esta integración es independiente de Adobe Asset Link, pero Adobe Asset Link reconoce estos recursos guardados de Stock de esa manera y muestra metadatos adicionales y el icono de almacenamiento en estos recursos en la interfaz de usuario de la extensión de Adobe Asset Link en Photoshop, Illustrator o InDesign. Los archivos están disponibles para su exploración, apertura, etc., ya que son recursos AEM normales cuando se guardan en AEM.
Los usuarios creativos que trabajen en aplicaciones Creative Cloud con la extensión Vínculo de recursos de Adobe presente, además de tener acceso a recursos con licencia de Adobe Stock en AEM, también pueden utilizar el panel Bibliotecas Creative Cloud para buscar, previsualización y obtener licencias de recursos de Adobe Stock.
Los recursos de Adobe Stock con licencia y guardados en AEM estarán disponibles para los equipos más amplios que accedan a la implementación de AEM Assets, mientras que los recursos de licencias de creativos de Adobe Stock mediante el panel de bibliotecas de Creative Cloud solo estarán disponibles de forma predeterminada en su cuenta de Creative Cloud.

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y de marketing/línea de negocios (LOB) y elegir las mejores capacidades de soporte, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué los recursos se almacenan en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM hace que sean fácilmente accesibles y asequibles. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan aprovechar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones solo almacenan los recursos que son relevantes para los procesos de mercadotecnia/LOB de flujo descendente (publicándolos en canales como el canal web a través de AEM Sites u otros canales que Adobe Experience Cloud (Marketing Cloud, Advertising Cloud y que Analytics Cloud miden, lo que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan activos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De este modo, DAM almacena principalmente activos que tienen altas posibilidades de aprovechar y evita almacenar activos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de los recursos. DAM proporciona servicios adicionales en torno a los recursos almacenados, como la extracción de metadatos, el control de versiones, la generación de previsualizaciones/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen más tiempo y recursos de infraestructura.

A menudo, no es deseable almacenar todos los recursos y las actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) no suelen estar interesados en almacenar recursos en cada etapa del ciclo vital de los recursos. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Recursos que aún no se han finalizado o que están sujetos a experimentación
* Recursos que no superan el ciclo de revisión creativo/interno del equipo
* En comparación con el activo en cuestión, el equipo tiene mejores candidatos para representar su trabajo en equipos externos

Normalmente, los siguientes recursos de clases se almacenan en DAM:

* Activos que alcanzaron un cierto vencimiento y se consideran listos para compartirse
* Recursos preseleccionados por el equipo creativo
* Formatos de recurso específicos que se pueden utilizar o se solicitan en la mercadotecnia, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos a partir de archivos RAW, TIFF/imágenes de originales PSD)

#### Cuando las actualizaciones de los recursos se almacenan en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla general, solo las actualizaciones de los recursos que son relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la línea de tiempo de recursos de DAM.

Generalmente, los cambios se relacionan con hitos principales en el ciclo de vida de los recursos. Por ejemplo, el recurso listo para la comercialización inicial o una actualización oficial basada en una solicitud o revisión proporcionada por el equipo creativo deben almacenarse y crearse versiones en DAM.

La actualización del equipo creativo para su revisión por parte del equipo de marketing tras una solicitud de cambio en el recurso existente en DAM es un ejemplo de una actualización relevante. Debe almacenarse y crearse una versión en DAM para consulta adicional o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que normalmente no son relevantes:

* Versiones iniciales de los recursos cargados antes de que estén listos para la revisión de marketing
* Cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso del usuario a DAM {#user-access-to-dam}

AEM Assets admite dos tipos de usuarios en función de su acceso a la implementación de AEM Assets. Normalmente, los usuarios dentro de la red empresarial (servidor de seguridad) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Generalmente, los equipos creativos internos o las agencias o los profesionales creativos integrados en la red interna tienen acceso a la instancia de DAM, incluido AEM inicio de sesión. Se puede configurar una infraestructura de red y AEM para permitir el acceso directo a partes externas -generalmente organizaciones de confianza como las agencias que trabajan para un cliente- para tener acceso a AEM a través de la red, por ejemplo, a través de una lista de permitidos VPN o IP.

En estos casos, el vínculo de recursos de Adobe o AEM aplicación de escritorio proporciona un acceso sencillo a los recursos finales o aprobados y le permite guardar en DAM los recursos listos para la creación.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Es posible que las agencias externas y los autónomos que no tienen acceso directo a la instancia de DAM necesiten acceder a los recursos aprobados o deseen añadir sus nuevos diseños al DAM.

Utilice las siguientes estrategias para proporcionar acceso a los activos finales o aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Utilice [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) para distribuir recursos de forma segura a socios externos
* Utilice una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice Control de acceso configurado en la infraestructura de red AEM y necesaria (por ejemplo, VPN e IP permitidas en la lista) para proporcionar a las partes externas acceso a un área específica de contenido en su DAM. Pueden utilizar AEM interfaz de usuario web para obtener recursos y cargar contenido nuevo en su DAM.

#### Trabajos en curso sobre los activos de AEM {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda llevar a cabo actualizaciones importantes de los recursos, a veces denominadas trabajo en curso, sin que todas las ediciones guardadas en el archivo local se carguen también en AEM como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de red utilizado y mantiene la línea de tiempo de los recursos limpia y centrada en actualizaciones importantes y controladas.

Adobe Asset Link oferta una buena compatibilidad para este caso de uso:

* Cuando los usuarios de Photoshop, InDesign o Illustrator intentan editar un archivo, ejecutan una operación de desprotección en el recurso determinado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud del usuario sincronizada con el disco por la aplicación de escritorio de Creative Cloud y el indicador de cierre de compra se activa en AEM del recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo almacenado localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios con cualquier frecuencia necesaria
* Además, como el recurso está en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, puede abrirse o editarse en una aplicación móvil de Creative Cloud dedicada) y puede compartirse con otros usuarios de Creative Cloud con fines de colaboración.
* Cuando el usuario creativo ha terminado con los cambios, puede ejecutar una operación de protección en ese archivo en la aplicación Creative Cloud, con un comentario opcional. El recurso correspondiente de AEM se crea en versiones y se actualiza con el nuevo binario. Los usuarios de AEM, como los especialistas en marketing o los usuarios de LOB, tienen acceso a los principales cambios de recursos o hitos a través de AEM interfaz de usuario de la línea de tiempo de recursos.

AEM aplicación de escritorio proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan en AEM automáticamente después de un breve tiempo. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en AEM y versiones, lo que crearía muchos desafíos de tráfico de red y escalabilidad potencial, sin mencionar versiones innecesarias en AEM.

El método recomendado aquí es utilizar una opción en AEM aplicación de escritorio para desactivar las actualizaciones automatizadas y cargar cambios en los recursos para AEM manualmente, aprovechando la acción de cambios de carga en la interfaz de usuario de estado de recursos de la aplicación.

#### Carga masiva a DAM {#bulk-upload-to-dam}

Es posible que tenga que cargar simultáneamente un número mayor de archivos en DAM en algunos casos, por ejemplo:

* Carga de los resultados de la sesión fotográfica o de proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Carga de recursos seleccionados de un conjunto más grande si la selección se realiza fuera de DAM

Tenga en cuenta que esta descripción se refiere a la carga operativa de archivos (por ejemplo, cada semana o con cada sesión fotográfica), como parte normal del flujo de trabajo del usuario del escritorio. Las migraciones de recursos grandes no se cubren aquí.

Puede aprovechar las siguientes funciones de carga:

* Para cargar carpetas grandes o jerárquicas de forma masiva, utilice AEM aplicación de escritorio que proporcione la funcionalidad [carga de carpetas](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload). También puede cargar estructuras de carpetas jerárquicas. Los recursos se cargan en segundo plano y, por lo tanto, no están vinculados a una sesión de explorador Web
* Para cargar algunos archivos desde una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web de AEM Assets.
* Según los requisitos comerciales, también puede utilizar el cargador personalizado.

#### Administración de recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Compartidos de archivos de red para administrar recursos digitales, el uso del recurso compartido de red asignado por AEM aplicación de escritorio podría considerarse un sustituto conveniente. Al realizar la transición desde los recursos compartidos de archivos de red, AEM interfaz web proporciona un completo conjunto de funciones de administración de recursos digitales que van mucho más allá de lo posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, previsualizaciones, etc.) y AEM aplicación de escritorio proporciona un vínculo práctico para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar AEM aplicación de escritorio para administrar recursos directamente en el recurso compartido de red de AEM Assets. Por ejemplo, evite utilizar AEM aplicación de escritorio para mover o copiar varios archivos. En su lugar, utilice la interfaz de usuario web de AEM Assets para arrastrar carpetas desde Finder/Explorer al recurso compartido de red o utilice la función de carga de carpetas de AEM Assets.

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
