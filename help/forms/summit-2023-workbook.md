---
title: Crear Forms con participación mediante componentes principales y sin encabezado
seo-title: Build Engaging Forms Using Core Components and Headless
description: Crear Forms con participación mediante componentes principales y sin encabezado
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: adbeb7a0e5cfd3e0179fad09943c57ea651fc94c
workflow-type: tm+mt
source-wordcount: '3609'
ht-degree: 3%

---


# Crear Forms con participación mediante componentes principales y sin encabezado

## Información general de Lab

En este laboratorio práctico, aprendes:

Cómo utilizar AEM Forms para crear fácilmente formularios adaptables utilizando los componentes principales más recientes que son coherentes con AEM Sites, permitir experiencias de captura de datos omnicanal al enviar los formularios adaptables como formularios sin encabezado a la Web, dispositivos móviles y chat. También aprende las prácticas recomendadas sobre el estilo, las personalizaciones y el desarrollo front-end.

## Principales tomas

* **Agilidad empresarial**: Como usuario empresarial, puedo crear fácilmente experiencias de formulario para varios canales.

* **Capacidad de desarrollador de front-end**: Como desarrollador de front-end, puedo controlar la experiencia del usuario final mediante formularios sin encabezado.

* **Developer Velocity**: Como desarrollador, puedo personalizar de forma fácil y consistente los componentes de Sites y Forms.

## Requisitos previos


+++AEM Forms como simulador para pruebas de Cloud Service


<table>
        <thead>
            <tr><th>name</th><th>username</th><th>URL de instancia de autor</th><th>URL de instancia de publicación</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>L716+001@summitlab.us</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>L716+002@summitlab.us</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>L716+003@summitlab.us</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>L716+004@summitlab.us</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>L716+005@summitlab.us</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>L716+006@summitlab.us</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>L716+007@summitlab.us</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>L716+008@summitlab.us</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>L716+009@summitlab.us</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>L716+010@summitlab.us</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>L716+011@summitlab.us</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>L716+012@summitlab.us</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>L716+013@summitlab.us</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>L716+014@summitlab.us</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>L716+015@summitlab.us</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>L716+016@summitlab.us</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>L716+017@summitlab.us</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>L716+018@summitlab.us</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>L716+019@summitlab.us</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>L716+020@summitlab.us</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>L716+021@summitlab.us</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>L716+022@summitlab.us</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>L716+023@summitlab.us</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>L716+024@summitlab.us</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>L716+025@summitlab.us</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>L716+026@summitlab.us</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>L716+027@summitlab.us</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>L716+028@summitlab.us</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>L716+029@summitlab.us</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>L716+030@summitlab.us</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>L716+031@summitlab.us</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>L716+032@summitlab.us</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>L716+033@summitlab.us</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>L716+034@summitlab.us</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>L716+035@summitlab.us</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>L716+036@summitlab.us</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>L716+037@summitlab.us</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>L716+038@summitlab.us</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>L716+039@summitlab.us</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>L716+040@summitlab.us</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>L716+041@summitlab.us</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>L716+042@summitlab.us</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>L716+043@summitlab.us</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>L716+044@summitlab.us</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>L716+045@summitlab.us</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>L716+046@summitlab.us</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>L716+047@summitlab.us</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>L716+048@summitlab.us</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>L716+049@summitlab.us</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>L716+050@summitlab.us</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>L716+051@summitlab.us</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>L716+052@summitlab.us</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>L716+053@summitlab.us</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>L716+054@summitlab.us</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>L716+055@summitlab.us</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>L716+056@summitlab.us</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>L716+057@summitlab.us</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>L716+058@summitlab.us</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>L716+059@summitlab.us</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>L716+060@summitlab.us</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>L716+061@summitlab.us</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>L716+062@summitlab.us</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>L716+063@summitlab.us</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>L716+064@summitlab.us</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>L716+065@summitlab.us</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>L716+066@summitlab.us</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>L716+067@summitlab.us</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>L716+068@summitlab.us</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>L716+069@summitlab.us</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>L716+070@summitlab.us</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>L716+071@summitlab.us</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>L716+072@summitlab.us</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>L716+073@summitlab.us</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>L716+074@summitlab.us</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>L716+075@summitlab.us</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>L716+076@summitlab.us</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>L716+077@summitlab.us</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>L716+078@summitlab.us</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>L716+079@summitlab.us</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>L716+080@summitlab.us</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>L716+081@summitlab.us</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>L716+082@summitlab.us</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>L716+083@summitlab.us</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>L716+084@summitlab.us</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>L716+085@summitlab.us</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>L716+086@summitlab.us</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>L716+087@summitlab.us</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>L716+088@summitlab.us</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>L716+089@summitlab.us</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>L716+090@summitlab.us</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>L716+091@summitlab.us</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>L716+092@summitlab.us</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>L716+093@summitlab.us</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>L716+094@summitlab.us</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>L716+095@summitlab.us</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>L716+096@summitlab.us</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>L716+097@summitlab.us</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>L716+098@summitlab.us</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>L716+099@summitlab.us</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>L716+100@summitlab.us</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## Lección 1

