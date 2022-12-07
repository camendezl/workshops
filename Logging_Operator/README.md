# Verificación de instalación del operador OpenShift Logging

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com.

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

Ingrese a la opción Home > Projects del panel izquierdo, y busque el proyecto openshift-logging. Este proyecto no debe exitir aun debido a que es creado automaticamente por el operador del servicio Red Hat OpenShift logging.

![alt text](images/without_project.png?raw=true)

Debido a que este servicio solamente puede ser desplegado una vez en el cluster (solo puede haber una instancia de OpenShift Logging), solicite al instructor presentar pantalla y realizar el despliegue del operador de manera que todos los estudiantes este sincronizados en las actividades.

El instructor en este punto debe ingresar a Home > OperatorHub y buscar el Red Hat OpenShift Logging operator. Luego procedera con la instalación del mismo acorde a las buenas practicas.

Luego de la confirmación de instalado, verifique nuevamente que se haya creado el proyecto openshift-logging 

![alt text](images/project.png?raw=true)
