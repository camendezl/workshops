# Verificación de instalación del operador OpenShift Logging

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com.

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

Ingrese a la opción Home > Projects del panel izquierdo, y busque el proyecto openshift-logging. Este proyecto no debe exitir aun debido a que es creado automaticamente por el operador del servicio Red Hat OpenShift logging.

![alt text](images/without_project.png?raw=true)

Debido a que este servicio solamente puede ser desplegado una vez en el cluster (solo puede haber una instancia de OpenShift Logging), solicite al instructor presentar pantalla y realizar el despliegue del operador de manera que todos los estudiantes este sincronizados en las actividades.

El instructor en este punto debe ingresar a Home > OperatorHub y buscar el Red Hat OpenShift Logging operator. Luego procedera con la instalación del mismo acorde a las buenas practicas.

![alt text](images/install_operator.png?raw=true)
![alt text](images/success.png?raw=true)

Luego de la confirmación de instalado, verifique nuevamente que se haya creado el proyecto openshift-logging en Home > Projects.

![alt text](images/project.png?raw=true)

Luego pulse sobre el nombre del proyecto, he ingrese a la pestaña "Workloads". Pulse sobre el deployment llamado "cluster-logging-operator". Identifique el nombre y la cantidad de replicas que se estan ejecutando de este Deployment. Tambien podra identificar el nombre del "Service" y los puertos de escucha tanto del servicio como de los PODs. Recuerde que los recursos "Services" son el punto unico de entrada de trafico hacia los PODs y funcionan como un balanceador de carga, escuchando en un puerto e ip principal, y redirigiendo el trafico a los PODs que este balanceados.

![alt text](images/workloads.png?raw=true)

Para ver en detalle los endpoints del "Service" (PODs que estan balanceados), pulse sobre el nombre del "Service" y luego sobre la pestaña PODs. Allí debe visualizar un unico pod cuyo nombre inicia por cluster-logging-operator-.

![alt text](images/workloads.png?raw=true)

Pulse sobre el nombre del POD, y luego sobre la pestaña Logs. Debera visualizar algunos pocos registros relacionados con el inicio del POD.

En este punto, el pod que esta en ejecución es el operador que tiene la logica del funcionamiento del servicio de logging, y esta a la espera de indicaciones para desplegar el cluster del stack EFK (ElasticSearch - Fluentd - Kibana).

Regrese al proyecto, he ingrese a la pestaña "Workloads" nuevamente. Solicite al instructor crear la 
