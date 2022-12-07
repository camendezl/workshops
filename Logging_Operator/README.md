# Instalación y funcionamiento de un Operador del Catalogo de OpenShift

## Red Hat OpenShift Logging Operator

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com.

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

Ingrese a la opción Operators > Projects del panel izquierdo, y busque el proyecto openshift-logging. Este proyecto no debe exitir aun debido a que es creado automaticamente por el operador del servicio Red Hat OpenShift logging.

![alt text](images/without_project.png?raw=true)

Debido a que este servicio solamente puede ser desplegado una vez en el cluster (solo puede haber una instancia de OpenShift Logging), solicite al instructor presentar pantalla y realizar el despliegue del operador de manera que todos los estudiantes este sincronizados en las actividades.

**--- Aqui inician las tareas que ejecuta el Instructor ---** 
El instructor en este punto debe ingresar a Operators > OperatorHub y buscar el Red Hat OpenShift Logging operator. Luego procedera con la instalación del mismo acorde a las buenas practicas.

![alt text](images/install_operator.png?raw=true)

![alt text](images/success.png?raw=true)

**--- Aqui terminan las tareas que ejecuta el Instructor ---** 

Luego de la confirmación de instalado, verifique nuevamente que se haya creado el proyecto openshift-logging en Home > Projects.

![alt text](images/project.png?raw=true)

Luego pulse sobre el nombre del proyecto, y verifique en el campo de inventario los recursos que se encuentran desplegados al momento. Navegue por cada uno de ellos para ver el detalle.

Ingrese a la pestaña "Workloads" dentro del proyecto. Pulse sobre el deployment llamado "cluster-logging-operator". Identifique el nombre y la cantidad de replicas que se estan ejecutando de este Deployment. Tambien podra identificar el nombre del "Service" y los puertos de escucha tanto del servicio como de los PODs. Recuerde que los recursos "Services" son el punto unico de entrada de trafico hacia los PODs y funcionan como un balanceador de carga, escuchando en un puerto e ip principal, y redirigiendo el trafico a los PODs que este balanceados.

![alt text](images/workloads.png?raw=true)

Para ver en detalle los endpoints del "Service" (PODs que estan balanceados), pulse sobre el nombre del "Service" y luego sobre la pestaña PODs. Allí debe visualizar un unico pod cuyo nombre inicia por cluster-logging-operator-.

![alt text](images/service_pods.png?raw=true)

Pulse sobre el nombre del POD, y luego sobre la pestaña Logs. Debera visualizar algunos pocos registros relacionados con el inicio del POD.

![alt text](images/logs.png?raw=true)

En este punto, el pod que esta en ejecución representa al operador que tiene la logica del funcionamiento del servicio de logging, y esta a la espera de indicaciones para desplegar el cluster del stack EFK (ElasticSearch - Fluentd - Kibana).

Pulse sobre Operators > Install Operators, y en el campo "Projects" garantice que este seleccionada la opción "All projects". Localice el operador "Red Hat OpenShift Logging" (desplegado por el instructor) y luego pulse sobre su nombre. Ingrese entonces a la pestaña "Subscription". Verifique las siguientes opciones sin hacer cambios:

* Verifique los canales a los que puede suscribir dicho operador. Esto es util para forza el despliegue de un operador e una versión especifica.
* Verifique cual es la estrategia para la instalación de actualizaciones. Cuando esta seleccionada la opción "Automatic", el operador junto con sus componentes administrados seran actualizados luego que una nueva versión ha sido publicada en el canal suscrito.
* Estado del operador. En esta sección se informa si esta correctamente instalado y si tienen actualizaciones pendientes.
* localice el catalogo fuente que proporciona dicho operador. 

![alt text](images/subs.png?raw=true)

Cambie a la pestaña "All instances". No deberia existir alguna en este punto.

Regrese al proyecto, he ingrese a la pestaña "Workloads" nuevamente. Solicite al instructor la creación de la instancia del servicio de logging, quien a su vez debe garantizar que todos los participantes esten en éste mismo punto.

El instructor ahora debe ingresar a Operators > Installed Operators e ingresar al Red Hat OpenShift Logging operator. Luego procedera con el despliegue de una instancia del Cluster Logging. 

Una vez se confirme la creación de la instancia, verifique los recursos creados por el operador en la pestaña "Workloads". Intente identificar los siguientes recursos de OpenShift que aparecen en pantalla con su nombre corto:

* CronJobs.
* Deployments.
* DeamonSet.
* Pods.

![alt text](images/resources.png?raw=true)

En este punto, el servicio de Logging ya se encuentra en operación. Ingrese nuevamente al proyecto y verifique nuevamente el campo de Inventario. Navegue por cada uno de ellos para conocer el detalle de todos los recursos desplegados.

Cambie a la perspectiva "Developer", seleccione la opción "Topology" del panel de la izquierda, y seleccione el proyecto "openshift-logging". Note la agrupación de los recursos que realiza de manera automatica el operador Red Hat OpenShift Logging.

![alt text](images/topology.png?raw=true)

Finalice la sesión haciendo click sobre el nombre del usuario en la esquina superior derecha de la pantalla, y luego "Log out".
