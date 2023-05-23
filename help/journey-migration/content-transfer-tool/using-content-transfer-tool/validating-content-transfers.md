---
title: Validación de transferencias de contenido
description: Utilice la herramienta de transferencia de contenido para validar las transferencias de contenido
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: c1f60a1ead466b47694b8918e5b39011041c5f25
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 2%

---

# Validación de transferencias de contenido {#validating-content-transfers}

## Introducción {#getting-started}

Los usuarios pueden determinar de forma fiable si todo el contenido extraído por la herramienta de transferencia de contenido se ha introducido correctamente en la instancia de destino. Esta función de validación funciona comparando un resumen de las rutas de todos los nodos implicados durante la extracción con un resumen de las rutas de todos los nodos implicados durante la ingesta. Si hay rutas de nodos incluidas en el compendio de extracción que falten en el compendio de ingesta, se considera que la validación ha fallado y que puede ser necesaria una validación manual adicional.

>[!INFO]
>
>Esta función estará disponible a partir de la versión de la herramienta de transferencia de contenido (CTT) 1.8.x. El entorno de destino de AEM Cloud Service debe ejecutar al menos la versión 6158 o buena. También requiere que se configure el entorno de origen para ejecutarse [copia previa](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). La función de validación busca el archivo azcopy.config en el origen. Si no encuentra este archivo, no se ejecutará la validación. Para obtener más información sobre cómo configurar un archivo azcopy.config, consulte [esta página](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

La validación de una transferencia de contenido es una función opcional. Al habilitar esta función, se aumentará el tiempo necesario para realizar una extracción y una ingesta. AEM Para utilizar la función, habilítela en la consola del sistema del entorno de origen de la interfaz de usuario de la interfaz de usuario de origen, siguiendo estos pasos:

1. Vaya a la consola web de Adobe Experience Manager en la instancia de origen, en **Herramientas - Operaciones - Consola web** o directamente a la dirección URL en *https://serveraddress:serverport/system/console/configMgr*
1. Buscar por **Configuración del servicio de extracción de herramienta de transferencia de contenido**
1. Utilice el botón del icono de lápiz para editar sus valores de configuración
1. Habilite la **Habilitar validación de migración durante la extracción** configuración, luego pulse **Guardar**:

   ![imagen](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

Con esta configuración habilitada y el entorno de AEM Cloud Service de destino ejecutando una versión compatible, la validación de la migración se producirá durante todas las extracciones e ingestas posteriores.

Para obtener más información sobre cómo instalar la herramienta de transferencia de contenido, consulte [Introducción a la herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## Validación de una transferencia de contenido {#how-to-validate-a-content-transfer}

AEM Con la validación de migración habilitada en el entorno de origen de la, inicie una extracción.

If **Sobrescribir contenedor de almacenamiento provisional durante la extracción** está activada, todos los nodos implicados en la extracción se registrarán en el resumen de la ruta de extracción. Cuando se utiliza esta configuración, es importante habilitar la variable **Borrar contenido existente en la instancia de Cloud antes de la ingesta** configuración durante la ingesta; de lo contrario, puede parecer que faltan nodos en el compendio de ingesta. Estos son los nodos que ya están presentes en el destino desde ingestas anteriores.

Para ver una ilustración gráfica de esto, consulte los ejemplos siguientes:

### Ejemplo 1 {#example-1}

* **Extracción (sobrescribir)**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **Ingesta (borrado)**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **Notas**

   Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes, incluso para ingestas repetidas.

### Ejemplo 2 {#example-2}

* **Extracción**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **Ingesta**

   ![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **Notas**

   Esta combinación de &quot;Sobrescribir&quot; y &quot;Borrar&quot; dará como resultado resultados de validación coherentes para la ingesta inicial.

   Si se repite la ingesta, el resumen de la ingesta estará vacío y la validación parecerá haber fallado. El resumen de ingesta estará vacío porque todos los nodos de esta extracción ya estarán presentes en el destino.

Una vez finalizada la extracción, comience la ingesta.

La parte superior del registro de ingesta contendrá una entrada, similar a `aem-ethos/tools:1.2.438`. Asegúrese de que este número de versión sea **1,2,438** o buena AEM, de lo contrario, la validación no es compatible con la versión de los as a Cloud Service de validación que está utilizando.

Una vez completada la ingesta y iniciada la validación, se anotará la siguiente entrada de registro en el registro de ingesta:

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

Para comparar, el aspecto que tendría un informe de validación si la validación hubiera fallado es este:

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
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

El ejemplo de error anterior se obtuvo ejecutando una ingesta y volviendo a ejecutar la misma ingesta con la opción Borrar deshabilitada, de modo que no había nodos involucrados durante la ingesta; todo estaba presente en el destino.

Además de incluirse en el registro de ingesta, también se puede acceder al informe de validación desde el **Trabajos de ingesta** interfaz de usuario en Cloud Acceleration Manager. Para ello, haga clic en los tres puntos (**...**) y haga clic en **Informe de validación** en la lista desplegable para ver el informe de validación.


![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## Validación de la migración de entidades principales {#how-to-validate-principal-migration}

Consulte [Asignación de usuarios y migración de principales](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) para leer los detalles de las migraciones principales y por qué es necesario.

Una vez que la extracción y la ingesta se hayan completado correctamente, estará disponible un resumen y un informe de la migración principal. Esta información se puede utilizar para validar qué usuarios y grupos se migraron correctamente y, quizás, para determinar por qué no se migraron algunos.

Para ver esta información, vaya a Cloud Acceleration Manager. Haga clic en la tarjeta de proyecto y en la tarjeta Transferencia de contenido. Vaya a **Trabajos de ingesta** y busque la ingesta que desea comprobar. Haga clic en los tres puntos (**...**) para esa ingesta, luego haga clic en **Ver resumen principal** en la lista desplegable.

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

Verá un cuadro de diálogo con la información de resumen. Utilice los iconos de ayuda para leer una descripción más completa. Haga clic en **Descargar informe** para descargar el informe completo separado por comas (CSV).

![imagen](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>Si la asignación de usuarios está deshabilitada, se mostrará otra variante de este cuadro de diálogo. Indicará que la asignación de usuarios estaba deshabilitada y no mostrará los 3 campos que proporcionan valores de asignación de usuarios.

## Solución de problemas {#troubleshooting}

### Error de validación. ¿Y ahora qué?  {#validation-fail}

El primer paso es determinar si la ingesta falló realmente o si el contenido extraído ya está presente en el entorno de destino. Esto puede ocurrir si se repite una ingesta con el **Borrar contenido existente en la instancia de Cloud antes de la ingesta** opción desactivada.

Para verificarla, elija una ruta en el informe de validación y compruebe si está presente en el entorno de destino. Si es un entorno de publicación, puede limitarse a comprobar páginas y recursos directamente. Si necesita ayuda con este paso, abra una incidencia con el Servicio de atención al cliente.

### El recuento de nodos es menor de lo que esperaba. ¿Por qué? {#node-count-lower-than-expected}

Algunas rutas de los resúmenes de extracción e ingesta se excluyen a propósito para mantener el tamaño de estos archivos manejable, con el objetivo de poder calcular el resultado de validación de migración en un plazo de dos horas desde que se completó la ingesta.

Las rutas que excluimos actualmente de los resúmenes incluyen: `cqdam.text.txt` representaciones, nodos dentro de `/home`y nodos dentro de `/jcr:system`.
