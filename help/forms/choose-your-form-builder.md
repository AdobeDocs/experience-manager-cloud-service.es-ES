---
title: 'Generador de formularios: elija un enfoque'
description: Compare creadores de formularios y encuentre el método adecuado para crear formularios adaptables. Ya sea que sea un creador de formularios que necesita plantillas o que esté creando formularios complejos, elija el mejor generador de formularios para sus necesidades.
keywords: form builder, formularios AEM, creador de formularios, crear formularios, creador de formularios, formularios adaptables, componentes principales, componentes de base, servicios de envío de Edge, crear formularios
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---


# Generador de formularios: elija un enfoque {#choose-your-form-builder}

Adobe Experience Manager (AEM) Forms proporciona tres enfoques potentes de creación de formularios, cada uno diseñado para diferentes casos de uso, requisitos técnicos y destinos de publicación. Tanto si es un creador de formularios que busca plantillas como si es un desarrollador que crea formularios complejos, esta guía le ayuda a elegir el creador de formularios adecuado para su proyecto.

## Guía de decisión rápida

Utilice esta referencia rápida para identificar el mejor generador de formularios para sus necesidades:

| **Si lo necesita...** | **Elegir** |
|-------------------|------------|
| **Formularios modernos y escalables con las últimas características** | Componentes principales |
| **Formularios muy rápidos para sitios web de mucho tráfico** | Editor universal |
| **Mantener formularios existentes o integraciones heredadas** | Componentes de base |
| **Creación visual de arrastrar y soltar** | Componentes principales o editor universal |
| **Creación de formularios basada en hojas de cálculo** | Creación basada en documentos |
| **Envío omnicanal (web, móvil, quioscos)** | Componentes principales (con API sin encabezado) |
| **Aplicaciones de front-end personalizadas (React, Angular)** | Componentes principales (con API sin encabezado) |
| **Control total sobre la representación de formularios** | Componentes principales (con API sin encabezado) |

## Explicación de las opciones de Forms Builder

AEM Forms ofrece tres enfoques principales de creación de formularios, cada uno diseñado para diferentes tipos de creadores de formularios y casos de uso. Tanto si necesita un creador de formularios sencillo para tareas rápidas como si necesita funciones avanzadas del creador de formularios para proyectos complejos, existe un enfoque que se adapta a sus necesidades:

### Generador de formularios de componentes base

Los componentes de base representan la experiencia de creación clásica de AEM Forms. Aunque siguen siendo compatibles, se recomiendan principalmente para mantener los formularios existentes en lugar de crear otros nuevos.

**Características clave:**

- Interfaz de creación tradicional de AEM
- Estabilidad comprobada para flujos de trabajo existentes
- Limitado a publicaciones solo de AEM
- Biblioteca de componentes básica

### Generador de formularios de componentes principales

Los componentes principales proporcionan las funciones de AEM Forms más recientes con un rendimiento, una accesibilidad y una flexibilidad mejorados. Este generador de formularios es ideal para los creadores de formularios que necesitan resultados profesionales con características modernas. Admite la publicación tanto de AEM como de Edge Delivery Services, y produce automáticamente formularios sin encabezado para la entrega basada en API en varias plataformas.

**Características clave:**

- Componentes modernos y estandarizados
- Rendimiento y accesibilidad mejorados
- Opciones de publicación flexibles (AEM + Edge Delivery)
- Funciones de personalización avanzadas
- Arquitectura preparada para el futuro
- Generación automática de formularios sin encabezado para entrega omnicanal

### Editor universal (Edge Delivery Services)

Universal Editor proporciona dos poderosos enfoques de creación para Edge Delivery Services: creación visual de WYSIWYG y creación basada en documentos mediante hojas de cálculo. Este método de creación de formularios es perfecto para los usuarios que desean crear formularios rápidamente con un rendimiento excepcional.

**Características clave:**

- Rendimiento excepcional (puntuaciones altas en Lighthouse)
- Dos métodos de creación: WYSIWYG y basado en documentos
- Optimizado para Edge Delivery Services
- Rendimiento y SEO excepcionales
- Desarrollo e implementación rápidos


## Comparación detallada

### Capacidades técnicas

| **Capacidad** | **Base** | **Núcleo** | **Editor universal** | **Basado en documentos** |
|----------------|----------------|----------|---------------------|-------------------|
| **Complejidad de formulario** | Básica | Avanzado  | Avanzado  | De simple a moderado |
| **Motor de reglas** | Avanzado  | Avanzado  | Avanzado  | Limitado |
| **Componentes personalizados** | ✅ | ✅ | ✅ | ✅ |
| **Temas** | ✅ | ✅ | Nivel de proyecto | Nivel de proyecto |
| **Plantillas** | ✅ | ✅ | Solo contenido inicial |  |
| **Fragmentos** | ✅ | ✅ | ✅ | ✅ |
| **Localización** | ✅ | ✅ | Mediante AEM Sites | Manual/Funciones |

### Integración y envío

