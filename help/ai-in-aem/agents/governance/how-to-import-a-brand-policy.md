---
title: Cómo importar una política de marca
description: Uso del agente de control de Adobe para importar una política de marca
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 94d671ebbd5aeb5992fdbc9d779ffbca51f82585
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---


# Cómo importar una política de marca {#how-to-import-a-brand-policy}

## Información general {#overview}

Una política de marca define las reglas, estándares y restricciones que garantizan que todo el contenido producido o actualizado por Adobe Experience Manager sea coherente con la identidad de marca de una empresa. Esto suele incluir el tono de voz, la terminología, las directrices visuales y las reglas editoriales.

El agente de gobernanza utiliza las políticas de marca como fuente fiable para analizar las páginas existentes y guiar la generación de contenido. Los clientes pueden proporcionar sus propias políticas de marca originales, que el agente de gobernanza convierte automáticamente en comprobaciones de políticas legibles por IA. Estas comprobaciones se utilizan para validar el contenido y proporcionar al agente de producción un marco de trabajo fiable y aplicable para generar o actualizar páginas que permanezcan alineadas con la marca.

## ¿Qué es una política de marca en el agente de gobernanza? {#what-is-a-brand-policy-in-the-governance-agent}

En el contexto del agente de gobernanza, una política de marca es una representación estructurada de las reglas de marca que AI puede entender y aplicar. En lugar de exigir a los clientes que reescriban sus directrices en un formato técnico, el agente de gobernanza acepta las políticas de marca en su forma original (por ejemplo, documentos, directrices o descripciones de reglas).

Una vez importada, la directiva se transforma en un conjunto de comprobaciones de directivas de IA que pueden:

* Analizar las páginas existentes para detectar incoherencias de marca
* Marcar desviaciones de tono, terminología o reglas obligatorias
* Proporcionar una guía clara a los agentes intermedios
* Asegúrese de que el contenido generado o actualizado sigue siendo compatible con la marca por diseño

Este enfoque permite a los equipos reutilizar la documentación de marca existente y, al mismo tiempo, beneficiarse del control automatizado y de la producción de contenido escalable.

## Uso de las directivas de marca {#how-brand-policies-are-used}

Después de importar una política de marca:

* El agente de gobernanza interpreta y normaliza la política en comprobaciones de IA ejecutables
* Las páginas se pueden analizar con respecto a la política para identificar lagunas o violaciones
* El agente de producción utiliza estas comprobaciones como restricciones al generar o actualizar contenido
* El cumplimiento de la marca se vuelve coherente, repetible y auditable en todos los sitios y equipos


## Importar una directiva de marca {#import-a-brand-policy}

Para importar una marca en el agente de gobernanza:

1. Cree una marca dando un nombre y un dominio principal. Para ello, haga clic en el botón **Contexto de administración** en el panel de navegación izquierdo de su página de inicio de Experience Manager y luego presione el botón **+ Agregar marca**, como se muestra a continuación:

   ![Agregando una nueva marca](/help/ai-in-aem/agents/governance/assets/add_brand.png){width="70%"}

1. Configure el nombre de la marca y una descripción en la siguiente ventana

   ![Nombrar la marca](/help/ai-in-aem/agents/governance/assets/add_brand_dialogue.png){width="60%"}

1. Las nuevas marcas se crean en estado de borrador. Asegúrese de cambiar la marca recién creada a un estado Activo, haciendo clic en la tarjeta de la marca, presionando la opción Editar (lápiz) en la esquina superior derecha de la pantalla, establezca **Estado** a **Activo** en la siguiente ventana y haga clic en **Guardar cambios**. Debe habilitar las marcas configurándolas como Activas antes de poder utilizarlas.

   ![Establecer el estado de la marca en Activo](/help/ai-in-aem/agents/governance/assets/set_brand_active.png){width="60%"}

