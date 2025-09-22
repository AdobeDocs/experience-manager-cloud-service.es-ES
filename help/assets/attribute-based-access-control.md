---
title: Control de acceso basado en atributos
description: Obtenga información sobre cómo habilitar el control de acceso basado en atributos para definir reglas basadas en metadatos para definir el nivel de acceso a los recursos disponibles en Content Hub
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: 0833e31d37c473d37e16ee037823e61611622322
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 4%

---

# Control de acceso basado en atributos {#attribute-based-access-control}

El control de acceso basado en atributos (ABAC) permite a los administradores de Content Hub definir reglas basadas en metadatos para definir el nivel de acceso a los recursos disponibles en Content Hub.

Los administradores de una organización definen reglas para los grupos de usuarios, que se asignan a un ID de grupo. Las reglas son una combinación de [operadores lógicos y de comparación](#supported-rule-constructs), y los administradores pueden definir tantas reglas como necesiten para administrar el acceso a los recursos en Content Hub.

Las reglas se basan en metadatos y, si las condiciones definidas en la regla coinciden con los metadatos del recurso, este se muestra al grupo de usuarios. Content Hub analiza los metadatos de los recursos, incluidos los metadatos personalizados, de todos los recursos disponibles en **Todos los Assets** y **Colecciones**, para mostrar los resultados a los grupos de usuarios.

Por ejemplo, PERMITIR el acceso al grupo de usuarios con ID de grupo = 1011, cuando los metadatos de los recursos coincidan con &quot;Marca = Marca X&quot; Y &quot;Región = EMEA O América&quot;. Content Hub solo muestra esos recursos al grupo de usuarios con id. = 1011 donde marca = `Brand X` y región = `EMEA` o `Americas`.

Algunas de las ventajas clave del control de acceso basado en atributos son:

* Elimina la dependencia de la estructura de carpetas para los permisos

* Permite a los administradores cargar recursos y determinar de forma retroactiva las estructuras de permisos

* Reduce el número de duplicados: mejora la integridad de los recursos. Los duplicados son necesarios en los permisos basados en carpetas cuando los mismos recursos se comparten con diferentes grupos.

## ¿Cómo se habilita el control de acceso basado en atributos? {#enable-attribute-based-access-control}

Por el momento, no puede crear reglas de control de acceso basadas en atributos por su cuenta mediante la interfaz de usuario de Content Hub.

Haga clic en **Descargar hoja de cálculo** para descargar y definir reglas en una hoja de cálculo. Cree un ticket de asistencia de Adobe y proporcione las reglas definidas en la hoja de cálculo a Adobe.

[!BADGE Descargar hoja de cálculo]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}


Defina las reglas en la hoja de cálculo siguiendo las directrices definidas en este artículo.

>[!IMPORTANT]
>
> Después de definir las reglas, vaya a la ficha **Errores de validación** de la hoja de cálculo y haga clic en **Ejecutar validaciones ABAC**. **Todas las validaciones pasadas** confirman que puede proporcionar las reglas definidas a Adobe.

## Ejemplo de caso de uso de Control de acceso basado en atributos {#example-metadata-based-rules}

Para admitir una implementación de marketing a gran escala, varios integrantes del equipo de todas las regiones y marcas necesitan tener acceso a los recursos digitales. Cada persona tiene un ámbito específico basado en la región y la marca. ABAC aplica estas reglas automáticamente a través de los metadatos del recurso. La siguiente tabla ilustra los diferentes tipos de personas para este caso de uso y las reglas aplicadas:

| Grupo de usuarios | Función | Descripción de rol | Identificador de grupo | Regla ABAC |
|---------------------|----------------|-----------------|------------|------------|
| John | Responsable de marketing EMEA | Supervisa la ejecución de marketing en todas las marcas de EMEA. Necesita acceso a recursos aprobados para todas las marcas destinadas a los mercados de EMEA. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | Responsable de marketing de APAC | Supervisa la ejecución de marketing en todas las marcas de APAC. Necesita acceso a recursos aprobados para todas las marcas destinadas a los mercados APAC. | group-apac-marketing | region = &quot;APAC&quot; |
| Sophie | Brand X Manager (EMEA) | Gestiona la identidad de la marca X en EMEA. Necesita ver únicamente el contenido aprobado por la Marca X adaptado a los mercados de EMEA. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | Administrador de marca Y (APAC) | Administra la identidad de la marca Y en APAC. Necesita ver únicamente contenido aprobado por la Marca Y y adaptado a los mercados APAC. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

