---
title: API de comunicaciones de AEM Forms as a Cloud Service
description: Genere, manipule y proteja documentos con las API de comunicación de AEM Forms en la nube
Keywords: document generation, PDF manipulation, document security, batch processing, document conversion, PDF/A compliance
feature: Adaptive Forms, APIs & Integrations, Document Services
role: Admin, Developer, User
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: a9eed5b6219163e721d81c9d77a31604666a2ac5
workflow-type: tm+mt
source-wordcount: '1432'
ht-degree: 8%

---


# API de comunicaciones de AEM Forms as a Cloud Service {#communications-apis-overview}

> **Disponibilidad de la versión**
>
> * **AEM 6.5**: [Información general de AEM Document Services](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/overview-aem-document-services.html?lang=es)
> * **AEM as a Cloud Service**: este artículo

## Introducción

Las API de comunicaciones de AEM Forms as a Cloud Service le ayudan a crear documentos estandarizados, personalizados y aprobados por la marca para sus necesidades comerciales. Estas API potentes le permiten generar, manipular y proteger documentos mediante programación, ya sea bajo demanda o en procesos por lotes de gran volumen.


### Ventajas principales

* **Generación de documentos optimizada**: cree documentos personalizados combinando plantillas con datos de clientes
* **Potente manipulación de documentos**: combine, reorganice y valide documentos de PDF mediante programación
* **Opciones de implementación flexibles**: use API a petición para necesidades de baja latencia o API por lotes para operaciones de alto rendimiento
* **Seguridad mejorada**: aplique firmas digitales, certificación y cifrado para proteger documentos confidenciales
* **Arquitectura nativa de la nube**: aproveche la infraestructura de nube escalable y segura sin sobrecarga de mantenimiento

## Capacidades clave

Las API de comunicaciones proporcionan un conjunto completo de funcionalidades de procesamiento de documentos organizadas en las siguientes áreas funcionales:


| Generación de documentos | Manipulación de documentos | Extracción de documentos | Conversión de documentos | Seguro del documento |
|---------------------|----------------------|---------------------|---------------------|-------------------|
| Generar documentos personalizados combinando plantillas con datos en varios formatos, incluidos PDF y los formatos de impresión. | Combine, reorganice y valide documentos de PDF mediante programación para crear nuevos paquetes de documentos. | Extraiga propiedades, metadatos y contenido de documentos de PDF para un procesamiento posterior. | Convierta documentos entre formatos, incluida la validación de la conformidad con PDF/A para las necesidades de archivo. | Aplique firmas digitales, certificación y cifrado para proteger y proteger documentos. |

## Generación de documentos

Las API de generación de documentos de comunicaciones combinan plantillas (XFA o PDF) con datos de clientes (XML) para crear documentos personalizados en PDF y varios formatos de impresión (PS, PCL, DPL, IPL, ZPL).

### Funcionamiento de la generación de documentos

El flujo de trabajo habitual incluye:

1. Creando una plantilla con [Designer](use-forms-designer.md)
2. Preparación de datos XML para rellenar la plantilla
3. Usar las API de comunicaciones para combinar la plantilla con los datos
4. Generar documentos de salida en el formato deseado

![Flujo de trabajo de generación de documentos de comunicaciones](assets/communicaions-workflow.png)

### Crear documentos de PDF

Las API de generación de documentos permiten crear documentos de PDF no interactivos combinando datos XML con plantillas de formulario:

![Crear documentos de PDF](assets/outPutPDF_popup.png)

Puede enviar los PDF generados a los usuarios mediante descargas, almacenarlos en un repositorio o, opcionalmente, cargarlos en Azure Blob Storage.

<span class="preview">La carga de archivos PDF generados al almacenamiento del blob de Azure está disponible a través del [Programa de usuarios que lo adoptaron por anticipado](/help/forms/early-access-ea-features.md). Póngase en contacto con aem-forms-ea@adobe.com desde su correo electrónico oficial para unirse.</span>

### Crear documentos de formato de impresión

Generar documentos en formatos de impresión, incluidos:
* PostScript (PS)
* Lenguaje de comandos de impresora (PCL)
* Zebra Printing Language (ZPL)

Estos formatos son ideales para operaciones de impresión de gran volumen y necesidades de impresión especializadas.

### Procesamiento por lotes para varios documentos

Procesar grandes volúmenes de documentos de forma eficaz mediante las API por lotes:

![Flujo de trabajo de procesamiento por lotes](assets/ou_OutputBatchMany_popup.png)

El procesamiento por lotes le permite:

* Generar documentos independientes para cada registro en una fuente de datos XML
* Procesar documentos de forma asíncrona para obtener un mejor rendimiento
* Configure varios parámetros de conversión para el proceso por lotes

## Manipulación de documentos

Las API de manipulación de documentos le ayudan a combinar, reorganizar y transformar documentos de PDF mediante programación.

### Ensamblado de documento

Combine varios documentos PDF o XDP en un único documento coherente:

