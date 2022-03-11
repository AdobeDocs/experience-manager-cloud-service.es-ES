---
title: Crear una página para dispositivos móviles
description: Al crear un elemento para móvil, puede cambiar entre varios emuladores para ver qué es lo que verá el usuario final
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 98%

---

# Crear una página para dispositivos móviles  {#authoring-a-page-for-mobile-devices}

Las páginas de Adobe Experience Manager se basan en un diseño adaptable. [El diseño adapta el contenido para que se ajuste automáticamente al dispositivo de destino, lo que elimina la necesidad de crear contenido específico para diferentes dispositivos.](/help/sites-cloud/authoring/features/responsive-layout.md)

Cuando se crea una página móvil, esta se muestra de un modo que emula al dispositivo móvil. Al crear la página, puede cambiar entre varios emuladores para ver lo que verá el usuario final al acceder a la página.

Los dispositivos se agrupan en las categorías característica, inteligente y táctil, según las capacidades de los dispositivos para procesar una página. Cuando el usuario final accede a una página para móvil, AEM detecta el dispositivo y envía la representación correspondiente al grupo de dispositivos.

>[!NOTE]
>
>Para crear un sitio para móvil según un sitio estándar existente, cree una Live Copy del sitio estándar. Consulte [Creación de Live Copies.](/help/sites-cloud/administering/msm/creating-live-copies.md)
>
>Los desarrolladores de AEM pueden crear nuevos grupos de dispositivos. Consulte Crear filtros de grupo de dispositivos.

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

Utilice el siguiente procedimiento para crear una página para móvil:

1. En la navegación global, abra la consola **Sitios**.
1. Edite una página de contenido.
1. Cambie al emulador que quiera usar haciendo clic en el icono **Emulador** en la parte superior de la página.

   ![Icono Emulador](/help/sites-cloud/authoring/assets/emulator.png)

1. Arrastre y suelte los componentes desde el navegador de componentes o el explorador de recursos a la página.
1. [Modifique el diseño adaptable](/help/sites-cloud/authoring/features/responsive-layout.md) de la página y sus componentes en función del dispositivo seleccionado.

La página presenta un aspecto similar al siguiente:

![Ejemplo para móvil](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>Los emuladores se desactivan cuando se solicita una página de la instancia del autor desde un dispositivo móvil.