1. Una vez creada la marca, crea un dominio principal en la siguiente ventana presionando el vínculo **Dominios** de la izquierda:

   ![Configurar un dominio para la marca](/help/ai-in-aem/agents/governance/assets/add_domain.png)

   >[!IMPORTANT]
   >
   >Al igual que las nuevas marcas, los nuevos dominios se crean con un estado de Borrador predeterminado. Para cambiar esto, ve a tu Marca, haz clic en **Dominios**, luego edita tu dominio usando el icono de lápiz y establece su estado en **Activo**.

1. Una vez configurado el dominio principal, puede cargar el documento de la directiva de marca. Para ello, vaya a **Políticas** en la esquina superior izquierda de la ventana y presione el botón **+ Agregar directiva**.

   ![Agregando una directiva desde la tarjeta de marca](/help/ai-in-aem/agents/governance/assets/add_policy_treeview.png)

   >[!NOTE]
   >
   >También puede agregar directivas si cambia a la ficha **Directivas** y presiona el vínculo **+ Agregar directiva**.

1. En la siguiente ventana, presione **Cargar PDF** y seleccione los documentos de política de marca en formato PDF

   ![Cargar el documento de la política de marca](/help/ai-in-aem/agents/governance/assets/upload_brand_policy_document.png){width="70%"}

   El agente de gobernanza analizará las directrices de la política de marca utilizando un lenguaje natural y extraerá las comprobaciones obtenidas del documento y las traducirá en tareas reales. Una vez procesado el documento, puede ver un resumen de la importación, que incluye el número de comprobaciones y el estado de la directiva, como se muestra a continuación:

   ![Ventana de información general sobre el estado de la directiva de marca](/help/ai-in-aem/agents/governance/assets/policy_status.png)

1. Una vez creada la marca y cargado el documento de la póliza, puede obtener una vista detallada por marca en la ficha **Marcas** y haciendo clic en la tarjeta de una marca. Esta es la vista que desea usar para crear categorías de comprobaciones, presionando los tres puntos junto a una categoría existente y seleccionando **+ Agregar categoría**, como se muestra en la captura de pantalla siguiente:

   ![Agregar categoría](/help/ai-in-aem/agents/governance/assets/add_category.png)

   También puede utilizar esta vista para crear, editar y eliminar comprobaciones, que detallaremos en los pasos siguientes.

1. Para obtener una vista más detallada de cada comprobación individual, puede pasar a la ficha **Comprobaciones** y ver una lista de cada comprobación individual extraída de los documentos de instrucciones. Puede filtrar las comprobaciones según la marca o el estado:

   ![Ver comprobaciones de marca individuales](/help/ai-in-aem/agents/governance/assets/see_brand_checks.png)

   Además, puede ver detalles adicionales de cada comprobación individual haciendo clic en los tres puntos (**...**) a la izquierda de la comprobación y presionando **Ver detalles**. Se abrirá una nueva ventana con más información sobre la comprobación:

   ![Ver detalles de comprobación individual](/help/ai-in-aem/agents/governance/assets/view_check_details.png)

   También puede eliminar comprobaciones presionando **Eliminar** desde la misma ubicación del menú o editarlas presionando **Editar**:

   ![Editando una comprobación](/help/ai-in-aem/agents/governance/assets/edit_check.png)

1. Puede agregar manualmente una comprobación presionando **Agregar comprobación** en la esquina superior izquierda de la ventana Comprobaciones:

   ![Agregando un cheque](/help/ai-in-aem/agents/governance/assets/add_check.png)

   En la siguiente pantalla, puede configurar detalles como:

   * El nombre del cheque
   * La regla, descrita en lenguaje natural
   * La categoría
   * El ámbito o ámbitos a los que se aplica

   ![Configuración de los detalles de comprobación](/help/ai-in-aem/agents/governance/assets/add_check_window.png)

1. Por último, para obtener una lista de los dominios y las marcas con las que están asociados, presione la pestaña **Dominios**. Esta sección le permite agregar, eliminar o modificar dominios de la lista.

