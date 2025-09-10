---
title: Este artículo describe varios casos de uso para el editor de reglas en un formulario adaptable basado en componentes principales.
description: Este artículo explora varios casos de uso del editor de reglas en un formulario adaptable basado en componentes principales. También se resalta cómo se pueden utilizar las funciones personalizadas para crear reglas adaptadas para los formularios.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 062ed441-6e1f-4279-9542-7c0fedc9b200
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 0%

---

# Mejoras y casos de uso del Editor de reglas

<span class="preview">: estas son funciones previas al lanzamiento disponibles a través de nuestro <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=es#new-features">canal previo al lanzamiento</a>. Estas mejoras también se aplican a Edge Delivery Services Forms.

Este artículo presenta las últimas mejoras del editor de reglas en Forms adaptable. Estas actualizaciones están diseñadas para ayudarle a definir el comportamiento del formulario con mayor facilidad, sin necesidad de escribir código personalizado, y para crear experiencias de formulario más dinámicas, adaptables y personalizadas.

En la tabla siguiente se enumeran las mejoras recientes del editor de reglas en Forms adaptable, junto con una breve descripción y las ventajas clave de cada función:

| Mejora | Descripción | Ventajas |
|---|----|---|
| **Validación mediante el método `validate()`** | Disponible en la lista de funciones para validar campos individuales, paneles o todo el formulario. | - Validación granular en el nivel de panel, campo o formulario <br> - Mejor experiencia del usuario con mensajes de error de destino <br> - Evita la progresión con datos incompletos <br> - Reduce los errores de envío del formulario |
| **Descargar documento de registro** | Función predeterminada disponible en el editor de reglas para descargar el documento de registro (DoR). | - No se requiere desarrollo personalizado para descargar el documento de registro <br> - Experiencia de descarga coherente en todos los formularios |
| **Variables dinámicas** | Cree reglas utilizando variables que cambien según los datos introducidos por el usuario u otras condiciones. | - Habilita condiciones de regla flexibles <br> - Reduce la necesidad de lógica duplicada <br> - Elimina el requisito de crear campos ocultos |
| **Reglas personalizadas basadas en eventos** | Defina reglas que respondan a eventos personalizados más allá de los déclencheur estándar. | - Admite casos de uso avanzados <br> - Mayor control sobre cuándo y cómo se ejecutan las reglas <br> - Mejora la interactividad |
| **Ejecución repetible de panel según el contexto** | Las reglas ahora se ejecutan en el contexto correcto para cada panel repetido, en lugar de solo la última instancia. | - Aplicación precisa de reglas para cada instancia repetida <br> - Reduce los errores en las secciones dinámicas <br> - Mejora la experiencia del usuario con el contenido repetido |
| **Compatibilidad con parámetros de cadena de consulta, UTM y explorador** | Cree reglas que adapten el comportamiento del formulario en función de parámetros de URL o valores específicos del explorador. | - Habilita la personalización basada en el origen o el entorno <br> - Útil para el marketing o los flujos específicos de seguimiento <br> - No es necesario realizar scripts ni personalizaciones adicionales |

