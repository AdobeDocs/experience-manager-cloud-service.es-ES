---
title: Rellenado previo de los campos del formulario adaptable
description: Utilice los datos existentes para rellenar previamente los campos de un formulario adaptable. Los usuarios pueden rellenar previamente la información básica de un formulario iniciando sesión con sus perfiles de redes sociales.
feature: Adaptive Forms, Edge Delivery Services
role: User, Developer
level: Beginner, Intermediate
time: 45-60 minutes
keywords: rellenar previamente un formulario adaptable, edge delivery services con formularios adaptables, autorrellenar formularios adaptables
exl-id: 7b6224e2-a19c-4146-8545-0ce9d1da9b29
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 94%

---

# Configuración del servicio de rellenado previo en formularios adaptables mediante Edge Delivery Services

El rellenado previo de formularios es el proceso de cumplimentar automáticamente los campos de formulario con datos pertinentes de fuentes externas en cuanto un usuario abre el formulario. Al aprovechar la información de perfiles de usuario, bases de datos, borradores guardados u otros sistemas back-end, el rellenado previo optimiza la experiencia de cumplimentación de formularios, lo que reduce la entrada manual, minimiza los errores y acelera la finalización. Esto no solo mejora la satisfacción del usuario, sino que también aumenta la probabilidad de que los envíos de formularios se realicen correctamente.

## Ventajas del rellenado previo de formularios

| Ventaja | Descripción |
|---------|-------------|
| **Finalización más rápida** | Reduce la entrada manual de datos, lo que ayuda a los usuarios a completar formularios rápidamente |
| **Experiencia del usuario mejorada** | Los formularios dan la sensación de ser más personalizados y prácticos, especialmente para los usuarios que regresan |
| **Tasas de conversión más altas** | Reduce el abandono de formularios minimizando el esfuerzo necesario del usuario |
| **Errores de entrada reducidos** | Los datos de fuentes de confianza reducen los errores tipográficos y las entradas incorrectas |
| **Mejor calidad de datos** | Garantiza datos estructurados, precisos y coherentes para los sistemas back-end |

## Funcionamiento del rellenado previo

En el diagrama siguiente se ilustra el proceso de rellenado previo automático que se produce cuando un usuario abre un formulario adaptable:

![Flujo del proceso de rellenado previo de formularios](/help/edge/docs/forms/universal-editor/assets/prefill-process-flow.svg)

El proceso de rellenado previo incluye cuatro pasos clave:

1. **El usuario abre el formulario**: el usuario accede a un formulario adaptable a través de una URL o mediante navegación
1. **Identificar la fuente de datos**: el servicio de rellenado previo determina el origen de datos configurado (modelo de datos de formulario o servicio de borrador)
1. **Recuperar datos**: el sistema recupera datos de usuario pertinentes en función del contexto, los parámetros o la identificación del usuario
1. **Asignar y mostrar**: los datos se asignan a campos de formulario mediante propiedades `bindRef` y el formulario rellenado se muestra al usuario

Este proceso automatizado garantiza que los usuarios vean un formulario previamente rellenado con su información pertinente, lo que mejora significativamente la experiencia del usuario y las tasas de finalización del formulario.

## Estructura de datos para rellenado previo

Los formularios adaptables admiten dos tipos de campos:

- **Campos enlazados**: campos conectados a una fuente de datos con una propiedad `bindRef` que no está vacía
- **Campos no enlazados**: campos independientes con valores `bindRef` vacíos

La estructura de datos de rellenado previo incluye:

- **afBoundData**: contiene datos para campos y paneles enlazados
- **afUnBoundData**: contiene datos para campos no enlazados

El formato de datos debe coincidir con el modelo de formulario:

- **Formularios XFA**: XML compatible con esquema de plantilla XFA
- **Formularios de esquema XML**: XML que coincide con la estructura de esquema
- **Formularios de esquema JSON**: JSON compatible con el esquema
- **Formularios de modelo de datos de formulario (FDM)**: JSON que coincide con la estructura de FDM
- **Formularios sin esquema**: ninguno de los campos está enlazado y todos ellos utilizan XML sin enlazar