| **Función** | **Base** | **Núcleo** | **Editor universal** | **Basado en documentos** |
|-------------|----------------|----------|---------------------|-------------------|
| **Modelos de datos** | FDM, personalizado | FDM, personalizado | FDM, personalizado | Personalizado |
| **Acciones de envío** | Varias opciones | Varias opciones | Varias opciones | Sólo hoja de cálculo |
| **Relleno previo** | ✅ | ✅ | Mediante el asistente | ✅ |
| **CAPTCHA** | Varios tipos | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **Archivos adjuntos** | ✅ | ✅ | ✅ | Acceso temprano |
| **Firmas digitales** | ✅ |  |  |  |

### Publicación y rendimiento

| **Aspecto** | **Base** | **Núcleo** | **Editor universal** | **Basado en documentos** |
|------------|----------------|----------|---------------------|-------------------|
| **Publicación** | Solo AEM | AEM + Edge Delivery + API sin encabezado | Edge Delivery | Edge Delivery |
| **Rendimiento** | Estándar | Mejorado | Puntuaciones de High Lighthouse | Puntuaciones de High Lighthouse |
| **Optimización de SEO** | Básica | Bien | Excelente | Excelente |
| **Capacidad de respuesta móvil** | Bien | Excelente | Excelente | Excelente |

## Elección del generador adecuado

### Elegir componentes de base si:

- Está manteniendo los formularios existentes basados en Foundation
- Necesita integración de firma digital
- El flujo de trabajo depende de las funciones de base establecidas
- Está trabajando dentro de los requisitos de publicación solo de AEM

**Ideal para:** Mantenimiento de formularios, integración de sistemas heredados, flujos de trabajo establecidos

### Elija los componentes principales si:

- Estás construyendo formas nuevas y modernas
- Necesita flexibilidad para publicar en AEM o Edge Delivery Services
- Desea las últimas funciones
- Necesita personalización avanzada y temas
- La accesibilidad y el rendimiento son prioridades
- Desea una tecnología preparada para el futuro

**Ideal para:** Proyectos nuevos, soluciones escalables y experiencias web modernas

### Elija el editor universal si:

- Necesitas un rendimiento excepcional y SEO
- Está creando para los sitios de Edge Delivery Services
- Necesita formularios complejos con acciones personalizadas
- Se requiere la integración con sistemas externos

**Ideal para:** sitios de alto rendimiento, Edge Delivery Services, flujos de trabajo de creación visual

### Elija la creación basada en documentos si:

- Los usuarios empresariales prefieren la creación basada en hojas de cálculo
- Necesita crear prototipos e implementarlos rápidamente
- Forms son relativamente sencillas (encuestas, registros, comentarios)
- La recopilación de datos en hojas de cálculo satisface sus necesidades
- No se requieren flujos de trabajo de envío avanzados

**Ideal para:** implementación rápida, creación de usuarios empresariales, recopilación sencilla de datos


## Consideraciones de migración

### De la base a los componentes principales

- **Enfoque recomendado:** Use la [herramienta de utilidad de migración](/help/forms/migration-utility-tool-for-af-core-components.md)
- **Ventajas:** Funciones modernas, mejor rendimiento, capacidad de publicación dual
- **Esfuerzo:** de moderado a alto, según la complejidad del formulario

### Del editor tradicional al universal

- **Enfoque:** Reconstruir formularios utilizando WYSIWYG o la creación basada en documentos en el editor universal
- **Ventajas:** Rendimiento excepcional, experiencia de desarrollo moderno, puntuaciones de SEO elevadas
- **Esfuerzo:** alto para formularios complejos, bajo para formularios simples

## Introducción

Una vez que haya elegido el generador de formularios:

### Componentes de base

1. [Creación de un formulario adaptable (componentes básicos)](/help/forms/creating-adaptive-form.md)
2. [Guía de creación de componentes de base](/help/forms/introduction-forms-authoring.md)

### Componentes principales

1. [Creación de un formulario adaptable (componentes principales)](/help/forms/creating-adaptive-form-core-components.md)
2. [Resumen de funciones de componentes principales](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### Editor universal (Edge Delivery Services)

1. **Creación en WYSIWYG:** [Introducción al editor universal](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **Creación basada en documentos:** [Cree su primer formulario con hojas de cálculo](/help/edge/docs/forms/tutorial.md)


## ¿Necesita ayuda para decidir?

¿Todavía no está seguro de qué generador de formularios elegir? Tenga en cuenta estos factores:

- **Experiencia en el equipo:** ¿Cuál es el nivel de habilidad técnica de su equipo?
- **Escala de tiempo del proyecto:** ¿Con qué rapidez necesita implementarlo?
- **Requisitos de rendimiento:** ¿La velocidad y la optimización de los motores de búsqueda son esenciales?
- **Escalabilidad futura:** ¿Necesitará expandir o modificar formularios con frecuencia?
- **Destino de publicación:** ¿Dónde se publicarán los formularios?

Para obtener una guía personalizada, consulte con su equipo de implementación de AEM Forms o con el servicio de asistencia de Adobe.

## Artículos relacionados

- [Comparación detallada de la creación de formularios](/help/edge/docs/forms/authoring-a-form.md)
- [Información general sobre los componentes principales de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es)
- [Información general sobre Edge Delivery Services para Forms](/help/edge/docs/forms/overview.md)
- [Forms adaptable sin encabezado con componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