>[!NOTE]
>
> Las mejoras también se aplican al [Editor de reglas de Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

Ahora vamos a explorar en detalle cada método con casos de uso específicos para ayudarle a comprender cómo se pueden utilizar estas funciones para ofrecer una experiencia personalizada a los usuarios

## Método Validate en la lista de funciones

Funcionalidades de validación mejoradas que permiten utilizar el método **validate()** en la lista de funciones para validar paneles, campos o formularios completos. Por ejemplo, en un formulario de solicitud de préstamo de varios pasos, debe validar diferentes secciones antes de permitir a los usuarios continuar con el siguiente paso.

**Escenario:** Una institución financiera ofrece un formulario de solicitud de préstamo de varios pasos en el que los usuarios deben completar diferentes secciones, como:

* Datos personales
* Detalles de empleo
* Detalles del préstamo
* Revisar y enviar

Antes de que un usuario pase de un paso al siguiente, el formulario debe validar solo los campos de la sección actual. Por ejemplo, no se debe permitir al usuario continuar con &quot;Datos laborales&quot; a menos que todos los campos obligatorios en &quot;Datos personales&quot; estén correctamente rellenados.

**Implementación mediante validate() en el editor de reglas**

Un botón **Siguiente** en cada panel déclencheur una regla con el método **validate()**. La regla comprueba si todos los campos del panel actual son válidos. Si la validación se realiza correctamente, el formulario se desplaza al siguiente panel. Si no es así, se muestran mensajes de error que guían al usuario a corregir la entrada.

La captura de pantalla siguiente muestra la regla aplicada al botón **Siguiente**:

![Validar botón Siguiente](/help/forms/assets/validate-next.png)

En la regla anterior, el botón **Siguiente** comprueba si los campos de la sección **Datos personales** son válidos. Si los detalles no son válidos, el enfoque se mueve al campo **Nombre** en el panel **Detalles personales**.

![salida](/help/forms/assets/valid-output.png)

>[!NOTE]
>
>Puede usar el método **validate()** en formularios, fragmentos o campos individuales. Cuando se incluye un fragmento en un formulario, tanto el formulario como el fragmento aparecen como opciones en el contexto de validación. En este caso, el fragmento hace referencia a los campos que contiene, mientras que el formulario hace referencia al formulario principal en el que está incrustado el fragmento.

## Descargar documento como función OOTB en el editor de reglas

El uso de la función **DownloadDor()** predeterminada (OOTB) en el Editor de reglas permite al usuario descargar el documento de registro si el formulario está configurado para generar el documento de registro.

>[!NOTE]
>
>Si el formulario no está configurado para el documento de registro, se muestra un mensaje de error cuando se aplica la regla con la función **downloadDoR()** al botón.

**Escenario**: una agencia gubernamental proporciona un formulario de solicitud digital para emitir certificados. Después de enviar el formulario, los solicitantes a menudo necesitan una copia del formulario completado para sus registros o para compartirlo con otro departamento. Para mejorar la experiencia del usuario, la agencia quiere dar a los solicitantes la opción de descargar un documento de registro (DoR) inmediatamente después del envío o en cualquier etapa antes del envío final.

**Implementación mediante DownloadDor() en el editor de reglas**

Se agrega un botón **Descargar** al formulario mediante el Editor de reglas; se configura una regla para almacenar en déclencheur la función **DescargarPuerta()** al hacer clic en el botón.

La captura de pantalla siguiente muestra la regla aplicada al botón **Descargar**:

![Regla de botón de descarga](/help/forms/assets/download-button-rule.png)

>[!NOTE]
>
> El campo **Entrada** permite al usuario especificar el nombre de archivo para un documento descargable. Este es un parámetro opcional.

Si el formulario está configurado para la generación de DoR, esta función genera y descarga PDF instantáneamente, sin requerir ninguna función personalizada.

![Documento de registro](/help/forms/assets/download-dor-output.png)

## Compatibilidad con variables dinámicas en reglas

El editor de reglas mejorado admite la creación y el uso de variables dinámicas (temporales). Estas variables se pueden establecer y recuperar a lo largo del ciclo de vida del formulario mediante las funciones integradas **Establecer valor de variable** y **Obtener valor de variable**.
Estas variables:

* No se envían con los datos del formulario.
* Puede contener valores intermedios o calculados.
* Se puede utilizar en lógica condicional y acciones.

**Escenario**: un formulario de compra en línea permite a los usuarios seleccionar un producto, introducir una cantidad y elegir un país para el envío. El precio del producto es un valor fijo capturado a través de un campo de formulario, mientras que los gastos de envío varían dinámicamente según el país seleccionado.

Para evitar saturar el formulario con campos ocultos, la empresa decide almacenar los gastos de envío en una variable temporal y utilizarla para cálculos en tiempo real.

**Implementación mediante las funciones Establecer valor de variable y Obtener valor de variable en el Editor de reglas**

>[!VIDEO](https://video.tv.adobe.com/v/3471607/get-set-variable-final-video/?quality=12&learn=on)

Se ha configurado una regla en el fragmento **Address** mediante la función **Set Variable Value** para asignar una variable temporal denominada **extracharge**. El valor de esta variable cambia dinámicamente según el país seleccionado. Por ejemplo:

* Si el usuario selecciona Estados Unidos, **extracharge** se establece en 500.
* Para cualquier otro país, **extracharge** está establecido en 100.

![Establecer valor de variable](/help/forms/assets/setvalue.png)

Más adelante, cuando se calcule el **Costo total de envío**, se utilizará la función **Obtener valor de variable** para recuperar el valor de **extracharge**. Este valor se agrega a **Precio del producto × Cantidad del producto** para calcular el importe final a pagar al hacer clic en el botón.

![Obtener valor de variable](/help/forms/assets/getvalue.png)

El campo **Costo de envío total** se actualiza dinámicamente para reflejar tanto el costo del producto como el cargo de envío a medida que el usuario cambia el país o la cantidad.
![salida](/help/forms/assets/getsetvalue-output.png)

>[!NOTE]
>
> También puede agregar la función **Obtener valor de variable** en la condición When.
> > ![Obtener función de valor de variable en la condición When](/help/forms/assets/when-get-variable.png){width=50%,height=50%, align=center}

Este método permite realizar cálculos dinámicos en tiempo real sin agregar campos adicionales al formulario, lo que mantiene la estructura limpia y fácil de usar.

## Compatibilidad con reglas basadas en eventos personalizados

El editor de reglas mejorado admite la administración de eventos personalizados mediante las funciones **Evento de envío** y **Evento de Déclencheur**. Estas funciones permiten que diferentes partes del formulario se comuniquen emitiendo y escuchando eventos personalizados, lo que permite una lógica modular más limpia sin acoplar estrechamente las acciones a campos específicos.

**Escenario**: se ha creado un formulario de inicio de sesión con un fragmento de inicio de sesión reutilizable que contiene los campos **Introducir nombre de usuario** y **Introducir contraseña**. Cuando un usuario proporciona credenciales válidas, el formulario valida la entrada e inicia el proceso **Obtener OTP**. Una vez que el usuario introduce un OTP válido, se le redirige a la página adecuada.

En lugar de enlazar la lógica directamente a los campos, el formulario usa un método basado en eventos con **Evento de envío** y **Evento de Déclencheur** para mejorar la modularidad y la capacidad de mantenimiento.

**Implementación mediante evento de envío y evento de Déclencheur**


>[!VIDEO](https://video.tv.adobe.com/v/3471610/dispatch-trigger-final/?quality=12&learn=on)

El fragmento de inicio de sesión se agrega al formulario, que contiene campos predefinidos para Nombre de usuario y Contraseña. Se ha configurado una regla en el botón **Obtener OTP** para mostrar el **Panel de validación**, que incluye el campo de entrada para introducir y validar el OTP.

![Obtener regla OTP](/help/forms/assets/get-otp-rule.png)

En el **Panel de validación**, hay una regla configurada en el botón Validar. La integración de API se usa para validar el OTP introducido en el campo **Introducir OTP**. Si la validación es correcta, se activará un **evento de envío** denominado **LoggedIn** con la carga útil de evento que contiene la respuesta de API.

![En regla de evento de déclencheur](/help/forms/assets/trigger-event-rule.png)

A nivel de formulario, hay una regla configurada para escuchar el evento **LoggedIn**. Cuando se activa este evento, la regla muestra el mensaje de redirección y lleva al usuario a la página del panel.

![regla de evento de envío](/help/forms/assets/dispatch-event-rule.png)

Cuando el usuario envía el formulario con las credenciales correctas y una OTP válida, el inicio de sesión se realiza correctamente y se redirige al usuario a su panel.

Compatibilidad con eventos personalizados que permite a los desarrolladores crear y almacenar en déclencheur eventos personalizados que pueden utilizarse como condiciones en el editor de reglas.

## Ejecución de reglas basadas en el contexto para paneles repetibles

Los Forms adaptables admiten la ejecución de reglas según el contexto para paneles repetibles. Esto permite que las reglas se apliquen específicamente a la instancia del panel en la que interactúa el usuario, en lugar de afectar a todas las instancias o de establecer el valor predeterminado en la última.

**Escenario**: un formulario de pedido de productos permite a los usuarios agregar varios productos en paneles independientes. Cada panel incluye un campo **Número de productos** y un campo **Costo total**. Cuando un usuario actualiza la cantidad de un producto, el formulario debe volver a calcular el precio total, pero solo para ese panel específico, no para todos los demás.

**Implementación mediante reglas según el contexto en el editor de reglas**

Se ha configurado una regla en el campo **Número de productos** dentro del panel de productos repetibles.

La siguiente captura de pantalla muestra la regla para el campo **Número de productos** dentro del panel de productos repetible:

![número de regla de producto](/help/forms/assets/number-of-product-rule.png)

Cuando se cambia la cantidad, la regla recupera el precio unitario del producto seleccionado y calcula el coste total solo para ese panel.

![Salida de regla según el contexto](/help/forms/assets/context-aware-rule-output.png)

## Reglas basadas en parámetros de explorador y URL en Forms adaptable

Los Forms adaptables admiten la ejecución dinámica de reglas utilizando parámetros externos pasados a través de la dirección URL del formulario o derivados del entorno del explorador del usuario. Esto permite experiencias de formulario personalizadas y según el contexto en función del lugar de donde procede el visitante o del dispositivo que esté utilizando.

## Tipos de parámetros permitidos

| Tipo de parámetro | Opciones compatibles | Descripción | Valor de ejemplo |
| --- | --- | --- | ---|
| Parámetro de consulta | `ref` (solo valores de cadena) | Par de clave-valor genérico en la dirección URL después de `?` | `?ref=partner123` |
| Parámetro UTM | Contenido de UTM Source<br>UTM Medium<br>UTM Campaign<br>UTM Term<br>UTM | Parámetros de consulta especiales utilizados para el seguimiento de campañas | `?utm_source=google&utm_medium=email` |
| Parámetro de URL | Nombre de host<br>Ruta | Extrae los componentes estructurales de la URL del formulario | `hostname=www.example.com`, `path=/signup` |
| Parámetro de explorador | Agente del explorador<br>Idioma del explorador<br>Plataforma del explorador | Valores derivados del explorador o dispositivo del usuario | `Browser Agent=Mozilla`, `Language=en-US` |

**Escenario**: un formulario de generación de posibles clientes debe adaptar su mensaje de bienvenida en función del origen de tráfico. Cuando un usuario aterriza en el formulario a través de una campaña de publicidad de Google (con utm_source=google en la dirección URL), el formulario debe mostrar un saludo personalizado.

**Implementación mediante el parámetro UTM**

Se ha configurado una regla en un campo de texto que muestra un mensaje personalizado a los usuarios de Google y que usa el parámetro **utm_source**.

La siguiente captura de pantalla muestra la regla configurada en el mensaje de texto:

![regla en mensaje de texto](/help/forms/assets/utm-param-rule.png)

Si el valor del parámetro **utm_source** es igual a &quot;google&quot;, se mostrará un mensaje personalizado como &quot;Hola usuarios de Google, bienvenidos al anuncio de Campaign&quot;. se muestra.

![utm-param-output](/help/forms/assets/utm-param-output.png)

Esto permite a los especialistas en marketing enviar contenido relevante a los usuarios en función de la campaña que los llevó al formulario sin requerir la entrada manual del campo ni scripts personalizados.

Estas mejoras amplían considerablemente las capacidades del editor de reglas de Forms adaptable, lo que proporciona a los desarrolladores potentes herramientas para crear formularios más dinámicos, interactivos e inteligentes. Cada mejora aborda las necesidades comerciales específicas, a la vez que mantiene la facilidad de uso que hace que el Editor de reglas sea accesible tanto para los usuarios técnicos como para los no técnicos.

## Recursos adicionales

{{see-also-rule-editor}}
