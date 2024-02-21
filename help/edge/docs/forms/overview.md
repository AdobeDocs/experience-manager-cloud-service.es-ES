---
title: Información general sobre el servicio AEM Forms Edge Delivery
description: El servicio de entrega perimetral de AEM Forms está diseñado para ofrecer un rendimiento máximo, lo que le permite visualizar el futuro de la recopilación de datos y la participación del usuario optimizadas.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: b94bd6cd70af541444fda1d03f502b4588fd879b
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---


# Servicio de entrega perimetral de AEM Forms {#aem-forms-edge-delivery-service-overview}

El servicio de entrega perimetral de AEM Forms es un servicio maquetable ofrecido por Adobe que le permite crear y entregar formularios web de alto impacto y rendimiento rápido. Este servicio de composición se integra a la perfección con Adobe Experience Manager AEM () para permitirle diseñar, crear e implementar formularios web de alto impacto y velocidad excepcional con un flujo de trabajo intuitivo y eficaz.

El servicio de entrega perimetral de AEM Forms le ayuda a:

* **Diseñar formularios visualmente impresionantes**: Elimine los diseños suaves y suaves y cautive a los usuarios con formas modernas y dinámicas que reflejen la identidad de su marca. Aproveche los componentes creados previamente o cree sus propios componentes personalizados para dar vida a su visión de forma rápida y sencilla.

* **Crear formularios con una puntuación de faro perfecta**: cree formularios que se carguen y procesen rápidamente, incluso con conexiones a Internet lentas. Los tiempos de carga más rápidos y la experiencia de usuario optimizada contribuyen a tasas de finalización de formularios más altas y tasas de conversión mejoradas.

* **Simplificar la creación y los envíos**: cree formularios con herramientas conocidas como Microsoft Excel o Hojas de cálculo de Google en lugar de los entornos de creación tradicionales. Envíe formularios directamente a las hojas de cálculo de Microsoft Excel o Google y utilice su ecosistema para procesar fácilmente los datos enviados.

## Introducción al servicio de entrega de AEM Forms Edge

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
            <br><b style="margin-top: 5px;">Creación de un formulario</b>
        </a>
        <p>Cree formularios que se carguen y procesen rápida y automáticamente en los dispositivos móviles.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/validate-forms.md">
            <img src="/help/edge/assets/smock_condition_18_n.svg" alt="Agregar validaciones a campos de formulario" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Aplicar validaciones de campo</b>
        </a>
        <p>Reduzca los errores y la frustración comprobando que las entradas del formulario tengan el formato adecuado.</p>
    </div>
    <div class="card-container">
        <a href="/help/edge/docs/forms/form-fragments.md">
            <img src="/help/edge/assets/smock_documentfragment_18_n.svg" alt="Uso de fragmentos de formulario en un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Creación de fragmentos de formulario</b>
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
        <a href="/help/edge/docs/forms/style-theme-forms.md">
            <img src="/help/edge/assets/smock_imageautomode_18_N.svg" alt="Aplicar estilos o temáticas a un formulario de extremos" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Personalizar una temática</b>
        </a>
        <p>Crear una imagen de marca coherente aplicando la misma temática a todos los formularios.</p>
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
    <div class="card-container">
        <a href="/help/edge/docs/forms/create-forms.md#manually-configure-a-spreadsheet-to-accept-data">   
            <img src="/help/edge/assets/smock_platformdatamapping_18_n.svg" alt="Enviar formulario" alt="Uso de fragmentos de formulario en un formulario EDS" style="border-radius: 5px;"> </b>
            <br><b style="margin-top: 5px;">Enviar formulario a hoja de cálculo</b>
        </a>
        <p>Envíe formularios directamente a las hojas de cálculo de Microsoft Excel o Google.</p>
    </div>
</div>


</br>









