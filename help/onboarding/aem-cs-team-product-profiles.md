---
title: Perfiles de AEM as a Cloud Service Team y de producto
description: Aprenda cómo los perfiles de equipo y de producto de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones de Adobe con licencia.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 86bb2e020a003fd418f8b1cf7bdf55987a2eaf3d
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 98%

---


# Perfiles de AEM as a Cloud Service Team y de producto {#product-profiles}

Aprenda cómo los perfiles de equipo y de producto de AEM as a Cloud Service pueden conceder y limitar el acceso a sus soluciones de Adobe con licencia.

## Perfiles de producto {#profiles}

Al conceder a un usuario acceso a una solución de Adobe específica, no es necesario que les proporcione acceso completo. Los perfiles de producto permiten que cada solución tenga su propio conjunto de permisos de usuario. Están disponibles y son accesibles a través de [Admin Console](/help/journey-onboarding/admin-console.md).

Adobe Admin Console tiene una jerarquía estructurada de productos, instancias de productos y perfiles de productos en la que se puede asignar la pertenencia a los usuarios internos de una organización, lo que les permite acceder a las soluciones y funciones para las que se ha obtenido licencia.

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## Perfiles de producto de AEM as a Cloud Service {#aem-product-profiles}

AEM as a Cloud Service es una oferta totalmente nativa de la nube que ofrece AEM como servicio. Ofrece AEM de forma nativa en la nube, con nuevos atributos como “siempre activado”, “siempre actuales”, “siempre seguros” y “siempre a escala”. Al mismo tiempo, conserva la propuesta de valor principal que proporciona AEM como plataforma personalizable a los clientes y permite que los equipos de clasificación empresarial se integren en sus procedimientos de desarrollo y envío. Consulte [Introducción a Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md) para obtener más información sobre AEM as a Cloud Service.

### Instancias de producto de nivel de organización {#org-level-product-instances}

