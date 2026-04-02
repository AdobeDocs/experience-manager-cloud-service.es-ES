---
title: Prueba de conectividad de red
description: Use la Prueba de conectividad de red en Cloud Manager para validar la configuración avanzada de red y VPN desde la ruta de salida del programa antes de habilitar la red en entornos.
feature: Security
role: Admin
source-git-commit: b29b3a980a0bc1c619fb23c52acda79fae9bf945
workflow-type: tm+mt
source-wordcount: '2047'
ht-degree: 2%

---


# Prueba de conectividad de red {#network-connectivity-test}

La **Prueba de conectividad de red** es una herramienta de diagnóstico de Cloud Manager que le permite validar la configuración avanzada de redes y VPN antes de habilitar la conexión avanzada en sus entornos y antes de que se ponga en marcha. Utilícelo para comprobar que los hosts y puertos a los que debe llegar AEM, incluidos los extremos internos o privados, son accesibles a través de la misma ruta de conectividad que utilizará Advanced Networking.

La prueba se ejecuta desde la **infraestructura de proxy de salida** que pertenece a la configuración de redes avanzadas del programa, no desde un pod de autor o publicación. Utiliza la misma ruta de red saliente que utiliza AEM cuando la Red avanzada está activa. Ese diseño es especialmente útil para los escenarios de **VPN**: puede confirmar la resolución de DNS, el enrutamiento de red, las reglas del firewall y la disponibilidad del servicio para sistemas privados o locales antes de que se ponga en marcha.

Para obtener información general sobre el aprovisionamiento de VPN, IP de salida dedicada o salida de puerto flexible, consulte [Configuración de redes avanzadas para AEM as a Cloud Service](/help/security/configuring-advanced-networking.md).

>[!IMPORTANT]
>
>Una prueba de conectividad exitosa demuestra que la ruta de red de Advanced Networking puede llegar a su destino. El código de su aplicación debe seguir configurado para utilizar el proxy de redes avanzadas donde sea necesario (por ejemplo, variables de entorno relacionadas con el proxy y reenvío de puertos). Si el código omite el proxy, es posible que no vea el tráfico de la ruta de salida esperada incluso cuando la prueba se supere.

## Cuándo utilizar esta herramienta {#when-to-use}

* Después de **Advanced Networking** se crea en el nivel de **programa** y **antes de** o mientras se habilita en **entornos**.
* Para validar la conectividad de **VPN** con sistemas privados o locales que usted opera (por ejemplo, nombres de host internos o direcciones IP privadas).
* Para reducir los problemas de DNS en comparación con los problemas de firewall o enrutamiento cuando un servicio no responde según lo esperado.

>[!NOTE]
>
>Esta herramienta es para programas que utilizan redes avanzadas (VPN, IP de salida dedicada o salida de puerto flexible). No es una prueba de uso general de conectividad estándar de AEM sin redes avanzadas.

## Requisitos previos {#prerequisites}

* Un programa de Cloud Manager.
* Ya se ha creado la infraestructura de redes avanzadas para el programa (consulte [Configuración de redes avanzadas](/help/security/configuring-advanced-networking.md)).

## Cómo ejecutar una prueba {#how-to-run-a-test}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y abra su organización y programa.
1. Abra la ficha **Entornos** del programa. En la barra lateral izquierda, seleccione **Infraestructura de red**.

1. En la página **Infraestructura de red**, busque su infraestructura en la tabla. Seleccione una fila para abrir la experiencia de prueba o abra el menú de acciones de fila (![Adobe Spectrum Small More icon para el menú de acciones de fila de puntos suspensivos horizontales](assets/ellipsis.svg)) y elija **Prueba**.

   ![El área Entornos de programa de Cloud Manager con la tabla Infraestructura de red, las filas de infraestructura y el menú de acciones de fila usado para iniciar la Prueba de conectividad de red](assets/network-connectivity-test-cloud-manager-open-test-from-infrastructure-list.png)

