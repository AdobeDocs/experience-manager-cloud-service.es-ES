---
title: Prácticas recomendadas para la integración con [!DNL Adobe Creative Cloud]
description: Las prácticas recomendadas integran una implementación de Experience Manager con Adobe Creative Cloud para optimizar los flujos de trabajo de transferencia de recursos y lograr la máxima eficacia.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration,Adobe Asset Link,Desktop App
role: Architect,User,Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 80ac947976bab2b0bfedb4ff9d5dd4634de6b4fc
workflow-type: tm+mt
source-wordcount: '3495'
ht-degree: 16%

---

# Prácticas recomendadas para la integración de Adobe Experience Manager y Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

Adobe Experience Manager Assets es una solución de administración de recursos digitales (DAM) que se puede integrar con Adobe Creative Cloud para ayudar a los usuarios de DAM a trabajar con equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

Adobe Creative Cloud proporciona a los equipos creativos un ecosistema de soluciones y servicios que les ayudan a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, así como mercados como Adobe Stock.

Siga leyendo para saber qué integraciones escoger entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>El uso compartido de Experience Manager a Creative Cloud ya no se utiliza y ya no se trata más adelante. Adobe recomienda funciones más nuevas, como Adobe Asset Link o la aplicación de escritorio de Experience Manager, para proporcionar a los usuarios creativos acceso a los recursos administrados en Experience Manager.

## Necesidad de colaboración de creativos, especialistas en marketing y usuarios de DAM {#collaboration-need-of-creatives-marketers-and-dam-users}

| Requisitos  | Caso de uso | Superficies implicadas |
|---|---|---|
| Simplificar la experiencia para creativos en equipos de escritorio | Optimice el acceso a los recursos desde un DAM ([!DNL Assets]) para profesionales creativos o, en términos más generales, para usuarios de escritorio que trabajen en aplicaciones nativas de creación de recursos. Necesitan una forma sencilla y sencilla de descubrir, utilizar (abrir), editar y guardar cambios en el Experience Manager, así como cargar nuevos archivos. | escritorio Win o Mac; aplicaciones Creative Cloud |
| Proporcionar recursos listos para usar de alta calidad desde [!DNL Adobe Stock] | Los especialistas en marketing ayudan a acelerar el proceso de creación de contenido mediante la asistencia en el abastecimiento y descubrimiento de recursos. Los profesionales creativos utilizan los recursos aprobados directamente desde sus herramientas creativas. | [!DNL Assets]; [!DNL Adobe Stock] marketplace; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/las sucursales locales y los socios, distribuidores y agencias externos utilizan los recursos aprobados compartidos por la organización principal. La organización desea compartir de forma segura y transparente los recursos creados para una reutilización más amplia. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Generar automáticamente variaciones predefinidas de los recursos cargados | Procese automáticamente los recursos aprovechando la tecnología única de transformación y gestión de medios de Adobe para las acciones predefinidas. Cree una lógica personalizada para definir sus propias acciones mediante API y microservicios de recursos. | [!DNL Assets]Interfaz de usuario |