>[!NOTE]
>
> Algunas de las instancias y perfiles de producto descritos en este artículo pueden aparecer solo para entornos recién creados. Consulte la sección [Agregar perfiles de producto para entornos existentes](#adding-product-profiles-for-existing-environments) para ver cómo modernizar los entornos.

Cuando Adobe procesa las licencias de una solución de AEM por primera vez, aparecen dos instancias de producto en Adobe Admin Console, en el producto de Adobe Experience Manager as a Cloud Service:

* **Nivel de organización de AEM**: contiene uno o varios perfiles de producto que representan el acceso a funciones que están definidas para todos los entornos de AEM, en lugar de para uno solo.
* **Cloud Manager**: contiene perfiles de producto correspondientes a diferentes niveles de acceso a las características de Cloud Manager.

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![Instancias de producto de nivel de organización](/help/onboarding/assets/orglevel.png)

Dentro de la instancia de producto de nivel de organización de AEM hay un perfil de producto denominado “Informadores de nivel de organización de AEM”, que no se utiliza en este momento, pero podría utilizarse en el futuro para representar el acceso a la recuperación de información sobre licencias de productos de AEM.

Cuando se obtiene una licencia para una solución de comunicación de formularios, también aparecerá un perfil de producto correspondiente en la instancia de producto a nivel de organización de AEM.

![Perfil de producto de informadores](/help/onboarding/assets/org-level-reporters.png)

### Instancias de producto de entorno y nivel {#environment-and-tier-level-product-instances}

Al aprovisionar nuevos programas con uno o más entornos de AEM, aparecerán dos instancias de producto por entorno, que contendrán perfiles de producto para la creación y la publicación, respectivamente.

![Instancias de producto de entorno](/help/onboarding/assets/env-productinstances.png)

A continuación se muestran los perfiles de producto en una instancia de producto de creación, para una organización que ha aprovisionado un entorno en un programa que contiene AEM Sites:

![Instancias de producto de Sites](/help/onboarding/assets/sites-product-instances.png)

En la siguiente tabla se describe una lista de los posibles perfiles de producto debajo de una instancia de producto específica de nivel y de entorno.

<table style="table-layout:auto">
    <tr>
        <th>Instancia de producto</th>
        <th>Convención de nomenclatura</th>
        <th>Servicio predeterminado</th>
        <th>Descripción</th>
    </tr>
    <tr>
        <td>AEM Author</td>
        <td>Administradores de contenido de AEM Sites - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Administradores de contenido de AEM Sites</td>
        <td>
            <ul>
                <li>Está pensado para el acceso controlado a las funciones de creación de AEM Sites en este entorno. Los usuarios de este perfil de producto serán miembros del grupo de autores de contenido de AEM Sites, que se crea automáticamente en AEM.  Los permisos de grupo de AEM deben configurarse en AEM con el nivel de acceso deseado.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de usuarios de AEM “Administradores de contenido de AEM Sites: servicio”.</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Administradores de AEM - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Administradores de AEM</td>
        <td>
            <ul>
                <li>Destinado al acceso sin restricciones a las funciones del entorno de creación y publicación de AEM. Los usuarios de este perfil de producto serán miembros del grupo de administradores de creación de AEM que se crea automáticamente en AEM.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de AEM “Administradores de AEM: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Usuarios de AEM - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios de AEM </td>
        <td>
            <ul>
                <li>Destinado a un acceso muy limitado a las funciones del entorno de creación de AEM.  Los usuarios de este perfil de producto serán miembros del grupo de AEM “Colaboradores” que se crea automáticamente en AEM</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de AEM “Usuarios de AEM: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Informadores de AEM - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Informadores de AEM</td>
        <td>
            <ul>
                <li>No se utilizan actualmente, pero en el futuro pueden proporcionar acceso a la creación de informes sobre el nivel de creación para este entorno.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Colaborador de AEM Assets - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios colaboradores de AEM Assets</td>
        <td>
        <ul>
                <li>Está pensado para el acceso de solo lectura a DAM. Los usuarios de este perfil de producto serán miembros del grupo de AEM “Colaboradores” que se crea automáticamente en AEM.
                </li>
                <li>
                Además, otorga derechos de Adobe Express para crear variaciones de recursos.
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>Usuario avanzado de AEM Assets - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios avanzados de AEM Assets</td>
<td>
        <ul>
                <li>Está pensado para el acceso de solo lectura a DAM. Los usuarios de este perfil de producto serán miembros del grupo de AEM “Colaboradores” que se crea automáticamente en AEM.
                </li>
                <li>
                Además, otorga derechos de Adobe Express para crear variaciones de recursos.
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>Administradores de contenido de AEM Forms - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Administradores de contenido de AEM Forms</td>
        <td>
            <ul>
                <li>Está pensado para el acceso controlado a las funciones de creación de AEM Forms en este entorno. Los usuarios de este perfil de producto serán miembros del grupo de AEM de usuarios de formularios de AEM Forms, que se crea de forma automática en AEM.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de usuarios de AEM “Administradores de contenido de AEM Forms: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Desarrolladores de AEM Forms - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Desarrolladores de AEM Forms</td>
        <td>
            <ul>
                <li>Está pensado para el acceso controlado a las funciones de creación de AEM Forms en este entorno. Los usuarios de este perfil de producto serán miembros del grupo de AEM de usuarios avanzados de formularios de AEM Forms, que se crea de forma automática en AEM. Estos usuarios tienen derechos para cargar XDP y crear modelos de datos de formulario, además de las tareas normales de creación de formularios.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de AEM “Desarrolladores de AEM Forms: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Usuarios del servicio de comunicaciones de AEM Forms - Creación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios del servicio de comunicaciones de AEM Forms</td>
        <td>
            <ul>
                <li>Está pensado para el acceso controlado a las funciones del servicio de comunicaciones de AEM Forms en este entorno. Los usuarios de este perfil de producto serán miembros del grupo de AEM de usuarios de formularios de AEM Forms, que se crea de forma automática en AEM.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de usuarios de AEM “Servicio de comunicaciones de AEM Forms: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>Publicación de AEM</td>
        <td>Usuarios de AEM - Publicación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios de AEM </td>
        <td>
            <ul>
                <li>Destinado a un acceso muy limitado a las funciones del entorno de creación de AEM.  Los usuarios de este perfil de producto serán miembros del grupo de AEM “colaboradores” que se crea automáticamente en AEM</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de AEM “Usuarios de AEM: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>Informadores de AEM - Publicación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Informadores de AEM</td>
        <td>
            <ul>
                <li>No se utilizan actualmente, pero en el futuro pueden proporcionar acceso a la creación de informes sobre el nivel de publicación para este entorno.</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>Usuarios del servicio de comunicaciones de AEM Forms - Publicación - Programa <code>id</code> - Entorno <code>id</code></td>
        <td>Usuarios del servicio de comunicaciones de AEM Forms</td>
        <td>
            <ul>
                <li>Está pensado para el acceso controlado a las funciones del servicio de comunicaciones de AEM Forms en este entorno. Los usuarios de este perfil de producto serán miembros del grupo de AEM de usuarios de formularios de AEM Forms, que se crea de forma automática en AEM.</li><br>
                <li>Si el servicio predeterminado permanece seleccionado,
                    <ul>
                        <li>los usuarios de este perfil de producto también serán miembros del grupo de usuarios de AEM “Servicio de comunicaciones de AEM Forms: servicio”.</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

Tenga en cuenta que cada perfil de producto tiene un servicio de perfil de producto asociado habilitado de forma predeterminada. A menos que tenga requisitos de acceso complejos, se recomienda mantener seleccionado solo el servicio predeterminado. Se creará un grupo de AEM correspondiente en AEM con la convención de nomenclatura `<Product Profile Prefix> - Service` (por ejemplo, **Administradores de contenido de AEM Sites: servicio**), y los usuarios de los perfiles de producto principales se convertirán automáticamente en miembros de ese grupo de AEM correspondiente.

El grupo de AEM en AEM asociado con el servicio tendrá el conjunto agregado de usuarios que existen en todos los perfiles de producto asociados de ese servicio para esa combinación de entorno y nivel.

![Servicios](/help/onboarding/assets/services.png)

La siguiente imagen representa los grupos de AEM que reflejan el nivel de creación del perfil de producto y el servicio de los administradores de contenido de AEM Sites.

![Asignación de grupo a servicio de AEM](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>Todos los usuarios asignados a un perfil de producto de AEM as a Cloud Service tienen acceso de solo lectura a Cloud Manager a través de la función del **Usuario de Cloud Manager**.
>
>Los usuarios con solo la función de **Usuario de Cloud Manager** pueden iniciar sesión en Cloud Manager y navegar a los entornos de creación de AEM (si existen) utilizando las opciones del menú **Programas**. La función de **Usuario de Cloud Manager** no es suficiente para acceder a los detalles del programa. Si se necesita dicho acceso, el administrador del sistema debe otorgar a los usuarios funciones adicionales.

>[!WARNING]
>
>El nombre del perfil del producto **Administradores de AEM** no debe cambiarse. Cambiar el nombre del perfil del producto **Administradores de AEM** quitará los derechos de administrador de todos los usuarios asignados a dicho perfil.

>[!TIP]
>
>* Para obtener más información acerca de los perfiles de producto de AEM, consulte [Asignación de perfiles de producto de AEM](/help/journey-onboarding/assign-profiles-aem.md).
>* Para obtener más información sobre el proceso de incorporación, consulte [recorrido de incorporación](/help/journey-onboarding/overview.md).

### Adición de perfiles de producto para entornos existentes {#adding-product-profiles-for-existing-environments}

Es posible que a los entornos creados antes de principios de abril de 2024 les falte la instancia de producto de nivel de organización descrita en las secciones anteriores, así como ciertos perfiles de producto. A los perfiles de producto existentes también les faltarán los conmutadores de servicio. Se recomienda actualizar esos perfiles de producto, lo que es un requisito previo para acceder a algunas API futuras.

Si uno o más entornos de un programa necesitan que se actualicen sus perfiles de producto, Cloud Manager mostrará el aviso a continuación. Tenga en cuenta que un entorno debe estar en la última versión de AEM antes de poder actualizar sus perfiles de producto.

![Modernizar perfiles de producto](/help/onboarding/assets/modernize-product-profiles.png)

Al hacer clic en el botón **Añadir perfiles de producto**, se abre un menú que muestra las opciones para añadir nuevos perfiles de producto a todos los entornos disponibles en el programa o en entornos individuales.

![Reemplazar entornos](/help/onboarding/assets/choose-env-r.png)

Haga clic en **Todos los entornos** para añadir los nuevos perfiles de producto a todos los entornos del programa. También puede hacer clic en **Entornos individuales** para añadir los nuevos perfiles de producto a los entornos seleccionados; esto lleva al usuario a una página de lista de entornos, donde se puede seleccionar una acción **Añadir perfiles de producto** del icono **Más opciones**.

![Entornos individuales](/help/onboarding/assets/individual-environments.png)

También puede añadir perfiles de producto a entornos seleccionados navegando a la sección Entornos de la página Información general del programa, haciendo clic en el icono Más opciones correspondiente a un entorno y seleccionando Añadir perfiles de producto.

El estado del entorno muestra “Añadir perfiles de producto” mientras se añaden los nuevos perfiles de producto y, a continuación, muestra “En ejecución” cuando se completa el proceso.


## Perfiles de producto de Cloud Manager {#cloud-manager-product-profiles}

Cloud Manager tiene perfiles de producto preconfigurados que se pueden considerar como permisos basados en roles. El administrador del sistema es responsable de configurar el equipo de Cloud Manager asignándolo a estos perfiles de producto.

>[!TIP]
>
>Consulte [Permisos basados en funciones en Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) para obtener más información.

Cada uno de los perfiles de producto tiene permisos específicos asociados a ellos.

* **Propietario del negocio**
   * En este rol, tiene permiso para agregar un nuevo programa o editarlo, agregar o actualizar un entorno, implementar código en un entorno de AEM o ejecutar comprobaciones de calidad del código.
   * Este usuario es responsable de definir los indicadores clave de rendimiento (KPI), aprobar implementaciones de producción y anular errores importantes de tres niveles cuando sea necesario.
* **Administrador de implementación**
   * En este rol, tiene permiso para agregar o actualizar un entorno, ejecutar cualquier canalización e implementar código en un entorno de AEM, o ejecutar comprobaciones de calidad del código.
   * Este usuario gestiona las operaciones de implementación y utiliza Cloud Manager para ejecutar implementaciones de ensayo/producción, editar las canalizaciones CI/CD, aprobar errores importantes de tres niveles cuando sea necesario y puede acceder al repositorio de Git.
* **Desarrollador**
   * En este rol, tiene permiso para generar tókenes de acceso personal para acceder a Git.
   * Este usuario desarrolla y prueba el código de aplicación personalizado y emplea principalmente Cloud Manager para ver el estado de implementación y puede acceder al repositorio de Git para confirmaciones de código.
* **Administrador de programa**
   * En este rol, tiene permiso para programar canalizaciones, anular las puertas de calidad de tres niveles y proporcionar la aprobación de producción.
   * Este usuario emplea Cloud Manager para realizar la configuración del equipo, revisar el estado y ver los indicadores clave de rendimiento (KPI) y puede aprobar errores importantes de tres niveles cuando sea necesario.

Se puede asignar un usuario a varios perfiles de producto. Por ejemplo, si se asignan ambos roles, **Propietario del negocio** y **Administrador de implementación** a un usuario, le da la suma de estos permisos.

Su equipo de Cloud Manager incluirá al menos lo siguiente:

* Un **Propietario del negocio**, que suele ser también el administrador del sistema y debe ser la primera persona en iniciar sesión y acceder a Cloud Manager
* Un **Administrador de implementación**
* Un **Desarrollador**

>[!NOTE]
>
>Para que se le conceda acceso a AEM as a Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto: `AEM Users` o `AEM Administrators`. Los permisos para administrar Cloud Manager no serán suficientes.

>[!TIP]
>
>* Para obtener más información sobre los perfiles de producto de Cloud Manager, consulte [Asignación de integrantes del equipo a perfiles de producto de Cloud Manager](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Para obtener más información sobre el proceso de incorporación, consulte [recorrido de incorporación](/help/journey-onboarding/overview.md).