1. Se abre el cuadro de diálogo **Prueba de red**. Escriba **Host** y **Puerto**, seleccione **Prueba** y revise la resolución de DNS, la apertura de puerto, la conectividad HTTP y la accesibilidad en el área de resultados. Las acciones opcionales como **Copiar al portapapeles** y el historial de pruebas recientes aparecen en el cuadro de diálogo. Consulte [Comprender los resultados](#understanding-results) para saber cómo interpretar cada sección.

   ![Cuadro de diálogo de prueba de conectividad de red de Cloud Manager con los campos Host y Puerto, Acción de prueba y resultados para la resolución de DNS, apertura de puerto, conectividad HTTP y accesibilidad](assets/network-connectivity-test-cloud-manager-results-dialog.png)

### Campos de entrada {#input-fields}

| Campo | Descripción | Ejemplos |
| --- | --- | --- |
| **Host** | El nombre de host o la dirección IP del servicio que AEM debe contactar. | `internal-api.example.com`, `10.0.1.50` |
| **Puerto** | Puerto TCP en el host de destino (1-65535). Los valores comunes pueden aparecer en una lista de accesos directos (por ejemplo, 80, 443, 587, 22). | `443` |

### Etapas {#test-steps}

1. Escriba **Host** y **Puerto**.
1. Seleccione **Prueba**. Los resultados suelen aparecer en unos segundos.
1. Opcional: use **Copiar al portapapeles** para capturar el resultado JSON completo (útil para casos de soporte técnico).
1. Las pruebas recientes pueden enumerarse para volver a ejecutarlas rápidamente.

## Comprender los resultados {#understanding-results}

La herramienta informa de varias dimensiones. Juntos describen si el objetivo es accesible desde la red avanzada y cómo se comportan las comprobaciones según HTTP.

### Resolución de las DNS {#dns-resolution}

| Resultado | Significado |
| --- | --- |
| `ips: ["10.0.1.50"]` | Resolución de DNS correcta. El nombre de host se resolvió en las direcciones IP enumeradas mediante los solucionadores asociados con la configuración de red avanzada. |
| `error: "DNS resolution error: ..."` | Error de resolución de DNS. Los servidores DNS configurados no pudieron resolver el nombre de host (nombre incorrecto, resolución no accesible, falta registro y causas similares). |

>[!NOTE]
>
>Si escribe una **IP numérica** en lugar de un nombre de host, se omitirá la resolución DNS para ese valor y la IP se utilizará directamente.

### Puerto abierto {#port-open}

| Resultado | Significado |
| --- | --- |
| `Yes` / true | Conexión TCP correcta: el puerto está abierto y acepta conexiones. |
| `No` / falso | El puerto está cerrado, filtrado por un cortafuegos o el host no está accesible. |

### Conexión HTTP {#http-connectivity}

Se intenta una solicitud HTTP/HTTPS en **cada puerto**. La herramienta siempre intenta **HTTPS** primero y vuelve a **HTTP**. Si ninguno de los dos funciona, el resultado se asigna a un mensaje de **error** corto y legible (consulte la tabla siguiente).

**Resultados de éxito**

| Salida | Significado |
| --- | --- |
| `protocol: "https"`, `status_code: 200`, `reason: "200 OK"` | Conexión HTTPS correcta. |
| `protocol: "http"`, `status_code: 301`, `reason: "301 Moved Permanently"` | Conexión HTTP correcta; el servicio se redirige (normalmente a HTTPS). Esto es normal. |

**Salidas de error clasificadas**

| Error | Nota | Significado |
| --- | --- | --- |
| `"Not an HTTP/HTTPS service"` | `"The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."` | El puerto está abierto, pero el servicio no habla HTTP. Esto es lo que se espera para bases de datos, SFTP, TCP personalizado y servicios similares. |
| `"Connection refused"` | `"The port is not accepting connections. Verify the service is running and listening on this port."` | Nada está escuchando en este puerto. |
| `"Connection timed out"` | `"The connection timed out. Check firewall rules and network routing."` | Un problema con el firewall o el enrutamiento impide la conexión. |
| `"No IPs resolved for host"` | — | Error de resolución de DNS; no se puede probar HTTP. |

>[!NOTE]
>
>Cualquier código de estado HTTP del servicio de destino (por ejemplo, `200`, `301`, `302`, `403`, `404` o `500`) es una **señal de éxito** para la conectividad, lo que significa que la **ruta de acceso de red** funciona. El código de estado refleja la propia respuesta del servicio, no el estado general de la red. Para los servicios que no son HTTP, la herramienta indica **No es un servicio HTTP/HTTPS**; use **Puerto abierto** y **Accesibilidad** como indicadores confiables para esos servicios.

### Accesibilidad {#reachability}

| Resultado | Significado |
| --- | --- |
| **Accesible** | Se puede acceder al host y al puerto de destino desde la infraestructura de red avanzada. La configuración de red es correcta. |
| **Inaccesible: puerto no accesible** | DNS se resolvió correctamente, pero TCP al puerto no se realizó correctamente. Suele ser un firewall o un problema de enrutamiento. |
| **Inaccesible: error de resolución de DNS** | No se ha podido resolver el nombre de host con su configuración. Esto indica un problema de configuración de DNS. |

### Varios solucionadores de DNS {#multiple-dns-resolvers}

Si su infraestructura de red avanzada define **más de una resolución DNS**:

* Cuando **todas las resoluciones devuelven resultados idénticos**, verá **un solo resultado consolidado** etiquetado como `default`.
* Cuando las resoluciones devuelven **resultados diferentes**, el resultado de cada resolución se muestra **por separado** (con la etiqueta `resolver_1`, `resolver_2`, etc.), **con la IP de resolución**, para que pueda ver qué servidor DNS está causando la incoherencia.

## Solución de problemas {#troubleshooting}

Los siguientes escenarios combinan lo que es probable que vea en la herramienta con pasos para reducir la causa. Para obtener una copia completa de **Copy al portapapeles** JSON que ilustra las mismas situaciones, consulte [Ejemplo de resultados](#example-outputs).

### Error de resolución de DNS {#dns-failed}

#### Salida

El nombre de host no se resolvió usando la configuración de DNS de red avanzada, por lo que la herramienta no puede probar el puerto. En la vista de resultados, **Resolución de DNS** muestra una cadena de error y **Accesibilidad** informa de un error de DNS:

```
DNS Resolution: error: "DNS resolution error: ..."
Reachability: "Unreachable: DNS resolution failed"
```

#### Recomendaciones

1. **Compruebe que el nombre de host es correcto**; compruebe si hay errores tipográficos y que está utilizando la **zona DNS** deseada (la zona incorrecta es un error común).
1. Asegúrese de que **sus resoluciones DNS** (las configuradas en la infraestructura de red) estén **accesibles desde el intervalo CIDR de redes avanzadas** (el mismo espacio de direcciones que la herramienta y AEM usan para las comprobaciones salientes). Si confía en DNS privados, debe poder acceder a esos servidores a través del túnel VPN o dentro del espacio de direcciones de red que expone el enrutamiento a la red avanzada.
1. **Compruebe que los servidores DNS configurados pueden resolver el nombre de host**. La red avanzada usa **solo** los solucionadores definidos en la configuración de la infraestructura de red, **no** DNS públicos (por ejemplo, `8.8.8.8`). Si el DNS interno no tiene ningún registro para ese nombre de host, la resolución falla.
1. **Para configuraciones de VPN:** Confirme que las direcciones IP del servidor DNS se encuentran en el espacio de direcciones VPN (el CIDR de red remota para el que se creó el túnel). No se puede acceder a los solucionadores de una subred que no se enrute a través del túnel VPN desde la red avanzada.

### DNS funciona pero el puerto no es accesible {#dns-ok-port-blocked}

#### Salida

La herramienta puede resolver el host, pero TCP al puerto no funciona. Un resumen suele tener este aspecto:

```
DNS Resolution: ips: ["10.0.1.50"]
Port Open: No
Reachability: "Unreachable: Port not accessible"
```

#### Recomendaciones

1. **Revise las reglas de cortafuegos y de lista de permitidos en el servicio de destino**; se debe permitir el tráfico entrante desde el intervalo CIDR de la infraestructura de red avanzada (y las direcciones IP de salida que utiliza AEM). Si utiliza una VPN, incluya los CIDR de red remota como su diseño requiere.
1. **Compruebe que el servicio se está ejecutando** y **escuchando en el host y el puerto** que ingresó en la prueba.
1. **Para configuraciones de VPN:** Confirme que el túnel está activo, el enrutamiento llega a la subred de destino y la dirección de destino se encuentra en el espacio de direcciones de red remota que se transfiere a través de la VPN.
1. En su infraestructura, revise **grupos de seguridad de red (NSG), reglas de seguridad o equivalentes** que podrían bloquear el puerto entre Advanced Networking y el destino.
1. **Confirme el número de puerto**; asegúrese de que el proceso esté escuchando en el puerto que está probando.

### La prueba muestra que es accesible, pero AEM no se conecta {#reachable-but-aem-fails}

#### Salida

La comprobación de conectividad se realiza correctamente. Un resumen conciso suele tener este aspecto:

```
Port Open: Yes
Reachability: "Reachable"
```

Ese resultado significa que la ruta desde la red avanzada hasta el host y el puerto que ha probado está abierta. No garantiza que el tráfico de la aplicación AEM esté utilizando esa ruta: cuando se ejecuta el código, es posible que los registros del servicio aún no muestren solicitudes de la IP de salida que espera.

#### Recomendaciones

1. **El código de la aplicación debe estar configurado para usar el proxy**. La prueba de conectividad demuestra que la ruta de red funciona, pero AEM debe enrutar explícitamente las solicitudes a través del **proxy de redes avanzadas** (por ejemplo, a través de la variable de entorno **`AEM_PROXY_HOST`**). Si el código realiza conexiones directas sin el proxy, el tráfico no pasa a través de la infraestructura de red avanzada.
1. **Revise la configuración de proxy en sus clientes HTTP**. Los clientes HTTP deben usar la misma configuración de proxy (`AEM_PROXY_HOST` y el reenvío de puertos cuando corresponda).
1. **Compruebe la configuración del reenvío de puertos** para la red avanzada en el nivel **entorno**: en `portForwards`, cada entrada debe asignar **`portOrig`** a **`portDest`** en el **host de destino correcto**. **`portOrig`** es el **puerto al que se conecta el código de su aplicación AEM** cuando abre la conexión saliente a través del proxy. **`portDest`** es el **puerto real en el servicio de destino** donde el proceso remoto está escuchando. El **host de destino** es el **nombre de host o dirección de ese servicio** tal como se usa en el reenvío. Los tres deben coincidir con la forma en que se escribe la aplicación para conectarse.
1. **Comprobar`nonProxyHosts`**. Si el host de destino aparece en la lista, solicita **omitir el proxy** para ese host y no seguirá la ruta de red avanzada que validó.

### HTTP muestra un error pero el puerto está abierto {#http-error-port-open}

#### Salida

TCP se ejecuta correctamente, pero el sondeo HTTP/HTTPS sigue informando de un error. Un resumen suele tener este aspecto:

```
Port Open: Yes
HTTP Connectivity: error: "Connection error: ..." or "Both HTTPS and HTTP failed. ..."
Reachability: "Reachable"
```

#### Recomendaciones

1. **Es posible que el servicio no hable HTTP o HTTPS**; por ejemplo, TCP sin procesar, gRPC u otro protocolo. El sondeo HTTP puede dar error mientras `Port open: Yes` y `Reachability: Reachable` sigan confirmando que la ruta de acceso de red funciona. Utilice esos campos como fuente fiable para servicios que no sean HTTP.
1. **Investigue TLS y la configuración del certificado**. Si HTTPS falla pero HTTP tiene éxito (a veces indicado por una nota como `HTTPS failed, HTTP succeeded`), el servicio puede tener problemas de certificado o solo puede ofrecer HTTP en ese puerto.

### Tiempo de espera de solicitud {#timeout}

#### Salida

```json
{ "error": "Request timeout" }
```

#### Recomendaciones

1. **Permitir tiempo de respuesta del servicio**: la comprobación utiliza un tiempo de espera de 5 segundos. Los objetivos que respondan más lentamente se agotarán incluso cuando, por lo demás, estén sanos.
1. **Cuenta para latencia de red**. En conexiones VPN, una latencia alta o un túnel en mal estado puede superar el límite de ida y vuelta; revise el estado y el enrutamiento del túnel.
1. **Vuelva a ejecutar la prueba**. Los problemas de red únicos pueden producir un tiempo de espera que no se repite.

## Salidas de ejemplo {#example-outputs}

### Prueba HTTPS correcta (por ejemplo, API interna en el puerto 443) {#example-output-successful-https}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "protocol": "https",
        "status_code": 200,
        "reason": "200 OK"
      },
      "reachability": "Reachable"
    }
  ]
}
```

### Prueba de servicio no HTTP correcta (por ejemplo, base de datos en el puerto 5432) {#example-output-successful-non-http}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": true,
      "http_connectivity": {
        "error": "Not an HTTP/HTTPS service",
        "note": "The service appears to be a non-HTTP service (e.g., database, message queue, or custom TCP). Use the port_open and reachability fields to verify connectivity."
      },
      "reachability": "Reachable"
    }
  ]
}
```

