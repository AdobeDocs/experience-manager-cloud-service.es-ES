---
title: Creación de programas de producción
description: Aprenda a utilizar Cloud Manager para crear su propio programa de producción y alojar tráfico en directo.
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: ht
source-wordcount: '581'
ht-degree: 100%

---


# Creación de programas de producción {#create-production-program}

Un programa de producción está diseñado para un usuario que esté familiarizado con AEM y Cloud Manager y que esté listo para empezar a escribir, crear y probar código con el objetivo de implementarlo para alojar tráfico en vivo.

Obtenga más información sobre los tipos de programas en el documento [Explicación de los programas y sus tipos.](program-types.md)

## Creación de un programa de producción {#create}

Siga estos pasos para crear un programa de producción.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en **Agregar programa** en la esquina superior derecha de la pantalla.

   ![Página de aterrizaje de Cloud Manager](assets/log-in.png)

1. Seleccione **Configurar para producción** en el asistente Crear programa para crear un programa de producción y proporcionar un nombre de programa.

   ![Creación del asistente del programa](assets/create-production-program.png)

1. Para añadir, si lo desea, una imagen al programa, arrastre y suelte un archivo de imagen en el destino **Añadir una imagen del programa** o haga clic en él para seleccionar una imagen de un explorador de archivos. Haga clic o pulse **Continuar**.

1. Si tiene derechos de seguridad mejorada, la pestaña **Seguridad mejorada** le ofrecerá la opción **Habilitar seguridad mejorada** para su programa de producción. Si es necesario, marque la opción para habilitar la seguridad mejorada y toque o haga clic en **Continuar**.

   * La seguridad mejorada no se puede habilitar ni deshabilitar después de la creación del programa.
   * [Más información](https://www.adobe.com/go/hipaa-ready_es) acerca de la implementación de la solución compatible con HIPAA de Adobe.

   ![Opción Seguridad mejorada](assets/create-production-program-enhanced.png)

1. En la pestaña **Soluciones y complementos**, seleccione las soluciones que desea incluir en el programa.

   * Si tiene dudas sobre si necesita uno o más programas para las distintas soluciones disponibles, seleccione la que le interese. Si desea activar soluciones adicionales, [puede editar el programa](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md) más tarde. Consulte el [Documento de introducción a los programas de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) para conocer más recomendaciones sobre la configuración del programa.
   * Si ha seleccionado anteriormente la opción **Habilitar seguridad mejorada**, solo podrá seleccionar tantas soluciones como derechos HIPAA estén disponibles.

   ![Seleccionar soluciones](assets/setup-prod-select.png)

1. Haga clic en el elemento adicional antes de los nombres de las soluciones para mostrar complementos opcionales, como seleccionar la opción de complemento **Comercio** en **Sites**.

   ![Seleccionar complementos](assets/setup-prod-commerce.png)

1. Con las soluciones y los complementos seleccionados, haga clic en **Continuar**.

1. En la pestaña **Fecha de lanzamiento**, introduzca la fecha en la que planea que su programa de producción se ponga en marcha.

   ![Definir la fecha de lanzamiento planeada](assets/setup-go-live.png)

   * Esta fecha se puede editar en cualquier momento.
   * Esta fecha es solo para uso informativo y activa el widget Go Live en la página de descripción general del programa para proporcionar vínculos internos del producto a la documentación de prácticas recomendadas de AEM as a Cloud Service de forma oportuna para que se ajuste a su recorrido y que culmine en una experiencia Go Live correcta y sin problemas.

1. Haga clic en **Crear**.

El programa lo crea Cloud Manager y aparece y se puede seleccionar en la página de aterrizaje.

![Información general de Cloud Manager](assets/navigate-cm.png)

## Acceso a su programa {#acessing}

1. Una vez que vea la tarjeta del programa en la página de aterrizaje, seleccione el botón de tres puntos para ver las opciones de menú disponibles.

   ![Información general del programa](assets/program-overview.png)

1. Seleccione **Información general del programa** para navegar a la página **Información general**.

1. La tarjeta de llamada a la acción principal de la página de información general le guiará a través de la creación de un entorno, una canalización que no sea de producción y, finalmente, una canalización de producción.

   ![Información general del programa](assets/set-up-prod5.png)

Si en cualquier momento necesita cambiar a otro programa o volver a la página de información general para crear otro programa, haga clic en el nombre del programa en la parte superior izquierda de la pantalla para mostrar la opción **Vaya a**.

![Vaya a](assets/create-program-a1.png)

>[!NOTE]
>
>A diferencia de un [programa de zona protegida,](introduction-sandbox-programs.md#auto-creation) un programa de producción requerirá que el usuario con la función adecuada de Cloud Manager cree el proyecto y añada un entorno a través de la interfaz de usuario de autoservicio.
