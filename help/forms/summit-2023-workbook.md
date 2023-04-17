---
title: Creación de formularios atractivos con componentes principales y sin encabezado
seo-title: Build Engaging Forms Using Core Components and Headless
description: Creación de formularios atractivos con componentes principales y sin encabezado
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: ht
source-wordcount: '3412'
ht-degree: 100%

---


# Creación de formularios atractivos con componentes principales y sin encabezado

## Información general del laboratorio

En este laboratorio práctico, aprenderá lo siguiente:

Cómo utilizar AEM Forms para crear fácilmente formularios adaptables utilizando los componentes principales más recientes que son coherentes con AEM Sites, habilitar experiencias de captura de datos omnicanal al enviar los formularios adaptables como formularios sin encabezado a la web, dispositivos móviles y chat. También aprenderá las prácticas recomendadas sobre el estilo, las personalizaciones y el desarrollo front-end.

## Puntos clave

* **Agilidad del negocio**: como usuario empresarial, puedo crear fácilmente experiencias de formularios para varios canales.

* **Capacidad de desarrollador front-end**: como desarrollador front-end, puedo controlar la experiencia del usuario final mediante formularios sin encabezado.

* **Velocidad de desarrollo**: como desarrollador, puedo personalizar fácilmente y de forma coherente los componentes de Sites y Forms.

## Requisitos previos


+++Zona protegida de AEM Forms as Cloud Service



<table>
        <thead>
            <tr><th>ID de laboratorio</th><th>URL de instancia de creación</th><th>URL de instancia de publicación</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lección 1

### Objetivo

Familiarícese con el entorno de AEM Forms as a Cloud Service.

### Contexto de la lección

En esta lección, puede familiarizarse con el entorno de AEM Forms as a Cloud Service navegando por la interfaz de usuario.

### Ejercicio

1. Abra el explorador e introduzca la dirección URL del entorno de creación de Cloud Service. Por ejemplo:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Inicie sesión en el entorno de creación de Cloud Service. Las credenciales de inicio de sesión para el entorno de creación se compartirán con usted durante el laboratorio.

1. Una vez que haya iniciado sesión, vaya a la IU de AEM Forms. Haga clic en **Formularios**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Haga clic en **Formularios y documentos**. Descarte cualquier elemento emergente relacionado con las preferencias o la información.

   ![](/help/forms/assets/screenshot2028113929.png)

   Se muestran todos los formularios disponibles.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lección 2

### Objetivo

Cree un formulario adaptable utilizando los componentes principales más recientes, configúrelo y envíelo.

### Contexto de la lección

En esta lección, como usuario empresarial, creará un formulario adaptable para varios canales como web, móvil y chat mediante la creación de formularios adaptables con componentes principales listos para usarse estandarizados para la captura de datos.

### Ejercicio

1. Cree un punto final de envío para el formulario:

   1. Abra <https://requestbin.com/> en una nueva pestaña del explorador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Haga clic en **Crear un grupo público** y copie la dirección URL del punto final.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Cree un formulario adaptable mediante la interfaz del asistente:

   1. En la pestaña del explorador utilizada en la Lección 1, vaya a la interfaz web de AEM Forms as Cloud Service y a Formularios y documentos.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Haga clic en **Crear** y seleccione Formulario adaptable.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleccione la plantilla **En blanco con componentes principales** de la pantalla de selección de plantillas como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Haga clic en la pestaña **Estilo** y seleccione **wknd-theme** como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Haga clic en la pestaña **Envío** y seleccione la tarjeta **Enviar al punto final de REST** y especifique el grupo público en
      el campo **URL de la petición POST** como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Haga clic en **Crear**. Especifique un nombre y título para el formulario. Por ejemplo, **contacto**. Haga clic en **Crear**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Se abre el editor de formularios adaptables. Descarte cualquier ventana emergente o diálogo para obtener preferencias o información. Haga clic en el explorador de componentes en el carril izquierdo y agregue el componente **Pie de página** al final del formulario en blanco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. El encabezado forma parte de la plantilla de formulario adaptable. Permite proporcionar un encabezado y pie de página coherente en todos los formularios adaptables. También puede optar por mantenerlo editable en el formulario, tal como se ve para el componente Pie de página en el siguiente paso.

   1. Agregue el componente **Título** en el medio del formulario.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Agregue el componente **Entrada de texto** después del componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Agregue el componente **Entrada de número**.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Agregue el componente **Botón de envío** al formulario.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Haga clic en el componente **Título** para que se muestre el **menú emergente**. Haga clic en el **icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Escriba `Contact Us` como texto del título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Haga clic en el componente **Entrada de texto** para que se muestre el menú emergente. Haga clic en el **icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Escriba el **Nombre completo** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Haga clic en el componente **Entrada de número** para que se muestre el menú emergente. Haga clic en el **icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Escriba el **Número de teléfono** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Agregue validaciones al formulario:

   1. Haga clic en el componente **Número de teléfono** para que se muestre el menú emergente. Haga clic en el componente **icono de llave inglesa** en el menú para configurar el campo.
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra la **pestaña Validaciones**, marque el campo **Requerido** y haga clic en **Listo**. Se muestra el mensaje de éxito.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Haga clic en **Vista previa** para obtener una vista previa del formulario desde la perspectiva de usuario final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Rellene el formulario con datos ficticios
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar el formulario
      ![](/help/forms/assets/screenshot2028125729.png)

   1. En la pestaña Grupo de solicitudes, compruebe los datos enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Ahora, para el resto del ejercicio, utilice un formulario de registro creado previamente.