### Objetivo

Familiarícese con el entorno as a Cloud Service de AEM Forms.

### Contexto de la lección

En esta lección, puede familiarizarse con el entorno as a Cloud Service de AEM Forms navegando por la interfaz de usuario.

### Ejercicio

1. Abra el explorador e introduzca la dirección URL del entorno de creación del Cloud Service. Por ejemplo:
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. Inicie sesión en el entorno de creación de Cloud Service según las credenciales compartidas. Por ejemplo: Nombre de usuario: [L716+001@summitlab.us](mailto:L716%2B001@summitlab.us)
Contraseña: 
**¡Adobe 123!**

1. Una vez que haya iniciado sesión, vaya a la interfaz de usuario de AEM Forms. Haga clic en **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. Haga clic en **Forms y documentos**. Descartar cualquier elemento emergente relacionado con las preferencias o la información.

   ![](/help/forms/assets/screenshot2028113929.png)

   Se muestran todos los formularios disponibles.

   ![](/help/forms/assets/screenshot2028114029.png)

## Lección 2

### Objetivo

Cree un formulario adaptable utilizando los componentes principales más recientes, configure y envíe el formulario.

### Contexto de la lección

En esta lección, como usuario empresarial, creará un formulario adaptable para varios canales como web, móvil y chat mediante la creación de formularios adaptables con componentes principales OOTB estandarizados para la captura de datos.

### Ejercicio

