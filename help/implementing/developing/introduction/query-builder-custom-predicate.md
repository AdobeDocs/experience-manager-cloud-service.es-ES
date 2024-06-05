---
title: Implementación de un evaluador de predicados personalizado para el Generador de consultas
description: AEM El Generador de consultas de ofrece una forma fácil y personalizable de consultar el repositorio de contenido en la que se encuentra
exl-id: 8c2f8c22-1851-4313-a1c9-10d6d9b65824
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Implementación de un evaluador de predicados personalizado para el Generador de consultas {#implementing-a-custom-predicate-evaluator-for-the-query-builder}

Este documento describe cómo ampliar el [Generador de consultas](query-builder-api.md) implementando un evaluador de predicados personalizado.

## Información general {#overview}

El [Generador de consultas](query-builder-api.md) ofrece una forma sencilla de consultar el repositorio de contenido. AEM viene con [un conjunto de evaluadores de predicados](#query-builder-predicates.md) que le ayudan a consultar sus datos.

Sin embargo, es posible que desee simplificar las consultas implementando un evaluador de predicados personalizado que oculte cierta complejidad y garantice una mejor semántica.

Un predicado personalizado también podría realizar otras acciones que no son directamente posibles con XPath, por ejemplo:

* Consulta de datos desde otro servicio
* Filtrado personalizado basado en un cálculo

>[!NOTE]
>
>Los problemas de rendimiento deben tenerse en cuenta al implementar un predicado personalizado.

>[!TIP]
>
>Puede encontrar ejemplos de consultas en la [Generador de consultas](query-builder-api.md) documento.

>[!TIP]
>
>Puede encontrar el código de esta página en GitHub
>
>* [Abra el proyecto aem-search-custom-predicate-evaluator en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator)
>* Descargue el proyecto como [un archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-search-custom-predicate-evaluator/archive/master.zip)

>[!NOTE]
>
>Este código vinculado en GitHub y los fragmentos de código de este documento se proporcionan únicamente con fines de demostración.

### Evaluador de predicados en detalle {#predicate-evaluator-in-detail}

Un evaluador de predicados administra la evaluación de ciertos predicados, que son las restricciones de definición de una consulta.

Asigna una restricción de búsqueda de nivel superior (por ejemplo, `width>200`) a una consulta JCR específica que se ajuste al modelo de contenido real (por ejemplo, `metadata/@width > 200`). O puede filtrar manualmente nodos y comprobar sus restricciones.

>[!TIP]
>
>Para obtener más información sobre `PredicateEvaluator` y el `com.day.cq.search` consulte el [Documentación de Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html?com/day/cq/search/package-summary.html).

### Implementación de un evaluador de predicados personalizado para metadatos de replicación {#implementing-a-custom-predicate-evaluator-for-replication-metadata}

Como ejemplo, esta sección describe cómo crear un evaluador de predicados personalizado que ayude a los datos en función de los metadatos de replicación:

* `cq:lastReplicated` que almacena la fecha de la última acción de replicación
* `cq:lastReplicatedBy` que almacena el id del usuario que activó la última acción de replicación
* `cq:lastReplicationAction` que almacena la última acción de replicación (por ejemplo, Activación, Desactivación)

#### Consulta de metadatos de replicación con evaluadores de predicado predeterminados {#querying-replication-metadata-with-default-predicate-evaluators}

La siguiente consulta recupera la lista de nodos en `/content` rama que ha activado: `admin` desde el comienzo del año.

```xml
path=/content

1_property=cq:lastReplicatedBy
1_property.value=admin

2_property=cq:lastReplicationAction
2_property.value=Activate

daterange.property=cq:lastReplicated
daterange.lowerBound=2013-01-01T00:00:00.000+01:00
daterange.lowerOperation=>=
```

Esta consulta es válida, pero difícil de leer y no resalta la relación entre las tres propiedades de replicación. La implementación de un evaluador de predicados personalizado reducirá la complejidad y mejorará la semántica de esta consulta.

#### Objetivos {#objectives}

El objetivo del `ReplicationPredicateEvaluator` es admitir la consulta anterior mediante la siguiente sintaxis.

```xml
path=/content

replic.by=admin
replic.since=2013-01-01T00:00:00.000+01:00
replic.action=Activate
```

Agrupar predicados de metadatos de replicación con un evaluador de predicados personalizado ayuda a crear una consulta significativa.

#### Actualización de dependencias de Maven {#updating-maven-dependencies}

>[!TIP]
>
>AEM La configuración de nuevos proyectos de, incluido el uso de maven, se explica en detalle por [el tutorial de WKND.](develop-wknd-tutorial.md)

En primer lugar, debe actualizar las dependencias Maven del proyecto. El `PredicateEvaluator` forma parte de `cq-search` por lo que debe añadirse a su archivo pom de Maven.

>[!NOTE]
>
>El ámbito de la `cq-search` la dependencia se establece en `provided` porque `cq-search` es proporcionada por el `OSGi` contenedor.

El siguiente fragmento muestra las diferencias en la variable `pom.xml` archivo, en [formato de diferencia unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

```text
@@ -120,6 +120,12 @@
             <scope>provided</scope>
         <dependency>
+            <groupid>com.day.cq</groupid>
+            <artifactid>cq-search</artifactid>
+            <version>5.6.4</version>
+            <scope>provided</scope>
+        </dependency>
+        <dependency>
             <groupid>junit</groupid>
             <artifactid>junit</artifactid>
             <version>3.8.1</version></dependency>
```

#### Escritura De ReplicationPredicateEvaluator {#writing-the-replicationpredicateevaluator}

El `cq-search` El proyecto contiene el `AbstractPredicateEvaluator` clase abstracta. Esto se puede ampliar con algunos pasos para implementar su propio evaluador de predicados personalizado `(PredicateEvaluator`).

>[!NOTE]
>
>El siguiente procedimiento explica cómo generar un `Xpath` expresión para filtrar datos. Otra opción sería implementar el `includes` que selecciona los datos en base a filas. Consulte la [Documentación de Java](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/search/eval/PredicateEvaluator.html) para obtener más información.

1. Cree una nueva clase Java que extienda `com.day.cq.search.eval.AbstractPredicateEvaluator`
1. Anote su clase con un `@Component` como muestra un fragmento en [formato de diferencia unificado](https://en.wikipedia.org/wiki/Diff#Unified_format)

   ```text
   @@ -19,8 +19,11 @@
     */
    package com.adobe.aem.docs.search;
   
   +import org.apache.felix.scr.annotations.Component;
   +import com.day.cq.search.eval.AbstractPredicateEvaluator;
   
   +@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")
    public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {
   
    }
   ```

   >[!NOTE]
   >
   >El `factory`debe ser una cadena única que comience por `com.day.cq.search.eval.PredicateEvaluator/`y terminan con el nombre de su personalizado `PredicateEvaluator`.

   >[!NOTE]
   >
   >El nombre del `PredicateEvaluator` es el nombre del predicado que se utiliza para crear consultas.

1. Anular:

   ```java
   public String getXPathExpression(Predicate predicate, EvaluationContext context)
   ```

   En el método override se genera un `Xpath` expresión basada en la variable `Predicate` dado en el argumento.

### Ejemplo de un evaluador de predicados personalizado para metadatos de replicación {#example-of-a-custom-predicate-evaluator-for-replication-metadata}

La implementación completa de esto `PredicateEvaluator` puede ser similar a la siguiente clase.

```java
/*
 * #%L
 * aem-docs-custom-predicate-evaluator
 * %%
 * Copyright (C) 2013 Adobe Research
 * %%
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 * #L%
 */

package com.adobe.aem.docs.search;

import org.apache.felix.scr.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.search.Predicate;
import com.day.cq.search.eval.AbstractPredicateEvaluator;
import com.day.cq.search.eval.EvaluationContext;

@Component(metatype = false, factory = "com.day.cq.search.eval.PredicateEvaluator/repli")

public class ReplicationPredicateEvaluator extends AbstractPredicateEvaluator {

    static final String PE_NAME = "replic";


    static final String PN_LAST_REPLICATED_BY = "cq:lastReplicatedBy";
    static final String PN_LAST_REPLICATED = "cq:lastReplicated";
    static final String PN_LAST_REPLICATED_ACTION = "cq:lastReplicationAction";

    static final String PREDICATE_BY = "by";
    static final String PREDICATE_SINCE = "since";
    static final String PREDICATE_SINCE_OP = " >= ";
    static final String PREDICATE_ACTION = "action";

    Logger log = LoggerFactory.getLogger(getClass());

    /**
     * Returns a XPath expression filtering by replication metadata.
     *
     * @see com.day.cq.search.eval.AbstractPredicateEvaluator#getXPathExpression(com.day.cq.search.Predicate,
     *      com.day.cq.search.eval.EvaluationContext)
     */

    @Override

    public String getXPathExpression(Predicate predicate,
            EvaluationContext context) {

        log.debug("predicate {}", predicate);

        String date = predicate.get(PREDICATE_SINCE);
        String user = predicate.get(PREDICATE_BY);
        String action = predicate.get(PREDICATE_ACTION);

        StringBuilder sb = new StringBuilder();

        if (date != null) {

            sb.append(PN_LAST_REPLICATED).append(PREDICATE_SINCE_OP);
            sb.append("xs:dateTime('").append(date).append("')");

        }

        if (user != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_BY);
            sb.append("='").append(user).append("'");

        }

        if (action != null) {

            addAndOperator(sb);
            sb.append(PN_LAST_REPLICATED_ACTION);
            sb.append("='").append(action).append("'");

        }

        String xpath = sb.toString();

        log.debug("xpath **{}**", xpath);

        return xpath;

    }

    /**
     * Add an and operator if the builder is not empty.
     *
     * @param sb a {@link StringBuilder} containing the query under construction
     */

    private void addAndOperator(StringBuilder sb) {

        if (sb.length() != 0) {

            sb.append(" and ");

        }

    }

}
```
