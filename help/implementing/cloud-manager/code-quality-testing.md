---
title: 'Prueba de calidad del código: Cloud Services'
description: 'Prueba de calidad del código: Cloud Services'
translation-type: tm+mt
source-git-commit: 25ba5798de175b71be442d909ee5c9c37dcf10d4
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---


# Prueba de calidad del código {#code-quality-testing}

La prueba de calidad del código evalúa la calidad del código de la aplicación. Es el objetivo central de una tubería de sólo calidad de código y se ejecuta inmediatamente después del paso de construcción en todos los gasoductos que no sean de producción y producción.

Consulte [Configuración de la canalización](/help/implementing/cloud-manager/configure-pipeline.md) CI-CD para obtener más información sobre los distintos tipos de canalizaciones.

## Comprender las reglas de calidad de código personalizadas {#understanding-code-quality-rules}

En la prueba de calidad del código, se analiza el código fuente para asegurarse de que cumple ciertos criterios de calidad. Actualmente, esto se implementa mediante una combinación de SonarQube y un examen a nivel de paquete de contenido con OakPAL. Existen más de 100 reglas que combinan reglas genéricas de Java y reglas específicas de AEM. Algunas de las reglas específicas de AEM se crean en base a las optimizaciones de AEM ingeniería y se denominan Reglas [de calidad de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizado.

>[!NOTE]
>Puede descargar la lista completa de reglas [aquí](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest.xlsx).

Los resultados de este paso se entregan como *Clasificación*. La siguiente tabla resume la clasificación para los criterios de prueba:

| Nombre | Definición | Categoría | Umbral de error |
|--- |--- |--- |--- |
| Clasificación de seguridad | A = 0 Vulnerabilidad <br/>B = al menos 1 vulnerabilidad<br/> menor C = al menos 1 vulnerabilidad grave <br/>D = al menos 1 vulnerabilidad crítica <br/>E = al menos 1 vulnerabilidad de bloqueador | Crítico | &lt; B |
| Clasificación de confiabilidad | A = 0 Error <br/>B = al menos 1 Error menor <br/>C = al menos 1 Error mayor <br/>D = al menos 1 Error crítico E = al menos 1 Error de bloqueo | Importante | &lt; C |
| Clasificación de mantenimiento | El costo de corrección sobresaliente de los olores de código es: <br/><ul><li>&lt;=5% del tiempo que ya ha pasado a la aplicación, la clasificación es A </li><li>entre el 6 y el 10 % la calificación es B </li><li>entre el 11 y el 20 % la calificación es una C </li><li>entre el 21 y el 50 % la calificación es una D</li><li>cualquier cosa superior al 50% es una E</li></ul> | Importante | &lt; A |
| Cobertura | Combinación de cobertura de la línea de prueba unitaria y cobertura de condición mediante esta fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <br/>donde: CT = condiciones que se han evaluado en &#39;true&#39; al menos una vez mientras se ejecutan las pruebas unitarias <br/>CF = condiciones que se han evaluado en &#39;false&#39; al menos una vez mientras se ejecutan las pruebas unitarias <br/>LC = líneas cubiertas = líneas_to_cover - líneasdescubiertas <br/><br/> B = número total de condiciones <br/>EL = número total de líneas ejecutables (lines_to_cover) | Importante | &lt; 50% |
| Pruebas unitarias omitidas | Número de pruebas unitarias omitidas. | Información | > 1 |
| Problemas abiertos | Tipos de problemas generales: Vulnerabilidades, errores y huecos de código | Información | > 0 |
| Líneas duplicadas | Número de líneas involucradas en bloques duplicados. <br/>Para que un bloque de código se considere como duplicado: <br/><ul><li>**Proyectos que no son de Java:**</li><li>Debe haber al menos 100 tokens sucesivos y duplicados.</li><li>Estos tokens deben propagarse al menos en: </li><li>30 líneas de código para COBOL </li><li>20 líneas de código para ABAP </li><li>10 líneas de código para otros idiomas</li><li>**Proyectos de Java:**</li><li> Debe haber al menos 10 declaraciones sucesivas y duplicadas, independientemente del número de tokens y líneas.</li></ul> <br/>Las diferencias en sangría y en literales de cadena se omiten al detectar duplicaciones. | Información | > 1% |
| Compatibilidad con Cloud Service | Número de problemas de compatibilidad con Cloud Service identificados. | Información | > 0 |

>[!NOTE]
>
>Consulte Definiciones [de métricas](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) para obtener definiciones más detalladas.


>[!NOTE]
>
>Para obtener más información sobre las reglas de calidad de código personalizadas ejecutadas por [!UICONTROL Cloud Manager], consulte Reglas [de calidad de código](/help/implementing/cloud-manager/custom-code-quality-rules.md)personalizado.

## Tratar con falsos positivos {#dealing-with-false-positives}

El proceso de análisis de calidad no es perfecto y a veces identifica incorrectamente problemas que no son realmente problemáticos. Esto se denomina &quot;falso positivo&quot;.

En estos casos, el código fuente se puede anotar con la anotación estándar de Java `@SuppressWarnings` que especifica el ID de la regla como el atributo de anotación. Por ejemplo, un problema común es que la regla SonarQube para detectar contraseñas codificadas puede ser agresiva sobre cómo se identifica una contraseña codificada.

Para ver un ejemplo específico, este código sería bastante común en un proyecto AEM que tiene código para conectarse a algún servicio externo:

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube generará una vulnerabilidad de bloqueador. Después de revisar el código, se identifica que no se trata de una vulnerabilidad y se puede anotar con la identificación de regla adecuada.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Sin embargo, por otro lado, si el código era en realidad esto:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

A continuación, la solución correcta es quitar la contraseña codificada.

>[!NOTE]
>
>Si bien es recomendable que la anotación sea lo más específica posible, es decir, que solo haga una anotación de la sentencia o bloque específico que causa el problema, es posible realizar anotaciones a nivel de clase. `@SuppressWarnings`

>[!NOTE]
>Aunque no hay un paso explícito de la prueba de seguridad, todavía hay reglas de calidad de código relacionadas con la seguridad evaluadas durante el paso de calidad del código. Consulte Información general [de seguridad para AEM como Cloud Service](/help/security/cloud-service-security-overview.md) para obtener más información sobre la seguridad en Cloud Service.
