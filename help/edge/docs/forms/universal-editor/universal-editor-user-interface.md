---
title: Vaya a la interfaz del editor universal para AEM Forms
description: Domine la interfaz del editor universal para crear formularios de AEM Forms con Edge Delivery Services. Conozca las herramientas, los métodos abreviados y los flujos de trabajo esenciales para crear formularios de forma eficaz con esta completa guía de interfaz.
keywords: editor universal, AEM Forms, Edge Delivery Services, guía de interfaz, creación de formularios, editor WYSIWYG, herramientas para generar formularios, navegación de interfaz de usuario
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '2390'
ht-degree: 95%

---


# Vaya a la interfaz del editor universal para AEM Forms

El [editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) proporciona una interfaz visual para crear formularios de AEM Forms con Edge Delivery Services. Ofrece una experiencia **What You See Is What You Get (WYSIWYG)** que muestra exactamente cómo aparecerán los formularios a los usuarios.

![Información general sobre la interfaz del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

Esta guía le ayuda a comprender la interfaz para crear formularios de forma eficaz. Tanto si es nuevo en la creación de formularios como si es un desarrollador experimentado, esta guía le ayudará a lo siguiente:

**Aprender habilidades esenciales:**

- Navegar por la interfaz con confianza y eficientemente
- Utilizar las herramientas adecuadas para las tareas comunes de creación de formularios
- Aprovechar los métodos abreviados del teclado para aumentar la productividad
- Solucionar problemas comunes de la interfaz

**Flujos de trabajo de clave maestra:**

- Configurar su espacio de trabajo para obtener una productividad óptima
- Generar formularios desde el concepto hasta la publicación
- Probar y previsualizar formularios en varios dispositivos
- Colaborar con integrantes del equipo en proyectos de formularios



## Introducción rápida

**Usuarios nuevos:** empiece con [Herramientas esenciales](#essential-tools-for-form-building) para conocer las funciones principales que usará con más frecuencia.

**Usuarios experimentados:** vaya a [Características avanzadas](#advanced-features-and-integrations) para obtener herramientas e integraciones especializadas.

**Referencia rápida:** utilice las secciones [Información general de la interfaz](#interface-overview) y [Métodos abreviados de teclado](#keyboard-shortcuts) para realizar búsquedas rápidas.

>[!NOTE]
>
> ¿Es nuevo en la creación de formularios? Consulte [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) para obtener instrucciones paso a paso para la creación de formularios.

## Información general de la interfaz

La interfaz del editor universal está organizada en cuatro áreas principales, cada una diseñada para tareas específicas:

![Diseño de la interfaz del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Área** | **Propósito** | **Uso principal** |
|----------|-------------|----------------|
| **[A: encabezado de Experience Cloud](#experience-cloud-header)** | Navegación y administración de cuentas | Cambiar entre herramientas de Adobe, acceder a la ayuda, administrar notificaciones |
| **[B: barra de herramientas del editor universal](#universal-editor-toolbar)** | Edición y publicación de formularios | Crear, editar, previsualizar y publicar formularios |
| **[C: panel Propiedades](#properties-panel)** | Configuración de componentes | Configurar campos de formulario, administrar la estructura de contenido y acceder a funciones avanzadas |
| **[D: lienzo del editor](#editor-canvas)** | Generación de formularios visuales | Agregar componentes, organizar el diseño, ver previsualización en tiempo real |

**Flujo de interfaz:** la mayoría de los usuarios trabajan principalmente en el **Lienzo del editor** (D) y en el **Panel Propiedades** (C), utilizando la **Barra de herramientas** (B) para acciones como previsualizar y publicar.

## Herramientas esenciales para la creación de formularios

Comience aquí si es nuevo con el uso del editor universal. Estas son las herramientas principales que utilizará para la mayoría de las tareas de creación de formularios:

### **1. Lienzo del editor: su espacio de trabajo principal**

El **Lienzo del editor** es donde se generan los formularios visualmente. Muestra exactamente el aspecto que tendrá el formulario para los usuarios.

![Lienzo del editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Acciones clave:**

- **Añadir componentes** haciendo en el botón **Añadir** en el panel Propiedades
- **Seleccionar elementos** haciendo clic directamente en ellos en el lienzo
- **Ver cambios en tiempo real** a medida que se configuran los componentes
- **Interacciones de prueba** en modo de vista previa

### **2. Panel Propiedades: configurar los componentes**

En el **Panel de propiedades** (lado derecho) se personalizan los componentes seleccionados y se administra la estructura del formulario.

![Panel Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Características esenciales:**

- **Modo de propiedades** (acceso directo `d`): definir la configuración del componente seleccionado
- **Árbol de contenido** (acceso directo `f`): desplazarse por la estructura del formulario
- **Agregar componentes** (acceso directo `a`): insertar nuevos campos de formulario
- **Acciones de componente**: duplicar o eliminar elementos seleccionados

### **3. Aspectos básicos de la barra de herramientas: previsualización y publicación**

La **Barra de herramientas del editor universal** proporciona acciones clave para probar y publicar formularios.

![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Herramientas imprescindibles:**

- **Modo de vista previa** (acceso directo `p`): probar el formulario tal y como lo verán los usuarios
- **Modo adaptable**: compruebe el aspecto del formulario en dispositivos móviles
- **Abrir página** (acceso directo `o`): ver formulario en una nueva pestaña
- **Publicar**: activar el formulario para los usuarios

### **4. Flujo de trabajo de inicio rápido**

**Para su primer formulario:**

1. **Agregar un componente de formulario adaptable** - Inserte el componente `Adaptive Form` en una sección.
2. **Comenzar a generar** : agregar componentes mediante el botón **Añadir** (`a`)
3. **Configurar campos**: seleccionar componentes y usar **Modo de propiedades** (`d`)
4. **Probar el formulario**: usar **Modo de vista previa** (`p`) para interactuar con el formulario
5. **Comprobar vista móvil**: cambiar a **Modo adaptable** para pruebas móviles
6. **Activar**: hacer clic en **Publicar** cuando esté listo

>[!NOTE]
>
> Para conocer los pasos detallados para crear formularios en el editor universal, consulte [Crear y publicar Forms adaptable con Edge Delivery Services](/help/edge/docs/forms/universal-editor/create-forms.md).

**Puntos de comprobación de validación:**

- ¿Puede añadir y configurar campos de formulario?
- ¿Funciona correctamente el modo de previsualización?
- ¿Están correctamente configurados todos los campos obligatorios?
- ¿Se muestra bien el formulario en los dispositivos móviles?

## Encabezado de Experience Cloud

El **encabezado de Experience Cloud** proporciona herramientas de navegación y administración de cuentas. La mayoría de los creadores de formularios lo utilizan ocasionalmente para cambiar entre las herramientas de Adobe o acceder a la ayuda.

![Encabezado de Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Elementos clave:**

| **Elemento** | **Propósito** | **Cuándo se debe usar** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Navegar a otras herramientas de Adobe | Cambio entre sitios, recursos y formularios |
| **Organización** | Cambio entre organizaciones | Situaciones de acceso de varias organizaciones |
| **Ayuda** | Acceder a documentación y asistencia técnica | Cuando necesite pautas o desee enviar comentarios |
| **Notificaciones** | Ver tareas y alertas asignadas | Comprobación del estado del flujo de trabajo |
| **Soluciones** | Acceso rápido a otras soluciones de Adobe | Desplazamiento entre diferentes productos de Adobe |
| **Perfil del usuario** | Configuración de cuenta y cierre de sesión | Administración de cuentas o cambio de usuarios |

**Usos más comunes:**

- **Obtención de ayuda**: haga clic en el icono Ayuda para obtener documentación y asistencia técnica.
- **Cambio de organizaciones**: utilice la lista desplegable Organización si tiene acceso de varias organizaciones.

## Barra de herramientas del editor universal

La **Barra de herramientas del editor universal** contiene las herramientas principales de edición y publicación de formularios. Están organizados por frecuencia de uso y flujo de trabajo habitual.

![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Herramientas de flujo de trabajo diario**

**Estas herramientas se utilizan en la mayoría de las sesiones de creación de formularios:**

#### **Modo de vista previa** (acceso directo `p`)

**Propósito:** probar el formulario exactamente como lo experimentarán los usuarios\
**Cuándo se debe usar:** antes de publicar, después de realizar cambios, para probar la funcionalidad del formulario.

![Modo vista previa](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Práctica recomendada:** vista previa después de cada cambio importante para detectar los problemas con antelación.

#### **Modo adaptable**

**Propósito:** comprobar cómo se muestra el formulario en dispositivos móviles\
**Cuándo se debe usar:** después de generar el formulario, antes de publicar

![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Práctica recomendada:** probar siempre la vista móvil (muchos usuarios tendrán acceso a los formularios en los teléfonos).

#### **Abrir página** (acceso directo `o`)

**Propósito:** ver el formulario en una nueva pestaña sin la interfaz del editor\
**Cuándo se debe usar:** para pruebas a pantalla completa y uso compartido con las partes interesadas para su revisión

![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Publicar**

**Propósito:** hacer que el formulario esté activo y accesible para los usuarios\
**Cuándo se debe usar:** después de realizar pruebas exhaustivas en los modos Previsualización y Adaptable

![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Lista de comprobación de validación antes de la publicación:**

- Formulario probado en modo Previsualización
- Respuesta móvil verificada
- Todos los campos obligatorios configurados
- Acciones de envío que funcionan correctamente

### **Herramientas de navegación**

#### **Botón de inicio**

**Propósito:** volver a la página de inicio del editor universal\
**Cuándo se debe usar:** empezar a trabajar en un formulario diferente

![Botón de inicio](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Barra de ubicación** (acceso directo `l`)

**Propósito:** navegar directamente a cualquier formulario por dirección URL\
**Cuándo se debe usar:** cambiar rápidamente entre formularios específicos

![Barra de ubicación](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Herramientas de configuración avanzada**

**Estas herramientas se utilizan en escenarios específicos o en configuraciones avanzadas:**

#### **Propiedades del formulario AEM**

**Propósito:** configure las opciones de nivel de formulario, como el modelo de datos de formulario (FDM), la configuración de acciones de envío y las fechas de publicación\
**Cuándo se debe usar:** configuración de integraciones de datos, programación de publicaciones

![Propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Asistente para propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

El panel Propiedades del formulario incluye las siguientes secciones:

- **Envío**: defina lo que sucede después de que un usuario envíe el formulario. Elija entre varias acciones de envío, como enviar datos por correo electrónico, enviar a SharePoint, utilizar un modelo de datos de formulario o integrar con servicios como Adobe Experience Platform o Microsoft Power Automate. Para obtener una lista completa de las acciones de envío admitidas, consulte el artículo [Acción de envío](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Rellenar previamente**: configure cómo se rellenan automáticamente los campos de formulario antes de que el usuario interactúe con el formulario. Puede conectarse a fuentes de datos, como un modelo de datos de formulario (FDM) o utilizar parámetros de URL para rellenar previamente los campos, lo que mejora la experiencia del usuario y reduce los datos introducidos manualmente. Para obtener más información, consulte el artículo [Servicio de rellenado previo](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Gracias**: personalice lo que los usuarios ven después de enviar el formulario. Puede mostrar un mensaje de confirmación o redirigirlo a otra página web, lo que garantiza una experiencia de finalización fluida y profesional. Para obtener información sobre cómo configurar un mensaje de agradecimiento para formularios, consulte el artículo [Configurar mensaje de agradecimiento](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Editor de reglas** (acceso anticipado)

**Propósito:** agregar comportamientos dinámicos, validaciones y lógica condicional\
**Cuándo se debe usar:** creación de formularios interactivos con lógica empresarial compleja

![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Característica de acceso anticipado:** el Editor de reglas requiere acceso especial. Póngase en contacto con [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para habilitar esta función.
>
> **Más información:** consulte la [Guía del Editor de reglas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) para obtener instrucciones detalladas.

#### **Configuración del encabezado de autenticación**

**Propósito:** establecer encabezados de autenticación personalizados para las pruebas de desarrollo\
**Cuándo se debe usar:** desarrollo local con formularios requeridos para autenticación

![Encabezados de autenticación](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Opciones adicionales** (menú de puntos suspensivos)

**Propósito:** acceder a acciones menos comunes como cancelar la publicación\
**Cuándo se debe usar:** desconectar formularios y obtener acceso a opciones avanzadas

![Opciones adicionales](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Panel Propiedades

El **Panel de propiedades** (lado derecho) es el centro de control para generar y configurar formularios. Cambia en función de lo que seleccione y proporciona diferentes herramientas para diferentes tareas.

![Panel Propiedades](/help/edge/docs/forms/universal-editor/assets/text-properties-ue.png)

### **Herramientas de creación de formularios básicos**

**Estas herramientas son esenciales para crear y organizar los formularios:**

#### **Agregar componentes** (acceso directo `a`)

**Propósito:** insertar nuevos campos y elementos de formulario\
**Cómo funciona:** muestra los componentes disponibles para el contenedor seleccionado

![Añadir componentes](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Componentes comunes:**

- Entrada de texto, correo electrónico, campos de teléfono
- Lista desplegable, botones de radio, casillas de verificación
- Carga de archivo, selector de fecha
- Paneles y secciones para la organización

#### **Modo Propiedades** (acceso directo `d`)

**Propósito:** definir la configuración de los componentes seleccionados\
**Cuándo de debe usar:** después de agregar cualquier componente para personalizar su comportamiento

![Modo Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Configuración de clave:**

- Etiquetas de campo y texto de marcador de posición
- Reglas de validación (obligatorio, formato, longitud)
- Valores predeterminados y texto de ayuda
- Reglas de visibilidad condicionales

#### **Árbol de contenido** (acceso directo `f`)

**Objetivo:** navegar por la estructura del formulario y organizarla \
**Cuándo se debe usar:** formularios complejos con varias secciones, que buscan componentes específicos

![Árbol de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Ventajas:**

- Navegación rápida a cualquier componente
- Jerarquía de formulario visual
- Reorganización sencilla de elementos

#### **Acciones de componente**

**Propósito:** administrar componentes existentes\
**Acciones disponibles:**

- **Duplicar**: copiar componentes rápidamente ![Duplicar](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Eliminar**: quitar componentes (sin mensaje de confirmación) ![Eliminar](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Funciones e integraciones avanzadas**

**Estas herramientas habilitan la funcionalidad de formulario sofisticada:**

+++Integración de datos

#### **Fuente de datos**

**Propósito:** conectar formularios a sistemas de datos back-end\
**Cuándo se debe usar:** formularios que necesitan realizar operaciones de lectura y escritura en bases de datos o servicios externos

![Fuente de datos](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Capacidades:**

- Configuración del modelo de datos de formulario (FDM)
- Población de datos dinámicos
- Envío a sistemas externos

+++

+++Herramientas con tecnología de IA

#### **Generar variaciones**

**Objetivo:** usar IA para crear distintas versiones del contenido del formulario\
**Cuándo se debe usar:** experimentar con texto, diseños o enfoques diferentes

¡    ![Generar variaciones](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Más Información:** [Generar guía de variaciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Borradores de contenido**

**Propósito:** crear y guardar versiones de texto preliminares\
**Cuándo se debe usar:** iterar en la copia del formulario y guardar opciones de texto alternativo

![Borradores de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Pruebas y optimización

#### **Pruebas A/B**

**Propósito:** comparar variaciones de formularios para optimizar el rendimiento\
**Cuándo se debe usar:** optimización de tasas de conversión y prueba de diferentes diseños

![Pruebas A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Experimentación**

**Propósito:** ejecutar pruebas controladas en diseños de formulario\
**Cuándo se debe usar:** optimización de formularios basada en datos, pruebas de experiencia del usuario

¡    ![Experimentación](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Herramientas de Collaboration

#### **Administración de tareas**

**Propósito:** organizar el flujo de trabajo del equipo para proyectos de formularios\
**Cuándo se debe usar:** desarrollo de formularios entre varias personas, seguimiento de proyectos

![Administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalización**

**Propósito:** conectar con Adobe Experience Platform para obtener experiencias adaptadas\
**Cuándo se debe usar:** creación de formularios personalizados basados en datos de usuario

¡    ![Personalización](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Lienzo del editor

El **Lienzo del editor** es el área de trabajo principal donde se generan visualmente los formularios. Muestra exactamente cómo se mostrará el formulario a los usuarios y proporciona comentarios en tiempo real a medida que realiza cambios.

![Lienzo del editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Funciones principales:**

- **Edición WYSIWYG**: ver los cambios inmediatamente a medida que se realizan
- **Interacción directa**: hacer clic en cualquier componente para seleccionarlo y editarlo
- **Vista previa en tiempo real**: cambiar al modo Previsualización para probar la funcionalidad
- **Pantalla interactiva**: cambiar las vistas de los dispositivos para comprobar la compatibilidad con dispositivos móviles

**Prácticas recomendadas:**

- **Comenzar con estructura**: agregar secciones principales antes de los componentes detallados
- **Realizar pruebas con frecuencia**: utilizar el modo Previsualización periódicamente para detectar problemas de forma anticipada
- **Pensar primero en los dispositivos móviles**: comprobar el modo Adaptable durante todo el proceso de diseño

## Métodos abreviados de teclado

Domine estos métodos abreviados para crear formularios de forma más rápida y eficaz:

| **Método abreviado** | **Acción** | **Cuándo se debe usar** |
|--------------|------------|----------------|
| `a` | Abrir lista de componentes | Adición de nuevos campos de formulario |
| `d` | Abrir propiedades de componentes | Configuración de elementos seleccionados |
| `f` | Conmutar árbol de contenido | Navegación por formularios complejos |
| `p` | Conmutar modo de previsualización | Prueba de funcionalidad del formulario |
| `o` | Abrir formulario en ficha pestaña | Pruebas a pantalla completa |
| `l` | Enfocar la barra de ubicación | Cambio a diferentes formularios |

**Sugerencia profesional:** use estos métodos abreviados en combinación; por ejemplo, seleccione un componente, presione `d` para configurarlo y, a continuación, presione `p` para probar los cambios.

## Flujos de trabajo comunes

### **Creación de su primer formulario**

1. **Agregar estructura**: usar `a` para agregar un panel para secciones de formulario
2. **Agregar campos**: insertar entrada de texto, correo electrónico y otros componentes
3. **Configurar propiedades**: seleccionar cada campo y presionar `d` para establecer las etiquetas y la validación
4. **Probar funcionalidad**: presionar `p` para obtener una vista previa y probar el formulario
5. **Comprobar la vista móvil**: utilizar el modo adaptable para comprobar la pantalla móvil
6. **Publicar**: hacer clic en Publicar cuando esté listo para su lanzamiento

### **Edición de formularios existentes**

1. **Desplazarse por la estructura**: usar el árbol de contenido (`f`) para buscar componentes rápidamente
2. **Seleccionar y modificar**: hacer clic en los componentes directamente o usar el árbol de contenido
3. **Probar los cambios**: previsualizar (`p`) después de cada cambio significativo
4. **Validar flujo de trabajo**: probar el flujo de formulario completo antes de volver a publicar

### **Colaboración con equipos**

1. **Usar Administración de tareas**: asignar secciones de formulario específicas a los integrantes del equipo
2. **Compartir para revisión**: usar Abrir página (`o`) para compartir vistas previas limpias
3. **Realizar pruebas juntas**: usar el modo Previsualización en las sesiones de pruebas de colaboración
4. **Seguimiento del progreso**: comprobar notificaciones para actualizaciones de tareas

## Solución de problemas comunes

### **Problemas de interfaz**

+++Elementos de interfaz no cargados

**Problema:** los botones de la barra de herramientas, el Panel de propiedades u otros elementos de la interfaz no aparecen

**Soluciones:**

- **Actualizar la página**: una simple actualización del explorador suele resolver los problemas de carga
- **Comprobar la compatibilidad del explorador**: usar Chrome, Firefox o Safari
- **Borrar caché del explorador**: eliminar los archivos en caché que puedan estar obsoletos
- **Verificar permisos**: asegurarse de que dispone del acceso adecuado para editar formularios

+++

+++Los componentes no responden

**Problema:** no se pueden seleccionar componentes o el Panel de propiedades no se actualiza

**Soluciones:**

- **Hacer clic directamente en los componentes**: evitar hacer clic en áreas vacías
- **Usar árbol de contenido**: presionar `f` y seleccionar componentes del árbol
- **Comprobar si hay elementos superpuestos**: algunos componentes podrían estar bloqueando otros
- **Volver a cargar el formulario**: usar la barra de ubicación (`l`) para volver a cargar el formulario actual

+++

+++Problemas del modo de vista previa

**Problema:** el modo Previsualización no funciona correctamente o muestra errores

**Soluciones:**

- **Comprobar la validación del formulario**: asegúrese de que todos los campos obligatorios estén correctamente configurados
- **Primero probar en modo de edición**: comprobar que los componentes funcionan antes de previsualizarlos
- **Borrar caché del explorador**: los scripts en caché podrían interferir con la previsualización
- **Comprobar la configuración del componente**: revisar la configuración del modo Propiedades para ver si hay errores

+++

## Prácticas recomendadas para la generación eficaz de formularios

### **Sugerencias para la organización**

- **Usar nombres descriptivos**: etiquetar claramente los componentes en el modo Propiedades
- **Campos relacionados con el grupo**: utilizar los paneles para organizar las secciones de formulario de forma lógica
- **Planificar antes de generar**: crear un boceto de la estructura del formulario antes de comenzar
- **Mantenerlo simple**: evitar abrumar a los usuarios con demasiados campos

### **Experiencia del usuario**

- **Realizar pruebas con frecuencia**: usar el modo de vista previa después de cada cambio importante
- **Pensar como usuarios**: considerar la posibilidad de rellenar todos los formularios
- **Proporcionar etiquetas claras**: hacer que los propósitos de los campos sean obvios para los usuarios
- **Agregar texto útil**: usar texto de ayuda para campos complejos

### **Optimización de rendimiento**

- **Minimizar componentes**: utilizar solo los campos de formulario necesarios
- **Optimizar imágenes**: comprimir todas las imágenes utilizadas en los formularios
- **Probar en dispositivos móviles**: garantizar un buen rendimiento en conexiones móviles más lentas
- **Validar de forma anticipada**: configurar la validación adecuada para evitar errores de envío

## Próximos pasos

Ahora que comprende la interfaz del editor universal:

1. **Practicar con un formulario sencillo**: empezar con los campos básicos para sentirse cómodo
2. **Explorar características avanzadas**: probar herramientas e integraciones con tecnología de IA cuando esté listo
3. **Aprender a crear formularios**: consultar la [Guía de introducción](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Editor de reglas maestro**: agregar comportamientos dinámicos con la [Guía del editor de reglas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Recordatorio:** el editor universal está diseñado para hacer que la generación de formularios sea intuitiva. Empiece con lo esencial y explore gradualmente las funciones avanzadas a medida que sus necesidades aumenten.