1. Cree un extremo de envío para el formulario:

   1. Apertura <https://requestbin.com/> en una nueva pestaña del explorador.
      ![](/help/forms/assets/screenshot2028114329.png)

   1. Haga clic en **Creación de un grupo público** y copie la dirección URL del extremo.
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. Cree un formulario adaptable mediante la interfaz del asistente:

   1. En la ficha del explorador utilizada en la lección 1, vaya a la interfaz web de AEM Forms as Cloud Service y vaya a Forms y Documentos.
      ![](/help/forms/assets/screenshot2028114029.png)

   1. Haga clic en **Crear** y seleccione Formulario adaptable.
      ![](/help/forms/assets/screenshot2028114629.png)

   1. Seleccione el **En blanco con componentes principales** plantilla de la pantalla de selección de plantillas como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. Haga clic en el **Estilo** y seleccione **wknd-theme** como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. Haga clic en el **Envío** y seleccione **Enviar al punto final de REST** y especifique el grupo público en el
      **URL de la solicitud del POST** como se muestra a continuación:
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. Haga clic en **Crear**. Especifique un nombre y un título para el formulario. Por ejemplo, **contactus**. Haga clic en **Crear**.
      ![](/help/forms/assets/screenshot2028123329.png)

   1. Se abre el editor de formularios adaptables. Descartar ventanas emergentes o diálogos para obtener preferencias o información. Haga clic en el navegador de componentes en el carril izquierdo y añada la variable **Pie de página** al final del formulario en blanco.
      ![](/help/forms/assets/screenshot2028121929.png)

   1. El encabezado forma parte de la plantilla de formulario adaptable. Permite proporcionar un encabezado y pie de página coherente en todos los formularios adaptables. También puede optar por mantenerlo editable en el formulario, tal como se ve para el componente Pie de página en el siguiente paso.

   1. Agregue un **Título** al medio del formulario.
      ![](/help/forms/assets/screenshot2028122129.png)

   1. Agregue un **Entrada de texto** componente después del componente de título.
      ![](/help/forms/assets/screenshot2028122329.png)

   1. Agregue un **Entrada de número** componente.
      ![](/help/forms/assets/screenshot2028122429.png)

   1. Agregue un **Botón de envío** al formulario.
      ![](/help/forms/assets/screenshot2028122529.png)

   1. Haga clic en el **Título** para que **menú emergente** se muestra. Haga clic en el **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122629.png)

   1. Entrar `Contact Us` como texto del título.
      ![](/help/forms/assets/screenshot2028122829.png)

   1. Haga clic en el **Entrada de texto** para que se muestre el menú emergente. Haga clic en el **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028122929.png)

   1. Entrar **Nombre completo** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123029.png)

   1. Haga clic en el **Entrada de número** para que se muestre el menú emergente. Haga clic en el **Icono Editar** en el menú para editar la etiqueta.
      ![](/help/forms/assets/screenshot2028123129.png)

   1. Introduzca la variable **Número de teléfono** como etiqueta de campo.
      ![](/help/forms/assets/screenshot2028123829.png)


1. Agregue validaciones al formulario:

   1. Haga clic en el **Número de teléfono** para que se muestre el menú emergente. Haga clic en el **Icono de llave inglesa** en el menú para configurar el campo .
      ![](/help/forms/assets/screenshot2028123429.png)

   1. Abra el **ficha validaciones**, marque el campo **Requerido** y haga clic en **Listo**. Se muestra el mensaje de éxito.
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. Haga clic en **Vista previa** para obtener una vista previa del formulario desde una perspectiva de usuario final.
      ![](/help/forms/assets/screenshot2028125529.png)

   1. Rellene el formulario con datos ficticios
      ![](/help/forms/assets/screenshot2028125629.png)

   1. Enviar el formulario
      ![](/help/forms/assets/screenshot2028125729.png)

   1. En la ficha Grupo de solicitudes , compruebe los datos enviados.
      ![](/help/forms/assets/screenshot2028125829.png)

Ahora, para el resto del ejercicio, utilice un formulario de registro creado previamente.

1. Abra la interfaz de administración de AEM Forms, por ejemplo, . `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`y seleccione el formulario de registro.

   ![](/help/forms/assets/screenshot2028115529.png)

