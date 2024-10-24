---
title: Uso del transformador de contenido
description: Aprenda a transformar la estructura de contenido como preparación para la migración a AEM as a Cloud Service.
exl-id: 40516ff7-5686-42e6-bdd1-c9c6de432b09
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# Uso del transformador de contenido {#using-ct}

## Consideraciones importantes sobre el uso del transformador de contenido {#imp-considerations-ct}

En la sección siguiente se comprenden las consideraciones importantes al utilizar el transformador de contenido (CT):

* Para utilizar el transformador de contenido, primero debe ejecutar el Analizador de prácticas recomendadas en el entorno de Adobe Experience Manager AEM ().
* Aunque puede ejecutar el transformador de contenido en el entorno de producción, se recomienda ejecutar el transformador de contenido en un clon del entorno de producción. Lo que es más importante, debe asegurarse de que el BPA y la TC se ejecuten en el mismo entorno.
* Debe ser administrador en el entorno en el que desea ejecutar el transformador de contenido.
* Cualquier operación que pueda cambiar el contenido de origen ( mover/quitar/cambiar nombre ) creará de forma predeterminada un paquete de copia de seguridad de las rutas de origen en `/etc/packages/content-transformation` antes de la transformación. Aunque cada cuadro de diálogo de operación tiene una opción para deshabilitar/habilitar la creación de paquetes de copia de seguridad, se recomienda tener siempre seleccionada la opción para habilitar la creación de paquetes.
* Cada página del transformador de contenido está configurada para enumerar un máximo de 50 conclusiones, por lo que a la vez se puede transformar un máximo de 50 conclusiones. Esto se hace para proporcionar una respuesta de puntualidad en la interfaz de usuario.

## Disponibilidad {#availability-ct}

El transformador de contenido está empaquetado con la [herramienta de transferencia de contenido](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md) que se puede descargar como archivo zip desde el portal de distribución de software. AEM Puede instalar el paquete mediante el Administrador de paquetes en la instancia de origen de la.

>[!NOTE]
>El transformador de contenido está disponible con la herramienta de transferencia de contenido v2.0.20 o superior.

## Abrir el transformador de contenido {#opening-ct}

1. AEM Inicie sesión en la instancia de origen de la como administrador y vaya a la página de inicio: https://host:port/aem/start.html.
1. Vaya a Herramientas > Operaciones > Migración de contenido

   ![imagen](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > Asegúrese de haber ejecutado el informe de BPA anteriormente y compruébelo con la URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html

1. Haga clic en la tarjeta con el título **Transformador de contenido para el informe de BPA**

   ![imagen](/help/journey-migration/content-transformer/assets/ct-2.png)

   A continuación se muestra un ejemplo del aspecto que tendrá la página Información general del transformador de contenido si la creación del informe de BPA se realizó correctamente y si encontró problemas relacionados con el contenido.

   El tiempo de caducidad que queda para el informe BPA se muestra en la barra lateral. Se recomienda ejecutar el transformador de contenido con el último informe de BPA para evitar perder cualquier resultado relacionado con el contenido.

   ![imagen](/help/journey-migration/content-transformer/assets/ct-3.png)

1. Puede filtrar los problemas según `Pattern Code`, `Subtype`, `Importance` y `Source`.

   ![imagen](/help/journey-migration/content-transformer/assets/ct-4.png)

1. Puede seleccionar todos los problemas o problemas específicos y moverlos, quitarlos o cambiarles el nombre para resolverlos. También se pueden agregar rutas personalizadas usando el botón **Agregar rutas** de la esquina superior derecha.

   >[!NOTE]
   > Al utilizar la operación de mover, se recomienda mover todas las rutas a una sola carpeta (por ejemplo, en `/etc/packages/content-transformation/paths`), de modo que cuando se instalen los paquetes de copia de seguridad para devolver la instancia al estado original, se pueda eliminar la carpeta (`/etc/packages/content-transformation/paths`) mediante la operación de quitar para reducir el tamaño del repositorio.

   ![imagen](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![imagen](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > Cualquier operación que pueda cambiar el contenido de origen (`move`/`remove`/`rename`) creará de forma predeterminada un paquete de copia de seguridad de las rutas de origen en `/etc/packages/content-transformation` antes de la transformación. Aunque cada cuadro de diálogo de operación tiene una opción para deshabilitar/habilitar la creación de paquetes de copia de seguridad, se recomienda tener siempre seleccionada la opción para habilitar la creación de paquetes.

1. A continuación, se muestra un ejemplo de un paquete de copia de seguridad creado para la operación de movimiento de las rutas, haga clic en Instalar para recuperar las rutas de origen. La instalación solo devuelve las rutas de origen a su ubicación original y no elimina las rutas a las que se movieron durante la transformación. Para eliminar las rutas de acceso en la ubicación desplazada, haga clic en el botón **Agregar rutas** para agregar la ubicación (por ejemplo, `/etc/packages/content-transformation/paths`), seleccione la ubicación y haga clic en **Quitar**.

   >[!CAUTION]
   > No elimine `/etc/packages/content-transformation`, ya que es la ubicación donde residen los paquetes de copia de seguridad. Solo cuando esté seguro de que ya no necesita estos paquetes, puede eliminar esta ubicación para reducir el tamaño del repositorio.

   ![imagen](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![imagen](/help/journey-migration/content-transformer/assets/ct-8.png)
