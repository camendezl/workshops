# Navegación de la consola web de OpenShift - Perspectiva Administrator

## Revisión y conexion con nodos de OpenShift

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. 

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

![alt text](images/dashboard.png?raw=true)

Ingrese a Compute > Nodes en el panel izquierdo. Identique en la pantalla la totalidad de nodos que componen el cluster, su rol (Master o Worker) y los recursos de hardware usados / disponibles.

Haga click sobre cualquiera de los nodos, y luego haga click en la pestaña "Terminal".

![alt text](images/connect_node.png?raw=true)

Una vez abierta la terminal en el nodo, identifique la versión del sistema operativo que ejecuta la terminal. Para saberlo un metodo efectivo es visualizar el contenido del archivo /etc/os-release. Para ello, ejecute el siguiente comando en la terminal del nodo:

```
$ cat /etc/os-release
```

La versión completa del OS se encuentra en la variable PRETTY_NAME. Recuerdela.

***tcpdump*** es un analizador de trafico de red muy usado en entornos linux, que permite el analisis de trafico en las tarjetas de red de un sistema. Ejecute el siguiente comando para determinal la versión de tcpdump instalada: 

```
$ tcpdump --version
```

Ahora, ejecute el siguiente comando en la terminal del nodo:

```
$ chroot /host
```

Y verifique nuevamente la versión del sistema operativo y de tcpdump:

```
$ cat /etc/os-release
$ tcpdump --version
```

* ¿**Que sucedio con la version del sistema operativo**?
* ¿**Que sucedio con tcpdump**?
* ¿**Puede imaginar porque las versiones son diferentes**?

Si tiene dudas al respecto, comentelas con el instructor.

Por ultimo, cambie la vista a la perspectiva de administrador y observe las opciones disponibles en el panel de navegación. Seleccione la opcion "Topology" y en la opcion "Project", seleccione "All Projects". Note que tiene acceso a todos los proyectos desplegados en OpenShift (**No realice cambios en los proyectos**).

![alt text](images/all_projects.png?raw=true)

Finalice la sesión haciendo click sobre el nombre del usuario en la esquina superior derecha de la pantalla, y luego "Log out".
