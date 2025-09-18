---
title: Forms Experience Builder
description: Introducción a Forms Experience Builder
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: 69f17a4abddf025207448caed11f138c275e7b33
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 44%

---


# Introducción a Forms Experience Builder

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta documentación se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las funciones, los comandos y los ejemplos pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

AEM Forms Experience Builder aprovecha el poder de la IA generativa para democratizar y acelerar la creación y actualización de experiencias de formularios digitales. Al habilitar flujos de trabajo basados en la intención e impulsados por interacciones de lenguajes naturales, permite a los usuarios diseñar, modificar y optimizar formularios sin problemas con velocidad y sencillez.

Basado en tecnologías web modernas y con tecnología de servicios de IA avanzados, Forms Experience Builder permite tanto a usuarios técnicos como no técnicos crear formularios sofisticados de calidad profesional mediante interfaces conversacionales. Este revolucionario enfoque reduce el tiempo de respuesta de días a horas, elimina las barreras técnicas mediante la simplicidad de la interfaz y escala los esfuerzos de modernización en todo el ecosistema de formularios.

## Funciones principales

Forms Experience Builder ofrece dos flujos de trabajo principales para crear formularios digitales potentes:

### &#x200B;1. Creación de formularios con tecnología de IA

**Generación de formularios de lenguaje natural**

Cree formularios completos desde cero con descripciones simples en inglés. Describa simplemente sus necesidades, como &quot;Crear un formulario de comentarios de cliente con escalas de clasificación y campos de comentarios&quot;, y Forms Experience Builder generará la estructura de formulario adecuada. Puede usar el generador de experiencias de los editores visuales para agregar más campos, reglas de validación y lógica de envío.

**Administración dinámica de campos**

Añada, modifique o quite campos de formulario mediante comandos conversacionales. La IA comprende el contexto y puede sugerir de forma inteligente tipos de campo, reglas de validación y mejoras en la interfaz de usuario en función de sus necesidades.

**Optimización del diseño**

Actualice los diseños y las configuraciones de formulario mediante lenguaje natural. Solicite cambios como &quot;Cambiar el diseño del formulario al diseño del asistente&quot; y Forms Experience Builder aplicará los ajustes de estilo y diseño adecuados.

**Configuración completa de la acción de envío**

Configure los envíos de formularios para integrarlos con los sistemas empresariales existentes:

- **Integración de correo electrónico**: configuración de notificaciones y confirmaciones de correo electrónico automatizadas
- **Puntos finales de API REST**: conexión con aplicaciones y servicios personalizados
- **Almacenamiento en la nube**: integración con Azure Blob Storage, SharePoint y OneDrive
- **Automatización del flujo de trabajo**: Conexión con Power Automate y Workfront Fusion
- **Plataformas de mercadotecnia**: integración directa con Marketo para la gestión de posibles clientes
- **Flujos de trabajo de AEM**: utilización de las capacidades existentes del flujo de trabajo de AEM

### &#x200B;2. Importación y conversión inteligentes

**Formatos de importación compatibles**

Transforme formularios y documentos existentes en experiencias digitales interactivas. Forms Experience Builder es compatible con:

- **Acroforms**: PDF forms interactivo con estructuras de campo existentes
- **PDF XFA**: arquitecturas de formularios complejas basadas en XML
- **PDF planos**: documentos estáticos convertidos en formularios interactivos
- **Imágenes y capturas de pantalla**: Formatos JPG y PNG (consultar con el equipo las limitaciones de tamaño)
- **Forms dibujado a mano**: bocetos y fotografías en papel

**Proceso de conversión inteligente**

El contenido cargado se analiza en:

- Detectar tipos de campo y relaciones
- Conservar el diseño en la medida de lo posible
- Mejore con un diseño interactivo moderno
- Agregar validación avanzada y lógica condicional
- Optimizar para accesibilidad y experiencia móvil

## Funcionamiento

Forms Experience Builder sigue un enfoque sencillo y conversacional:

    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │ 1. Describir    │───▶│ 2. AI crea │───▶│ 3. Restringir y    │
    │ su formulario      │    │ formulario inicial   │    │ Configurar      │
    │ requisitos   │    │                 │    │                 │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
    │                       │                       │
    │                       │                       │
    ▼                       ▼                       ▼
    ┌───────────────────────────────────────────────────────────────────────────┐
    │ &quot;Crear un formulario de solicitud de préstamo&quot; → formulario con datos relevantes                  │
    │ &quot;Agregar campo de correo electrónico&quot;           → y campos básicos                          │
    │ &quot;Establecer valor de campo de correo electrónico en @firstname@gmail.com&quot; → reglas de validación   │
    └───────────────────────────────────────────────────────────────────────────┘

