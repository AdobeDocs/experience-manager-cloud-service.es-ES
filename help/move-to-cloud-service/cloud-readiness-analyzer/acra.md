---
title: Información general de AEM System
description: Información general de AEM System
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# Información general de AEM System {#aem-system}

En esta página se describe AEM como un servicio en la nube que ofrece nuevas funciones con una arquitectura que supone una mejora significativa con respecto a las versiones anteriores de AEM. La actualización a esta nueva arquitectura requiere un esfuerzo considerable.

## Descripción {#background}

El meta-patrón ACRA se utiliza para identificar varios problemas relacionados con las actualizaciones a AEM como servicio de nube. Admite varios tipos de información de asesoramiento mediante una combinación de los valores *de referencia* y &quot;referenciadoPor&quot; del patrón y su objeto de *contexto* . El valor de *tipo* dentro del objeto de *contexto* determina el problema específico que se ha detectado.

Se prevé que los problemas de preparación incluidos en el modelo ACRA tengan relativamente pocos casos que provoquen el asesoramiento. Hay otros problemas de preparación relacionados con AEM como servicio de nube que pueden tener muchas instancias que necesitan atención y a las que se les da su propio código de patrón. (Consulte IU y URL).

## Datos del patrón {#pattern-data}

En la representación JSON del patrón se incluyen los siguientes objetos:

* **item.message**: Tipo de problema de disponibilidad. (Ver más abajo).
* **data**: Un objeto JSON que contiene los datos correspondientes al tipo.

### Posibles consecuencias y riesgos {#possible-implications}

Por determinar

### Posibles soluciones  {#possible-solutions}

Por determinar
