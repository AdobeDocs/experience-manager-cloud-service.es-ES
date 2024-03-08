---
title: Información general sobre Edge Delivery Services AEM Forms
description: Los Edge Delivery Services de AEM Forms están diseñados para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 0%

---

# Edge Delivery Services de AEM Forms

Optimice la creación de formularios y aumente las tasas de finalización con los Edge Delivery Services de AEM Forms de Adobe. Este servicio potente y componible le permite crear formularios de nivel empresarial con un rendimiento excepcional y un atractivo visual. AEM La priorización de la experiencia del usuario y los objetivos de su empresa es prioridad, lo que garantiza tiempos de carga increíblemente rápidos y mayores conversiones de formularios.

Puede utilizar el servicio para lo siguiente:

* **Cree experiencias de inscripción excepcionales**: cree experiencias de inscripción que se carguen y procesen rápidamente, incluso con conexiones a Internet lentas. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a tasas de finalización de formularios más altas y tasas de conversión mejoradas.

* **Cree experiencias de inscripción con las herramientas que elija**: aumente la eficacia de la creación mediante la desvinculación de fuentes de contenido. De forma predeterminada, puede utilizar ambas **creación basada en documentos** (Microsoft SharePoint o Google Drive) y **AEM creación de** AEM (Editores de la revista). De este modo, puede trabajar con varios orígenes de contenido en el mismo formulario y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Hojas de cálculo de Google o Editor de Forms adaptable.

* **Utilice un conjunto de herramientas fácil de desarrollar:** AEM Forms utiliza HTML sin formato, CSS moderno y JavaScript convencional para crear experiencias excepcionales sin la sobrecarga habitual. Cualquier desarrollador con conocimientos básicos de HTML, CSS y JS debe poder crear sus propios componentes y no tener que aprender ningún lenguaje o módulo específico. No es necesario canalizar ni esperar, proteja su código en Github y los cambios estarán activos. Además, no es necesario realizar ninguna canalización ni esperar, proteja el código en Github y los cambios se activarán.


## Creación de una experiencia de inscripción digital

AEM Forms ofrece ambas **creación basada en documentos** (Microsoft SharePoint o Google Drive) y **AEM creación de** AEM (Editores de la revista). Puede usar el complemento [Bloque de Forms adaptable](/help/edge/docs/forms/create-forms.md) para agregar un formulario al sitio de Edge Delivery Services.


>[!BEGINTABS]

>[!TAB Creación basada en documentos]

La creación basada en documentos es una opción versátil adecuada para crear formularios simples con funcionalidades esenciales. Permite integrar varios tipos de entrada, como campos de texto, menús desplegables y botones de opción, lo que permite recopilar datos de usuario de forma eficaz. Ofrece una versión básica de las reglas para agregar un comportamiento dinámico a los formularios. Las funciones clave de la creación basada en documentos son:

* **[Componentes de campo de formulario basados en HTML5](/help/edge/docs/forms/form-components.md)**: los Edge Delivery Services de AEM Forms le permiten crear formularios interactivos y fáciles de usar utilizando componentes de formulario basados en HTML5 [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">área de texto</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, y <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elementos. Estos componentes se adaptan a diferentes tipos de recopilación de datos y se pueden personalizar fácilmente para adaptarlos a sus necesidades específicas.

* **Accesibilidad**: Se puede acceder a los campos del bloque del formulario. Cada etiqueta está vinculada con su elemento de entrada respectivo y los ID se generan automáticamente para la vinculación. Las descripciones asociadas a los campos se vinculan mediante el atributo aria-described by. Se admite la navegación mediante el teclado utilizando las teclas estándar Tab/Mayús + Tab.

* **[Estilo](/help/edge/docs/forms/style-theme-forms.md)**: cada campo de formulario tiene una estructura de HTML fija que se puede decorar fácilmente con archivos CSS o JavaScript personalizados. Los selectores para los campos de segmentación en CSS y JS se proporcionan en función del tipo y el nombre. Puede crear fácilmente nuevos selectores debido a la estructura estandarizada y al estilo del formulario.

* **Reglas básicas**: cree fácilmente una lógica que ajuste la visibilidad, validación y comportamiento del campo en función de la entrada del usuario o de condiciones predefinidas. Las reglas ofrecen una forma flexible e intuitiva de agregar inteligencia a los formularios, lo que garantiza que se adapten sin problemas en función de las entradas del usuario.

* **Validaciones**: antes del envío, el formulario se valida y los campos no válidos se marcan correctamente con mensajes de error mostrados al usuario. Los bloques de Forms adaptables son compatibles con toda la validación de formularios del HTML, admitida por los exploradores modernos, y proporcionan un mecanismo de validación adicional, como script de validación, tamaño de archivo, tipo de archivo, tamaño de archivo general y mucho más.

* **Cargas de archivos**: puede agregar funcionalidades de archivos adjuntos a los formularios. Tanto si necesita recopilar documentos, imágenes u otros archivos de los usuarios, la funcionalidad de carga de archivos le resulta muy útil. Con las opciones de gestión personalizadas disponibles, puede adaptar el proceso de carga de archivos para adaptarlo a sus necesidades específicas.

* **reCAPTCHA**: aproveche la integración perfecta de Google reCAPTCHA en sus formularios con nuestra compatibilidad predeterminada (OOTB). Proteja sus formularios contra actividades fraudulentas, correo no deseado y abusos, a la vez que mantiene una experiencia de usuario fluida e ininterrumpida. El bloque de Forms adaptable es compatible con reCaptcha V3 y reCaptcha Enterprise.

* **Enviar notificación por correo electrónico al enviar el formulario**: elimine la molestia de los seguimientos manuales y garantice una comunicación oportuna con nuestra automatización de correo electrónico integrada para los envíos de formularios. Esta solución integrada le permite notificar sin esfuerzo a las partes relevantes, incluido el envío de datos de formulario, cada vez que alguien rellene un formulario en su sitio web. No necesita configuraciones complejas ni herramientas adicionales: está listo para usar de forma predeterminada.

>[!TAB AEM Creación de]

AEM La creación de formularios desbloquea capacidades adicionales más allá de la creación basada en documentos, lo que le permite crear formularios más complejos e interactivos. AEM Además de las funciones de la creación basada en documentos, la creación de documentos de la ofrece las siguientes funciones adicionales:

* Reglas avanzadas: defina acciones basadas en lógica dentro de los formularios. Puede utilizar reglas para mostrar u ocultar condicionalmente secciones de formulario, rellenar previamente campos basados en los datos introducidos por el usuario y realizar varias validaciones para garantizar la integridad de los datos.

* Extensibilidad del lado del servidor: amplíe las funcionalidades de los formularios integrándolas con lógica del lado del servidor. Esto le permite realizar cálculos complejos, interactuar con sistemas externos y automatizar tareas específicas en función de las acciones del usuario dentro del formulario.
* AEM Optimice los flujos de trabajo y la administración de datos: aproveche la potencia de los flujos de trabajo para lo siguiente:
   * AEM Diseñe formularios fáciles de usar con editores de formularios de la.
   * Genere un &quot;documento de registro&quot; para un archivado seguro y a prueba de manipulaciones de los datos enviados.
   * Facilite la firma electrónica con Adobe Sign para disfrutar de una experiencia de firma sencilla y segura.
   * AEM Automatice los procesos empresariales a través de flujos de trabajo de, activando acciones basadas en los envíos de formularios.
   * Se integra sin esfuerzo con varias fuentes de datos, lo que permite un flujo de datos e intercambio fluidos.

>[!ENDTABS]








## Empezar a crear formularios

<div>

<style>
    .card-container {
        width: calc(33.33% - 10px);;
        margin: 5px;
        border: 1px solid #ccc;
        border-radius: 5px;
        padding: 5px;
        box-sizing: border-box;
        transition: background-color 0.3s ease; /* Adding transition effect */
    }
    .card-container:hover {
        background-color: #f0f0f0; /* Changing background color on hover */
    }
</style>

<div style="display: flex; flex-wrap: wrap; justify-content: space-between; margin: -5px;">
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md">
            <img src="/help/edge/assets/smock_devices_18_n.svg" alt="Crear un formulario con formularios terminados" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Crear un formulario con hojas de Google o Microsoft Excel</b>
        </a>
        <p>Cree formularios que se carguen y procesen rápida y automáticamente en los dispositivos móviles.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulario" alt="Uso de fragmentos de formulario en un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Enviar formulario a hoja de cálculo</b>
        </a>
        <p>Envíe formularios directamente a las hojas de cálculo de Microsoft Excel o Google.</p>
    </div>
     <div class="card-container">
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos o temáticas a un formulario de extremos" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizar una temática</b>
        </a>
        <p>Crear una imagen de marca coherente aplicando la misma temática a todos los formularios.</p>
    </div>
      <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Agregar validaciones a campos de formulario" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validaciones de campo</b>
        </a>
        <p>Reduzca los errores y la frustración comprobando que las entradas del formulario tengan el formato adecuado.</p>
    </div> 
            <div class="card-container">
        <a href="/help/edge/docs/forms/rules-forms.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Usar reglas para agregar un comportamiento dinámico a un formulario" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar reglas para agregar un comportamiento dinámico a un formulario</b>
        </a>
        <p>Reutilizar fragmentos preconfigurados en varios formularios.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traducción de un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Traducción de un formulario</b>
        </a>
        <p>Amplíe el alcance de los formularios manteniendo los costes bajo control.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/repeatable-forms.md">  
            <img src="/help/edge/assets/smock_addto_18_n.svg" alt="Adición de secciones repetibles a un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Añadir secciones repetibles</b>
        </a>
        <p>Cree y agregue sin esfuerzo secciones repetibles a un formulario.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/custom-components-forms.md"> 
            <img src="/help/edge/assets/smock_userdeveloper_18_n.svg" alt="Crear componentes de formularios personalizados con JavaScript y CSS estándar"  style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creación de componentes personalizados</b>
        </a>
        <p>Utilice JavaScript y CSS estándar para crear componentes y temáticas.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/recaptacha-forms.md">  
            <img src="/help//edge/assets/smock_keyclock_18_n.svg" alt="Uso de reCAPTCHA en un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Usar reCAPTCHA</b>
        </a>
        <p>Utilice la integración reCAPTCHA de OOTB para una sólida protección contra spam y bots.</p>
    </div>


</div>


</br>
