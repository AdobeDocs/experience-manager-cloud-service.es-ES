---
title: Información general sobre el servicio AEM Forms Edge Delivery
description: El servicio de entrega perimetral de AEM Forms está diseñado para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: d63d0f1152d0a23623c197924a44bc6b1e69fb42
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---


# Servicio de entrega perimetral de AEM Forms

Optimice la creación de formularios y aumente las tasas de finalización con el servicio de entrega perimetral de AEM Forms de Adobe. Este potente servicio de composición le permite crear formularios de nivel empresarial con un rendimiento excepcional y un atractivo visual. AEM La priorización de la experiencia del usuario y los objetivos de su empresa es prioridad, lo que garantiza tiempos de carga increíblemente rápidos y un mayor número de finalizaciones de formularios.

Puede utilizar el servicio para lo siguiente:

* **Usuarios Captivate con formularios increíbles**: cree formularios complejos y atractivos con facilidad mediante una biblioteca de componentes creados previamente. Integre reCAPTCHA fácilmente, envíe formularios directamente al correo electrónico y permita cargas de archivos sin problemas a soluciones de almacenamiento seguro como Sharepoint, Azure Storage y Amazon S3. Incluso puede crear sus propios componentes de formularios personalizados para dar vida a su visión única.

* **Cree experiencias de inscripción digital con las herramientas que elija**: aumente la eficacia de la creación mediante la desvinculación de fuentes de contenido. De forma predeterminada, puede utilizar la creación basada en documentos (Microsoft 365 y Google AEM AEM Workspace) y la creación de (editores de listas de edición). De este modo, puede trabajar con varios orígenes de contenido en el mismo sitio web y utilizar sus herramientas de creación preferidas, como Microsoft Excel, Hojas de cálculo de Google o Editor de Forms adaptable.

