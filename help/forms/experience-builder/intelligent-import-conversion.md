---
title: Importación y conversión inteligentes
description: Aprenda a transformar documentos, PDF e imágenes existentes en formularios digitales interactivos mediante las funciones inteligentes de importación y conversión de Forms Experience Builder.
hide: true
index: false
hidefromtoc: true
role: Admin, Architect, Developer
source-git-commit: de524aeddd5f53cbd713ff0523222966752ebbc0
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Importación y conversión inteligentes

>[!NOTE]
>
> Forms Experience Builder está disponible en un programa de acceso anticipado. Antes de empezar, asegúrese de que ha solicitado y de que se le ha concedido acceso.

La función inteligente de importación y conversión de Forms Experience Builder le permite transformar documentos, PDF e imágenes existentes en formularios digitales modernos e interactivos mediante el análisis y la conversión con tecnología de IA.

## Formatos de origen admitidos

### Documentos de PDF

**PDF de AcroForm:**

- PDF forms interactivo con campos de formulario
- PDF estáticos con diseños similares a formularios
- Documentos de varias páginas con contenido estructurado

**PDF basados en XFA:**

- Formularios XFA (arquitectura de Forms XML) heredados
- Formularios empresariales complejos con diseños avanzados
- Formularios gubernamentales y empresariales

**PDF estáticos:**

- Documentos y formularios escaneados
- Formularios listos para imprimir sin elementos interactivos
- Documentos con estructuras similares a formularios

### Archivos de imagen

**Formatos compatibles:**

- PNG, JPG, JPEG, GIF
- Análisis de alta resolución de formularios en papel
- Capturas de pantalla de formularios digitales
- Esbozos y mallas metálicas dibujados a mano

**Requisitos de calidad de imagen:**

- Mínimo de 300 ppp para el reconocimiento de texto
- Texto claro y legible y elementos de formulario
- Buen contraste entre texto y fondo
- Orientación correcta (no girada)

### Archivos de diseño

**Diseños de Figma:**

- Modelos y prototipos de formularios
- Archivos de diseño de IU/UX
- Diseños de formulario basados en componentes

**Otros formatos de diseño:**

- Archivos Adobe XD
- Diseños de bocetos
- Documentos de malla metálica

## Importación y conversión

### Paso 1: Acceso a la función de importación

1. Abra Forms Experience Builder
2. Haga clic en el icono de datos adjuntos en la interfaz
3. Seleccione la opción &quot;Importar y convertir&quot;
4. Elija el archivo de origen

### Paso 2: cargar el documento

**Para archivos PDF:**

1. Seleccione el documento de PDF
2. Espere a que la IA analice la estructura
3. Revisión de los elementos de formulario detectados
4. Confirmar la configuración de conversión

**Para archivos de imagen:**

1. Cargue la imagen (PNG, JPG, etc.)
2. La API analizará el diseño y el texto
3. Revisar los campos de formulario detectados
4. Realice los ajustes necesarios

**Para archivos de diseño:**

1. Cargar el archivo de diseño
2. La IA extraerá componentes del formulario
3. Revisar los elementos convertidos
4. Personalizar la estructura del formulario

### Paso 3: revisar y personalizar

Después de la conversión inicial:

1. **Revisar campos detectados**: compruebe que todos los elementos de formulario estén correctamente identificados
2. **Ajustar tipos de campo**: Modificar tipos de campo (texto, lista desplegable, casilla de verificación, etc.)
3. **Agregar validación**: configure las reglas de validación de campos
4. **Personalizar estilo**: aplicar temas y personalización de marca
5. **Probar funcionalidad**: compruebe el comportamiento y la lógica del formulario

## Ejemplos de conversión

### Conversión de formularios PDF

**Formulario original de PDF:**

- Formulario de contacto estático con nombre, correo electrónico, campos de teléfono
- Sección de información de empresa
- Área de comentarios

**Formulario adaptable convertido:**

- Campos de texto interactivos con validación
- Menú desplegable del tamaño de la empresa
- Área de texto multilínea para comentarios
- Botón Enviar con integración de correo electrónico

### Conversión de imagen a formulario

**Imagen original:**

- Foto de un formulario de registro en papel
- Formulario escrito a mano con casillas de verificación
- Varias secciones para obtener información diferente

**Formulario adaptable convertido:**