1. Haga clic en **Publicar**.

   ![](/help/forms/assets/screenshot2028115629.png)

   Se muestra el mensaje de éxito.

   ![](/help/forms/assets/screenshot2028115729.png)

   La URL de publicación del formulario sería similar a `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. Para ver el formulario publicado, reemplace el ID de programa (pXXXXXX) y el ID de entorno (eXXXXXX) en la URL anterior con los ID de su entorno.

## Lección 3

### Objetivo

Actualice los estilos utilizando las prácticas recomendadas de desarrollo de front-end.

### Contexto de la lección

En esta lección, como desarrollador de front-end, aprenderá a actualizar fácilmente el estilo del formulario adaptable creado anteriormente.

### Ejercicio

Configure el repositorio local del tema:

1. Abra el símbolo del sistema o shell con derechos de administrador:

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta

   ```Shell
   cd c:\git
   ```

1. Utilice el siguiente comando para clonar el código de front-end del tema:

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. Utilice el siguiente comando en el orden de la lista para ir a la **aem-forms-theme-canvas** y abra Visual Studio Code.

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. Select **Confíe en los autores de todos los archivos de la carpeta principal** y haga clic en **Sí, confío en los autores**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube, cambie el nombre de la función `env_template` archivo.  Para cambiar el nombre del archivo, haga clic con el botón derecho en el **env_template** y seleccione **Cambiar nombre** .

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. Establezca los siguientes valores para las variables del archivo .env y guarde el archivo:

   * **AEM_URL**: Especifique el entorno de publicación del servicio de nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com/`. 

   * **AEM_ADAPTIVE_FORM**: Especifique la ruta del formulario. Por ejemplo, si la ruta del formulario es `/content/forms/af/registration`, el valor de esta variable sería `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * Si recibe un mensaje pidiendo que actualice npm a través de la `npm notice Run npm nstall -g npm@9.6.0`ignore el mensaje.
   > * No ejecute otros comandos npm a menos que se indique en el libro.


1. Ejecute el siguiente comando para obtener una vista previa del formulario.

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   Una vez ejecutado el comando anterior, espere a que `webpack compiled` mensaje. El formulario se muestra en una ficha del explorador.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el navegador después de ejecutar la `npm run live` durante más de 3-4 minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Entrar**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. En Visual Studio Code, abra la `PROJECT\src\site\_variables.scss` archivo. Observe que `$error` el color es una sombra de rojo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. En el explorador, envíe el formulario para ver el color rojo en la variable **Nombre** campo .

   ![](/help/forms/assets/screenshot2028120829.png)

1. Configure las variables **$error** color a **#5736eb** y guarde el archivo.

   ![](/help/forms/assets/screenshot2028120729.png)

1. Actualice el explorador y envíe el formulario. El color del error de aviso en el campo de nombre ha cambiado según corresponda.

   ![](/help/forms/assets/screenshot2028121129.png)

1. En el símbolo del sistema, presione **CTRL+C**, introduzca **Y** y pulse **Entrar** clave para finalizar el proceso npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.
1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.

## Lección 4

### Objetivo

Procese el formulario en web/móvil y otras interfaces como un formulario sin encabezado.

### Contexto de la lección

En esta lección, como desarrollador de front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante el marco de diseño del espectro de reacción.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio de Reacción:

1. Abra el símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)

1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta

   ```Shell
   cd c:\git
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. Utilice los siguientes comandos en el orden de la lista para ir a la **react-starter-kit-aem-headless-forms** y abra Visual Studio Code.

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   Se abre la ventana Código de Visual Studio.

   ![](/help/forms/assets/screenshot2028117429.png)

Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube:

1. Cambie el nombre del archivo env_template a .env . Para cambiar el nombre, haga clic con el botón derecho en el **env_template** y seleccione **Cambiar nombre** .

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo.

   * **AEM_URL**: Especifique la URL del entorno de publicación del servicio de nube. Por ejemplo, `https://publish-p105303-e986623.adobeaemcloud.com`. 

   * **AEM_FORM_PATH**: Especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, `/content/forms/af/registration/`. 

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. Abra la ventana de comandos, compruebe que se encuentra en el directorio react-starter-kit-aem-headless-forms y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   El comando anterior inicia un servidor de desarrollo local que procesaría la definición del formulario recuperada de AEM de forma automática utilizando la biblioteca de front-end del espectro de reacción.

   >[!NOTE]
   >
   > 
   > Si aparece una pantalla en blanco en el navegador después de ejecutar la `npm start` durante más de 3-4 minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Entrar**.

   ![](/help/forms/assets/screenshot2028118229.png)

Comprobemos la ejecución de las reglas de esta forma sin encabezado:

1. Seleccione el **Marque la casilla para recibir un 5 % de descuento** . Se desactiva la opción siguiente para la tarjeta de crédito.

   ![](/help/forms/assets/screenshot2028126229.png)

1. Desmarcar **Marque la casilla para recibir un 5 % de descuento** para activar la opción de tarjeta de crédito.

   ![](/help/forms/assets/screenshot2028126329.png)

Hagamos cambios en el formulario del servidor como usuario empresarial y veamos automáticamente los cambios reflejados en el formulario sin encabezado.