1. Abra la interfaz de administración de AEM Forms, por ejemplo, `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`, y seleccione el formulario de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Haga clic en **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Se muestra el mensaje de éxito.

   ![](/help/forms/assets/screenshot2028115729.png)

   La URL de publicación del formulario es similar a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para ver el formulario publicado, reemplace el ID de programa (pXXXXXX) y el ID de entorno (eXXXXXX) en la URL anterior con los ID de su
entorno.

## Lección 3

### Objetivo

Actualice los estilos utilizando las prácticas recomendadas de desarrollo front-end.

### Contexto de la lección

En esta lección, como desarrollador front-end, aprenderá a actualizar fácilmente el estilo del formulario adaptable creado anteriormente.

### Ejercicio

Configure el repositorio local del tema:

1. Abra el símbolo del sistema o shell con derechos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a la carpeta **c:\git**

   ```Shell
   cd c:\git
   ```

1. Use el siguiente comando para clonar el código front-end del tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Use el siguiente comando en el orden de la lista para ir al directorio **aem-forms-theme-canvas** y abra Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Seleccione **Confiar en los autores de todos los archivos de la carpeta principal** y haga clic en **Sí, confío en los autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube, cambie el nombre del archivo `env_template`.  Para cambiar el nombre, haga clic con el botón derecho en el archivo **env_template** y seleccione la opción **Cambiar nombre**.

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Establezca los siguientes valores para las variables del archivo .env y guarde el archivo:

   * **AEM_URL**: especifique el entorno de publicación de su servicio en la nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`. 

   * **AEM_ADAPTIVE_FORM**: especifique la ruta del formulario. Por ejemplo, si la ruta del formulario es `/content/forms/af/registration`, el valor de esta variable sería `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Si recibe un mensaje pidiendo que actualice npm a través del comando `npm notice Run npm nstall -g npm@9.6.0`, ignore el mensaje.
   > * No ejecute otros comandos npm a menos que se indique en el libro de trabajo.


1. Ejecute el siguiente comando para obtener una vista previa del formulario.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una vez ejecutado el comando anterior, espere al mensaje `webpack compiled`. El formulario se muestra en la pestaña del explorador.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el explorador después de ejecutar el comando `npm run live` durante más de tres o cuatro minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Intro**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. En Visual Studio Code, abra el archivo `PROJECT\src\site\_variables.scss`. Observe que el color de `$error` es un tono de rojo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. En el explorador, envíe el formulario para ver el color rojo en el campo **Nombre**.

   ![](/help/forms/assets/screenshot2028120829.png)

1. Configure el color del **$error** en **#5736eb**, y guarde el archivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Actualice el explorador y envíe el formulario. El color del error del aviso en el campo de nombre ha cambiado como corresponde.

   ![](/help/forms/assets/screenshot2028121129.png)

1. En el símbolo del sistema, presione **CTRL+C**, escriba **Y**, y pulse la tecla **Intro** para finalizar el proceso de npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.
1. Cierre las ventanas de Visual Studio Code y del símbolo del sistema.