* **Crear formularios con una puntuación de Lighthouse perfecta**: cree formularios que se carguen y procesen rápidamente, incluso con conexiones a Internet lentas. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a tasas de finalización de formularios más altas y tasas de conversión mejoradas.

  <div>
    <style>
    .image-container {
    text-align: center; 
    }
    .image-container img {
        width: 100%; /* Set image width to 100% of the container 
    }
</style>
    <div class="image-container">
    <img src="/help/edge/assets/eds-forms-key-features.png" alt="Características principales de EDS Forms">
    </div>


</div>

<!--

<!--

    ![Enrollment forms](/help/edge/assets/enrollment-form.png)

* **Build forms with perfect lighthouse score**: Build forms that load and render quickly, even on slow internet connections. Faster loading times and optimized user experience contribute to higher form completion rates and improved conversion rates.

    ![perfect lighthouse score for your forms](/help/edge/assets/lighthouse-forms.png)

* **Create digital enrollment experiences with tools of your choice**: Increase authoring efficiency by decoupling content sources. Out of the box you can use both AEM authoring and document-based authoring. As such, you can work with multiple content sources on the same website and use your preferred authoring tools, such as Microsoft Excel, Google Sheets, or AEM Editors.

    ![Edge Delivery forms authoring tools](/help/edge/assets/edge-delivery-forms-authoring-tools.png)
    
<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
    >[!NOTE]
    >[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Funciones principales

* **Componentes de campo de formulario basados en HTML5**: el servicio de entrega perimetral de AEM Forms le permite crear formularios interactivos y fáciles de usar utilizando componentes de formulario basados en HTML5 [tipos de entrada](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types), <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea">área de texto</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">select</a>, y <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">fieldset</a>  elementos. Estos componentes se adaptan a diferentes tipos de recopilación de datos y se pueden personalizar fácilmente para adaptarlos a sus necesidades específicas.

* **Accesibilidad**: Se puede acceder a los campos del bloque del formulario. Cada etiqueta está vinculada con su elemento de entrada respectivo y los ID se generan automáticamente para la vinculación. Las descripciones asociadas a los campos se vinculan mediante el atributo aria-described by. Se admite la navegación mediante el teclado utilizando las teclas estándar Tab/Mayús + Tab.

* **Estilo**: cada campo de formulario tiene una estructura de HTML fija que se puede decorar fácilmente con archivos CSS o JavaScript personalizados. Los selectores para los campos de segmentación en CSS y JS se proporcionan en función del tipo y el nombre. Puede crear fácilmente nuevos selectores debido a la estructura estandarizada.

* **Reglas**: cree fácilmente una lógica que ajuste la visibilidad, validación y comportamiento del campo en función de la entrada del usuario o de condiciones predefinidas. Las reglas ofrecen una forma flexible e intuitiva de agregar inteligencia a los formularios, lo que garantiza que se adapten sin problemas en función de las entradas del usuario.

* **Validaciones**: antes del envío, el formulario se valida y los campos no válidos se marcan correctamente con mensajes de error mostrados al usuario. Hay varios patrones disponibles para mostrar estos errores.

Hay algunas funciones avanzadas disponibles bajo petición:

* **Cargas de archivos**: puede agregar funcionalidades de archivos adjuntos a los formularios. Tanto si necesita recopilar documentos, imágenes u otros archivos de los usuarios, la funcionalidad de carga de archivos le resulta muy útil. Con las opciones de gestión personalizadas disponibles, puede adaptar el proceso de carga de archivos para adaptarlo a sus necesidades específicas.

* **reCAPTCHA**: aproveche la integración perfecta de Google reCAPTCHA en sus formularios con nuestra compatibilidad predeterminada (OOTB). Proteja sus formularios contra actividades fraudulentas, correo no deseado y abusos, a la vez que mantiene una experiencia de usuario fluida e ininterrumpida.

* **Enviar notificación por correo electrónico al enviar el formulario**: elimine la molestia de los seguimientos manuales y garantice una comunicación oportuna con nuestra automatización de correo electrónico integrada para los envíos de formularios. Esta solución integrada le permite notificar sin esfuerzo a las partes relevantes, incluido el envío de datos de formulario, cada vez que alguien rellene un formulario en su sitio web. No necesita configuraciones complejas ni herramientas adicionales: está listo para usar de forma predeterminada.


## Bloques de Forms disponibles

El servicio de entrega perimetral de AEM Forms ofrece dos tipos de bloques de formularios para satisfacer diferentes necesidades:

* **Bloque básico de Forms**: Esta es una opción versátil adecuada para crear formularios simples con funcionalidades esenciales. Permite integrar varios tipos de entrada, como campos de texto, menús desplegables y botones de opción, lo que permite recopilar datos de usuario de forma eficaz.

* **Bloque de Forms adaptable**: este bloque avanzado desbloquea funciones adicionales más allá del bloque básico de Forms, lo que le permite crear formularios más complejos e interactivos. A continuación se muestra un desglose de sus características principales:

   * Reglas: defina acciones basadas en lógica dentro de los formularios. Puede utilizar reglas para mostrar u ocultar condicionalmente secciones de formulario, rellenar previamente campos basados en los datos introducidos por el usuario y realizar varias validaciones para garantizar la integridad de los datos.

   * Extensibilidad del lado del servidor: amplíe las funcionalidades de los formularios integrándolas con lógica del lado del servidor. Esto le permite realizar cálculos complejos, interactuar con sistemas externos y automatizar tareas específicas en función de las acciones del usuario dentro del formulario.

   * AEM Cross Walk: Optimice los flujos de trabajo y la administración de datos: Aproveche la potencia de los flujos de trabajo para lo siguiente

      * AEM Diseñe formularios fáciles de usar con editores de formularios de la.

      * Genere un &quot;documento de registro&quot; para un archivado seguro y a prueba de manipulaciones de los datos enviados.

      * Facilite la firma electrónica con Adobe Sign para disfrutar de una experiencia de firma sencilla y segura.

      * AEM Automatice los procesos empresariales a través de flujos de trabajo de, activando acciones basadas en los envíos de formularios.

      * Se integra sin esfuerzo con varias fuentes de datos, lo que permite un flujo de datos e intercambio fluidos.

  El uso del bloque de Forms adaptable requiere una licencia adicional.

### Elegir el bloque de Forms adecuado

La selección entre los bloques Básico y Adaptable de Forms depende de sus requisitos específicos. Si necesita una solución directa para recopilar información básica del usuario, el bloque básico de Forms es la solución perfecta. AEM Sin embargo, si los formularios requieren una lógica intrincada, manipulación de datos, integración con sistemas externos o flujos de trabajo optimizados que utilicen funciones de, y **tiene la licencia necesaria**, el bloque de Forms adaptable proporciona la potencia y flexibilidad necesarias para lograr sus objetivos.


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