![Combinar un documento PDF simple desde varios documentos PDF](assets/as_document_assembly.png)

Las capacidades de ensamblado de documentos incluyen:
* Creación de documentos de PDF simples a partir de varias fuentes
* Creación de portafolios de PDF
* Agrupar documentos cifrados
* Adición de la numeración Bates para documentos legales
* Acoplar y combinar formularios interactivos

### Desensamblado de documento

Desglose los documentos grandes de PDF en componentes más pequeños y manejables:

![Dividir un documento de origen basado en marcadores en varios documentos](assets/as_intro_pdfsfrombookmarks.png)

El desensamblado de documentos le permite:
* Extraer páginas específicas de documentos de origen
* Dividir documentos según marcadores
* Crear conjuntos de documentos lógicos a partir de compilaciones más grandes

>[!NOTE]
>
> AEM Forms incluye muchas fuentes integradas que se integran perfectamente con los archivos PDF. Para obtener una lista completa de las fuentes compatibles, [haga clic aquí](/help/forms/supported-out-of-the-box-fonts.md).

## Extracción de documentos

La extracción de <span class="preview">documentos está disponible a través del [Programa para usuarios que adoptan anticipadamente](/help/forms/early-access-ea-features.md). Póngase en contacto con aem-forms-ea@adobe.com desde su correo electrónico oficial para unirse.</span>

Las API de extracción de documentos permiten recuperar información de documentos de PDF, como:

* Propiedades del documento (si es un formulario que se puede rellenar, tiene archivos adjuntos, etc.)
* Derechos y permisos de uso
* Información de metadatos con Adobe Extensible Metadata Platform (XMP)

Esta capacidad es especialmente útil para sistemas de gestión de documentos, soluciones de archivado y automatización del flujo de trabajo.

## Conversión de documentos

### Conversión y validación de PDF/A

Convierta documentos estándar de PDF al formato PDF/A para su archivo a largo plazo:

* Compatibilidad con los estándares PDF/A-1a, 1b, 2a, 2b, 3a y 3b
* Validación de la conformidad con PDF/A
* Conservación de la integridad del documento con fuentes incrustadas y contenido sin comprimir

### Conversión de PDF a XDP

La conversión de <span class="preview">PDF a XDP está disponible a través del [Programa para usuarios que adoptan anticipadamente](/help/forms/early-access-ea-features.md). Póngase en contacto con aem-forms-ea@adobe.com desde su correo electrónico oficial para unirse.</span>

Convierta documentos de PDF que contengan flujos XFA al formato XDP para editarlos y reutilizarlos.

## Seguro del documento {#doc-assurance}

Document Assurance incluye las API de firma y cifrado para proteger los documentos durante todo el ciclo de vida.

### API de firmas

Proteja los documentos de PDF con firmas digitales y certificación:

* Agregar campos de firma visibles o invisibles
* Firmar digitalmente campos de firma
* Certificar documentos para integridad
* Quitar firmas de documentos
* Eliminar campos de firma de documentos

<span class="preview">La eliminación de firmas y la eliminación de campos de firma están disponibles a través del [Programa para pioneros](/help/forms/early-access-ea-features.md). Póngase en contacto con aem-forms-ea@adobe.com desde su correo electrónico oficial para unirse.</span>

### Las API de cifrado

Proteger el contenido del documento con cifrado:

* Cifrar documentos de PDF con contraseñas
* Quitar cifrado basado en contraseña
* Determinar tipos de seguridad aplicados a documentos
* Recuperar información de seguridad de documentos protegidos

### Utilidades de documento {#doc-utility}

Las utilidades de documentos proporcionan funciones adicionales para trabajar con documentos de PDF:

#### API de derechos de uso (extensión de Reader)

<span class="preview">Los derechos de uso (extensión de Reader) están disponibles a través del [Programa para usuarios que adoptan anticipadamente](/help/forms/early-access-ea-features.md). Póngase en contacto con aem-forms-ea@adobe.com desde su correo electrónico oficial para unirse.</span>

Amplíe la funcionalidad de Adobe Reader añadiendo derechos de uso a los documentos de PDF, lo que permite funciones como las siguientes:

* Rellenar y guardar formularios
* Adición de comentarios y anotaciones
* Firma digital
* Archivos adjuntos
* Importación/exportación de datos de formulario
* Acceso a servicios web y bases de datos

Los derechos de uso disponibles incluyen:

* **Interacción De Formulario**: Rellenar Formulario, Importar/Exportar Datos De Formulario, Campos/Páginas De Formulario Dinámico
* **Anotaciones**: Comentarios (en línea y sin conexión), firmas digitales
* **Administración de documentos**: archivos incrustados, enviar independiente, descodificación de códigos de barras
* **Servicios en línea**: Forms en línea, acceso a servicios web

## Tipos de API de comunicaciones {#types}

Las comunicaciones ofrecen dos tipos de API para adaptarlas a diferentes casos de uso:

### API sincrónicas

