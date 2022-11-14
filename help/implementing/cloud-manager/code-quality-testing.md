---
title: Prueba de calidad del código
description: Descubra cómo funcionan las pruebas de calidad del código de las canalizaciones y cómo pueden mejorar la calidad de las implementaciones.
exl-id: e2981be9-fb14-451c-ad1e-97c487e6dc46
source-git-commit: d60659f443d130a195fd81cfe4773cd87df28264
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 100%

---

# Prueba de calidad del código {#code-quality-testing}

Descubra cómo funcionan las pruebas de calidad del código de las canalizaciones y cómo pueden mejorar la calidad de las implementaciones.

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_codequalitytests"
>title="Prueba de calidad del código"
>abstract="Las pruebas de calidad del código evalúan el código de la aplicación en función de un conjunto de reglas de calidad. Es el propósito principal de una canalización solo de calidad de código y se ejecuta inmediatamente después del paso de compilación en todas las canalizaciones de producción y no de producción."

## Introducción {#introduction}

Las pruebas de calidad del código evalúan el código de la aplicación en función de un conjunto de reglas de calidad. Es el propósito principal de una canalización solo de calidad de código y se ejecuta inmediatamente después del paso de compilación en todas las canalizaciones de producción y no de producción.

Consulte el documento [Configuración de la canalización de CI-CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los distintos tipos de canalizaciones.

## Reglas de calidad de código {#understanding-code-quality-rules}

Las pruebas de calidad del código analizan el código fuente para asegurarse de que cumple determinados criterios de calidad. Esto se lleva a cabo mediante una combinación de SonarQube y un examen a nivel de paquete de contenido usando OakPAL. Hay más de 100 reglas, que combinan reglas genéricas de Java y reglas específicas de AEM. Algunas de las reglas específicas de AEM se crean en función de las prácticas recomendadas de AEM Engineering y se denominan [reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

>[!NOTE]
>
>Puede descargar la lista completa de reglas [con este vínculo.](/help/implementing/cloud-manager/assets/CodeQuality-rules-latest-CS.xlsx)

### Clasificaciones en tres niveles {#three-tiered-gate}

Los problemas identificados por las pruebas de calidad del código se asignan a una de las tres categorías.

* **Crítico**: estos son problemas que causan un fallo inmediato de la canalización.

* **Importante**: estos son problemas que hacen que la canalización introduzca un estado pausado. Un administrador de implementación, un administrador de proyectos o un propietario empresarial pueden anular los problemas, en cuyo caso la canalización continúa, o pueden aceptar los problemas, en cuyo caso la canalización se detiene con un error.

* **Información**: se trata de problemas que se proporcionan exclusivamente con fines informativos y que no afectan a la ejecución de la canalización

>[!NOTE]
>
>En una canalización de solo calidad de código, no se pueden anular los errores importantes en la puerta de calidad de código, ya que el paso de prueba de calidad de código es el último paso de la canalización.

### Clasificaciones {#ratings}

Los resultados de este paso se entregan como **Clasificaciones**.

En la tabla siguiente se resumen las clasificaciones y los umbrales de fallo de cada una de las categorías críticas, importantes e informativas.

| Nombre | Definición | Categoría | Umbral de error |
|--- |--- |--- |--- |
| Clasificación de seguridad | A = Sin vulnerabilidades <br/>B = Al menos 1 vulnerabilidad menor<br/> C = Al menos 1 vulnerabilidad importante <br/>D = Al menos 1 vulnerabilidad crítica <br/>E = Al menos 1 vulnerabilidad de bloqueo | Crítico | &lt; B |
| Clasificación de fiabilidad | A = No hay errores <br/>B = Al menos 1 error menor <br/>C = Al menos 1 error mayor <br/>D = Al menos 1 error crítico <br>E = Al menos 1 error de bloqueo | Crítico | &lt; D |
| Puntuación de mantenimiento | Definido por el coste de corrección pendiente de los olores de código como un porcentaje del tiempo que ya ha pasado a la aplicación<br/><ul><li>A = &lt;=5 %</li><li>B = 6-10 %</li><li>C = 11-20 %</li><li>D = 21-50 %</li><li>E = >50 %</li></ul> | Importante | &lt; A |
| Cobertura | Definido por una combinación de cobertura de línea de prueba unitaria y cobertura de condición mediante la fórmula: <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`  <ul><li>`CT` = Condiciones que se han evaluado como `true` al menos una vez al ejecutar las pruebas unitarias</li><li>`CF` = Condiciones que se han evaluado como `false` al menos una vez al ejecutar las pruebas unitarias</li><li>`LC` = Líneas cubiertas = líneas_por_cubrir - líneas_descubiertas</li><li>`B` = número total de condiciones</li><li>`EL` = número total de líneas ejecutables (líneas_por_cubrir)</li></ul> | Importante | &lt; 50% |
| Pruebas unitarias omitidas | Número de pruebas unitarias omitidas | Información | > 1 |
| Problemas abiertos | Tipos de problemas generales: Vulnerabilidades, errores y huecos de código | Información | > 0 |
| Líneas duplicadas | Se define como el número de líneas involucradas en bloques duplicados. Un bloque de código se considera duplicado en las siguientes condiciones.<br>Proyectos que no son de Java:<ul><li>Debe haber al menos 100 tokens sucesivos y duplicados.</li><li>Estos tokens deben propagarse por lo menos: </li><li>30 líneas de código para COBOL </li><li>20 líneas de código para ABAP </li><li>10 líneas de código para otros idiomas</li></ul>Proyectos Java:<ul></li><li> Debe haber al menos 10 instrucciones sucesivas y duplicadas, independientemente del número de tokens y líneas.</li></ul>Las diferencias en la sangría y en los literales de cadena se ignoran al detectar duplicados. | Información | > 1 % |
| Compatibilidad de Cloud Service | Número de problemas de compatibilidad de servicios en la nube identificados | Información | > 0 |

>[!NOTE]
>
>Consulte [Definiciones de métricas de SonarQube](https://docs.sonarqube.org/latest/user-guide/metric-definitions/) para obtener definiciones más detalladas.

>[!NOTE]
>
>Para obtener más información sobre las reglas de calidad de código personalizadas ejecutadas por [!UICONTROL Cloud Manager], consulte el documento [Reglas de calidad de código personalizadas](/help/implementing/cloud-manager/custom-code-quality-rules.md).

## Tratar con falsos positivos {#dealing-with-false-positives}

El proceso de digitalización de la calidad no es perfecto y a veces identifica incorrectamente los problemas que no son realmente problemáticos. Esto se conoce como **falso positivo**.

En estos casos, el código fuente se puede anotar con la anotación de Java estándar `@SuppressWarnings` que especifica el ID de regla como atributo de anotación. Por ejemplo, un falso positivo común es que la regla SonarQube para detectar contraseñas codificadas puede ser agresiva sobre cómo se identifica una contraseña codificada.

El siguiente código es bastante común en un proyecto de AEM, que tiene código para conectarse a algún servicio externo.

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube generará una vulnerabilidad de bloqueo. Pero después de revisar el código, reconoce que no se trata de una vulnerabilidad y puede anotar el código con el ID de regla adecuado.

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

Sin embargo, si el código era realmente así:

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

A continuación, la solución correcta es quitar la contraseña codificada.

>[!NOTE]
>
>Aunque es recomendable hacer que la anotación `@SuppressWarnings` sea lo más específica posible, es decir, anotar solo la declaración o el bloque específico que causa el problema; es posible realizar anotaciones a nivel de clase.

>[!NOTE]
>Aunque no hay ningún paso explícito de prueba de seguridad, hay reglas de calidad de código relacionadas con la seguridad evaluadas durante el paso de calidad del código. Consulte el documento [Información general de seguridad para AEM as a Cloud Service](/help/security/cloud-service-security-overview.md) para obtener más información sobre la seguridad en Cloud Service.

## Optimización del análisis de paquetes de contenido {#content-package-scanning-optimization}

Como parte del proceso de análisis de calidad, Cloud Manager realiza un análisis de los paquetes de contenido producidos por la compilación de Maven. Cloud Manager ofrece optimizaciones para acelerar este proceso, que son efectivas cuando se observan ciertas restricciones de empaquetado. Lo más significativo es la optimización realizada para proyectos que generan un paquete de contenido único, generalmente denominado paquete “todo”, que contiene otros paquetes de contenido producidos por la compilación, que se marcan como omitidos. Cuando Cloud Manager detecta este escenario, en lugar de desempaquetar el paquete “todo”, los paquetes de contenido individuales se analizan directamente y se ordenan según las dependencias. Por ejemplo, considere la siguiente salida de compilación.

* `all/myco-all-1.0.0-SNAPSHOT.zip` (content-package)
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` (skipped-content-package)
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` (skipped-content-package)

Si los únicos elementos dentro de `myco-all-1.0.0-SNAPSHOT.zip` son los dos paquetes de contenido omitidos, entonces los dos paquetes incrustados se analizarán en lugar del paquete de contenido “todo”.

Para los proyectos que producen decenas de paquetes incrustados, se ha demostrado que esta optimización ahorra más de 10 minutos por ejecución de canalización.

Se puede producir un caso especial cuando el paquete de contenido “todo” contiene una combinación de paquetes de contenido omitidos y paquetes OSGi. Por ejemplo, si `myco-all-1.0.0-SNAPSHOT.zip` contenía los dos paquetes incrustados mencionados anteriormente, así como uno o más paquetes OSGi, luego se construye un nuevo paquete de contenido mínimo con solo los paquetes OSGi. Este paquete siempre tiene el nombre `cloudmanager-synthetic-jar-package` y los paquetes contenidos se colocan en `/apps/cloudmanager-synthetic-installer/install`.

>[!NOTE]
>
>* Esta optimización no afecta a los paquetes que se implementan en AEM.
>* Debido a que la coincidencia entre los paquetes de contenido incrustado y los paquetes de contenido omitido se basa en los nombres de archivo, esta optimización no se puede realizar si varios paquetes de contenido omitidos tienen exactamente el mismo nombre de archivo o si el nombre de archivo se cambia al incrustar.