## Lección 4

### Objetivo

Procese el formulario en web/móvil y otras interfaces como un formulario sin encabezado.

### Contexto de la lección

En esta lección, como desarrollador de front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante el marco de trabajo de diseño del espectro de reacción.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio de reacción:

1. Abra el símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a la carpeta **c:\git**

   ```Shell
   cd c:\git
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Utilice los siguientes comandos en el orden de la lista para ir al directorio **react-starter-kit-aem-headless-forms** y abra Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Se abre la ventana de Visual Studio Code.

   ![](/help/forms/assets/screenshot2028117429.png)

Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube, haga lo siguiente:

1. Cambie el nombre del archivo env_template a .env. Para cambiar el nombre, haga clic con el botón derecho en el archivo **env_template** y seleccione la opción **Cambiar nombre**.

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo.

   * **AEM_URL**: especifique la URL del entorno de publicación del servicio en la nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com`. 

   * **AEM_FORM_PATH**: especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, `/content/forms/af/registration/`. 

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra la ventana Comandos, compruebe que se encuentra en el directorio react-starter-kit-aem-headless-forms y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   El comando anterior inicia el servidor de desarrollo local que procesa la definición del formulario recuperada de AEM de una forma sin encabezado utilizando la biblioteca de front-end del espectro de reacción.

   >[!NOTE]
   >
   > 
   > Si aparece una pantalla en blanco en el explorador después de ejecutar el comando `npm start` durante más de tres o cuatro minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Intro**.

   ![](/help/forms/assets/screenshot2028118229.png)

Comprobemos la ejecución de las reglas de esta forma sin encabezado:

1. Seleccione la opción **Marque la casilla para recibir un 5 % de descuento**. La opción posterior para solicitar tarjeta de crédito está desactivada.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desactive **Marque la casilla para recibir un 5 % de descuento** para habilitar la opción de tarjeta de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Haga cambios en el formulario del servidor como usuario empresarial y vea los cambios reflejados automáticamente en el formulario sin encabezado.

