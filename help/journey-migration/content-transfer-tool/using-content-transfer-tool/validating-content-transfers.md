---
title: Validación de transferencias de contenido
description: Utilice la herramienta de transferencia de contenido para validar las transferencias de contenido
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---


# Validación de transferencias de contenido {#validating-content-transfers}

## Introducción {#getting-started}

Los usuarios pueden determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se ha introducido correctamente en la instancia de destino. Esta función de validación funciona comparando un resumen de las rutas de todos los nodos implicados durante la extracción con un resumen de las rutas de todos los nodos implicados durante la ingesta. Si hay rutas de nodos incluidas en el compendio de extracción que falten en el compendio de ingesta, se considera que la validación ha fallado y que puede ser necesaria una validación manual adicional.

>[!INFO]
>
>Esta función estará disponible a partir de la versión de la herramienta de transferencia de contenido (CTT) 1.8.x. El entorno de destino de AEM Cloud Service debe ejecutar al menos la versión 6158 o superior. También requiere que se configure el entorno de origen para ejecutar [la copia previa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La función de validación busca el archivo azcopy.config en el origen. Si no encuentra este archivo, no se ejecutará la validación. Para obtener más información sobre cómo configurar un archivo azcopy.config, consulte [Gestión de repositorios de contenido grandes: configurar un archivo azcopy.config](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La validación de una transferencia de contenido es una función opcional. Al habilitar esta función, se aumentará el tiempo necesario para realizar una extracción y una ingesta. Para utilizar la función, actívela en la consola del sistema del entorno de AEM de origen siguiendo estos pasos:

1. Vaya a la consola web de Adobe Experience Manager en la instancia de origen, en **Herramientas - Operaciones - Consola web** o directamente a la dirección URL en *https://serveraddress:serverport/system/console/configMgr*
1. Buscar **Configuración del servicio de extracción de herramienta de transferencia de contenido**
1. Utilice el botón del icono de lápiz para editar sus valores de configuración
1. Habilite la opción **Habilitar validación de migración durante la extracción** y, a continuación, presione **Guardar**:

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Con esta configuración habilitada y el entorno de AEM Cloud Service de destino ejecutando una versión compatible, la validación de la migración se producirá durante todas las extracciones e ingestas posteriores.

Para obtener más información sobre cómo instalar la herramienta de transferencia de contenido, consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Validación de una transferencia de contenido {#how-to-validate-a-content-transfer}

Con la validación de migración habilitada en el entorno de AEM de origen, inicie una extracción.

Si **Sobrescribir contenedor de almacenamiento provisional durante la extracción** está habilitado, todos los nodos involucrados con la extracción se registrarán en el resumen de la ruta de extracción. Cuando se usa esta configuración, es importante habilitar la opción **Borrar el contenido existente en la instancia de Cloud antes de la ingesta** durante la ingesta; de lo contrario, puede que parezca que faltan nodos en el resumen de la ingesta. Estos son los nodos que ya están presentes en el destino desde ingestas anteriores.

Para ver una ilustración gráfica de esto, consulte los siguientes ejemplos:

### Ejemplo 1 {#example-1}

* **Extracción (sobrescribir)**

  ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/example1-extraction.png)

* **Ingesta (borrado)**

  ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

  Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes, incluso para ingestas repetidas.

### Ejemplo 2 {#example-2}

* **Extracción**

  ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/example2-extraction.png)

* **Ingesta**

  ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

  Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes para la ingesta inicial.

  Si la ingesta se repite, el resumen de la ingesta está vacío y la validación parece haber fallado. El resumen de ingesta está vacío porque todos los nodos de esta extracción ya estarán presentes en el destino.

Una vez finalizada la extracción, comience la ingesta.

La parte superior del registro de ingesta contendrá una entrada, similar a `aem-ethos/tools:1.2.438`. Asegúrese de que este número de versión sea **1.2.438** o superior; de lo contrario, la versión de AEM as a Cloud Service que esté utilizando no admitirá validación.

Una vez finalizada la ingesta y iniciada la validación, se anota la siguiente entrada de registro en el &quot;log&quot; de ingesta:

```
Gathering artifacts for migration validation...
```

Los detalles de la validación siguen esta entrada. A continuación, puede ver un ejemplo de una migración de gran tamaño:

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

Este es un ejemplo de una validación que se ha realizado correctamente, ya que no faltaban entradas en el resumen de ingesta que estuvieran presentes en el resumen de extracción.

Para comparar, el aspecto que tendría un informe de validación si la validación hubiera fallado (o si se hubiera realizado una migración superior):

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

El ejemplo de error anterior se obtuvo ejecutando una ingesta y volviendo a ejecutar la misma ingesta con la opción Borrar deshabilitada, de modo que no había nodos involucrados durante la ingesta; todo estaba presente en el destino.

Además de incluirse en el registro de ingesta, también se puede acceder al informe de validación desde la interfaz de usuario de **Trabajos de ingesta** en Cloud Acceleration Manager. Para ello, haga clic en los tres puntos (**...**) y luego haga clic en **Informe de validación** en la lista desplegable para ver el informe de validación.


![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Validación de la migración de entidades principales {#how-to-validate-group-migration}

Consulte [Migración de grupos](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md) para leer los detalles principales de la migración y por qué es necesaria.

Una vez que la extracción y la ingesta se hayan completado correctamente, estará disponible un resumen y un informe de la migración principal. Esta información se puede utilizar para validar qué grupos se migraron correctamente y, quizás, para determinar por qué no se migraron algunos.

Para ver esta información, vaya a Cloud Acceleration Manager. Haga clic en la tarjeta del proyecto y en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y busque la ingesta que desea comprobar. Haga clic en los tres puntos (**...**) para esa ingesta y, a continuación, haga clic en **Ver resumen principal** en la lista desplegable.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

Verá un cuadro de diálogo con la información de resumen. Utilice los iconos de ayuda para leer una descripción más completa. Haga clic en el botón **Descargar informe** para descargar el informe completo separado por comas (CSV).  Tenga en cuenta también que al final de este informe se encuentra el Informe de usuarios, que puede utilizarse para la administración de usuarios después de la migración.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

El informe Migración principal informa de lo siguiente:

* Cada grupo migró y la primera ruta de contenido que activó la migración de ese grupo; el grupo también podría estar en otras rutas, pero solo se informa de la primera que se encuentra para un grupo determinado. También informa de si se ha encontrado en una directiva ACL o CUG.
* No se migraron todos los grupos y el motivo por el que no se migraron.  Por lo general, será por uno de estos motivos:
   * Es un grupo integrado
   * Ya está en el sistema de destino
   * No está en una directiva ACL o CUG en el contenido que se migra
   * Tiene un campo único duplicado (uno de rep:principalName, rep:authorizableId, jcr:uuid o rep:externalId ya está en el destino, pero todos deben ser únicos)

## Solución de problemas {#troubleshooting}

### Error de validación. ¿Y ahora qué? {#validation-fail}

El primer paso es determinar si la ingesta falló realmente o si el contenido extraído ya está presente en el entorno de destino. Esto puede ocurrir si se repite una ingesta con la opción **Borrar contenido existente en la instancia de Cloud antes de la ingesta** deshabilitada.

Para verificarla, elija una ruta en el informe de validación y compruebe si está presente en el entorno de destino. Si es un entorno de publicación, puede limitarse a comprobar páginas y recursos directamente. Abra un ticket con el Servicio de atención al cliente si necesita ayuda con este paso.

### El recuento de nodos es menor de lo que esperaba. ¿Por qué? {#node-count-lower-than-expected}

Algunas rutas de los resúmenes de extracción e ingesta se excluyen a propósito para mantener el tamaño de estos archivos manejable, con el objetivo de poder calcular el resultado de validación de migración en un plazo de dos horas desde que se completó la ingesta.

Las rutas de acceso que excluimos actualmente de los resúmenes incluyen: `cqdam.text.txt` representaciones, nodos dentro de `/home` y nodos dentro de `/jcr:system`.

### Grupos de usuarios cerrados {#validating-cugs}

Consulte [Migración de grupos de usuarios cerrados](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) para obtener consideraciones adicionales al utilizar una directiva de grupo de usuarios cerrados (CUG).