## Requisitos previos

Antes de configurar los servicios de rellenado previo, asegúrese de que tiene lo siguiente:

### Configuración exigida

- [Repositorio de GitHub configurado para Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)
- [Bloque de formularios adaptable añadido al proyecto](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)
- [Fuente de datos configurada](/help/forms/configure-data-sources.md)
- [Modelo de datos de formulario creado](/help/forms/create-form-data-models.md)

### Requisitos de acceso

- Acceso a AEM Forms as a Cloud Service
- Permisos para crear y editar formularios
- Acceso al editor universal con las extensiones requeridas habilitadas

>[!TIP]
>
> También puede editar formularios para integrar el modelo de datos de formulario (FDM) en el editor universal para recuperar datos de varias fuentes back-end. Para obtener más información, consulte el artículo [Integración de formularios con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md).

## Opciones del servicio de rellenado previo

El editor universal proporciona dos opciones de servicio de rellenado previo:

| Tipo de servicio | Función | Fuente de datos | Ideal para |
|--------------|---------|-------------|----------|
| **Rellenado previo de borradores en el portal de formularios** | Reanuda los formularios parcialmente completados | Borradores guardados en el portal de formularios | Continuación de aplicaciones incompletas |
| **Rellenado previo el modelo de datos del formulario** | Rellena campos de sistemas externos | Bases de datos back-end mediante FDM | Rellenado automático de datos de perfil del usuario |

### Comparación detallada

| Función | Servicio de rellenado previo de borradores | Servicio de rellenado FDM |
|---------|----------------------|---------------------|
| **Autenticación** | Requiere el inicio de sesión del usuario para acceder a los borradores | Configurable según la fuente de datos |
| **Complejidad de la configuración** | Configuración mínima | Requiere configuración y asignación de FDM |
| **Tipo de datos** | Datos guardados estáticos | Datos dinámicos en tiempo real |
| **Caso práctico** | Reanudar aplicaciones guardadas | Rellenar previamente desde perfiles de usuario o bases de datos |


## Configurar servicio de rellenado previo para un formulario

+++Fase 1: Configuración del modelo de datos de formulario

### Paso 1: Crear un modelo de datos de formulario

1. Iniciar sesión en la instancia de AEM Forms as a Cloud Service
1. Ir a **Adobe Experience Manager** > **Formularios** > **Integraciones de datos**
1. Seleccione **Crear** > **Modelo de datos de formulario**.
1. Elegir la información pertinente en **Configuración de fuente de datos** y seleccionar la opción **Fuente de datos** configurada

   ![Modelo de datos de formulario creado](/help/edge/docs/forms/universal-editor/assets/create-fdm.png)

   >[!TIP]
   >
   >Para obtener instrucciones detalladas sobre la creación de modelos de datos de formulario, consulte [Crear modelo de datos de formulario](/help/forms/create-form-data-models.md).

### Paso 2: Configurar los servicios de FDM

1. Ir a **Adobe Experience Manager** > **Formularios** > **Integraciones de datos**
1. Abrir el modelo de formulario de datos en modo de edición
1. Seleccionar un objeto de modelo de datos y haga clic en **Editar propiedades**
1. Configurar los servicios **Lectura** y **Escritura** para los objetos del modelo de datos seleccionados

   ![Configurar servicio de lectura/escritura](/help/edge/docs/forms/universal-editor/assets/configure-reda-write-service.png)

1. Configure los argumentos del servicio:

   - Hacer clic en el icono de edición del argumento del servicio de lectura
   - Enlazar el argumento a un **atributo de perfil de usuario**, **atributo de solicitud** o **valor literal**
   - Especificar el valor del enlace (por ejemplo, `petid` para un formulario de registro de mascota)

   ![Configurar argumento de ID de mascota](/help/edge/docs/forms/universal-editor/assets/pet-id-arguments.png)

1. Hacer clic en **Listo** para guardar el argumento y en **Guardar** para guardar el FDM

   >[!NOTE]
   >
   > Obtenga más información acerca de la configuración de servicios FDM en [Trabajar con el modelo de datos de formulario (FDM)](/help/forms/work-with-form-data-model.md).

