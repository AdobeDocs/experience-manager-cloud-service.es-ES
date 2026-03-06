---
title: Incrustar una temática de Forms adaptable en una temática de AEM Sites
description: Aprenda a integrar una temática de Forms adaptable (por ejemplo, Lienzo) en una temática de AEM Sites para que las páginas de Sites y la Forms adaptable incrustada compartan una temática e implementación unificadas.
keywords: tema de formularios adaptables, tema del sitio, tema de AEM Sites, integración de temas de formularios, canalización front-end, incrustación de temas
feature: Adaptive Forms, Core Components
role: Developer
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: e1593d26beea79ffd7d8c5075b99d84c6a98c3b0
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 1%

---

# Incrustar una temática de Forms adaptable en una temática de AEM Sites

Puede incrustar una temática de Forms adaptable (como la [temática de lienzo de AEM Forms](https://github.com/adobe/aem-forms-theme-canvas)) en la temática de AEM Sites. De este modo, un solo tema controla tanto las páginas del sitio como cualquier Forms adaptable incrustado en esas páginas, con una compilación y una implementación a través de la [canalización front-end de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=es).

Este artículo es para desarrolladores que mantienen o personalizan la temática estándar (o personalizada) de AEM Sites y que desean incluir el estilo del formulario adaptable sin administrar una implementación de temática de Forms independiente.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* **AEM as a Cloud Service** con la [canalización front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=es) configurada para el tema de su sitio.
* **Fuentes de temas del sitio**: por ejemplo, el [tema estándar de la plantilla del sitio](https://github.com/adobe/aem-site-template-standard) (el repositorio que contiene `theme/` con `src/theme.scss`, `src/components/`, etc.).
* **Fuentes de temas de Forms** - el [tema de lienzo de AEM Forms](https://github.com/adobe/aem-forms-theme-canvas) (u otro tema de Forms adaptable compatible) clonado o descargado localmente.
* **Node.js y npm**: para crear el tema del sitio (consulte el tema README para ver las versiones compatibles).
* **Maven**: si genera el paquete completo de plantillas del sitio (opcional para el trabajo de solo tema).

## Paso 1: Crear la carpeta de componentes del formulario adaptable {#step-1-create-folder}

En el repositorio de temas del sitio, cree la carpeta donde se almacenará el tema de Forms:

```text
theme/src/components/adaptiveform/
```

Todos los recursos de temas de Forms se sentarán en esta carpeta para que sean independientes de los componentes de sitio existentes.

## Paso 2: Copiar componentes e imágenes de temas de Forms {#step-2-copy-components-and-images}

Utilizando las rutas de acceso del **tema de Forms** (por ejemplo, `aem-forms-theme-canvas`) y del **tema del sitio**:

1. **Copiar carpetas de componentes**\
   Desde el tema de Forms, copie todo el contenido de `src/components/` en el tema del sitio como:

   ```text
   theme/src/components/adaptiveform/
   ```

   Así se obtienen rutas como:

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![agregar componentes de formulario adaptable](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **Copiar imágenes**\
   Copie las imágenes del tema de Forms en el tema del sitio:

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   Cree `theme/src/components/adaptiveform/resources/images/` si no existe y copie todos los recursos de imagen (por ejemplo, `question.svg`, `Chevron-Left.svg`, `busy-state.gif`, etc.).

   ![agregar imágenes](/help/forms/assets/theme-add-images.png)

## Paso 3: Copiar variables y mezclas {#step-3-copy-variables-and-mixins}

La temática de Forms usa variables y mezclas compartidas en `src/site/`. Copie solo estos dos archivos en la **raíz** de `adaptiveform/` (no dentro de una subcarpeta `site`):

| Source (tema de Forms) | Destino (tema del sitio) |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

**no** copia el resto de la carpeta `src/site/` del tema de Forms; solo se necesitan estos dos archivos para los estilos de formulario incrustados.

![agregar variables y mezclas](/help/forms/assets/theme-add-mixin-variable.png)

## Paso 4: Corregir rutas de imagen en SCSS {#step-4-fix-image-paths}

En el tema de Forms, los archivos SCSS de componente suelen hacer referencia a imágenes con rutas de acceso como `./resources/` o `url(resources/`. Después de copiar en el tema del sitio, esas rutas deben apuntar a `theme/src/components/adaptiveform/resources/images/`.

El **tema estándar de la plantilla del sitio** usa Parcel, que resuelve `url()` rutas de `theme/src/`. Por lo tanto, cuando las imágenes se encuentren en `theme/src/components/adaptiveform/resources/images/`, utilice la ruta de acceso **`components/adaptiveform/resources/images/`** (relativa a `theme/src/`).

**Buscar y reemplazar** en cada `.scss` en `theme/src/components/adaptiveform/`:

| Buscar | Reemplazar con |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**Ejemplo** - antes (tema de Forms):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**Después** (tema del sitio, imágenes en `adaptiveform/resources/images/`):

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![Cambiar URL de imágenes](/help/forms/assets/theme-change-url.png)

Repita el proceso para cada archivo SCSS bajo `adaptiveform/` que haga referencia a imágenes (botón, acordeón, asistente, contenedor, garabato, etc.). Se recomienda buscar/reemplazar en todo el proyecto en su IDE más de `theme/src/components/adaptiveform/`.

## Paso 5: Crear el SCSS de punto de entrada del formulario adaptable {#step-5-create-adaptiveform-scss}

Crear **`theme/src/components/adaptiveform/_adaptiveform.scss`** en el tema del sitio. Este archivo debe:

1. Importe las variables y mezclas compartidas.
2. Importe el archivo SCSS principal de cada componente del formulario adaptable.

Utilice lo siguiente como punto de entrada completo (coincide con la integración estándar con todos los componentes de formulario basados en componentes principales):

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![scss de formulario adaptable](/help/forms/assets/theme-adaptive-form-scss.png)

Si el tema de Forms omite algunos componentes (por ejemplo, no garabato ni captcha), quite o comente las `@import` líneas correspondientes para evitar errores de compilación. La lista anterior coincide con la estructura [Canvas theme](https://github.com/adobe/aem-forms-theme-canvas).

## Paso 6: importar la temática del formulario adaptable en la temática del sitio {#step-6-import-in-theme-scss}

En **`theme/src/theme.scss`**, agregue una sola importación al **final** del archivo (después de las importaciones de otros componentes):

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**Ejemplo** - fin de `theme.scss`:

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![agregar scss de formulario adaptable](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

Este es el único cambio necesario en la estructura del tema del sitio existente; todo el código específico del formulario permanece bajo `src/components/adaptiveform/`.

## Paso 7: Generación e implementación {#step-7-build-and-deploy}

1. Cree el tema del sitio desde la raíz del tema:

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![ejecutar compilación](/help/forms/assets/theme-mpm-run-build.png)

2. Implementar mediante su [canalización front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=es) existente. Después de la implementación, se aplicará el mismo tema CSS a ambas páginas del sitio y a los Forms adaptables incrustados.

## Solución de problemas {#troubleshooting}

| Problema | Qué comprobar |
|-------|-------------------------------|
| La compilación falla: &quot;archivo no encontrado&quot; para una imagen | Asegúrese de que todas las imágenes de formulario estén en `theme/src/components/adaptiveform/resources/images/`. En cada `.scss` de menos de `adaptiveform/`, use `url(components/adaptiveform/resources/images/...)` para que la ruta se resuelva a partir de `theme/src/` (requerido para la compilación de tema de sitio estándar con Parcel). No use `../resources/` o `resources/` solos a menos que el paquete resuelva las rutas de acceso por archivo; a continuación, use la ruta de acceso que coincida con la carpeta de imágenes. |
| Error de compilación: &quot;no se encontró el archivo&quot; para `_variables.scss` o `_mixin.scss` | Copie ambos archivos del tema de Forms `src/site/` en `theme/src/components/adaptiveform/` (la raíz del formulario adaptable), no dentro de una subcarpeta `site`. |
| La compilación falla: &quot;no se encontró el archivo&quot; para un componente (por ejemplo: `_scribble.scss`) | Es posible que la temática de Forms no incluya ese componente. En `theme/src/components/adaptiveform/_adaptiveform.scss`, quite o comente la línea `@import` para ese componente. |
| El formulario se procesa pero no tiene estilos | Confirme que la página utiliza la biblioteca de cliente que incluye el tema CSS creado y que `theme.scss` contiene la línea `@import './components/adaptiveform/_adaptiveform.scss';`, y que el tema se ha vuelto a crear e implementado. |
| Conflicto de estilos entre los componentes del sitio y del formulario | Las clases de componentes de formulario tienen un espacio de nombres (por ejemplo: `cmp-adaptiveform-button`). Si se producen conflictos, compruebe si el CSS del sitio personalizado anula esas clases y ajuste la especificidad o el orden. |

## Consulte también {#see-also}

* [Utilizar temáticas para aplicar estilo a Forms adaptable basado en componentes principales](/help/forms/using-themes-in-core-components.md)
* [Desarrollar con canalizaciones front-end](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html?lang=es)