>[!NOTE]
>
>Se espera el error HTTP para los servicios que no son HTTP. **Puerto abierto: true** y **Accesibilidad: accesible** confirman que la ruta de red funciona.

### Error de resolución DNS {#example-output-dns-resolution-failure}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "error": "DNS resolution error: dial udp 10.0.0.2:53: i/o timeout"
      },
      "port_open": false,
      "http_connectivity": {
        "error": "DNS resolution failed"
      },
      "reachability": "Unreachable: DNS resolution failed"
    }
  ]
}
```

### Puerto no accesible (cortafuegos/servicio inactivo) {#example-output-port-not-accessible}

```json
{
  "resolvers": [
    {
      "name": "default",
      "dns_resolution": {
        "ips": ["10.0.1.50"]
      },
      "port_open": false,
      "http_connectivity": {
        "error": "Connection error: dial tcp 10.0.1.50:443: i/o timeout"
      },
      "reachability": "Unreachable: Port not accessible"
    }
  ]
}
```

## Notas importantes {#important-notes}

### Qué no hace esta prueba {#what-this-test-does-not-do}

* La prueba no se ejecuta desde un pod de autor o publicación de AEM. Se ejecuta desde **infraestructura de proxy de salida**. Esto valida la capa de red, no la configuración proxy de nivel de aplicación, en el código.
* No valida la configuración del proxy de la aplicación de AEM. Aunque el resultado sea `Reachable`, el código AEM debe configurarse para usar el proxy.
* No valida por sí sola la configuración del reenvío de puertos a nivel de entorno. Prueba la conectividad sin procesar desde la ruta de infraestructura.
* No envía cargas útiles personalizadas. Las pruebas HTTP emiten una solicitud `GET` básica a `/`.

### Tiempo de respuesta {#response-time}

* **Típico:** de 2 a 3 segundos.
* **Máximo:** tiempo de espera de unos cinco segundos.
* **Todas las resoluciones DNS** y las comprobaciones de conectividad se ejecutan en paralelo.

### Servicios HTTP o no HTTP {#http-vs-non-http-services}

La herramienta intenta establecer una conexión HTTP/HTTPS en cada puerto. Para los servicios no HTTP (por ejemplo, PostgreSQL en el puerto 5432, MySQL en 3306, SFTP en 22, Redis en 6379), la comprobación HTTP puede fallar con un error de conexión; esto es lo que se espera. Confíe en `Port open` y `Reachability` para confirmar la conectividad de esos servicios.

## Información relacionada {#related-information}

* [Configurar la conexión avanzada para AEM as a Cloud Service](/help/security/configuring-advanced-networking.md)
* [Tutoriales avanzados de redes en Experience League](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/networking/advanced-networking)
