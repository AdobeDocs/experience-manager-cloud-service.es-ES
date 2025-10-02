---
title: Usar canalizaciones de configuración
description: Descubra cómo puede utilizar las canalizaciones de configuración para implementar diferentes configuraciones en AEM as a Cloud Service, como la configuración de reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias configuraciones de CDN.
feature: Operations
role: Admin
exl-id: bd121d31-811f-400b-b3b8-04cdee5fe8fa
source-git-commit: b0357c9fcc19d29c3d685e6b14369a6fcc6832e1
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 2%

---

# Usar canalizaciones de configuración {#config-pipelines}

Descubra cómo puede utilizar las canalizaciones de configuración para implementar diferentes configuraciones en AEM as a Cloud Service, como la configuración de reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias configuraciones de CDN.

## Información general {#overview}

Una canalización de configuración de Cloud Manager implementa archivos de configuración (creados en formato YAML) en un entorno de destino. Se pueden configurar varias funciones de AEM as a Cloud Service de esta manera, incluido el reenvío de registros, las tareas de mantenimiento relacionadas con la depuración y varias funciones de CDN.

Para los proyectos de **Publish Delivery**, las canalizaciones de configuración se pueden implementar mediante Cloud Manager en los tipos de entorno de desarrollo, ensayo y producción. Los archivos de configuración se pueden implementar en entornos de desarrollo rápido (RDE) con [herramientas de línea de comandos](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline).

Las canalizaciones de configuración también se pueden implementar a través de Cloud Manager para proyectos de **Edge Delivery**.

Las siguientes secciones de este documento proporcionan información importante sobre cómo se pueden utilizar las canalizaciones de configuración y cómo se deben estructurar las configuraciones para ellas. Describe conceptos generales compartidos en todas las funciones o en un subconjunto de ellas compatibles con las canalizaciones de configuración.