## Ofertas de Adobe para apoyar la necesidad de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas implicadas | oferta de Adobe | Superficies implicadas |
|---|---|---|
| Los usuarios creativos descubren recursos desde [!DNL Experience Manager], ábralas y utilícelas, edite y cargue cambios en [!DNL Experience Manager], así como cargar nuevos archivos en [!DNL Experience Manager], sin dejar su [!DNL Creative Cloud] aplicación. | [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator y InDesign. |
| Los usuarios empresariales simplifican la apertura y el uso de recursos, editan y cargan cambios en [!DNL Experience Manager]y cargando nuevos archivos en [!DNL Experience Manager] desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no sean de Adobe. | Aplicación de escritorio de [[!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | aplicación de escritorio de Experience Manager en Win y Mac Desktop |
| Los especialistas en marketing y los usuarios empresariales descubren, previsualizan, otorgan licencias y guardan, y administran los recursos de Adobe Stock desde Experience Manager. Los recursos con licencia y guardados proporcionan metadatos de Adobe Stock seleccionados para un mejor gobierno. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interfaz web |
| Mejore la colaboración entre diseñadores de productos digitales y especialistas en marketing. Permita que los diseñadores utilicen los recursos digitales en los modelos de diseño y de modelo de alambre en el lienzo de Adobe XD. | [[!DNL Adobe Asset Link] para [!DNL Adobe XD]](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Los especialistas en marketing pueden crear automáticamente variaciones y derivados basados en recursos cargados y acciones predefinidas creadas mediante la personalización. Utilice esta automatización para mejorar la velocidad de contenido y reducir el esfuerzo manual. | [Automatización del contenido](/help/assets/cc-api-integration.md) | [!DNL Experience Manager Assets] interfaz web |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Soluciones alternativas como [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), soluciones basadas en [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) componentes, [Compartir vínculos](share-assets.md), usando [Interfaz de usuario web de Experience Manager Assets](/help/assets/manage-digital-assets.md) deben revisarse sobre la base de requisitos específicos.

![Conexiones del Creative Cloud para el Experience Manager: Decidir qué capacidad utilizar](assets/creative-connections-aem.png)

Decidir qué capacidad utilizar

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

| Caso de uso | Adobe Asset Link | Aplicación de escritorio de Experience Manager | Observaciones o métodos alternativos |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Discover: examinar carpetas | Sí | IU web de Experience Manager + acciones de escritorio | Al examinar el recurso compartido de red, desactive las miniaturas para evitar descargar archivos binarios de recursos. |
| Discover: acceso a colecciones | Sí | IU web de Experience Manager + acciones de escritorio |  |
| Discover : buscar recursos | Sí | IU web de Experience Manager + acciones de escritorio |  |
| Usar - Abrir recurso | Sí | Sí: para cualquier aplicación | [Abrir desde la interfaz web](/help/assets/manage-digital-assets.md#previewing-assets) o desde Finder |
| Uso: colocación de un recurso de un Experience Manager en un documento | Sí: incrustar | Sí: vinculación o incrustación | La aplicación de escritorio de Experience Manager proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para edición | Sí: acción de cierre de compra | Sí: acción abierta (en el recurso compartido de red) | [Extracción en AAL](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) guarda el recurso en la cuenta de almacenamiento de creative cloud del usuario (sincronizada por la aplicación Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera del Experience Manager | Sí: el recurso está disponible en la cuenta de almacenamiento del Creative Cloud del usuario sincronizada con el escritorio. | Sí |  |
| Editar: cargar cambios | Sí - [Acción de protección](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí |  |
| Cargar: un solo archivo | Sí: carga el documento activo actual | Sí | [Carga mediante la interfaz web](/help/assets/manage-digital-assets.md#uploading-assets) |
| Cargar: varios archivos / estructuras de carpetas jerárquicas | No | Sí | [Carga mediante la interfaz web](/help/assets/manage-digital-assets.md#uploading-assets); Herramienta o secuencia de comandos personalizada |
| Misc: usuario e inicio de sesión | Se reconoce el nombre del usuario Creative Cloud que ha iniciado sesión en la aplicación de escritorio de Creative Cloud (SSO) | usuario Experience Manager / inicio de sesión | Los usuarios de ambas soluciones cuentan con la cuota de usuario del Experience Manager. |
| Misc: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación del Experience Manager a través de la red | Requiere acceso desde el escritorio del usuario a la implementación del Experience Manager a través de la red | Adobe Asset Link no comparte el entorno de proxy de red. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Para admitir casos de uso de distribución de recursos, considere las siguientes opciones:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para un complemento configurable de Assets para publicar recursos.

* Las soluciones personalizadas se crean en función de [Asset Share Commons](https://opensource.adobe.com/asset-share-commons/) base de código.
* Experience Manager [compartir vínculo](/help/assets/share-assets.md) para compartir recursos ad hoc mediante vínculos.
* [Interfaz web de recursos](/help/assets/manage-digital-assets.md) con áreas para partes externas aseguradas por la configuración de Control de Acceso de Experience Manager y con los ajustes de configuración de red/TI necesarios, lo que proporciona a estos usuarios externos acceso al Experience Manager.

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
* **Usuario de DAM:** Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al utilizar la integración de Experience Manager y Creative Cloud {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Este es un breve resumen de las prácticas recomendadas para la integración de Experience Manager y Creative Cloud. Lea el resto de este documento para conocer en detalle estos aspectos.

* **Para usuarios creativos que trabajan en Photoshop, InDesign o Illustrator:** Adobe Asset Link proporciona la mejor experiencia de usuario, incluida la gestión limpia del trabajo en curso en los recursos extraídos del Experience Manager
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** usar aplicación de escritorio de Experience Manager
* **Comprender por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a los recursos de Adobe Stock desde Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

[Integración de Experience Manager y Adobe Stock](/help/assets/aem-assets-adobe-stock.md) proporciona a los usuarios Experience Manager la capacidad de buscar, previsualizar, obtener licencias y guardar recursos de Adobe Stock en Experience Manager. Los recursos de Adobe Stock con licencia y guardados han seleccionado metadatos de Stock, que pueden utilizarse para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de existencias de Adobe se guardan en Experience Manager, se convierten en un Experience Manager Assets normal, con binario guardado en el repositorio de Experience Manager. Algunos metadatos relacionados con Adobe Stock se guardan para el recurso en Experience Manager; de lo contrario, el proceso de ingesta tiene el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, estas se añaden a estos recursos al guardarlos.
* El recurso guardado en el Experience Manager es una copia, no un vínculo en Adobe Stock.

**Uso de recursos guardados desde Adobe Stock en Experience Manager en Creative Cloud**. Esta integración es independiente de Asset Link de Adobe, pero Asset Link de Adobe reconoce estos recursos guardados de Stock de esa manera y muestra metadatos adicionales y el icono Stock de estos recursos en la interfaz de usuario de la extensión Asset Link de Adobe en Photoshop, Illustrator o InDesign. Los archivos están disponibles para explorar, abrir, etc., ya que son recursos de Experience Manager normales cuando se guardan en Experience Manager.
Los usuarios creativos que trabajen en aplicaciones de Creative Cloud con la extensión de Adobe Asset Link presente, además de tener acceso a recursos ya licenciados de Adobe Stock en Experience Manager, también pueden usar el panel Bibliotecas de Creative Cloud para buscar, obtener una vista previa y obtener una licencia para los recursos de Adobe Stock.
Los recursos de Adobe Stock con licencia y guardados en Experience Manager están disponibles para los equipos más amplios que acceden a la implementación de Experience Manager Assets, mientras que los recursos de licencia de creativos de Adobe Stock mediante el panel Bibliotecas de Creative Cloud solo se ponen a disposición de ellos de forma predeterminada en su cuenta de Creative Cloud.

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y los equipos de marketing/línea de negocios (LOB) y elegir las mejores capacidades de asistencia, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué los recursos se almacenan en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM los hace fácilmente accesibles y asequibles. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan aprovechar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones solo almacenan recursos que son relevantes para los procesos de marketing/LOB descendentes (publicándolos en canales como el canal web a través de Experience Manager Sites u otros canales servidos por Adobe Experience Cloud: Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, lo que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan activos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De esta manera, DAM almacena principalmente activos que tienen altas posibilidades de ser aprovechados y evita almacenar activos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de recursos. DAM proporciona servicios adicionales en torno a los recursos almacenados, incluida la extracción de metadatos, el control de versiones, la generación de vistas previas/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen tiempo y recursos de infraestructura adicionales.

A menudo, no es deseable almacenar todos los recursos y actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) no suelen estar interesados en almacenar recursos en cada etapa del ciclo de vida de los recursos. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Activos que aún no se han finalizado o que están sujetos a experimentación
* Recursos que no superan el ciclo de revisión del equipo creativo/interno
* En comparación con el recurso en cuestión, el equipo tiene mejores candidatos para representar su trabajo en equipos externos

Normalmente, las siguientes clases de activos se almacenan en DAM:

* Activos que han alcanzado un cierto vencimiento y que se consideran listos para compartirse
* Recursos preseleccionados por el equipo creativo
* Formatos de recurso específicos que el marketing puede utilizar o solicitar, en función de un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos a partir de archivos RAW, TIFF/imágenes de originales PSD)

#### Cuando las actualizaciones de los recursos se almacenan en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla, solo las actualizaciones de los recursos que sean relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la cronología de recursos de DAM.

Normalmente, los cambios se relacionan con hitos importantes del ciclo vital de los recursos. Por ejemplo, el recurso listo para el marketing inicial o una actualización oficial basada en una solicitud o revisión proporcionada por el equipo creativo deben almacenarse y crearse versiones en DAM.

La actualización del equipo creativo para que la revise el equipo de marketing después de una solicitud de cambio en el recurso existente en DAM es un ejemplo de una actualización relevante. Debe almacenarse y crearse una versión en DAM para su posterior referencia o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que normalmente no son relevantes:

* Versiones anteriores de recursos cargados antes de que estén listos para su revisión de marketing
* Cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso de usuario a DAM {#user-access-to-dam}

Experience Manager Assets admite dos tipos de usuarios en función de su acceso a la implementación de Experience Manager Assets. Normalmente, los usuarios de la red empresarial (firewall) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Normalmente, los equipos creativos o agencias/profesionales creativos internos incorporados a la red interna tienen acceso a la instancia de DAM, incluido el inicio de sesión del Experience Manager. Se puede configurar la infraestructura de Experience Manager y red para permitir el acceso directo a partes externas (generalmente organizaciones de confianza como las agencias que trabajan para un cliente) para tener acceso al Experience Manager a través de la red, por ejemplo, a través de una lista de permitidos VPN o IP.

En estos casos, Adobe Asset Link o la aplicación de escritorio de Experience Manager proporcionan fácil acceso a los recursos finales/aprobados y le permiten guardar en DAM recursos listos para la creación.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Las agencias externas y los trabajadores independientes sin acceso directo a la instancia de DAM pueden requerir acceso a los recursos aprobados o desean añadir sus nuevos diseños a DAM.

Utilice las siguientes estrategias para proporcionar acceso a los recursos finales/aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Uso [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir activos de forma segura a socios externos
* Utilice una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Utilice Access Control configurado en el Experience Manager y la infraestructura de red necesaria (por ejemplo, la lista de IP y VPN permitidas) para proporcionar a las partes externas acceso a un área específica de contenido en su DAM. Pueden utilizar la interfaz de usuario web de Experience Manager para obtener recursos y cargar contenido nuevo en su DAM.

#### Trabajo en curso en activos del Experience Manager {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda llevar a cabo actualizaciones importantes de los recursos, a veces denominadas trabajo en curso, sin tener que cargar también en el Experience Manager todas las ediciones guardadas en el archivo local como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de red utilizado y mantiene la línea de tiempo de los recursos limpia y centrada en actualizaciones importantes controladas.

Adobe Asset Link ofrece una buena compatibilidad para este caso de uso:

* Cuando los usuarios de Photoshop, InDesign o Illustrator intentan editar un archivo, ejecutan una operación de desprotección en el recurso determinado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud de los usuarios sincronizada con el disco por la aplicación de escritorio de Creative Cloud y el indicador de desprotección se activa en el Experience Manager del recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo que se almacena localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios en cualquier frecuencia necesaria
* Además, como el recurso se encuentra en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, se puede abrir o editar en una aplicación móvil de Creative Cloud dedicada) y se puede compartir con otros usuarios de Creative Cloud con fines de colaboración.
* Cuando el usuario creativo haya terminado con los cambios, puede ejecutar una operación de registro en ese archivo en su aplicación Creative Cloud, con un comentario opcional. El recurso correspondiente en el Experience Manager tiene versiones y se actualiza con el nuevo binario. Los usuarios de Experience Manager como los usuarios de Marketing o LOB tienen acceso a cambios o hitos importantes de recursos a través de la interfaz de usuario de la cronología de recursos de Experience Manager.

La aplicación de escritorio de Experience Manager proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De forma predeterminada, todos los cambios realizados localmente se cargan en Experience Manager automáticamente después de un rato. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en el Experience Manager y se versionarían, lo que crearía un montón de tráfico de red y posibles desafíos de escalabilidad, además de versiones innecesarias en el Experience Manager.

El método recomendado aquí es usar una opción en la aplicación de escritorio de Experience Manager para desactivar las actualizaciones automatizadas y cargar cambios en los recursos en el Experience Manager manualmente, aprovechando la acción de cambios de carga en la interfaz de usuario del estado de los recursos de la aplicación.

#### Carga masiva a DAM {#bulk-upload-to-dam}

Puede que tenga que cargar simultáneamente un mayor número de archivos en DAM en algunos casos, por ejemplo:

* Carga de resultados de sesión fotográfica o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Carga de recursos seleccionados de un conjunto mayor si la selección se realiza fuera de DAM

Tenga en cuenta que esta descripción se refiere a la carga de archivos operacionalmente (por ejemplo, cada semana o con cada sesión fotográfica ), como parte normal del flujo de trabajo del usuario del escritorio. Las migraciones de recursos grandes no se tratan aquí.

Puede aprovechar las siguientes capacidades de carga:

* Para cargar carpetas grandes/jerárquicas de forma masiva, utilice la aplicación de escritorio de Experience Manager que proporciona [carga de carpetas](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets) funcionalidad. También puede cargar estructuras de carpetas jerárquicas. Los recursos se cargan en segundo plano y, por lo tanto, no están vinculados a una sesión del explorador web
* Para cargar algunos archivos de una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear de la interfaz web de Experience Manager Assets.
* Según los requisitos empresariales, también puede utilizar el cargador personalizado.

#### Administración de recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si utiliza Recursos compartidos de archivos de red para administrar recursos digitales, el uso del recurso compartido de red asignado por la aplicación de escritorio de Experience Manager podría considerarse un sustituto conveniente. Al realizar la transición desde archivos compartidos de red, la interfaz web de Experience Manager proporciona un completo conjunto de funcionalidades de administración de recursos digitales que van mucho más allá de lo posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, vistas previas, etc.) y la aplicación de escritorio de Experience Manager proporciona un práctico vínculo para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite utilizar la aplicación de escritorio de Experience Manager para administrar recursos directamente en el recurso compartido de red de Experience Manager Assets. Por ejemplo, evite utilizar la aplicación de escritorio de Experience Manager para mover o copiar varios archivos. En su lugar, utilice la interfaz de usuario web de Experience Manager Assets para arrastrar carpetas desde Finder/Explorer al recurso compartido de red o utilice la función Carga de carpetas de Experience Manager Assets.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)
