---
title: Añadir un entorno de prueba especializado
description: Descubra cómo los entornos de prueba especializados en Cloud Manager proporcionan un espacio dedicado para validar funciones en condiciones casi de producción, ideal para pruebas de estrés y comprobaciones avanzadas previas a la implementación.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 815fb5c3-a171-4531-8727-b79183d85f06
source-git-commit: 837f1d0eb0bd0f8cf8c0e283db823255f4e53ae1
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 12%

---

# Añadir un entorno de prueba especializado{#add-special-test-enviro}

<!-- badge: label="Private beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
-->

>[!NOTE]
>
>Ya se pueden adquirir entornos de prueba especializados. Póngase en contacto con su representante de Adobe para realizar un pedido.


El Entorno de prueba especializado es un nuevo tipo de entorno de Cloud Manager que puede crear. Está diseñado para admitir casos de uso avanzados, como las Pruebas de aceptación de usuarios (UAT) y la validación de rendimiento. A diferencia de los entornos tradicionales de desarrollo, desarrollo rápido o ensayo, los entornos de prueba especializada funcionan fuera de la canalización de implementación de producción. Por lo tanto, ofrecen una mayor flexibilidad a la vez que mantienen un aislamiento estricto para evitar interferencias con los flujos de trabajo de producción.

Un entorno de prueba especializado se crea para reflejar el tamaño, la escalabilidad y las configuraciones de un entorno de ensayo típico. Este método garantiza que las pruebas realizadas en el entorno de prueba especializado puedan proporcionar una perspectiva realista del rendimiento del código y el contenido en condiciones similares a las de producción. El entorno también admite la copia directa de contenido desde Producción o Ensayo. También mantiene la paridad con los entornos de desarrollo en términos de flujos de trabajo de implementación, controles de acceso y configuraciones de red.

## Características y configuraciones clave de un entorno de prueba especializado {#key-features}

| Categoría | Comportamiento |
| --- | --- |
| Función | UAT y pruebas de rendimiento. |
| Tipo de canalización | No está en la canalización de producción. |
| Tamaño del entorno | Coincide con el entorno de ensayo. |
| Aislamiento | Totalmente aislado de otros entornos. |
| Canalizaciones de código | Igual que el entorno de desarrollo (validación, compilación, implementación). |
| Copiar contenido | Permitido desde producción, fase o un entorno de prueba especializado. |
| Restauración de contenido | Igual que el entorno de desarrollo. |
| Registros de acceso | Igual que el entorno de desarrollo. |
| Developer Console | Igual que el entorno de desarrollo. |
| `IP Allow List` | Igual que el entorno de desarrollo. |
| Redes | Igual que el entorno de desarrollo (servicios, nombre de dominio, certificados SSL, red avanzada). |

Consulte también [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md).

## Añadir un entorno de prueba especializado {#add-specialized-testing-environment}

Para agregar o editar un entorno, un usuario debe ser miembro del rol **Propietario del negocio**.

**Para agregar un entorno de prueba especializado:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en el programa para el que desea agregar un entorno.

1. Realice una de las siguientes acciones:

   * En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, en la tarjeta **Entornos**, haga clic en **Agregar entorno**.
Si la opción **Agregar entorno** está atenuada (deshabilitada), puede deberse a la falta de permisos o a que depende de los recursos con licencia.

     ![Tarjeta Entornos](assets/no-environments.png)

   * En el panel lateral izquierdo, haga clic en ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos** y luego, en la página Entornos, cerca de la esquina superior derecha, haga clic en **Agregar entorno**.

     ![Pestaña Entornos](assets/environments-tab.png)

1. En el cuadro de diálogo **Añadir entorno**, haga lo siguiente:

   * Haga clic en **Entorno de prueba especializado**.
   * Proporcione un entorno **Name**. El nombre del entorno no se puede cambiar una vez creado el entorno.
   * (Opcional) Proporcione una **Descripción** para el entorno.
   * Seleccione una **región principal** en la lista desplegable. Una vez creada, la región principal del entorno de pruebas especializadas (por ejemplo, *Reino Unido (sur)*) está bloqueada y no se puede cambiar.

     ![Cuadro de diálogo Añadir entorno con el botón de opción Entorno de prueba especializado seleccionado](assets/specialized-test-environment.png)

1. Haga clic en **Guardar**.

   La página **Información general** ahora muestra su nuevo entorno en la tarjeta **Entornos**. Ahora puede configurar canalizaciones para su nuevo entorno.

## Recursos adicionales {#additional-resources}

* Vídeo: [Explicación de los tipos de entorno en AEM Cloud Manager](https://experienceleague.adobe.com/en/perspectives/cloud-manager-environment-types)
* [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md)

