---
title: Rellenado previo de los campos del formulario adaptable
description: Utilice los datos existentes para rellenar previamente los campos de un formulario adaptable. Los usuarios pueden rellenar previamente la información básica de un formulario iniciando sesión con sus perfiles sociales.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: prerrellenar formularios adaptables, servicios de entrega de Edge de formularios adaptables, autorrellenar formularios adaptables
source-git-commit: 87650caea6eb907093f0f327f1dbc19641098e4a
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 3%

---


# Configuración del servicio de relleno previo en Forms adaptable mediante Edge Delivery Services

El rellenado previo de formularios es el proceso de rellenar automáticamente los campos de formulario con datos relevantes de fuentes externas en cuanto un usuario abre el formulario. Al aprovechar la información de perfiles de usuario, bases de datos, borradores guardados u otros sistemas backend, el rellenado previo optimiza la experiencia de rellenado de formularios, lo que reduce la entrada manual, minimiza los errores y acelera la finalización. Esto no solo mejora la satisfacción del usuario, sino que también aumenta la probabilidad de que los envíos de formularios se realicen correctamente.

## Ventajas del rellenado previo de formularios

| Beneficio | Descripción |
|---------|-------------|
| **Finalización más rápida** | Reduce la entrada manual de datos, lo que ayuda a los usuarios a completar formularios rápidamente |
| **Experiencia de usuario mejorada** | Forms se siente más personalizado y conveniente, especialmente para los usuarios que regresan |
| **Tasas de conversión más altas** | Reduce el abandono de formularios minimizando el esfuerzo necesario del usuario |
| **Errores de entrada reducidos** | Los datos de fuentes de confianza reducen los errores tipográficos y las entradas incorrectas |
| **Mejor calidad de datos** | Garantiza datos estructurados, precisos y coherentes para los sistemas back-end |

## Funcionamiento del relleno previo

El diagrama siguiente ilustra el proceso de relleno previo automático que se produce cuando un usuario abre un formulario adaptable:

![Flujo del proceso de rellenado previo de formularios](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

El proceso de rellenado previo incluye cuatro pasos clave:

1. **El usuario abre el formulario**: El usuario accede a un formulario adaptable a través de una URL o navegación
2. **Identificar Source de datos**: el servicio de relleno previo determina el origen de datos configurado (modelo de datos de formulario o servicio de borrador)
3. **Recuperar datos**: el sistema recupera datos de usuario relevantes en función del contexto, los parámetros o la identificación del usuario
4. **Asignar y mostrar**: los datos se asignan a campos de formulario con las propiedades `bindRef` y el formulario rellenado se muestra al usuario

Este proceso automatizado garantiza que los usuarios vean un formulario previamente rellenado con su información relevante, lo que mejora significativamente la experiencia del usuario y las tasas de finalización del formulario.

## Estructura de datos para relleno previo

El Forms adaptable admite dos tipos de campos:

- **Campos enlazados**: Campos conectados a un origen de datos con una propiedad `bindRef` que no está vacía
- **Campos no enlazados**: Campos independientes con valores `bindRef` vacíos

La estructura de datos de relleno previo incluye:

- **afBoundData**: contiene datos para campos y paneles enlazados
- **afUnBoundData**: contiene datos para campos independientes

El formato de datos debe coincidir con el modelo de formulario:

- **Formularios XFA**: XML compatible con esquema de plantilla XFA
- **Formularios de esquema XML**: XML que coincide con la estructura de esquema
- **Formularios de esquema JSON**: JSON compatible con el esquema
- **Formularios de modelo de datos de formulario (FDM)**: JSON que coincide con la estructura de FDM
- **Formularios sin esquema**: todos los campos son independientes y utilizan XML independiente


## Requisitos previos

Antes de configurar los servicios de relleno previo, asegúrese de lo siguiente:

### Ajustes necesarios

- [Repositorio de GitHub configurado para Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Bloque de Forms adaptable añadido al proyecto](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Fuente de datos configurada](/help/forms/configure-data-sources.md)
- [Modelo de datos de formulario (FDM) creado](/help/forms/create-form-data-models.md)

### Requisitos de acceso

- Acceso a AEM Forms as a Cloud Service
- Permisos para crear y editar formularios
- Acceso al Editor universal con las extensiones requeridas habilitadas

>[!TIP]
>
> También puede editar formularios para integrar el Modelo de datos de formulario (FDM) en el Editor universal para recuperar datos de varias fuentes back-end. Para obtener más información, consulte el artículo [Integrar formularios con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Opciones del servicio de prerrellenar

El editor universal proporciona dos opciones de servicio de relleno previo:

| Tipo de servicio | Función | Fuente de datos | Ideal para |
|--------------|---------|-------------|----------|
| **Relleno Previo Del Borrador Del Portal De Formularios** | Reanuda los formularios parcialmente completados | Borradores guardados en Forms Portal | Continuación de aplicaciones incompletas |
| **Relleno previo del modelo de datos de formulario** | Rellena campos de sistemas externos | Bases de datos back-end mediante FDM | Rellenado automático de datos de perfil de usuario |

### Comparación detallada

| Función | Servicio de relleno previo de borrador | Servicio de relleno previo de FDM |
|---------|----------------------|---------------------|
| **Autenticación** | Requiere el inicio de sesión del usuario para acceder al borrador | Configurable según la fuente de datos |
| **Complejidad de la instalación** | Configuración mínima | Requiere configuración y asignación de FDM |
| **Tipo de datos** | Datos guardados estáticos | Datos dinámicos en tiempo real |
| **Caso práctico** | Reanudar aplicaciones guardadas | Rellenar previamente desde perfiles de usuario o bases de datos |


## Configurar el servicio de rellenado previo para un formulario


+++Fase 1: Configuración del modelo de datos de formulario

### Paso 1: Crear un modelo de datos de formulario

1. Inicie sesión en la instancia de as a Cloud Service de AEM Forms
2. Vaya a **Adobe Experience Manager** > **Forms** > **Integraciones de datos**
3. Seleccione **Crear** > **Modelo de datos de formulario**
4. Elija su **Configuración de Data Source** y seleccione el **Source de datos** configurado

   ![Modelo de datos de formulario creado](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   > Para obtener instrucciones detalladas sobre la creación de modelos de datos de formulario, consulte [Crear un modelo de datos de formulario](/help/forms/create-form-data-models.md).

### Paso 2: Configurar los servicios de FDM

1. Vaya a **Adobe Experience Manager** > **Forms** > **Integraciones de datos**
2. Abra el modelo de datos de formulario en el modo Edición
3. Seleccione un objeto del modelo de datos y haga clic en **Editar propiedades**
4. Configure los servicios **Read** y **Write** para los objetos del modelo de datos seleccionado

   ![Configurar servicio de lectura/escritura](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

5. Configure los argumentos del servicio:
   - Haga clic en el icono de edición del argumento del servicio de lectura
   - Enlace el argumento a un **atributo de perfil de usuario**, **atributo de solicitud** o **valor literal**
   - Especifique el valor del enlace (por ejemplo, `petid` para un formulario de registro de mascota)

   ![Configurar el argumento del ID de la mascota](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

6. Haga clic en **Listo** para guardar el argumento y en **Guardar** para guardar el FDM

       >[!NOTA]
       >
   > Obtenga más información acerca de la configuración de servicios FDM en [Trabajar con el modelo de datos de formulario (FDM)](/help/forms/work-with-form-data-model.md).

+++

+++Fase 2: Creación y configuración del formulario adaptable

### Paso 3: Crear un formulario adaptable

1. Vaya a **Adobe Experience Manager** > **Forms** > **Forms y documentos**
2. Seleccione **Crear** > **Forms adaptable**
3. En la ficha **Source**, seleccione una plantilla de Edge Delivery Services:

   ¡    ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)
   
4. Haga clic en **Crear** para abrir el asistente de **Crear formulario**
5. Especifique los detalles del formulario:
   - **Nombre**: escriba un nombre descriptivo para el formulario
   - **Título**: proporcione un título descriptivo
   - **URL de GitHub**: escribe la URL del repositorio (por ejemplo, `https://github.com/wkndforms/edsforms`)

6. Haga clic en **Crear**

   ¡    ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)
   
El formulario se abrirá en el editor universal para la creación.

### Paso 4: Configurar Source de datos de formulario

1. Seleccione el formulario y haga clic en **Propiedades**

   ¡    ![Seleccionar propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)
   
2. Abra la ficha **Modelo de formulario**
3. En el menú desplegable **Seleccionar de**, elija **Modelo de datos de formulario (FDM)**
4. Seleccione el modelo de datos de formulario creado (por ejemplo, PetFDM) en la lista desplegable

   ¡    ![Seleccione la pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)
   
5. Haga clic en **Guardar y cerrar**
6. Abra el formulario para editarlo en el editor universal

Los elementos de formulario del FDM aparecen en la pestaña **Origen de datos** del **Explorador de contenido**.

### Paso 5: Agregar el enlace de datos a los campos de formulario

1. Seleccione elementos de datos de la ficha **Origen de datos**
2. Haga clic en **Agregar** o arrastre y suelte elementos para crear el formulario

   ![Captura de pantalla del editor universal que muestra el formulario basado en esquemas](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Agregar enlaces de datos a campos de formulario:
   - Seleccionar un campo de formulario
   - En el panel **Propiedades**, busque la propiedad **Referencia de enlace**
   - Seleccione la referencia de enlace de datos adecuada

     ![Enlace de datos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++Fase 3: Configuración del servicio de relleno previo

### Paso 6: Habilitar las extensiones necesarias

Asegúrese de que estas extensiones estén habilitadas en el editor universal:

1. **Extensión de propiedades de formularios AEM**
   - Abrir **Extension Manager** en el editor universal
   - Habilitar la extensión **Propiedades de formulario AEM**

   ![Icono de propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

2. **Extensión de Data Source**
   - Habilite la extensión **Fuente de datos** si no ve el icono **Fuentes de datos**

   ![Captura de pantalla de Universal Editor Extension Manager](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Para obtener instrucciones detalladas sobre la administración de extensiones, consulte [Características destacadas de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Paso 7: Configurar el servicio de relleno previo

1. Abra el formulario adaptable en el editor universal
2. Haga clic en el icono de extensión **Propiedades de formulario AEM**

   ![Seleccionar icono de propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Haga clic en la ficha **Rellenar previamente**
4. Seleccionar **servicio de prerrellenado del modelo de datos de formulario**

   ¡    ![Seleccionar servicio de relleno previo](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)
   
5. Haga clic en **Guardar y cerrar**

+++

+++Fase 4: Prueba De La Configuración De Relleno Previo

### Paso 8: Previsualización y pruebas

1. Ir a **Forms** > **Forms y documentos**
2. Seleccione el formulario adaptable
3. Elegir **vista previa como HTML**
4. Pruebe el relleno previo añadiendo parámetros a la dirección URL:

       https://your-preview-url.com?&lt;bindreferencefield>=&lt;value>
   
   **Ejemplo:**

       https://your-preview-url.com?petid=12345
       
   ¡    ![Rellenar previamente formulario](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)
   
El formulario debe rellenarse automáticamente con datos basados en el parámetro proporcionado.

+++

## Ejemplos

### Estructuras de datos de relleno previo de muestra

**Ejemplo de JSON para formulario basado en FDM:**

    &quot;
    
    {
    &quot;afBoundData&quot;: {
    &quot;user&quot;: {
    &quot;firstName&quot;: &quot;John&quot;,
    &quot;lastName&quot;: &quot;Doe&quot;,
    &quot;email&quot;: &quot;john.doe@example.com&quot;,
    &quot;phone&quot;: &quot;+1-555-0123&quot;
    }
    ,
    &quot;afUnBoundData&quot;: {
    &quot;additionalInfo&quot;: &quot;Preferencias de usuario cargado &quot;
    }
    }
    
    &quot;

**Ejemplo XML para formulario basado en XFA:**

    &quot;
    
    &lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?>
    &lt;afData>
    &lt;afBoundData>
    &lt;user>
    &lt;firstName>John&lt;/firstName>
    &lt;lastName>Doe&lt;/lastName>
    &lt;email>john.doe@example.com&lt;/email>
    &lt;/user>
    &lt;/afBoundData>
    &lt;/afData>
    
    &quot;

### URL de relleno previo de ejemplo

Las siguientes direcciones URL son solo ilustrativas y no funcionarán tal cual. Reemplace el host y los parámetros por los relevantes para su propio entorno al probar la funcionalidad de relleno previo.

**Prueba de relleno previo básica:**

    https://preview.example.com/form.html?userId=12345

**Prueba de varios parámetros:**

    https://preview.example.com/form.html?userId=12345&amp;category=premium


## Resolución de problemas

+++Problemas comunes y soluciones

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| **Los campos de formulario no se rellenan previamente** | Valores `bindRef` incorrectos | Verificar que `bindRef` coincida exactamente con los nombres de campo de FDM |
| **Errores de formato de datos** | Estructura de datos no coincidente | Asegúrese de que los datos de relleno previo coincidan con el esquema del modelo de formulario |
| **Servicio no encontrado** | Problemas de configuración de FDM | Compruebe que los servicios de FDM estén correctamente configurados y guardados |
| **Errores de autenticación** | Conectividad de fuente de datos | Verificar las credenciales y la conectividad de la fuente de datos |
| **Carga parcial de datos** | Faltan asignaciones de campo | Asegúrese de que todos los campos obligatorios tengan enlaces de datos adecuados |

+++

+++Pasos de depuración

1. **Verificar configuración de FDM:**
   - Comprobar si los servicios están correctamente configurados
   - Probar los servicios FDM de forma independiente
   - Validar conectividad de fuente de datos

2. **Comprobar configuración del formulario:**
   - Confirmar que el formulario está asociado al FDM correcto
   - Comprobar valores de campo `bindRef`
   - Formulario de prueba sin relleno previo primero

3. **Flujo de datos de prueba:**
   - Utilizar las herramientas para desarrolladores de exploradores para inspeccionar solicitudes de red
   - Buscar errores de JavaScript en la consola
   - Validar formato de datos de respuesta

4. **Mensajes de error comunes:**
   - &quot;Servicio de relleno previo no encontrado&quot;: comprobar la configuración del servicio
   - &quot;Error en el enlace de datos&quot;: Comprobar la precisión de `bindRef`
   - &quot;Formato de datos no válido&quot;: Asegúrese de que los datos coincidan con el esquema

+++

## Prácticas recomendadas

+++Prácticas recomendadas de configuración

- **Use un nombre descriptivo**: Asigne un nombre claro a sus FDM y servicios
- **Validar esquemas de datos**: Asegúrese de que la estructura de datos coincida con los requisitos del formulario
- **Probar de forma incremental**: configure y pruebe un campo a la vez
- **Asignaciones de documentos**: realice un seguimiento de las asignaciones de campo a datos

+++

+++Optimización del rendimiento

- **Minimizar el volumen de datos**: rellenar solo los campos necesarios
- **Usar almacenamiento en caché**: configure el almacenamiento en caché apropiado para los datos a los que se accede con frecuencia
- **Optimizar consultas**: Asegúrese de que las consultas de base de datos sean eficientes
- **Monitorizar el rendimiento**: haga un seguimiento de los tiempos de carga de los formularios con el relleno previo habilitado

+++

+++Consideraciones de seguridad

- **Validar parámetros de entrada**: validar siempre los parámetros de URL
- **Sanear datos**: limpie los datos antes de rellenar previamente los formularios
- **Implementar controles de acceso**: Asegúrese de que los usuarios solo puedan tener acceso a sus propios datos
- **Usar HTTPS**: Use siempre conexiones seguras para la transmisión de datos

+++

+++Directrices de experiencia del usuario

- **Proporcionar comentarios**: Mostrar indicadores de carga durante la captura de datos
- **Controlar correctamente los errores**: mostrar mensajes de error útiles
- **Permitir invalidaciones**: permita que los usuarios modifiquen los datos rellenados previamente
- **Mantener coherencia**: utilice un comportamiento de relleno previo coherente en todos los formularios

+++

## Preguntas frecuentes

+++¿Cómo puedo probar si el relleno previo funciona correctamente?

Obtenga una vista previa del formulario y anexe parámetros de relleno previo a la dirección URL con este formato: `?<bindreferencefield>=<value>`. Asegúrese de que el campo tenga un(a) `bindRef` válido(a) que coincida con la estructura de datos. Utilice las herramientas para desarrolladores de navegadores para inspeccionar las solicitudes de red y comprobar que los datos se recuperan correctamente.

+++

+++¿Qué formatos de datos se admiten para rellenar previamente Forms adaptable?

Los Forms adaptables admiten varios formatos según el modelo de formulario:

- **Formularios XFA**: XML que coincide con el esquema XFA
- **Formularios de esquema JSON**: los datos JSON cumplen con el esquema
- **Formularios FDM**: JSON que se asigna a la estructura del modelo de datos
- **Formularios de esquema XML**: XML que coincide con la estructura de esquema

+++

+++¿Puedo rellenar previamente tanto los campos enlazados como los no enlazados?

Sí, puede rellenar previamente ambos tipos de campos. Los campos enlazados utilizan la sección `afBoundData` y deben coincidir con el esquema del modelo de formulario. Los campos no enlazados utilizan la sección `afUnBoundData` y pueden contener cualquier dato adicional.

+++

+++¿Qué debo hacer si solo se rellenan previamente algunos campos?

Compruebe que todos los campos tengan `bindRef` valores correctos que coincidan exactamente con su FDM. Compruebe que el origen de datos contiene todos los campos obligatorios y que la estructura de datos coincide con el esquema del modelo de formulario.

+++

+++¿Cómo administro la autenticación para los servicios de relleno previo?

La autenticación depende de la configuración de la fuente de datos. Para el prerrellenado basado en FDM, configure la autenticación en la configuración de la fuente de datos. Para rellenar previamente borradores, los usuarios suelen tener que iniciar sesión para acceder a los borradores guardados.

+++

+++¿Puedo utilizar varios servicios de rellenado previo en un formulario?

Puede configurar un servicio de relleno previo principal por formulario. Sin embargo, puede combinar diferentes fuentes de datos dentro de un solo modelo de datos de formulario para lograr una funcionalidad similar.

+++

=
## Temas relacionados

- [Integración de formularios con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Crear modelos de datos de formulario](/help/forms/create-form-data-models.md)
- [Trabajar con el modelo de datos de formulario (FDM)](/help/forms/work-with-form-data-model.md)
- [Configuración de fuentes de datos](/help/forms/configure-data-sources.md)
- [Introducción a Edge Delivery Services para AEM Forms](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