+++

+++Fase 2: Creación y configuración del formulario adaptable

### Paso 3: Crear un formulario adaptable

1. Ir a **Adobe Experience Manager** > **Formularios** > **Formularios y documentos**
1. Seleccionar **Crear** > **Formularios adaptables**
1. En la pestaña **Fuente**, seleccione una plantilla basada en Edge Delivery Services:

   ![Plantilla de Edge Delivery Services](/help/edge/assets/create-eds-forms.png)

1. Hacer clic en **Crear** para abrir el asistente de **Crear formulario**

   >
   >
   > Puede configurar el origen de datos desde la ficha **Datos** o posterior editando las propiedades del formulario.

1. Especifique los detalles del formulario:

   - **Nombre**: escribir un nombre descriptivo para el formulario
   - **Título**: proporcionar un título descriptivo
   - **URL de GitHub**: escribir la URL del repositorio (por ejemplo, `https://github.com/wkndforms/edsforms`)

1. Haga clic en **Crear**

   ![Crear formulario basado en esquema](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form1.png)

El formulario se abre en el editor universal para la creación.

### Paso 4: Configurar la fuente de datos de formulario

1. Seleccionar el formulario y hacer clic en **Propiedades**

   ![Seleccionar propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/select-form-properties1.png)

2. Abrir la pestaña **Modelo de formulario**
3. En la lista desplegable **Seleccionar de**, elegir **Modelo de datos de formulario (FDM)**
4. Seleccionar el modelo de datos de formulario creado (por ejemplo, PetFDM) en la lista desplegable

   ![Seleccionar pestaña Modelo de formulario](/help/edge/docs/forms/universal-editor/assets/select-form-model1.png)

5. Hacer clic en **Guardar y cerrar**
6. Abrir el formulario para editarlo en el editor universal

Los elementos de formulario del FDM aparecen en la pestaña **Fuente de datos** de **Explorador de contenido**.

### Paso 5: Añadir el enlace de datos a los campos de formulario

1. Seleccionar elementos de datos de la pestaña **Fuente de datos**
2. Hacer clic en **Añadir** o arrastrar y soltar elementos para crear el formulario

   ![Captura de pantalla del editor universal que muestra el formulario basado en esquemas](/help/edge/docs/forms/universal-editor/assets/ue-form.png)

3. Añada enlace de datos a los campos del formulario:

   - Seleccionar un campo de formulario
   - En el panel **Propiedades**, buscar la propiedad **Referencia de enlace**
   - Seleccionar la referencia de enlace de datos adecuada

     ![Enlace de datos](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding1.png)

+++

+++Fase 3: Configuración del servicio de relleno previo

### Paso 6: Habilitar las extensiones necesarias

Asegúrese de que estas extensiones estén habilitadas en el editor universal:

1. **Extensión de propiedades de formularios AEM**

   - Abrir **Extension Manager** en el editor universal
   - Habilitar la extensión **Propiedades de formulario AEM**

   ![Icono de propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/form-edit-properties.png)