1. Abra la interfaz de administración de AEM Forms en el explorador. Por ejemplo, [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleccione el formulario de **registro** y haga clic en **Editar.** Abre el formulario en el editor de formularios adaptables.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleccione el campo **Número de teléfono** y haga clic en el **icono Editar (icono de lápiz)** en la barra de herramientas. Si no puede ver la barra de herramientas emergente, cambie al modo de edición haciendo clic en el botón **Editar** en la parte superior derecha, a la izquierda del botón **Vista previa**.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambie la etiqueta a Número de móvil. Haga clic en cualquier espacio vacío del formulario y se guardarán los cambios realizados en él.

   ![](/help/forms/assets/screenshot2028119729.png)

Publique el formulario actualizado para propagar los cambios al entorno de publicación.

1. En la pestaña de la interfaz de administración de AEM Forms, seleccione el formulario de registro y haga clic en **Cancelar la publicación**. Si no ve el botón **Cancelar la publicación**, vaya al paso 3 para publicar los cambios directamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Haga clic en **Cancelar la publicación**. Haga clic en **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Después de actualizar el explorador, seleccione el formulario de registro y haga clic en **Publicar**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Haga clic en **Publicar**. Haga clic en **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Actualice la pestaña del explorador con el formulario sin encabezado mostrado. Tenga en cuenta que la etiqueta de número de teléfono ha cambiado a Número de móvil.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra la ventana del símbolo del sistema que se utiliza para iniciar el proyecto **react-starter-kit-aem-headless-forms**, pulse **CTRL+C** y, a continuación, introduzca **Y** y pulse la tecla Intro para finalizar el proceso de npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.

1. Cierre las ventanas de Visual Studio Code y del símbolo del sistema.


## Lección 5

### Objetivo

Procesar el formulario como un formulario sin encabezado utilizando la IU de Google Material

### Contexto de la lección

En esta lección, como desarrollador de front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante la IU de Google Material.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio de la IU de Material:

1. Abra el símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a la carpeta **c:\git**:

   ```Shell
   cd c:\git
   ```

1. Ejecute los siguientes comandos en el orden indicado para crear una carpeta denominada mui y vaya a esta utilizando los siguientes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Utilice el siguiente comando en el orden de la lista para ir a la carpeta **react-starter-kit-aem-headless-forms** y abra el código en Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube, haga lo siguiente:

1. Cambie el nombre del archivo **env_template** a **.env**. Para cambiar el nombre, haga clic con el botón derecho en el archivo **env_template** y seleccione **Cambiar nombre**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo. Utilice la combinación de teclas **CTRL + S** para guardar el archivo.

   * **AEM_URL**: especifique la URL del entorno de publicación del servicio en la nube. Por ejemplo, [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Abra la ventana de comandos, asegúrese de que está en el directorio **react-starter-kit-aem-headless-forms** y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   El comando inicia un servidor de desarrollo local y procesa la definición de formulario recuperada de AEM en una forma sin encabezado mediante la biblioteca de front-end de la IU de Google Material.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el explorador después de ejecutar el comando `npm start` durante más de tres o cuatro minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Intro**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para evaluar la ejecución de la misma lógica empresarial en esta representación de formulario:

   Seleccione **Marque la casilla para recibir un 5 % de descuento**. La opción siguiente **¿Desea solicitar el formulario de tarjeta de crédito corporativa We.Finance?** se deshabilita.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lección 6

### Objetivo

Crear una apariencia alternativa del formulario sin encabezado mediante las variaciones de los componentes de la IU de Material

### Contexto de la lección

En esta lección, como desarrollador front-end, aprenderá a crear una representación alternativa de diferentes componentes mediante la IU de Material para el formulario adaptable creado anteriormente por el usuario empresarial.

### Ejercicio

Actualice la variación de los componentes en el proyecto sin encabezado. Cambiar la variante del componente de entrada de texto de la IU de material a `OutlinedInput`:

1. En Visual Code, vaya al componente de entrada de texto abriendo el archivo `index.tsx` en `src/components/textinput/index.tsx`.

1. Agregue `//` al principio de la línea de código 103. Convierte la línea en un comentario.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Agregue lo siguiente en la línea 104 para utilizar una variante diferente de componente y guardar el archivo. Utilice la combinación de teclas **CTRL + S** para guardar el archivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   Es esencial utilizar correctamente las mayúsculas y minúsculas para la variante “OutinedInput”, de lo contrario la compilación fallaría. La compilación del entorno de desarrollo local comienza automáticamente con el símbolo del sistema. Espere hasta que vea el siguiente mensaje

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Actualice el navegador, si no se actualiza automáticamente, para ver que el componente de entrada de texto utiliza una variante diferente.

   ![](/help/forms/assets/screenshot2028127729.png)


   Este cambio se produce para usuarios finales sin ningún cambio en la definición del formulario en el servidor de AEM Forms y es específico para el canal sin encabezado que se está considerando. Por ejemplo, el canal web en este laboratorio.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Cierre las ventanas de Visual Studio Code y del símbolo del sistema.

## Preguntas más frecuentes

+++ ¿Está disponible públicamente el asistente de Formularios adaptables?

Sí, está disponible con AEM Forms como Cloud Service.

+++


+++ ¿Los componentes principales están disponibles públicamente?

Sí, los componentes principales de Formularios adaptables están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado están disponibles públicamente?

Sí, los formularios sin encabezado están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado requieren una licencia independiente?

No, los formularios sin encabezado utilizan la misma métrica de valor de licencia y el mismo número de envíos de formularios.

+++

+++ ¿Los Componentes principales y los formularios sin encabezado están disponibles con AEM 6.5 Forms?

Sí, tanto los componentes principales de los formularios adaptables como los formularios sin encabezado están disponibles con el Service Pack 16 y posteriores de AEM Forms 6.5.

+++


## Pasos siguientes

Ahora que ha aprendido a crear formularios adaptables y distribuirlos en varios canales mediante formularios sin encabezado, puede intentar poner en práctica sus nuevas habilidades. Diviértase y siga creando y ofreciendo experiencias de captura de datos excepcionales a sus usuarios finales, donde estén, a mayor escala.

## Recursos

* [Introducción a los componentes principales del formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es)

* [Creación de formularios adaptables con componentes principales](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=es)

* [Actualización del estilo para el AF basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=es)

* [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es)

* [Uso del kit de inicio React sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=es)