- Campos de texto digital que coinciden con el diseño
- Casillas de verificación y botones de opción interactivos
- Secciones organizadas con el espaciado adecuado
- Diseño con capacidad de respuesta móvil

### Conversión de archivo de diseño

**Diseño original de Figma:**

- Modelo de IU moderna con componentes de formulario
- Estilo y colores de marca
- Diseño complejo con varios paneles

**Formulario adaptable convertido:**

- Pixel-perfecta recreación del diseño
- Elementos de formulario interactivos
- Comportamiento interactivo entre dispositivos
- Estilo coherente con la marca

## Funciones de conversión avanzadas

### Detección inteligente de campos

La API detecta y convierte automáticamente lo siguiente:

- **Campos de texto**: áreas de texto de una sola línea y de varias líneas
- **Campos de selección**: desplegables, botones de opción, casillas de verificación
- **Campos de fecha**: Selector de fecha con el formato adecuado
- **Campos numéricos**: Entradas numéricas con validación
- **Cargas de archivos**: áreas de carga de documentos e imágenes

### Conservación del diseño

La conversión mantiene:

- **Estructura original**: Conserva el diseño y la organización
- **Jerarquía visual**: Mantiene encabezados y saltos de sección
- **Espaciado y alineación**: mantiene el espaciado correcto del formulario
- **Elementos de marca**: conserva los logotipos y los elementos de estilo

### Validación inteligente

Añade automáticamente la validación adecuada:

- **Campos de correo electrónico**: Validación de formato de correo electrónico
- **Números de teléfono**: validación del formato de número de teléfono
- **Campos obligatorios**: Marca campos obligatorios obvios
- **Intervalos de fechas**: establece las restricciones de fechas apropiadas

## Prácticas recomendadas para la importación y conversión

### Preparación de documentos de origen

**Para archivos PDF:**

- Asegúrese de que el texto sea seleccionable (no solo las imágenes)
- Uso de análisis de alta calidad para PDF estáticos
- Organizar contenido en secciones lógicas
- Incluir etiquetas de campo borradas

**Para imágenes:**

- Utilice imágenes de alta resolución (300+ DPI)
- Garantizar un buen contraste y legibilidad
- Evitar imágenes rotadas o sesgadas
- Incluir todos los elementos de formulario en la imagen

**Para archivos de diseño:**

- Utilice una nomenclatura uniforme para los componentes del formulario
- Organizar las capas lógicamente
- Incluir todos los elementos de formulario necesarios
- Exportación en alta calidad

### Optimización posterior a la conversión

**Revisión y prueba:**

- Probar todos los campos y la validación del formulario
- Verificar la capacidad de respuesta móvil
- Comprobar el cumplimiento de accesibilidad
- Probar funcionalidad de envío

**Personalizar y mejorar:**

- Agregar lógica empresarial y reglas condicionales
- Implementar la gestión de errores adecuada
- Configurar extremos de envío
- Aplicar estilos y temas de marca

## Solución de problemas de conversión

### Problemas comunes

**Detección de campo insuficiente:**

- Mejore la calidad de imagen para la claridad del texto de PDF
- Ajustar manualmente los tipos de campo después de la conversión
- Uso de etiquetas de campo más descriptivas en el origen

**Problemas de diseño:**

- Ajuste manual del espaciado y la alineación
- Uso de principios de diseño interactivo
- Realizar pruebas en diferentes tamaños de pantalla

**Faltan elementos:**

- Adición manual de los campos que faltan
- Volver a importar con mejor calidad de origen
- Utilizar el método de conversión incremental

### Obtención de ayuda

Para problemas de conversión:

- [Preguntas frecuentes sobre Forms Experience Builder](forms-experience-builder-frequently-asked-questions.md)
- Revise la [guía de introducción](forms-experience-builder-getting-started.md)
- Póngase en contacto con el administrador del sistema para obtener asistencia técnica

## Artículos relacionados

- [Información general sobre Forms Experience Builder](product-overview.md)
- [Introducción a Forms Experience Builder](forms-experience-builder-getting-started.md)
- [Implementación y configuración de Forms Experience Builder](deploy-forms-experience-builder.md)
- [Envío e integración de formularios](form-submission-integration.md)
- [Preguntas frecuentes](forms-experience-builder-frequently-asked-questions.md)