Con estas reglas, los administradores de Content Hub tienen lo siguiente:

* **Acceso granular basado en reglas**: los usuarios solo ven los recursos relevantes para su región y marca; no hay asignaciones manuales de permisos.

* **Colaboración global perfecta**: Los equipos regionales y de marca trabajaron en paralelo sin conflictos de acceso.

* **Permisos escalables y con garantía de futuro**: a medida que se agregan nuevas regiones o marcas, las reglas se pueden actualizar en función de los metadatos.

>[!IMPORTANT]
>
> De manera predeterminada, se deniega el acceso a todos los demás grupos de usuarios, que no se han especificado con ninguna regla en la [hoja de cálculo](#enable-attribute-based-access-control). Si un usuario no forma parte de ningún grupo para el que se hayan definido reglas ABAC, no puede acceder a ningún recurso. Si necesita que algunos usuarios tengan acceso a todos los recursos (por ejemplo, administradores), debe mencionar un grupo con un ID de grupo en la hoja de cálculo con los detalles de que este grupo en particular necesita acceso a todos los recursos y Adobe lo configurará por usted.


## Construcciones de reglas compatibles {#supported-rule-constructs}

* **Operadores lógicos**:
   * Y: todas las condiciones deben ser verdaderas
   * O: Al menos una condición debe ser verdadera
* **Operadores de comparación**:
   * Igual a (=): comprueba si un usuario o atributo de recurso coincide con un valor
   * Not Equals (!)=): Comprueba si un usuario o atributo de recurso no coincide con un valor

Cuando los campos de metadatos del recurso contienen matrices (por ejemplo, varias regiones o etiquetas), `Equals` hace referencia a la lógica `contains` y `Not Equals` hace referencia a la lógica `does not contain`.

Esto le permite escribir reglas sencillas y expresivas, como: ALLOW if region = emea AND assetType != prototype AND tags != confidencial.

## Directrices {#guidelines-attribute-based-access-control}

* Las reglas ABAC solo son aplicables a los recursos aprobados para Content Hub. Para obtener más información, consulte [Aprobar Assets para Content Hub](/help/assets/approve-assets-content-hub.md).

* No asigne reglas DENEGAR; en su lugar, convierta siempre la regla DENEGAR a PERMITIR. Por ejemplo, `ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes` se puede convertir en `ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`.

* Las reglas ABAC se aplican a grupos de usuarios mediante el ID de grupo de IMS, que está disponible en Admin Console.


* Puede establecer el [Destino de aprobación](/help/assets/approve-assets-content-hub.md#set-approval-target) para los recursos mediante el entorno de creación de AEM as a Cloud Service. Las reglas ABAC se aplican a los recursos aprobados con el destino de aprobación = `Content Hub`, ya que el destino de aprobación = `Delivery` es para los recursos disponibles para `Delivery` + `Content Hub`. Assets marcado como Destino de aprobación = `Delivery` son visibles para todos en el Centro de contenido.

* Asegúrese de que los esquemas de metadatos utilizados en las reglas ABAC estén correctamente definidos y disponibles en AEM. Proporcione la ruta completa de los esquemas de metadatos de AEM que definen las propiedades a las que se hace referencia en las reglas ABAC. Opcionalmente, puede crear una carpeta de prueba con algunos recursos de muestra con valores de metadatos que coincidan con las condiciones ABAC. Esto ayuda a verificar el comportamiento de las reglas y evaluar el acceso con precisión.

* Capture la intención comercial de la regla en un comentario, independientemente de si la condición está escrita correctamente, ya que la intención nos ayuda a validar y corregir la lógica, si es necesario.

* Los archivos PDF de licencia, que se establecen para DRM deben ser visibles para todos, de modo que los usuarios puedan verlos cuando descarguen el recurso con la licencia.