* [Configuraciones compatibles](#configurations): Una lista de configuraciones que se pueden implementar con canalizaciones de configuración.
* [Crear y administrar canalizaciones de configuración](#creating-and-managing) - Cómo crear una canalización de configuración
* [Sintaxis común](#common-syntax): sintaxis compartida entre configuraciones.
* [Estructura de carpetas](#folder-structure): Describe la estructura que esperan las canalizaciones de configuración para las configuraciones.
* [Variables de entorno secretas](#secret-env-vars): ejemplos de uso de variables de entorno para no revelar secretos en las configuraciones.
* [Variables de canalización secretas](#secret-pipeline-vars): ejemplos de uso de variables de entorno para no revelar secretos en las configuraciones de proyectos de Edge Delivery Services.

## Configuraciones compatibles {#configurations}

La siguiente tabla ofrece una lista completa de estas configuraciones con vínculos a documentación dedicada que describe su sintaxis de configuración distinta y otra información.

| Tipo | Valor YAML `kind` | Descripción | Entrega de publicación | Edge Delivery |
|---|---|---|---|---|
| [Reglas de filtro de tráfico, incluido WAF](/help/security/traffic-filter-rules-including-waf.md) | `CDN` | Declarar reglas para bloquear el tráfico malintencionado | X | X |
| [Solicitar transformaciones](/help/implementing/dispatcher/cdn-configuring-traffic.md#request-transformations) | `CDN` | Declarar reglas para transformar la forma de la solicitud de tráfico | X | X |
| [Transformaciones de respuesta](/help/implementing/dispatcher/cdn-configuring-traffic.md#response-transformations) | `CDN` | Declarar reglas para transformar la forma de la respuesta de una solicitud determinada | X | X |
| [Redirecciones del lado del servidor](/help/implementing/dispatcher/cdn-configuring-traffic.md#server-side-redirectors) | `CDN` | Declarar redirecciones del lado del servidor de estilo 301/302 | X | X |
| [Selectores de origen](/help/implementing/dispatcher/cdn-configuring-traffic.md#origin-selectors) | `CDN` | Declarar reglas para enrutar el tráfico a diferentes back-ends, incluidas las aplicaciones que no son de Adobe | X | X |
| [Páginas de error de CDN](/help/implementing/dispatcher/cdn-error-pages.md) | `CDN` | Anule la página de error predeterminada si no se puede acceder al origen de AEM, haciendo referencia a la ubicación del contenido estático autoalojado en el archivo de configuración | X |  |
| [Purga de CDN](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token) | `CDN` | Declare las claves API de depuración utilizadas para depurar la CDN | X |  |
| [Token HTTP de CDN administrado por el cliente](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#CDN-HTTP-value) | `CDN` | Declare el valor de X-AEM-Edge-Key necesario para llamar a la CDN de Adobe desde una CDN de cliente | X |  |
| [Autenticación básica](/help/implementing/dispatcher/cdn-credentials-authentication.md#purge-API-token#basic-auth) | `CDN` | Declare los nombres de usuario y contraseñas para un cuadro de diálogo de autenticación básico que proteja ciertas direcciones URL. | X | X |
| [Tarea de mantenimiento de purga de versiones](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimizar el repositorio de AEM declarando reglas sobre cuándo se deben purgar las versiones de contenido | X |  |
| [Tarea de mantenimiento de purga del registro de auditoría](/help/operations/maintenance.md#purge-tasks) | `MaintenanceTasks` | Optimice el registro de auditoría de AEM para obtener un mayor rendimiento declarando reglas sobre cuándo se deben purgar los registros | X |  |
| [Reenvío de registros](/help/implementing/developing/introduction/log-forwarding.md) | `LogForwarding` | Configure los puntos de conexión y las credenciales para reenviar registros a varios destinos, como Azure Blob Storage, Datadog, HTTPS, Elasticsearch y Splunk | X | X |
| [Registro de un ID de cliente](/help/implementing/developing/open-api-based-apis.md) | `API` | Asigne proyectos de API de Adobe Developer Console a un entorno de AEM específico mediante el registro del ID de cliente. Necesario para el uso de API basadas en OpenAPI que requieren autenticación | X |  |

## Creación y administración de canalizaciones de configuración {#creating-and-managing}

Para obtener información sobre cómo crear y configurar canalizaciones de configuración de **Publish Delivery**, consulte [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline). Al crear una canalización de configuración en Cloud Manager, asegúrese de seleccionar una **implementación dirigida** en lugar de **código de pila completa** al configurar la canalización. Como se mencionó anteriormente, la configuración para RDE se implementa usando [herramientas de línea de comandos](/help/implementing/developing/introduction/rapid-development-environments.md#deploy-config-pipeline) en lugar de una canalización.

Para obtener información sobre cómo crear y configurar canalizaciones de configuración de **Edge Delivery**, consulte el artículo [Agregar una canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

## Sintaxis común {#common-syntax}

Cada archivo de configuración comienza con propiedades similares al siguiente fragmento de ejemplo:

```yaml
   kind: "LogForwarding"
   version: "1"
   metadata:
     envTypes: ["dev"]
```

| Propiedad | Descripción | Predeterminado |
|---|---|---|
| `kind` | Una cadena que determina qué tipo de configuración, como reenvío de registros, reglas de filtro de tráfico o transformaciones de solicitud | Obligatorio, sin valor predeterminado |
| `version` | Una cadena que representa la versión del esquema | Obligatorio, sin valor predeterminado |
| `envTypes` | Esta matriz de cadenas es una propiedad secundaria del nodo `metadata`. Para **Publish Delivery**, los valores posibles son dev, stage, prod o cualquier combinación, y determina para qué tipos de entorno se procesa la configuración. Por ejemplo, si la matriz solo incluye `dev`, la configuración no se carga en entornos de ensayo o producción, aunque la configuración esté implementada allí. Para **Edge Delivery**, solo se debe usar un valor de `prod`. | Todos los tipos de entorno, que es (dev, stage, prod) para Publish Delivery o solo prod para Edge Delivery. |

Puede usar la utilidad `yq` para validar localmente el formato YAML del archivo de configuración (por ejemplo, `yq cdn.yaml`).

## Estructura de carpetas {#folder-structure}

Una carpeta con el nombre `/config` o similar debe estar en la parte superior del árbol, con uno o más archivos YAML en algún lugar del árbol debajo de ella.

Por ejemplo:

```text
/config
  cdn.yaml
```

O bien

```text
/config
  /dev
    cdn.yaml
```

Los nombres de carpeta y archivos por debajo de `/config` son arbitrarios. Sin embargo, el archivo YAML debe incluir un valor de propiedad [`kind` válido](#configurations).

Normalmente, las configuraciones se implementan en todos los entornos. Si todos los valores de propiedad son idénticos para cada entorno, es suficiente un solo archivo YAML. Sin embargo, es común que los valores de las propiedades difieran entre entornos, por ejemplo al probar un entorno más bajo.

Las secciones siguientes ilustran algunas estrategias para estructurar los archivos.

### Un solo archivo de configuración para todos los entornos {#single-file}

La estructura de archivos es similar a la siguiente:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Utilice esta estructura cuando la misma configuración sea suficiente para todos los entornos y para todos los tipos de configuración (CDN, reenvío de registros, etc.). En este escenario, la propiedad de matriz `envTypes` incluiría todos los tipos de entorno.

```yaml
   kind: "cdn"
   version: "1"
   metadata:
     envTypes: ["dev", "stage", "prod"]
```

Mediante variables de entorno (o canalización) de tipo secreto, es posible que [propiedades secretas](#secret-env-vars) varíen por entorno, como se muestra en la siguiente referencia de `${{SPLUNK_TOKEN}}`.

```yaml
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

### Un archivo independiente por tipo de entorno {#file-per-env}

La estructura de archivos es similar a la siguiente:

```text
/config
  cdn-dev.yaml
  cdn-stage.yaml
  cdn-prod.yaml
  logForwarding-dev.yaml
  logForwarding-stage.yaml
  logForwarding-prod.yaml
```

Utilice esta estructura cuando pueda haber diferencias en los valores de las propiedades. En los archivos, se esperaría que el valor de la matriz `envTypes` se correspondiera con el sufijo. Por ejemplo, `cdn-dev.yaml` y `logForwarding-dev.yaml` con un valor de `["dev"]`, `cdn-stage.yaml` y `logForwarding-stage.yaml` con un valor de `["stage"]`, etc.

### Una carpeta por entorno {#folder-per-env}

En esta estrategia, hay una carpeta `config` independiente por entorno, con una canalización independiente declarada en Cloud Manager para cada una.

Este enfoque es especialmente útil si tiene varios entornos de desarrollo, donde cada uno tiene valores de propiedad únicos.

La estructura de archivos es similar a la siguiente:

```text
/config/dev1
  cdn.yaml
  logForwarding.yaml
/config/dev2
  cdn.yaml
  logForwarding.yaml
/config/prod  
  cdn.yaml
  logForwarding.yaml
```

Una variación de este enfoque es mantener una rama separada por entorno.

### Edge Delivery Services {#yamls-for-eds}

Las canalizaciones de configuración de Edge Delivery no tienen entornos de desarrollo, ensayo y producción independientes. En los entornos de envío de publicación, los cambios progresan en los niveles de desarrollo, ensayo y producción. Por el contrario, una canalización de configuración de Edge Delivery aplica la configuración directamente a todas las asignaciones de dominio registradas en Cloud Manager para un sitio de Edge Delivery.


Por lo tanto, implemente una estructura de archivos sencilla como:

```text
/config
  cdn.yaml
  logForwarding.yaml
```

Si una regla necesita ser diferente para cada sitio de Edge Delivery, use la sintaxis *when* para distinguir las reglas entre sí. Por ejemplo, observe que el dominio coincide con dev.example.com en el siguiente fragmento de código, que se puede distinguir del dominio www.example.com.

```
kind: "CDN"
version: "1"
data:
  trafficFilters:
    rules:
    # Block simple path
    - name: block-path
      when:
        allOf:
          - reqProperty: domain
            equals: "dev.example.com"
          - reqProperty: path
            equals: '/block/me'
      action: block
```

Si se incluye el campo de metadatos *envTypes*, solo se debe utilizar el valor **prod** (omitir el campo de metadatos envTypes también es correcto). Para *tier* reqProperty, solo se debe usar el valor **publish**.

## Variables de entorno secretas {#secret-env-vars}

Para que la información confidencial no tenga que almacenarse en el control de código fuente, los archivos de configuración admiten variables de entorno Cloud Manager de tipo **secret**. En algunas configuraciones, incluido el reenvío de registros, las variables de entorno secretas son obligatorias para determinadas propiedades.

Tenga en cuenta que las variables de entorno secretas se utilizan para proyectos de Entrega de publicación; consulte la sección Variables de canalización secretas para proyectos de Edge Delivery Services.

El siguiente fragmento es un ejemplo de cómo se utiliza la variable de entorno secreta `${{SPLUNK_TOKEN}}` en la configuración.

```
kind: "LogForwarding"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  splunk:
    default:
      enabled: true
      host: "splunk-host.example.com"
      token: "${{SPLUNK_TOKEN}}"
      index: "AEMaaCS"
```

Para obtener más información sobre cómo usar variables de entorno, consulte [Variables de entorno de Cloud Manager](/help/implementing/cloud-manager/environment-variables.md).

## Variables de canalización secretas {#secret-pipeline-vars}

Para proyectos de Edge Delivery Services, use variables de canalización de Cloud Manager de tipo **secret**, de modo que no sea necesario almacenar la información confidencial en el control de código fuente. El cuadro de selección *Paso aplicado* debe utilizar la opción **implementar**.

La sintaxis es idéntica al fragmento de código mostrado en la sección anterior.

Para obtener más información sobre cómo usar variables de canalización, consulte [Variables de canalización en Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).
