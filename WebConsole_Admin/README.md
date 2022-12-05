# Navegación de la consola web de OpenShift - Perpectiva Administrator

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. 

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

![alt text](images/dashboard.png?raw=true)

La plagina que despliega su navegador puede ser levemente diferente a la que se muestra en la imagen de ejemplo anterior, lo cual se debe al área de trabajo de la plantalla de su computador. Sin embargo, lo unico que cambia es el lugar donde de despliegan las vistas, dado que el contenido es el mismo.

En su computador, identifique la ubicación de las siguientes áreas:
1. Seleccionador de perspectiva
2. Panel de navegación.
3. Detalles de la instalación del cluster de OpenShift.
4. Inventario del cluster.
5. Estado de los componentes del cluster.
6. Alertas activas en el cluster.
7. Estado de recursos del cluster (sumatoria de los recursos de todos los nodos).
8. Ultimos eventos sobre la plataforma.

En el panel de navegación del panel izquierdo, ingrese a Operators > Operatorhub. Desplace la barrar vertical de la izquiera para poder visualizar la cantidad de operadores que el catalogo de OpenShift proporciona.

![alt text](images/operatorhub.png?raw=true)

Identifique los operadores instalados en el cluster de OpenShift ingresando a Operators > Installed Operators.

![alt text](images/installedoperators.png?raw=true)

Ingrese a Administration > Cluster Settings en el panel izquierdo. Identifique la version de OpenShift desplegada en el cluster. **¿Encuentra versiones disponibles para instalar?**


![alt text](images/update_status.png?raw=true)