## Ejemplos de escenarios

<!--
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Transform PDF Forms to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Transform PDF Forms to Digital Forms</p>
                    <p class="is-size-6">Convert Acroforms, XFA PDFs, or flat PDF documents into responsive, interactive digital forms with enhanced functionality.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Modernize Legacy XFA Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Modernize Legacy XFA Forms</p>
                    <p class="is-size-6">Transform complex XFA applications into modern, accessible digital experiences with improved user workflows.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Convert Screenshots to Digital Forms">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Convert Screenshots to Digital Forms</p>
                    <p class="is-size-6">Turn images, screenshots, or hand-drawn forms into fully functional digital experiences.</p>
                </div>
            </div>
        </div>
    </div>
</div>
-->

<!-- #### Import and Enhance Web Forms

Import existing HTML forms and enhance them with advanced features while preserving existing functionality.

**Key benefits:**

- Advanced validation and business logic
- Conditional field behaviors
- Multi-channel submission options
- Enhanced user experience design -->

## Forms Experience Builder vs. desarrollo tradicional

| Aspecto | Creación de formularios tradicionales | Forms Experience Builder |
|--------|---------------------------|----------------------|
| **Hora de crear** | 2-3 días | 2-3 horas |
| **Conocimiento técnico** | Necesario | No es necesario |
| **Reglas de validación** | Codificación manual | Lenguaje natural |
| **Accesibilidad** | Implementación manual | Cumplimiento integrado |


## Ventajas para las organizaciones

<!--
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Democratized Form Creation">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Democratized Form Creation</p>
                    <p class="is-size-6">Empower non-technical users to create sophisticated forms without programming knowledge through natural language conversations.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Reduced Time to Value (TTV)">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Reduced Time to Value (TTV)</p>
                    <p class="is-size-6">Dramatically accelerate form development from days to hours, enabling faster go-to-market for digital initiatives.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Interface Simplicity">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Interface Simplicity</p>
                    <p class="is-size-6">Eliminate the learning curve with an intuitive conversational interface, reducing training time and increasing adoption.</p>
                </div>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Scaling Modernization Efforts">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">Scaling Modernization Efforts</p>
                    <p class="is-size-6">Modernize legacy form portfolios efficiently, preserving business logic and enhancing user experience across your entire form ecosystem.</p>
                </div>
            </div>
        </div>
    </div>
</div>
-->

## Incorporación

Forms Experience Builder está disponible actualmente como parte del programa de acceso anticipado (EA). Para participar y obtener acceso, necesitará la siguiente información:

### Información necesaria

- **ID de organización de IMS**: su identificador de organización de Adobe
- **ID de programa**: el identificador de programa específico dentro de Adobe Experience Cloud
- **Detalles del proyecto**: escala de tiempo, ámbito y casos de uso previstos
- **Correo electrónico de trabajo oficial**: asociado a la cuenta de Adobe de su organización

### Cómo obtener el ID de organización de IMS y el ID de programa

Para ver los pasos detallados para localizar el ID de organización de IMS y el ID de programa, consulte:

- [Guía de configuración de Adobe Experience Cloud Organization](/help/onboarding/cloud-manager-introduction.md)
- [Administración de programas y entornos](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)

### Solicitar acceso

1. Recopile su ID de organización de IMS y el ID de programa mediante las guías anteriores
2. Enviar un correo electrónico a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para solicitar acceso
3. Incluya en su solicitud:
   - Nombre de organización e ID de organización de IMS
   - ID de programa
   - Cronología y ámbito del proyecto
   - Casos de uso previstos y objetivos empresariales

>[!IMPORTANT]
>
> **Programa de disponibilidad limitada**: el acceso a Forms Experience Builder está sujeto a la aprobación de los interesados internos. Adobe revisará su solicitud en función de la capacidad del programa y la alineación con los criterios de acceso anticipado. La aprobación no está garantizada y depende de la disponibilidad actual del programa.

Para obtener más información acerca del programa de acceso anticipado y sus funciones, consulte la [documentación de acceso anticipado de AEM Forms](/help/forms/early-access-ea-features.md).

## Introducción

Para empezar a usar Forms Experience Builder, visite la [documentación de Forms Experience Builder](forms-ai-assistant-getting-started.md). Puede acceder a Forms Experience Builder a través del Editor de AEM Forms o del Editor universal, según el flujo de trabajo que prefiera.

Para organizaciones que pretenden transformar sus procesos de creación de formularios, Forms Experience Builder ofrece una solución potente e intuitiva que combina la flexibilidad de la IA conversacional con la solidez de la administración de formularios de categoría empresarial.
