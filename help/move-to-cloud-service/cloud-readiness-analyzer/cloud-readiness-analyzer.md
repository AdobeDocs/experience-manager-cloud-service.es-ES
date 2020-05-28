---
title: Evaluación de la complejidad del cambio al servicio de nube
description: Evaluación de la complejidad del cambio al servicio de nube
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Analizador de preparación para la nube {#accesing-complexity}

## Información general {#overview}

El analizador de preparación para la nube (CRA) le permite comprobar si las instancias de AEM existentes están preparadas para pasar al servicio de nube mediante la detección de patrones que:

* Usar una función de AEM 6.x que no se admite actualmente en el servicio de nube

* Violar ciertas reglas que se verán afectadas por el cambio al servicio de nube

>[!NOTE]
>El resultado de la CRA acelera la evaluación del esfuerzo de desarrollo que será necesario para pasar a Cloud Service.

## Configuración del analizador de preparación para la nube {#setting-up-cra}

El CRA se publica como un paquete que trabaja con cualquier versión de origen de AEM de XX o posterior, y que explora el paso a Cloud Service.

Está disponible en el portal de distribución de software y se puede instalar mediante el Administrador de paquetes.

### Uso del analizador de preparación para la nube {#using-cra}

>[!NOTE]
> CRA se puede ejecutar en cualquier entorno, incluidas las instancias de desarrollo local.

>[IMPORTANTE]
>Sin embargo, para aumentar la tasa de detección y evitar cualquier ralentización en las instancias críticas del negocio, se recomienda ejecutarla en entornos de ensayo lo más cercanos posible a los de producción en las áreas de aplicaciones de usuario, contenido y configuraciones

### Visualización de resultados en el analizador de preparación para la nube {#viewing-output-cra}


1. Vaya a la consola web de AEM navegando a la configuración **de la consola web de** Adobe Experience Manager mediante `https://serveraddress:serverport/system/console/configMgr`.

1. Seleccione Estado - Analizador de preparación para la nube, como se muestra en la imagen siguiente.

1. También puede realizar la vista de la salida mediante una interfaz JSON normal o basada en texto reactivo.

>[!NOTE]
> Consulte el Detector [de](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) patrones para obtener más detalles sobre estos métodos). Debe agregar esta sección una vez que CRA esté listo para su uso.

## Próximos pasos para la preparación para la nube {#the-next-steps}

Para obtener más información sobre su preparación para el servicio en la nube, Adobe debe evaluar el resultado del CRA.

Siga los pasos a continuación para enviar el archivo:

1. Vaya a la consola web de AEM y descargue el archivo xx como se muestra en la imagen siguiente.

1. Abra un ticket de DayCare para enviar el archivo a Adobe mediante:
   1. Registro de un ticket de asistencia técnica en Daycare titulado como Salida del Analizador de preparación para **la nube**
   1. Adjuntar un archivo de salida al ticket

