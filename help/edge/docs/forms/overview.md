---
title: Información general sobre el servicio AEM Forms Edge Delivery
description: El servicio de entrega perimetral de AEM Forms está diseñado para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 78d40574e6fea8dde22414e43fd77215b9e7d2a1
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---


# Servicio de entrega perimetral de AEM Forms {#aem-forms-edge-delivery-service-overview}

El servicio de entrega perimetral de AEM Forms es un servicio maquetable ofrecido por Adobe que le permite crear y entregar formularios web de alto impacto y rendimiento rápido. Puede utilizar el servicio para lo siguiente:

* **Usuarios Captivate con formularios increíbles**: cree formularios complejos y atractivos con facilidad mediante una biblioteca de componentes creados previamente. Integre reCAPTCHA fácilmente, envíe formularios directamente al correo electrónico y permita cargas de archivos sin problemas a soluciones de almacenamiento seguro como Sharepoint, Azure Storage y Amazon S3. Incluso puede crear sus propios componentes de formularios personalizados para dar vida a su visión única.

  ![Formularios de inscripción](/help/edge/assets/enrollment-form.png)

* **Crear formularios con una puntuación de faro perfecta**: cree formularios que se carguen y procesen rápidamente, incluso con conexiones a Internet lentas. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a tasas de finalización de formularios más altas y tasas de conversión mejoradas.

  ![puntuación de faro perfecta para sus formularios](/help/edge/assets/lighthouse-forms.png)

* **Cree experiencias de inscripción digital con las herramientas que elija**: aumente la eficacia de la creación mediante la desvinculación de fuentes de contenido. De forma predeterminada, puede utilizar tanto la creación en AEM como la creación basada en documentos. De este modo, puede trabajar con varios orígenes de contenido en el mismo sitio web y utilizar las herramientas de creación que prefiera, como Microsoft Excel, Google AEM Sheets o Editores de páginas de la página de la página de la versión de la aplicación (en inglés).

  ![Herramientas de creación de formularios de entrega perimetral](/help/edge/assets/edge-delivery-forms-authoring-tools.png)

<!--
* **Measure customer impact and deliver effective forms**: Use our RUM dashboards to visualize form performance and identify areas for improvement. Experiment with different versions and continuously optimize your forms for maximum effectiveness, ensuring you capture the data you need and drive better business outcomes.

* **Use Integrated services:** Use integrated services to streamline and empowers your users with a one-stop shop for managing their digital enrollment journeys. Use e-signatures, automated workflows, document of record (DoR), and seamless data integration, simplify the entire digital enrollment process, accelerate approvals, and optimizes your business workflows. 

    
>[!NOTE]
    >
    >
    > WYSIWYG authoring capability, integrated services, and customer impact measuring features are available under early adopter program. You can write to aem-forms-early-adopter-program@adobe.com from your official email id to join the early adopter program and request access to the capability.

    -->

## Empiece con lo básico

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
        <a href="/help/edge/docs/forms/translate-forms.md">  
            <img src="/help/edge/assets/smock_abc_18_n.svg" alt="Traducción de un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Traducción de un formulario</b>
        </a>
        <p>Amplíe el alcance de los formularios manteniendo los costes bajo control.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Uso de fragmentos de formulario en un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creación de fragmentos de formulario</b>
        </a>
        <p>Reutilizar fragmentos preconfigurados en varios formularios.</p>
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









