---
title: Control de acceso basado en atributos
description: Obtenga información sobre cómo habilitar el control de acceso basado en atributos para definir reglas basadas en metadatos para definir el nivel de acceso a los recursos disponibles en Content Hub
role: Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: b736af556c8580d005097c27cceba050b21a57c9
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 2%

---


# Control de acceso basado en atributos {#attribute-based-access-control}

El control de acceso basado en atributos (ABAC) permite a los administradores de Content Hub definir reglas basadas en metadatos para controlar el nivel de acceso a los recursos disponibles en Content Hub.

Los administradores de una organización definen reglas para los grupos de usuarios, que se asignan a un ID de grupo. Las reglas son una combinación de [operadores lógicos y de comparación](#supported-rule-constructs), y los administradores pueden definir tantas reglas como sean necesarias para administrar el acceso a los recursos en Content Hub.

Las reglas se basan en metadatos. Si las condiciones definidas en una regla coinciden con los metadatos del recurso, este se muestra al grupo de usuarios. Content Hub analiza los metadatos de los recursos, incluidos los metadatos personalizados, de todos los recursos disponibles en **Todos los Assets** y **Colecciones** para mostrar los resultados a los grupos de usuarios.

Por ejemplo, PERMITIR el acceso al grupo de usuarios con ID de grupo = 1011 cuando los metadatos de los recursos coincidan con &quot;Marca = Marca X&quot; Y &quot;Región = EMEA O América&quot;. Content Hub muestra solo los recursos al grupo de usuarios con ID = 1011 donde &quot;Marca = Marca X&quot; y &quot;Región = EMEA o América&quot;.

Las reglas ABAC en Content Hub se pueden configurar mediante los siguientes métodos:

* **Configuración de autoservicio** con el [Asistente de IA en Content Hub](#configure-abac-using-ai-assistant-in-content-hub), con tecnología del agente de control de AEM
* **Configuración basada en hoja de cálculo** mediante [Soporte técnico de Adobe](#configure-abac-using-spreadsheet)

Con AI Assistant en Content Hub, los administradores pueden definir y administrar reglas ABAC mediante metadatos y lenguaje natural. Esto permite una configuración de reglas más rápida y reduce la dependencia de los flujos de trabajo de soporte manual.

Algunas de las ventajas clave del control de acceso basado en atributos son:

* Elimina la dependencia de la estructura de carpetas para los permisos
* Permite a los administradores cargar recursos y determinar de forma retroactiva las estructuras de permisos
* Reduce el número de duplicados y mejora la integridad del recurso. Los duplicados son necesarios en los permisos basados en carpetas cuando los mismos recursos se comparten con diferentes grupos.
* Habilita el acceso granular basado en reglas
* Admite administración escalable en marcas y regiones
* Mejora la administración de recursos

>[!VIDEO](https://video.tv.adobe.com/v/3475413/?learn=on&enablevpops){transcript=true}

## Cómo habilitar el control de acceso basado en atributos {#enable-attribute-based-access-control}

Las reglas ABAC en Content Hub se pueden configurar mediante los siguientes métodos:

* **Configuración de autoservicio mediante el Asistente de IA en Content Hub (con tecnología del Agente de control de AEM)**\
  Los administradores pueden definir y administrar reglas ABAC directamente utilizando el lenguaje natural en Content Hub.

* **Configuración basada en hoja de cálculo a través del soporte técnico de Adobe**\
  Los administradores pueden definir reglas ABAC en una hoja de cálculo y enviarlas al servicio de asistencia de Adobe para que las configuren.

## Configuración de ABAC mediante el asistente de IA en Content Hub

Con AI Assistant en Content Hub, con tecnología de AEM Governance Agent, puede crear y administrar reglas ABAC directamente en Content Hub utilizando lenguaje natural.

Puede hacer lo siguiente:
* Buscar reglas existentes
* Creación de reglas
* Actualizar reglas
* Eliminar reglas

Esto permite a los administradores crear y administrar reglas de acceso sin depender de flujos de trabajo de soporte.

### Antes de empezar {#before-you-begin-ai-assistant}

Asegúrese de lo siguiente antes de utilizar el Asistente de IA en Content Hub para la configuración de reglas ABAC:

* Tiene licencia para AEM as a Cloud Service
* El asistente de IA con tecnología del agente de control de AEM está disponible para su organización
* Si todavía no tiene acceso, póngase en contacto con su representante de Adobe y complete los pasos necesarios para la licencia
* No se necesita un piloto GenAI para el programa try-buy

### Pasos para configurar las reglas ABAC mediante el asistente de IA {#steps-ai-assistant}

1. Abra el Asistente de IA en Content Hub.

1. Comience con una instrucción sencilla.

   Por ejemplo:

   `Create a new rule in Content Hub`

   Un asistente de IA le guiará por la información necesaria para crear la regla.

1. Defina la regla en lenguaje natural.

   Por ejemplo:

   `Frescopa Web Marketers user group should have access to assets where product equals Frescopa`

1. Seleccione el entorno donde debe aplicarse la regla ABAC.

1. Revise la regla antes de aplicarla.

   El asistente de IA genera una previsualización estructurada de la regla. No se aplica nada automáticamente. Puede revisar la regla generada, ajustarla si es necesario o cancelar la acción antes de aplicarla.

1. Guarde y aplique la regla.

   Una vez guardada, la regla se aplica dinámicamente en función de los metadatos.

Este paso de revisión ayuda a garantizar la precisión antes de aplicar la regla.

### Administración de reglas ABAC mediante indicadores {#manage-abac-rules-using-prompts}

Después de empezar a utilizar el asistente de IA, puede administrar las reglas ABAC de forma conversacional.

**Descubrir reglas**

* Mostrar todas las reglas ABAC de Content Hub existentes

**Crear reglas**

* Cree una regla que proporcione acceso al grupo de marketing de producto a todos los recursos
* Conceder acceso al grupo de ventas a recursos cuya región sea igual a EMEA

**Actualizar reglas**

* Actualizar regla para el grupo de marketing de EMEA para incluir APAC

**Eliminar reglas**

* Eliminar la regla para el grupo de marketing de producto

**Explorar metadatos y grupos**

* Mostrar los grupos y las propiedades de metadatos disponibles para establecer las reglas

## Configurar ABAC mediante hoja de cálculo

Si el Asistente de IA no está habilitado para su organización, puede configurar reglas ABAC mediante el flujo de trabajo basado en hoja de cálculo.

Haga clic en **Descargar hoja de cálculo** para descargar y definir reglas en una hoja de cálculo. Cree un ticket de asistencia de Adobe y proporcione las reglas definidas en la hoja de cálculo a Adobe.

[!BADGE Descargar hoja de cálculo]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}

Defina las reglas en la hoja de cálculo siguiendo las directrices descritas en este artículo.

>[!IMPORTANT]
>
>Después de definir las reglas, vaya a la ficha **Errores de validación** de la hoja de cálculo y haga clic en **Ejecutar validaciones ABAC**. El mensaje **Todas las validaciones pasadas** confirma que puede proporcionar las reglas definidas a Adobe.

### Pasos para configurar las reglas ABAC mediante hoja de cálculo {#steps-spreadsheet}

1. Descargue la plantilla de hoja de cálculo ABAC.
1. Defina reglas en la hoja de cálculo utilizando condiciones basadas en metadatos.
1. Asigne cada regla al ID de grupo de IMS correspondiente.
1. Capture la intención comercial de la regla en los comentarios.
1. Envíe un ticket de asistencia de Adobe y comparta la hoja de cálculo completa con Adobe.
1. Adobe configura las reglas para su organización.

## Ejemplo de caso de uso de control de acceso basado en atributos {#example-metadata-based-rules}

Para admitir una implementación de marketing a gran escala, varios integrantes del equipo de todas las regiones y marcas necesitan tener acceso a los recursos digitales. Cada persona tiene un ámbito específico basado en la región y la marca. ABAC aplica estas reglas automáticamente usando metadatos de recursos. La siguiente tabla ilustra las personalidades de este caso de uso y las reglas aplicadas:

| Persona | Función | Descripción de rol | Identificador de grupo | Regla ABAC |
|---|---|---|---|---|
| John | Responsable de marketing EMEA | Supervisa la ejecución de marketing en todas las marcas de EMEA. Necesita acceso a recursos aprobados para todas las marcas destinadas a los mercados de EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Responsable de marketing de APAC | Supervisa la ejecución de marketing en todas las marcas de APAC. Necesita acceso a recursos aprobados para todas las marcas destinadas a los mercados APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Brand X Manager (EMEA) | Gestiona la identidad de la marca X en EMEA. Necesita ver únicamente el contenido aprobado por la Marca X adaptado a los mercados de EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | Administrador de marca Y (APAC) | Administra la identidad de la marca Y en APAC. Necesita ver únicamente contenido aprobado por la Marca Y y adaptado a los mercados APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Con estas reglas, los administradores de Content Hub tienen lo siguiente:

* **Acceso granular basado en reglas**: Los usuarios solo ven los recursos relevantes para su región y marca sin asignaciones manuales de permisos.
* **Colaboración global perfecta**: Los equipos regionales y de marca trabajan en paralelo sin conflictos de acceso.
* **Permisos escalables y con garantía de futuro**: a medida que se agregan nuevas regiones o marcas, las reglas se pueden actualizar en función de los metadatos.

### Casos adicionales en los que ABAC sea útil {#additional-scenarios-abac}

ABAC también puede ayudar a abordar los siguientes escenarios:

* **Marca global y acceso regional**: los equipos solo ven los activos relevantes para su marca y mercado.
* **Colaboración entre agencias y socios**: Las agencias externas y los socios solo pueden acceder a los activos de campaña relevantes para ellos.
* **Acceso basado en roles para diferentes equipos**: equipos como de marketing, ventas y legales pueden acceder a recursos relevantes para su función.
* **Cumplimiento legal específico de la región**: los usuarios pueden restringirse a los recursos aprobados para requisitos regulatorios o regionales específicos.

>[!IMPORTANT]
>
>De manera predeterminada, se deniega el acceso a todos los demás grupos de usuarios que no se han especificado con ninguna regla en la [hoja de cálculo](#configure-abac-spreadsheet). Si un usuario no forma parte de ningún grupo para el que se hayan definido reglas ABAC, no puede acceder a ningún recurso. Si algunos usuarios deben tener acceso a todos los recursos, por ejemplo los administradores, incluya un grupo con un ID de grupo en la hoja de cálculo y especifique que el grupo requiere acceso a todos los recursos para que Adobe pueda configurarlo en consecuencia.

## Construcciones de reglas compatibles {#supported-rule-constructs}

* **Operadores lógicos**:
   * Y: todas las condiciones deben ser verdaderas
   * O: Al menos una condición debe ser verdadera

* **Operadores de comparación**:
   * Igual a (=): comprueba si un usuario o atributo de recurso coincide con un valor
   * No es igual a (!=): comprueba si un atributo de usuario o de recurso no coincide con un valor

Cuando los campos de metadatos del recurso contienen matrices, por ejemplo, varias regiones o etiquetas, Igual a hace referencia a contiene lógica y No igual a no contiene lógica.

Esto le permite escribir reglas sencillas y expresivas, como PERMITIR si region = emea Y assetType != prototipo Y etiquetas != confidenciales.

## Directrices {#guidelines-attribute-based-access-control}

Las siguientes directrices se aplican a la configuración basada en el asistente de IA y en hojas de cálculo:

* Las reglas ABAC solo son aplicables a los recursos aprobados para Content Hub. Para obtener más información, consulte [Aprobar Assets para Content Hub](/help/assets/approve-assets-content-hub.md).
* No defina reglas DENY. Convierta siempre las reglas DENY en reglas ALLOW. Por ejemplo, PERMITIR si región = región-usuario DENEGAR si assetType = prototipo Y confidencial = sí se puede convertir en PERMITIR si región = región-usuario AND (assetType != prototipo OR confidencial != sí).
* Las reglas ABAC se aplican a grupos de usuarios mediante el ID de grupo de IMS, que está disponible en Admin Console.
* Puede establecer el [Destino de aprobación](/help/assets/approve-assets-content-hub.md#set-approval-target) para los recursos mediante el entorno de creación de AEM as a Cloud Service. Las reglas ABAC se aplican a los recursos aprobados con Approval Target = Content Hub, como Approval Target = Delivery es para recursos disponibles para Delivery + Content Hub. Assets marcado como Destino de aprobación = Entrega son visibles para todos en Content Hub.
* Asegúrese de que los esquemas de metadatos utilizados en las reglas ABAC estén correctamente definidos y disponibles en AEM. Proporcione la ruta completa del esquema de metadatos o los esquemas de AEM que definen las propiedades a las que se hace referencia en las reglas ABAC. Opcionalmente, puede crear una carpeta de prueba con recursos de muestra que coincidan con las condiciones de ABAC para ayudar a verificar el comportamiento de las reglas y evaluar el acceso con precisión.
* Capture la intención comercial de la regla en los comentarios, incluso si la condición está escrita correctamente, ya que la intención ayuda a validar y corregir la lógica si es necesario.
* Asegúrese de que los valores de metadatos utilizados para las reglas de acceso, como marca, región y producto, se mantengan de forma coherente en todos los recursos.
* Comience con casos de uso clave, como el acceso basado en la marca o en la región.
* Utilice indicaciones claras al definir reglas con el Asistente de IA. Describa la intención en el lenguaje empresarial para que el asistente de IA pueda traducirla en una regla estructurada.
* Los archivos PDF de licencia configurados para DRM deben permanecer visibles para todos los usuarios para que puedan revisar la información de licencia al descargar el recurso con la licencia.

## Preguntas frecuentes {#faqs-attribute-based-access-control-content-hub}

### ¿Qué es el Control de acceso basado en atributos (ABAC) en AEM Assets Content Hub?

Control de acceso basado en atributos (ABAC) en AEM Assets Content Hub permite a los administradores definir reglas basadas en metadatos para controlar el nivel de acceso de los distintos grupos de usuarios a los recursos digitales. El acceso se determina si los metadatos del recurso coinciden con las condiciones especificadas en las reglas, lo que permite una administración granular y dinámica de la visibilidad del recurso.

### ¿Cómo definen los administradores las reglas de acceso mediante ABAC en AEM Assets Content Hub?

Los administradores definen las reglas de acceso creando condiciones basadas en metadatos de recursos, como la marca o la región, y vinculándolas a ID de grupo de usuarios específicos. Estas reglas utilizan operadores lógicos y de comparación para especificar exactamente qué recursos son visibles para qué grupos de usuarios.

### ¿Cuáles son las principales ventajas de utilizar ABAC sobre los permisos tradicionales basados en carpetas en AEM Assets Content Hub?

ABAC elimina la dependencia de las estructuras de carpetas para los permisos, permite a los administradores cargar recursos y asignar permisos de forma retroactiva, y reduce el número de recursos duplicados necesarios. Esto mejora la integridad del recurso y simplifica la administración de permisos, especialmente cuando es necesario compartir los recursos con varios grupos.

### ¿Pueden los administradores configurar reglas ABAC directamente en la interfaz de Content Hub de los AEM Assets?

Los administradores pueden configurar reglas ABAC mediante el Asistente de IA en Content Hub, si está activado para su organización. También pueden seguir utilizando el flujo de trabajo basado en hojas de cálculo a través del Soporte de Adobe.

### ¿Qué tipos de condiciones de metadatos se pueden utilizar al configurar reglas ABAC en AEM Assets Content Hub?

Las reglas ABAC en AEM Assets Content Hub pueden utilizar operadores lógicos como AND y OR, y operadores de comparación como igual a y no igual a. Las propiedades de metadatos utilizadas en las reglas deben estar definidas correctamente y disponibles en los esquemas de metadatos de AEM, y pueden incluir campos como región, marca, producto, campaña, tipo de recurso o estado de publicación.

### ¿Por qué los AEM Assets de Content Hub ABAC son especialmente útiles para organizaciones con equipos grandes y diversas necesidades de recursos?

ABAC es útil para organizaciones con equipos grandes porque permite un acceso granular y basado en reglas a los recursos según los roles de usuario, las regiones, las marcas o las necesidades comerciales. Garantiza que los usuarios solo vean los activos relevantes para sus responsabilidades, sin asignaciones manuales de permisos ni duplicaciones excesivas de activos.

### ¿Cómo deben preparar los administradores la hoja de cálculo ABAC para AEM Assets Content Hub antes de enviarla al Soporte de Adobe?

Los administradores deben crear grupos de usuarios en Adobe Admin Console, anotar sus ID de grupo, definir claramente los permisos y las condiciones para cada grupo en la hoja de cálculo, garantizar que todas las propiedades de metadatos estén correctamente asignadas a los esquemas adecuados y utilizar la columna de comentarios para aclarar la intención empresarial de cada regla.