**Lo mejor para**: bajo demanda, baja latencia, generación de un solo documento
**Casos de uso**: generación de documentos activada por el usuario, aplicaciones interactivas
**Documentación**: [Referencia de API sincrónica](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

### API por lotes (asíncronas)

**Lo mejor para**: Programada, de alto rendimiento, generación de múltiples documentos
**Casos de uso**: extractos mensuales, facturas, avisos e informes programados
**Documentación**: [Referencia de API por lotes](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/)

## Introducción a las API de comunicaciones

### Proceso de incorporación

Las comunicaciones están disponibles como módulo independiente o complemento para los usuarios de as a Cloud Service de Forms:

1. Póngase en contacto con Ventas de Adobe o con su representante de Adobe para solicitar acceso
2. Adobe habilitará el acceso para su organización y concederá privilegios de administrador
3. A continuación, el administrador puede otorgar acceso a los desarrolladores de su organización

### Habilitar las comunicaciones en su entorno

Siga estos pasos para habilitar las comunicaciones para su entorno de Forms as a Cloud Service:

1. Inicie sesión en Cloud Manager y abra su instancia de AEM Forms as a Cloud Service
2. Abra la opción Editar programa y vaya a la pestaña Soluciones y complementos
3. Seleccione la opción **[!UICONTROL Forms - Comunicaciones]**

   ![Comunicaciones](assets/communications.png)

   Si ya habilitaste **[!UICONTROL Forms - Inscripción digital]**, selecciona la opción **[!UICONTROL Forms - Complemento de comunicaciones]** en su lugar.

   ![Complemento](assets/add-on.png)

4. Haga clic en **[!UICONTROL Actualizar]**
5. Ejecutar la canalización de compilación: las API de comunicaciones se habilitarán una vez completadas correctamente

>[!NOTE]
>
> Para habilitar las API de manipulación de documentos, agregue la siguiente regla a su [configuración de Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Documentación de referencia de API {#api-reference}

Las API de comunicaciones están organizadas en varias categorías funcionales, cada una con documentación de referencia detallada. Estas referencias de API proporcionan información completa sobre puntos de conexión, parámetros, formatos de solicitud/respuesta y requisitos de autenticación.

### API de generación de documentos

| API | Descripción | Vínculo de referencia |
|-----|-------------|----------------|
| Generación de documentos: sincrónico | Generar documentos bajo demanda con baja latencia para escenarios interactivos | [Referencia de API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/) |
| Generación de documentos - Lote | Procesar grandes volúmenes de documentos de forma asíncrona para operaciones programadas | [Referencia de API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/) |

### API de manipulación de documentos

| API | Descripción | Vínculo de referencia |
|-----|-------------|----------------|
| Manipulación de documentos: sincrónica | Combinar, dividir y transformar documentos de PDF con instrucciones DDX | [Referencia de API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/) |

### API de Document Assurance

| API | Descripción | Vínculo de referencia |
|-----|-------------|----------------|
| DocAssurance - Sincrónico | Aplicar firmas digitales, certificación, cifrado y extensiones de lector | [Referencia de API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/docassurance/) |

### Parámetros comunes de API

Cada categoría de API tiene parámetros específicos, pero algunos parámetros comunes incluyen:

#### Parámetros de generación de documentos

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|----------|-------------|
| `template` | Cadena | Sí | Ruta al archivo de plantilla XDP o PDF |
| `data` | Cadena | No | Datos XML para combinar con la plantilla |
| `outputOptions` | Objeto | No | Opciones de configuración para el documento de salida |

#### Parámetros de manipulación de documentos

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|----------|-------------|
| `ddx` | Cadena | Sí | Instrucciones DDX para el ensamblado o desensamblado de documentos |
| `inputDocuments` | Objeto | Sí | Mapa de documentos de entrada para procesar |
| `outputOptions` | Objeto | No | Opciones de configuración para el documento de salida |

#### Parámetros de Document Assurance

| Parámetro | Tipo | Requerido | Descripción |
|-----------|------|----------|-------------|
| `inputPDF` | Cadena | Sí | Documento de PDF de entrada que se debe proteger o firmar |
| `certificateAlias` | Cadena | Condicional | Alias del certificado para operaciones de firma |
| `credentialPassword` | Cadena | Condicional | Contraseña de la credencial utilizada en la firma |

Para obtener información completa sobre los parámetros, los requisitos de autenticación y las solicitudes/respuestas de ejemplo, consulte la documentación de referencia de la API específica vinculada en las tablas anteriores.

## Recursos adicionales {#see-also}

* [Procesamiento de comunicaciones: API sincrónicas](/help/forms/aem-forms-cloud-service-communications.md)
* [Procesamiento de comunicaciones: API por lotes](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
* [Arquitectura de AEM Forms as a Cloud Service](/help/forms/aem-forms-cloud-service-architecture.md)
* [Documentación de referencia de API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/)
* [Características del programa de usuarios pioneros](/help/forms/early-access-ea-features.md)
