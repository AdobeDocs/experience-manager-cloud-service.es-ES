---
title: Vaya a la interfaz del editor universal para AEM Forms
description: Domine la interfaz del editor universal para crear AEM Forms con Edge Delivery Services. Conozca las herramientas, los métodos abreviados y los flujos de trabajo esenciales para crear formularios de forma eficaz con esta completa guía de interfaz.
keywords: editor universal, formularios AEM, servicios de envío de edge, guía de interfaz, creación de formularios, editor de WYSIWYG, herramientas de form builder, navegación de interfaz de usuario
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 4%

---


# Vaya a la interfaz del editor universal para AEM Forms

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) proporciona una interfaz visual para crear AEM Forms con Edge Delivery Services. Esta guía le ayuda a comprender la interfaz para crear formularios de forma eficaz.

![Información general sobre la interfaz de editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Información general

El editor universal ofrece una experiencia **What You See Is What You Get (WYSIWYG)** que muestra exactamente cómo aparecerán los formularios a los usuarios. Tanto si es nuevo en la creación de formularios como si es un desarrollador experimentado, esta guía le ayudará a lo siguiente:

**Aprender habilidades esenciales:**

- Navegue por la interfaz de forma segura y eficaz
- Utilizar las herramientas adecuadas para las tareas comunes de creación de formularios
- Aproveche los métodos abreviados del teclado para aumentar la productividad
- Solución de problemas comunes de la interfaz

**Flujos de trabajo de clave maestra:**

- Configure su espacio de trabajo para obtener una productividad óptima
- Creación de formularios desde el concepto hasta la publicación
- Probar y previsualizar formularios en varios dispositivos
- Colaborar con integrantes del equipo en proyectos de formularios

## Introducción rápida

**Usuarios nuevos:** Empiece con [Herramientas esenciales](#essential-tools-for-form-building) para conocer las funciones principales que usará con más frecuencia.

**Usuarios experimentados:** Vaya a [Características avanzadas](#advanced-features-and-integrations) para obtener herramientas e integraciones especializadas.

**Referencia rápida:** Utilice las secciones [Información general de la interfaz](#interface-overview) y [Métodos abreviados de teclado](#keyboard-shortcuts) para realizar búsquedas rápidas.

>[!NOTE]
>
> ¿Es nuevo en la creación de formularios? Consulte [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) para obtener instrucciones paso a paso para la creación de formularios.

## Resumen de interfaz

La interfaz del editor universal está organizada en cuatro áreas principales, cada una diseñada para tareas específicas:

![Diseño de interfaz de editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

| **Área** | **Propósito** | **Uso principal** |
|----------|-------------|----------------|
| **[A: encabezado de Experience Cloud](#experience-cloud-header)** | Navegación y administración de cuentas | Cambiar entre herramientas de Adobe, acceder a la ayuda, administrar notificaciones |
| **[B: barra de herramientas del editor universal](#universal-editor-toolbar)** | Edición y publicación de formularios | Crear, editar, previsualizar y publicar formularios |
| **[C: panel Propiedades](#properties-panel)** | Configuración de componentes | Configurar campos de formulario, administrar la estructura de contenido y acceder a funciones avanzadas |
| **[D: lienzo del editor](#editor-canvas)** | Generación de formularios visuales | Agregar componentes, organizar el diseño, ver previsualización en tiempo real |

**Flujo de interfaz:** La mayoría de los usuarios trabajan principalmente en el **Lienzo del editor** (D) y en el **Panel de propiedades** (C), utilizando la **Barra de herramientas** (B) para acciones como previsualizar y publicar.

## Herramientas esenciales para la creación de formularios

Comience aquí si es nuevo en el editor universal. Estas son las herramientas principales que utilizará para la mayoría de las tareas de creación de formularios:

### **1. Lienzo del editor: tu Workspace principal**

El lienzo **Editor** es donde se crean los formularios visualmente. Muestra exactamente el aspecto que tendrá el formulario para los usuarios.

![Lienzo del editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Acciones clave:**

- **Agregar componentes** al hacer clic en el botón **Agregar** en el panel Propiedades
- **Seleccione elementos** haciendo clic directamente en ellos en el lienzo
- **Ver cambios en tiempo real** al configurar los componentes
- **Interacciones de prueba** en modo de vista previa

### **2. Panel Propiedades - Configurar sus componentes**

En el **Panel de propiedades** (lado derecho) se personalizan los componentes seleccionados y se administra la estructura del formulario.

![Panel Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

**Características esenciales:**

- **Modo de propiedades** (`d` acceso directo): configurar la configuración del componente seleccionado
- **Árbol de contenido** (`f` acceso directo): Desplazarse por la estructura del formulario
- **Agregar componentes** (`a` acceso directo) - Insertar nuevos campos de formulario
- **Acciones de componente**: duplicar o eliminar elementos seleccionados

### **3. Toolbar Essentials: vista previa y publicación**

La **Barra de herramientas del editor universal** proporciona acciones clave para probar y publicar formularios.

![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

**Herramientas imprescindibles:**

- **Modo de vista previa** (`p` acceso directo): pruebe el formulario tal y como lo verán los usuarios
- **Modo interactivo**: compruebe el aspecto del formulario en dispositivos móviles
- **Abrir página** (acceso directo `o`): ver formulario en una nueva pestaña
- **Publicar**: activa el formulario para los usuarios

### **4. Flujo de trabajo de inicio rápido**

**Para su primer formulario:**

1. **Comenzar a crear** - Agregar componentes con el botón **Agregar** (`a`)
2. **Configurar campos** - Seleccionar componentes y usar **Modo de propiedades** (`d`)
3. **Probar el formulario** - Usar **modo de vista previa** (`p`) para interactuar con el formulario
4. **Comprobar vista móvil** - Cambiar a **Modo interactivo** para pruebas móviles
5. **Activar** - Haga clic en **Publicar** cuando esté listo

**Puntos de comprobación de validación:**

- ¿Puede agregar y configurar campos de formulario?
- ¿Funciona correctamente el modo de vista previa?
- ¿Están correctamente configurados todos los campos obligatorios?
- ¿Se muestra bien el formulario en los dispositivos móviles?

## Encabezado de Experience Cloud

El **encabezado de Experience Cloud** proporciona herramientas de navegación y administración de cuentas. La mayoría de los creadores de formularios lo utilizan ocasionalmente para cambiar entre las herramientas de Adobe o acceder a la ayuda.

![Encabezado de Experience Cloud](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

**Elementos clave:**

| **Elemento** | **Propósito** | **Cuándo se debe usar** |
|-------------|-------------|----------------|
| **Adobe Experience Cloud** | Navegar a otras herramientas de Adobe | Cambio entre sitios, Assets, Forms |
| **Organización** | Cambio entre organizaciones | Situaciones de acceso de varias organizaciones |
| **Ayuda** | Acceso a documentación y asistencia | Cuando necesite orientación o desee enviar comentarios |
| **Notificaciones** | Ver tareas y alertas asignadas | Comprobación del estado del flujo de trabajo |
| **Soluciones** | Acceso rápido a otras soluciones de Adobe | Desplazamiento entre diferentes productos de Adobe |
| **Perfil del usuario** | Configuración de cuenta y cierre de sesión | Administración de cuentas o cambio de usuarios |

**Usos más comunes:**

- **Obteniendo ayuda** - Haga clic en el icono Ayuda para obtener documentación y soporte técnico
- **Cambio de organizaciones**: utilice la lista desplegable Organización si tiene acceso de varias organizaciones

## Barra de herramientas del editor universal

La **Barra de herramientas del editor universal** contiene sus herramientas principales de edición y publicación de formularios. Están organizados por frecuencia de uso y flujo de trabajo habitual.

![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

### **Herramientas de flujo de trabajo diario**

**Estas herramientas se utilizan en la mayoría de las sesiones de creación de formularios:**

#### **Modo de vista previa** (`p` acceso directo)

**Propósito:** Pruebe el formulario exactamente como lo experimentarán los usuarios\
**Cuándo se debe usar:** Antes de publicar, después de realizar cambios, para probar la funcionalidad del formulario

![Modo de vista previa](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

**Práctica recomendada:** Vista previa después de cada cambio importante para detectar los problemas con antelación.

#### **Modo adaptable**

**Propósito:** Compruebe cómo se muestra el formulario en dispositivos móviles\
**Cuándo se debe usar:** Después de crear el formulario, antes de publicar

![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

**Práctica recomendada:** Probar siempre la vista móvil: muchos usuarios tendrán acceso a los formularios en los teléfonos.

#### **Abrir página** (acceso directo `o`)

**Propósito:** Ver el formulario en una nueva pestaña sin la interfaz del editor\
**Cuándo se debe usar:** Para pruebas a pantalla completa, compartir con los interesados para su revisión

![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

#### **Publicar**

**Propósito:** hacer que el formulario esté activo y accesible para los usuarios\
**Cuándo se debe usar:** Después de realizar pruebas exhaustivas en los modos Vista previa y Adaptable

![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

**Lista de comprobación de validación antes de la publicación:**

- Formulario probado en modo de vista previa
- Respuesta móvil verificada
- Todos los campos obligatorios configurados
- Acciones de envío que funcionan correctamente

### **Herramientas de navegación**

#### **Botón de inicio**

**Propósito:** Volver a la página de inicio del editor universal\
**Cuándo se debe usar:** Iniciar el trabajo en un formulario diferente

![Botón de inicio](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

#### **Barra de ubicación** (`l` acceso directo)

**Propósito:** Navegue directamente a cualquier formulario por dirección URL\
**Cuándo se debe usar:** Cambiar rápidamente entre formularios específicos

![Barra de ubicación](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

### **Herramientas de configuración avanzada**

**Estas herramientas se utilizan en escenarios específicos o en configuraciones avanzadas:**

#### **Propiedades de formulario AEM**

**Propósito:** configure las opciones de nivel de formulario, como el modelo de datos de formulario (FDM) y las fechas de publicación\
**Cuándo se debe usar:** Configuración de integraciones de datos, programación de publicaciones

![Propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

![Asistente de propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/form-properties-ue.png)

El panel Propiedades del formulario incluye las siguientes secciones:

- **Envío**: defina lo que sucede después de que un usuario envíe el formulario. Elija entre varias acciones de envío, como enviar datos por correo electrónico, enviar a SharePoint, utilizar un modelo de datos de formulario o integrar con servicios como Adobe Experience Platform o Microsoft Power Automate. Para obtener una lista completa de las acciones de envío admitidas, consulte el artículo [Enviar acción](/help/edge/docs/forms/universal-editor/submit-action.md).

- **Rellenar previamente**: configure cómo se rellenan automáticamente los campos de formulario antes de que el usuario interactúe con el formulario. Puede conectarse a fuentes de datos como un modelo de datos de formulario (FDM) o utilizar parámetros de URL para rellenar previamente los campos, lo que mejora la experiencia del usuario y reduce los datos introducidos manualmente. Para obtener más información, consulte el artículo [Servicio de relleno previo](/help/edge/docs/forms/universal-editor/prefill-form.md).

- **Gracias**: Personalice lo que los usuarios ven después de enviar el formulario. Puede mostrar un mensaje de confirmación o redirigirlo a otra página web, lo que garantiza una experiencia de finalización fluida y profesional. Para obtener información sobre cómo configurar un mensaje de agradecimiento para formularios, consulte el artículo [Configurar mensaje de agradecimiento](/help/edge/docs/forms/universal-editor/configure-thankyou-message.md).

#### **Editor de reglas** (acceso anticipado)

**Propósito:** Agregar comportamientos dinámicos, validaciones y lógica condicional\
**Cuándo se debe usar:** Crear formularios interactivos con lógica empresarial compleja

![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

>[!IMPORTANT]
>
> **Característica de acceso anticipado:** El editor de reglas requiere acceso especial. Póngase en contacto con [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) para habilitar esta característica.
>
> **Más información:** Consulta la [Guía del editor de reglas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md) para obtener instrucciones detalladas.

#### **Configuración del encabezado de autenticación**

**Propósito:** establecer encabezados de autenticación personalizados para las pruebas de desarrollo\
**Cuándo usar:** Desarrollo local con formularios requeridos para autenticación

![Encabezados de autenticación](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

#### **Opciones adicionales** (menú de puntos suspensivos)

**Propósito:** Acceso a acciones menos comunes como cancelar la publicación\
**Cuándo se debe usar:** Desconectar formularios y obtener acceso a opciones avanzadas

![Opciones adicionales](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

## Panel Propiedades

El **Panel de propiedades** (lado derecho) es el centro de control para crear y configurar formularios. Cambia en función de lo que seleccione y proporciona diferentes herramientas para diferentes tareas.

![Panel Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

### **Herramientas de creación de formularios básicos**

**Estas herramientas son esenciales para crear y organizar los formularios:**

#### **Agregar componentes** (acceso directo `a`)

**Propósito:** Insertar nuevos campos y elementos de formulario\
**Cómo funciona:** Muestra los componentes disponibles para el contenedor seleccionado

![Agregar componentes](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

**Componentes comunes:**

- Entrada de texto, correo electrónico, campos de teléfono
- Lista desplegable, Botones de radio, Casillas de verificación
- Carga de archivo, Selector de fecha
- Paneles y secciones para la organización

#### **Modo Propiedades** (acceso directo `d`)

**Propósito:** Configurar la configuración de los componentes seleccionados\
**Cuándo usar:** Después de agregar cualquier componente para personalizar su comportamiento

![Modo Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

**Configuración de clave:**

- Etiquetas de campo y texto de marcador de posición
- Reglas de validación (obligatorio, formato, longitud)
- Valores predeterminados y texto de ayuda
- Reglas de visibilidad condicionales

#### **Árbol de contenido** (`f` acceso directo)

**Objetivo:** Navegar y organizar la estructura del formulario\
**Cuándo usar:** formularios complejos con varias secciones, que buscan componentes específicos

![Árbol de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

**Beneficios:**

- Navegación rápida a cualquier componente
- Jerarquía de formulario visual
- Reorganización sencilla de elementos

#### **Acciones de componente**

**Propósito:** Administrar componentes existentes\
**Acciones disponibles:**

- **Duplicado** - Copiar componentes rápidamente ![Duplicado](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)
- **Eliminar** - Quitar componentes (sin mensaje de confirmación) ![Eliminar](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### **Funciones e integraciones avanzadas**

**Estas herramientas habilitan la funcionalidad de formulario sofisticada:**

+++Integración de datos

#### **Fuente de datos**

**Propósito:** conectar formularios a sistemas de datos back-end\
**Cuándo usar:** Forms que necesitan leer/escribir en bases de datos o servicios externos

![Fuente de datos](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

**Capacidades:**

- Configuración del modelo de datos de formulario (FDM)
- Población de datos dinámicos
- Envío a sistemas externos

+++

+++Herramientas con tecnología de IA

#### **Generar variaciones**

**Objetivo:** Usar IA para crear distintas versiones del contenido del formulario\
**Cuándo usar:** Experimentar con texto, diseños o enfoques diferentes

¡    ![Generar variaciones](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

**Más Información:** [Generar Guía De Variaciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

#### **Borradores de contenido**

**Propósito:** crear y guardar versiones de texto preliminares\
**Cuándo se debe usar:** Iterar en la copia del formulario y guardar opciones de texto alternativo

![Borradores de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

+++

+++Pruebas y optimización

#### **Pruebas A/B**

**Propósito:** Comparar variaciones de formularios para optimizar el rendimiento\
**Cuándo se debe usar:** Optimizar las tasas de conversión y probar diferentes diseños

![Pruebas A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

#### **Experimentación**

**Propósito:** ejecutar pruebas controladas en diseños de formulario\
**Cuándo usar:** Optimización de formularios basada en datos, pruebas de experiencia del usuario

¡    ![Experimentación](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

+++

+++Herramientas de Collaboration

#### **Administración de tareas**

**Propósito:** organizar el flujo de trabajo del equipo para proyectos de formularios\
**Cuándo se debe usar:** Desarrollo de formularios en varias personas, seguimiento de proyectos

![Administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

#### **Personalización**

**Propósito:** conectar con Adobe Experience Platform para obtener experiencias adaptadas\
**Cuándo se debe usar:** Crear formularios personalizados basados en datos de usuario

¡    ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

+++

## Lienzo del editor

El lienzo **Editor** es el área de trabajo principal donde se generan visualmente los formularios. Muestra exactamente cómo se mostrará el formulario a los usuarios y proporciona comentarios en tiempo real a medida que realiza cambios.

![Lienzo del editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

**Características principales:**

- **Edición de WYSIWYG**: vea los cambios inmediatamente cuando los haga
- **Interacción directa**: haz clic en cualquier componente para seleccionarlo y editarlo
- **Vista previa en tiempo real** - Cambiar al modo de vista previa para probar la funcionalidad
- **Pantalla interactiva**: cambia las vistas de los dispositivos para comprobar la compatibilidad con dispositivos móviles

**Prácticas recomendadas:**

- **Comenzar con estructura**: agregue secciones principales antes de los componentes detallados
- **Realizar pruebas con frecuencia**: utilice el modo de vista previa regularmente para detectar problemas de forma anticipada
- **Piense en mobile-first**: compruebe el modo interactivo durante todo el proceso de diseño

## Métodos abreviados de teclado

Domine estos métodos abreviados para crear formularios de forma más rápida y eficaz:

| **Acceso directo** | **Acción** | **Cuándo se debe usar** |
|--------------|------------|----------------|
| `a` | Abrir lista de componentes | Adición de nuevos campos de formulario |
| `d` | Abrir propiedades del componente | Configuración de los elementos seleccionados |
| `f` | Alternar árbol de contenido | Navegación por formularios complejos |
| `p` | Alternar modo de vista previa | Prueba de funcionalidad de formulario |
| `o` | Abrir formulario en una pestaña nueva | Pruebas a pantalla completa |
| `l` | Barra de ubicación de enfoque | Cambio a diferentes formularios |

**Sugerencia profesional:** Use estos métodos abreviados en combinación: por ejemplo, seleccione un componente, presione `d` para configurarlo y, a continuación, `p` para probar los cambios.

## Flujos de trabajo comunes

### **Creando su primer formulario**

1. **Agregar estructura** - Use `a` para agregar un panel para secciones de formulario
2. **Agregar campos** - Insertar entrada de texto, correo electrónico y otros componentes
3. **Configurar propiedades** - Seleccione cada campo y presione `d` para establecer las etiquetas y la validación
4. **Probar funcionalidad** - Presione `p` para obtener una vista previa y probar el formulario
5. **Comprobar la vista móvil**: utilice el modo interactivo para comprobar la pantalla móvil
6. **Publicar** - Haga clic en Publicar cuando esté listo para su lanzamiento

### **Editando Forms Existente**

1. **Desplazarse por la estructura**: use el árbol de contenido (`f`) para buscar componentes rápidamente
2. **Seleccionar y modificar**: haga clic en los componentes directamente o use el árbol de contenido
3. **Cambios de prueba** - Vista previa (`p`) después de cada cambio significativo
4. **Validar flujo de trabajo**: pruebe el flujo de formulario completo antes de volver a publicar

### **Colaborando con equipos**

1. **Usar administración de tareas** - Asignar secciones de formulario específicas a los integrantes del equipo
2. **Compartir para revisión** - Usar Abrir página (`o`) para compartir vistas previas limpias
3. **Realizar pruebas juntas**: usar el modo de vista previa en las sesiones de pruebas de colaboración
4. **Seguimiento del progreso** - Comprobar notificaciones para actualizaciones de tareas

## Solución de problemas comunes

### **Problemas De Interfaz**

+++Los Elementos De La Interfaz No Se Cargan

**Problema:** Los botones de la barra de herramientas, el panel de propiedades u otros elementos de la interfaz no aparecen

**Soluciones:**

- **Actualizar la página**: una simple actualización del explorador suele resolver los problemas de carga
- **Comprobar la compatibilidad del explorador** - Usar Chrome, Firefox o Safari
- **Borrar caché del explorador**: elimine los archivos en caché que puedan estar obsoletos
- **Verificar permisos**: compruebe que dispone del acceso adecuado para editar formularios

+++

+++Los componentes no responden

**Problema:** No se pueden seleccionar componentes o el Panel de propiedades no se actualiza

**Soluciones:**

- **Haga clic directamente en los componentes** - Evite hacer clic en áreas vacías
- **Usar árbol de contenido** - Presione `f` y seleccione componentes del árbol
- **Comprobar si hay elementos superpuestos**: algunos componentes podrían estar bloqueando otros
- **Vuelva a cargar el formulario**. Use la barra de ubicación (`l`) para volver a cargar el formulario actual

+++

+++Problemas del modo de vista previa

**Problema:** El modo de vista previa no funciona correctamente o muestra errores

**Soluciones:**

- **Comprobar la validación del formulario** - Asegúrese de que todos los campos obligatorios estén correctamente configurados
- **Primero realice la prueba en modo de edición**: compruebe que los componentes funcionan antes de previsualizarlos
- **Borrar caché del explorador**: los scripts en caché podrían interferir con la vista previa
- **Comprobar la configuración del componente**: revise la configuración del modo Propiedades para ver si hay errores

+++

## Prácticas recomendadas para la creación eficaz de formularios

### **Sugerencias de organización**

- **Use nombres descriptivos** - Etiquete claramente los componentes en el modo Propiedades
- **Campos relacionados con el grupo**: utilice los paneles para organizar las secciones de formulario de forma lógica
- **Planificar antes de generar**: esboce la estructura del formulario antes de comenzar
- **Manténgalo simple** - Evite abrumar a los usuarios con demasiados campos

### **Experiencia del usuario**

- **Realizar pruebas con frecuencia**: usar el modo de vista previa después de cada cambio importante
- **Piense como usuarios**: considere la posibilidad de rellenar todos los formularios
- **Proporcionar etiquetas claras**: haga que los propósitos de los campos sean obvios para los usuarios
- **Agregar texto útil** - Usar texto de ayuda para campos complejos

### **Optimización del rendimiento**

- **Minimizar componentes**: utilice solo los campos de formulario necesarios
- **Optimizar imágenes**: comprima todas las imágenes utilizadas en los formularios
- **Prueba en dispositivos móviles**: garantiza un buen rendimiento en conexiones móviles más lentas
- **Validar antes**: configure la validación adecuada para evitar errores de envío

## Próximos pasos

Ahora que comprende la interfaz del editor universal:

1. **Practicar con un formulario sencillo** - Empiece con los campos básicos para sentirse cómodo
2. **Explorar características avanzadas**: pruebe herramientas e integraciones con tecnología de IA cuando esté listo
3. **Aprenda a crear formularios** - Consulte la [Guía de introducción](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
4. **Editor de reglas maestro** - Agregar comportamientos dinámicos con la [Guía del editor de reglas](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)

**Recuerde:** El editor universal está diseñado para hacer que la creación de formularios sea intuitiva. Empiece con lo esencial y explore gradualmente las funciones avanzadas a medida que sus necesidades crezcan.
