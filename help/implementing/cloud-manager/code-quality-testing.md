---
title: 'Prueba de calidad de código: Cloud Services'
description: 'Prueba de calidad de código: Cloud Services'
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: f8695dd8fdc9ffb203bab943c335ab2957df6251
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 2%

---

# Prueba de calidad de código {#code-quality-testing}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Prueba de calidad de código"
>abstract="La prueba de calidad del código evalúa la calidad del código de la aplicación. Es el objetivo central de una canalización solo de calidad de código y se ejecuta inmediatamente después del paso de compilación en todas las canalizaciones que no sean de producción y producción."

La prueba de calidad del código evalúa la calidad del código de la aplicación. Es el objetivo central de una canalización solo de calidad de código y se ejecuta inmediatamente después del paso de compilación en todas las canalizaciones que no sean de producción y producción.

Consulte [Configuración de la canalización de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los distintos tipos de canalizaciones.

## Comprender las reglas de calidad de código {#understanding-code-quality-rules}

En la prueba de calidad del código, se analiza el código fuente para asegurarse de que cumple determinados criterios de calidad. Actualmente, esto es implementado por una combinación de SonarQube y el examen de nivel de paquete de contenido usando OakPAL. Hay más de 100 reglas que combinan reglas genéricas de Java y reglas específicas de AEM. Algunas de las reglas específicas del AEM se crean en función de las prácticas recomendadas de AEM Engineering y se denominan [Reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>Puede descargar la lista completa de reglas [here](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx).

**Puerta de tres niveles**

Hay una estructura de tres niveles en este paso de prueba de calidad de código para los problemas identificados:

* **Importante**: Estos son problemas identificados por la puerta que causan un fallo inmediato de la tubería.

* **Importante**: Estos son problemas identificados por la puerta que hacen que la canalización introduzca un estado pausado. Un administrador de implementación, un administrador de proyectos o un propietario de empresa pueden anular los problemas, en cuyo caso la canalización continúa, o pueden aceptar los problemas, en cuyo caso la canalización se detiene con un error.

* **Información**: Estos son problemas identificados por la puerta que se proporcionan exclusivamente con fines informativos y no tienen impacto en la ejecución de la canalización

Los resultados de este paso se entregan como *Clasificaciones*.

La siguiente tabla resume las clasificaciones y los umbrales de error para cada una de las categorías Crítica, Importante e Información:

| Nombre | Definición | Categoría | Umbral de error |
|--- |--- |--- |--- |
| Clasificación de seguridad | A = 0 Vulnerabilidad <br/>B = al menos 1 vulnerabilidad menor<br/> C = al menos 1 vulnerabilidad mayor <br/>D = al menos 1 vulnerabilidad crítica <br/>E = al menos 1 Vulnerabilidad del bloqueador | Importante | &lt; B |
| Clasificación de fiabilidad | A = 0 Error <br/>B = al menos 1 error menor <br/>C = al menos 1 error mayor <br/>D = al menos 1 error crítico E = al menos 1 error bloqueador | Importante | &lt; C |
| Puntuación de mantenimiento | El coste de corrección pendiente de los olores de código es: <br/><ul><li>&lt;=5% del tiempo que ya ha pasado a la aplicación, la clasificación es A </li><li>entre el 6% y el 10% la calificación es a B </li><li>entre el 11% y el 20% la calificación es C </li><li>entre el 21 y el 50 % la calificación es D</li><li>cualquier valor superior al 50% es una E</li></ul> | Importante | &lt; A |
| Cobertura | Una combinación de cobertura de línea de prueba unitaria y cobertura de condición utilizando esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>donde: CT = condiciones que se han evaluado como &#39;true&#39; al menos una vez al ejecutar pruebas unitarias <br/>CF = condiciones que se han evaluado como &#39;false&#39; al menos una vez al ejecutar pruebas unitarias <br/>LC = líneas cubiertas = líneas_to_cover - uncovered_lines <br/><br/> B = número total de condiciones <br/>EL = número total de líneas ejecutables (lines_to_cover) | Importante | &lt; 50% |
| Pruebas unitarias omitidas | Número de pruebas unitarias omitidas. | Información | > 1 |
| Problemas abiertos | Tipos de problemas generales: Vulnerabilidades, errores y huecos de código | Información | > 0 |
| Líneas duplicadas | Número de líneas involucradas en bloques duplicados. <br/>Para que un bloque de código se considere duplicado: <br/><ul><li>**Proyectos que no son de Java:**</li><li>Debe haber al menos 100 tokens sucesivos y duplicados.</li><li>Estos tokens deben propagarse al menos en: </li><li>30 líneas de código para COBOL </li><li>20 líneas de código para ABAP </li><li>10 líneas de código para otros idiomas</li><li>**Proyectos Java:**</li><li> Debe haber al menos 10 afirmaciones sucesivas y duplicadas, independientemente del número de tokens y líneas.</li></ul> <br/>Las diferencias en la sangría y en los literales de cadena se ignoran al detectar duplicados. | Información | > 1% |
| Compatibilidad del Cloud Service | Número de problemas de compatibilidad con Cloud Service identificados. | Información | > 0 |

>[!NOTE]
>
>Consulte [Definiciones de métricas](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obtener definiciones más detalladas.


>[!NOTE]
>
>Para obtener más información sobre las reglas de calidad de código personalizadas ejecutadas por [!UICONTROL Cloud Manager], consulte [Reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Cómo tratar con falsos positivos {#dealing-with-false-positives}

El proceso de digitalización de la calidad no es perfecto y a veces identifica incorrectamente los problemas que no son realmente problemáticos. Esto se conoce como *falso positivo*.

En estos casos, el código fuente se puede anotar con el Java estándar `@SuppressWarnings` anotación que especifica el ID de regla como atributo de anotación. Por ejemplo, un problema común es que la regla SonarQube para detectar contraseñas codificadas puede ser agresiva sobre cómo se identifica una contraseña codificada.

Para ver un ejemplo específico, este código sería bastante común en un proyecto AEM que tiene código para conectarse a algún servicio externo:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube entonces generará una vulnerabilidad Blocker. Después de revisar el código, identifique que esta no es una vulnerabilidad y pueda anotarla con el id de regla adecuado.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Sin embargo, por otro lado, si el código era realmente así:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

A continuación, la solución correcta es quitar la contraseña codificada.

>[!NOTE]
>
>Aunque es recomendable hacer que la variable `@SuppressWarnings` anotación lo más específica posible, es decir, anotar solo la declaración o el bloque específico que causa el problema; es posible realizar anotaciones a nivel de clase.

>[!NOTE]
>Aunque no hay ningún paso explícito de Prueba de seguridad, aún hay reglas de calidad de código relacionadas con la seguridad evaluadas durante el paso de calidad del código. Consulte [Información general de seguridad para AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) para obtener más información sobre la seguridad en Cloud Service.