1. **Extensión de fuente de datos**

   - Habilitar la extensión **Fuente de datos** si no ve el icono **Fuentes de datos**

   ![Captura de pantalla de Extension Manager del editor universal](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

   >[!TIP]
   >
   > Para obtener instrucciones detalladas sobre la administración de extensiones, consulte [Características destacadas de las funciones de Extension Manager](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions).

### Paso 7: Configurar el servicio de rellenado previo

1. Abrir el formulario adaptable en el editor universal
2. Hacer clic en el icono de extensión **Propiedades de formulario AEM**

   ![Seleccionar el icono de propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/select-fdm-properties-icon.png)

3. Hacer clic en la pestaña **Prerrellenar**.
4. Seleccionar **Servicio de rellenado previo del modelo de datos de formulario**

   ![Seleccionar servicio de rellenado previo](/help/edge/docs/forms/universal-editor/assets/select-fdm-prefill.png)

5. Hacer clic en **Guardar y cerrar**

+++

+++Fase 4: Prueba De La Configuración De Relleno Previo

### Paso 8: Previsualizar y probar

1. Ir a **Formularios** > **Formularios y documentos**
2. Seleccionar el formulario adaptable
3. Elegir **Vista previa como HTML**
4. Pruebe el rellenado previo añadiendo parámetros a la URL:

   `https://your-preview-url.com?<bindreferencefield>=<value>`

   **Ejemplo:**

   https://your-preview-url.com?petid=12345

   ![Rellenado previo de un formulario](/help/edge/docs/forms/universal-editor/assets/prefill-form.png)

El formulario debe rellenarse automáticamente con datos basados en el parámetro proporcionado.

+++

## Ejemplos

### Estructuras de datos de rellenado previo de muestras

**Ejemplo de JSON para formulario basado en FDM:**

```
  {
    "afBoundData": {
      "user": {
        "firstName": "John",
        "lastName": "Doe",
        "email": "john.doe@example.com",
        "phone": "+1-555-0123"
      }
    },
    "afUnBoundData": {
      "additionalInfo": "User preferences loaded"
    }
  }
```

**Ejemplo XML para formulario basado en XFA:**

```
  <?xml version="1.0" encoding="UTF-8"?>
  <afData>
    <afBoundData>
      <user>
        <firstName>John</firstName>
        <lastName>Doe</lastName>
        <email>john.doe@example.com</email>
      </user>
    </afBoundData>
  </afData>
```

### URL de rellenado previo de ejemplo

Las siguientes URL son solo ilustrativas y no funcionarán tal cual. Reemplace el host y los parámetros por los que sean pertinentes para su propio entorno al probar la funcionalidad de rellenado previo.

**Prueba de rellenado previo básica:**

`https://preview.example.com/form.html?userId=12345`

**Prueba de varios parámetros:**

`https://preview.example.com/form.html?userId=12345&category=premium`


## Resolución de problemas

+++Problemas comunes y soluciones

| Problema | Causa posible | Solución |
|-------|----------------|----------|
| **Los campos de formulario no se rellenan previamente** | Valores `bindRef` incorrectos | Verificar que `bindRef` coincida exactamente con los nombres de campo de FDM |
| **Errores de formato de datos** | Estructura de datos no coincidente | Asegurarse de que los datos de rellenado previo coincidan con el esquema del modelo de formulario |
| **No se ha encontrado el servicio** | Problemas de configuración de FDM | Comprobar que los servicios de FDM estén correctamente configurados y guardados |
| **Errores de autenticación** | Conectividad de fuente de datos | Verificar las credenciales y la conectividad de la fuente de datos |
| **Carga parcial de datos** | Faltan asignaciones de campo | Asegurarse de que todos los campos obligatorios tengan enlaces de datos adecuados |

+++

+++Pasos de depuración

1. **Verificar configuración de FDM:**

   - Comprobar si los servicios están correctamente configurados
   - Probar los servicios FDM de forma independiente
   - Validar conectividad de fuente de datos

2. **Comprobar configuración del formulario:**

   - Confirmar que el formulario está asociado al FDM correcto
   - Comprobar valores `bindRef` de campo
   - Probar formulario sin rellenado previo primero

3. **Flujo de datos de prueba:**

   - Utilizar las herramientas para desarrolladores de exploradores para inspeccionar solicitudes de red
   - Buscar errores de JavaScript en la consola
   - Validar formato de datos de respuesta

4. **Mensajes de error comunes:**

   - “Servicio de rellenado previo no encontrado”: comprobar la configuración del servicio
   - “Error en el enlace de datos”: verificar la precisión de `bindRef`
   - “Formato de datos no válido”: asegurarse de que los datos coincidan con el esquema

+++

## Prácticas recomendadas

+++Prácticas recomendadas de configuración

- **Usar nombres descriptivos**: asignar un nombre claro a FDM y servicios
- **Validar esquemas de datos**: asegurarse de que la estructura de datos coincida con los requisitos del formulario
- **Probar de forma incremental**: configurar y probar un campo a la vez
- **Asignaciones de documentos**: realizar un seguimiento de las asignaciones de campo a datos

+++

+++Optimización de rendimiento

- **Minimizar el volumen de datos**: rellenar previamente solo los campos necesarios
- **Usar almacenamiento en caché**: configurar el almacenamiento en caché apropiado para los datos a los que se accede con frecuencia
- **Optimizar consultas**: asegurarse de que las consultas de base de datos sean eficientes
- **Monitorizar el rendimiento**: hacer un seguimiento de los tiempos de carga de los formularios con el rellenado previo habilitado

+++

+++Consideraciones sobre la seguridad

- **Validar parámetros de entrada**: validar siempre los parámetros de URL
- **Sanear los datos**: limpiar los datos antes de rellenar previamente los formularios
- **Implementar controles de acceso**: asegurarse de que los usuarios solo puedan acceder a sus propios datos
- **Usar HTTPS**: usar siempre conexiones seguras para la transmisión de datos

+++

+++Directrices de experiencia del usuario

- **Proporcionar comentarios**: mostrar indicadores de carga durante la captura de datos
- **Controlar correctamente los errores**: mostrar mensajes de error útiles
- **Permitir invalidaciones**: permitir que los usuarios modifiquen los datos rellenados previamente
- **Mantener coherencia**: utilizar un comportamiento de rellenado previo coherente en todos los formularios

+++

## Preguntas frecuentes

+++¿Cómo se comprueba si el relleno previo funciona correctamente?

Obtenga una vista previa del formulario y anexe parámetros de rellenado previo a la URL con este formato: `?<bindreferencefield>=<value>`. Asegúrese de que el campo tenga un `bindRef` válido que coincida con la estructura de datos. Utilice las herramientas para desarrolladores de explorador para inspeccionar las solicitudes de red y comprobar que los datos se recuperan correctamente.

+++

+++¿Qué formatos de datos se admiten para rellenar previamente Forms adaptable?

Los formularios adaptables admiten varios formatos según el modelo de formulario:

- **Formularios XFA**: XML que coincide con el esquema XFA
- **Formularios de esquema JSON**: los datos JSON cumplen con el esquema
- **Formularios FDM**: JSON que se asigna a la estructura del modelo de datos
- **Formularios de esquema XML**: XML que coincide con la estructura de esquema

+++

+++¿Puedo rellenar previamente tanto los campos enlazados como los no enlazados?

Sí, puede rellenar previamente ambos tipos de campos. Los campos enlazados utilizan la sección `afBoundData` y deben coincidir con el esquema del modelo de formulario. Los campos no enlazados utilizan la sección `afUnBoundData` y pueden contener cualquier dato adicional.

+++

+++¿Qué debo hacer si solo se rellenan previamente algunos campos?

Compruebe que todos los campos tengan valores `bindRef` correctos que coincidan exactamente con el FDM. Verifique que la fuente de datos contenga todos los campos obligatorios y que la estructura de datos coincida con el esquema del modelo de formulario.

+++

+++¿Puedo utilizar varios servicios de rellenado previo en un formulario?

Puede configurar un servicio de rellenado previo principal por formulario. Sin embargo, puede combinar diferentes fuentes de datos dentro de un solo modelo de datos de formulario para lograr una funcionalidad similar.

+++

+++¿Cómo administro la autenticación para los servicios de relleno previo?

La autenticación depende de la configuración de la fuente de datos. Para el rellenado previo basado en FDM, configure la autenticación en la configuración de la fuente de datos. Para rellenar previamente borradores, los usuarios suelen tener que iniciar sesión para acceder a los borradores guardados.

+++



## Temas relacionados

- [Integración de formularios con el modelo de datos de formulario en el editor universal](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)
- [Crear modelo de datos de formulario](/help/forms/create-form-data-models.md)
- [Trabajar con el modelo de datos de formulario (FDM)](/help/forms/work-with-form-data-model.md)
- [Configurar fuentes de datos](/help/forms/configure-data-sources.md)
- [Introducción a Edge Delivery Services para AEM Forms. ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