1. Abra la interfaz de administración de AEM Forms en el explorador. Por ejemplo, [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. Seleccione el **registro** formulario y haga clic en **Editar.** Abre el formulario en el editor de formularios adaptables.

   ![](/help/forms/assets/screenshot2028118529.png)

1. Seleccione el **Número de teléfono** y haga clic en el botón **Icono Editar (icono de lápiz)** en la barra de herramientas. Si no puede ver la barra de herramientas emergente, cambie al modo de edición haciendo clic en **Editar** en la parte superior derecha, de izquierda a derecha **Vista previa** botón.

   ![](/help/forms/assets/screenshot2028119629.png)

1. Cambie la etiqueta a Número móvil. Haga clic en cualquier espacio vacío del formulario y se guardarán los cambios realizados en él.

   ![](/help/forms/assets/screenshot2028119729.png)

Vamos a publicar el formulario actualizado para propagar los cambios al entorno de publicación.

1. En la pestaña AEM Forms management interface , seleccione el formulario de registro y haga clic en **Cancelar la publicación**. Si no ve la variable **Cancelar la publicación** , vaya al paso 3 para publicar los cambios directamente.

   ![](/help/forms/assets/screenshot2028119829.png)

1. Haga clic en **Cancelar la publicación**. Haga clic en **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. Después de actualizar el explorador, seleccione el formulario de registro y haga clic en **Publicación**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. Haga clic en **Publicar**. Haga clic en **Cerrar** en el cuadro de diálogo correspondiente.

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. Actualice la ficha del explorador con el formulario sin encabezado mostrado. Tenga en cuenta que la etiqueta de número de teléfono ha cambiado a Número de móvil.

   ![](/help/forms/assets/screenshot2028120529.png)

1. Abra la ventana del símbolo del sistema que se utiliza para iniciar el **react-starter-kit-aem-headless-forms** proyecto, pulse **CTRL+C** y, a continuación, introduzca **Y** y pulse Enter key para finalizar el proceso npm. Es importante detener el servidor npm para que no entre en conflicto con el siguiente conjunto de ejercicios.

1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.


## Lección 5

### Objetivo

Representar el formulario como un formulario sin encabezado mediante la IU de material de Google

### Contexto de la lección

En esta lección, como desarrollador de front-end, aprenderá a procesar el formulario adaptable creado anteriormente como formulario sin encabezado mediante la IU de Material de Google.

### Ejercicio

Configure el repositorio local mediante el proyecto de inicio de la interfaz de usuario de material:

1. Abra el símbolo del sistema con derechos de administrador.

   ![](/help/forms/assets/screenshot2028115829.png)


1. En el símbolo del sistema, utilice el siguiente comando para desplazarse a **c:\git** carpeta:

   ```Shell
   cd c:\git
   ```

1. Ejecute los siguientes comandos en el orden indicado para crear una carpeta denominada mui y vaya a la carpeta mui utilizando los siguientes comandos:

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. Utilice el siguiente comando para clonar el proyecto de inicio de reacción del formulario adaptable:

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. Utilice el siguiente comando en el orden de la lista para ir a la **react-starter-kit-aem-headless-forms** y abra el código en Visual Studio Code:

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

Para procesar el formulario alojado en el entorno de publicación de su servicio en la nube:

1. Cambiar el nombre de **env_template** a **.env** archivo. Para cambiar el nombre, haga clic con el botón derecho en el **env_template** y seleccione **Cambiar nombre**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. Establezca los siguientes valores para las variables del archivo .env. Después de actualizar las variables, guarde el archivo. Utilice la variable **CTRL + S** cambie a combinación para guardar el archivo.

   * **AEM_URL**: Especifique la URL del entorno de publicación del servicio de nube. Por ejemplo, [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**: Especifique la ruta del formulario adaptable creado en la lección anterior. Por ejemplo, /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. Abra la ventana de comandos, asegúrese de que está en la **react-starter-kit-aem-headless-forms** y ejecute el siguiente comando:

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. En la ventana Símbolo del sistema, ejecute el siguiente comando:

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   El comando inicia un servidor de desarrollo local y procesa la definición de formulario recuperada de AEM de forma automática mediante la biblioteca de front-end de la interfaz de usuario del material de Google.

   >[!NOTE]
   >
   >Si aparece una pantalla en blanco en el navegador después de ejecutar la `npm start` durante más de 3-4 minutos, cambie `localhost` en la dirección URL del explorador a 127.0.0.1 y pulse **Entrar**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. Para evaluar la ejecución de la misma lógica empresarial en esta representación de formulario:

   Select **Marque la casilla para recibir un 5 % de descuento**. La opción siguiente **¿Desea solicitar el formulario de tarjetas de crédito corporativas de We.Finance?** se desactiva.

   ![](/help/forms/assets/screenshot2028127329.png)

## Lección 6

### Objetivo

Crear un aspecto alternativo del formulario sin encabezado mediante las variaciones de los componentes de la IU de material

### Contexto de la lección

En esta lección, como desarrollador front-end, aprenderá a crear una representación alternativa de diferentes componentes mediante la IU de material para el formulario adaptable creado anteriormente por el usuario empresarial.

### Ejercicio

Actualice la variación de los componentes en el proyecto sin encabezado. Cambiar la variante del componente de entrada de texto de la IU de material a `OutlinedInput`:

1. En Código visual, vaya al componente de entrada de texto abriendo el `index.tsx` file at `src/components/textinput/index.tsx`.

1. Agregar `//` al principio de la línea de código 103. Convierte la línea en un comentario.

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. Añada lo siguiente en la línea 104 para utilizar una variante diferente de componente y guardar el archivo. Utilice la variable **CTRL + S** cambie a combinación para guardar el archivo.

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   Es esencial utilizar mayúsculas y minúsculas correctas para la variante &quot;OutinedInput&quot; de lo contrario la compilación fallaría. La compilación del entorno de desarrollo local comienza automáticamente en el símbolo del sistema. Espere hasta que vea el siguiente mensaje

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. Actualice el navegador, si no se actualiza automáticamente, para ver que el componente de entrada de texto utiliza una variante diferente.

   ![](/help/forms/assets/screenshot2028127729.png)


   Este cambio se produce para usuarios finales sin ningún cambio en la definición del formulario en el servidor de AEM Forms y es específico para el canal sin encabezado que se está considerando. Por ejemplo, el canal web en este laboratorio.

   ![](/help/forms/assets/screenshot2028127529.png)


1. Cierre las ventanas Código y Símbolo del sistema de Visual Studio.

## Preguntas más frecuentes

+++ ¿Está disponible públicamente el asistente de formularios adaptables?

Sí, está disponible con AEM Forms como Cloud Service.

+++


+++ ¿Los componentes principales están disponibles públicamente?

Sí, los componentes principales de Forms adaptable están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado están disponibles públicamente?

Sí, los formularios sin encabezado están disponibles con AEM Forms como Cloud Service.

+++

+++ ¿Los formularios sin encabezado requieren una licencia independiente?

No, los formularios sin encabezado utilizan la misma métrica de valor de licencia y el mismo número de envíos de formularios.

+++

+++ ¿Los componentes principales y los formularios sin encabezado están disponibles con AEM 6.5 Forms?

Sí, tanto los componentes principales de los formularios adaptables como los formularios sin encabezado están disponibles con AEM Forms 6.5 Service Pack 16 y posteriores.

+++


## Pasos siguientes

Ahora que ha aprendido a crear formularios adaptables y distribuirlos en varios canales mediante formularios sin encabezado, debe intentar poner en práctica sus nuevas habilidades. Diviértete y adelante creando y ofreciendo experiencias de captura de datos excepcionales a sus usuarios finales, donde estén, a escala!

## Recursos

* [Introducción a los componentes principales del formulario adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [Creación de formularios adaptables con componentes principales](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [Actualización del estilo para el AF basado en componentes principales](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [Formularios adaptables sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [Uso del kit de arranque React sin cabezales](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


