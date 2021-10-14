---
title: Adición de canalizaciones de producción
description: Adición de canalizaciones de producción
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# Creación de una canalización de producción {#create-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno utilizando la interfaz de usuario de [!UICONTROL Cloud Manager], estará listo para configurar la canalización de implementación.

Siga estos pasos para configurar el comportamiento y las preferencias de la canalización:

1. Haga clic en **Configuración de canalización** para configurar la canalización.

   ![](assets/set-up-pipeline1.png)

1. Aparece la pantalla **Configuración de canalización**. Seleccione la rama y haga clic en **Next**.

   ![](assets/setup-1.png)

1. Configure las opciones de implementación.

   ![](assets/setup-pipeline.png)

   Puede definir el déclencheur para iniciar la canalización:

   * **Manual** : al utilizar la IU, se inicia manualmente la canalización.
   * **Cambios en Git** : inicia la canalización CI/CD cada vez que se agregan confirmaciones a la rama git configurada. Incluso si selecciona esta opción, siempre puede iniciar la canalización manualmente.

   Durante la configuración o edición de la canalización, el administrador de implementación tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad.

   Esto resulta útil para los clientes que desean procesos más automatizados. Las opciones disponibles son:

   * **Pregunte cada vez** : esta es la configuración predeterminada y requiere una intervención manual en cualquier error importante.
   * **Cancelar inmediatamente** : si se selecciona, la canalización se cancelará siempre que se produzca un error importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Aprobar inmediatamente** : Si se selecciona, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.


1. La configuración de la canalización de producción incluye una tercera pestaña etiquetada como **Experience Audit**. Esta opción proporciona una tabla para las rutas URL que siempre deben incluirse en la auditoría de experiencias.

   >[!NOTE]
   >Debe hacer clic en **Agregar nueva página** para definir su propio vínculo personalizado.

   ![](assets/setup-3.png)

   Haga clic en **Agregar nueva página** para proporcionar una ruta URL que se incluirá en la auditoría de experiencias.

   Por ejemplo, si desea incluir `https://wknd.site/us/en/about-us.html` en la auditoría de experiencias, introduzca la ruta `us/en/about-us.html` en este campo y haga clic en **Guardar**.

   ![](assets/exp-audit4.png)

   La dirección URL que aparece en la tabla es:

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   Se puede incluir un máximo de 25 filas. Si el usuario no envía páginas en esta sección, la página principal del sitio se incluirá en la auditoría de experiencias de forma predeterminada.

   Consulte [Explicación de los resultados de auditoría de experiencias](/help/implementing/cloud-manager/experience-audit-testing.md) para obtener más información.

   >[!NOTE]
   > Las páginas configuradas se enviarán al servicio y se evaluarán según las pruebas de rendimiento, accesibilidad, SEO (Optimización del motor de búsqueda), prácticas recomendadas y PWA (Aplicación web progresiva).

1. Haga clic en **Guardar** en la pantalla **Editar canalización**. La página **Información general** ahora muestra la tarjeta **Implementar el programa**. Haga clic en el botón **Deploy** para implementar el programa.

   ![](assets/configure-pipeline5.png)

