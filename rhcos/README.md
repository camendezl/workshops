# Revisión y conexion de nodos de OpenShift

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. 

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE**: Este usuario tiene permisos de administrador del cluster, **por lo tanto NO REALICE modificaciones no solicitadas en éste taller.** Recuerde que este laboratorio de OpenShift es necesario para los futuros talleres.

Ingrese a Compute > Nodes en el panel izquierdo. Identique en la pantalla la totalidad de nodos que componen el cluster, su rol (Master o Worker) y los recursos de hardware usados / disponibles.

Haga click sobre cualquiera de los servidores "master", y luego haga click en la pestaña "Terminal".

![alt text](images/connect_node.png?raw=true)

Una vez abierta la terminal en el nodo, identifique la versión del sistema operativo que ejecuta la terminal. Para saberlo un metodo efectivo es visualizar el contenido del archivo /etc/os-release. Para ello, ejecute el siguiente comando en la terminal del nodo:

```
$ cat /etc/os-release
```

![alt text](images/os_release.png?raw=true)

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

Ahora que conoce que esta dentro del sistema Red Hat CoreOS (el sistema operativo de los nodos de OpenShift), puede realizar algunas labores de inspección (recuerde que este acceso es proporcionado por Red Hat **solo** por temas relativos a troubleshooting y los cambios directos sobre el sistema no son soportados).

Como se menciono anteriormente, RHCOS esta basado tambien en RHEL 8, por lo tanto muchos de los comandos que se tienen en RHEL tambien funcionan aqui. Por ejemplo, ejecute el siguiente comando para ver el estado de todas las interfaces de red. Aunque puede ser una unica interface de red fisica, el listado de interfaces será largo debido a las redes SDN que OpenShift crea para poder operar correctamente.

```
$ ip addr
```

Con el siguiente comando puede visualizar los registros (o logs) del sistema en tiempo real:

```
$ journalctl -f
```

Para finalizar el comando, presione las teclas Crtl + c.

Puede verificar el estado de los unicos servicios del sistema mediante la ejecución de los siguientes comandos. Estos siempre se deben reportar como activos y en ejecución. Para salir de la ejecución de los comandos, presione la tecla q.

Kubelet:
```
$ systemctl status kubelet
```

![alt text](images/kubelet.png?raw=true)

Crio:
```
$ systemctl status crio
```

![alt text](images/crio.png?raw=true)

Cualquier contenedor que se ejecute en los nodos tiene que haber descargado su imagen correspondiente del Registry al disco local. Ejecute el siguiente comando para visualizar todas las imagenes descargadas en disco. Puede utilizar la barra de desplazamiento vertical para visualizar todos los registros. Note que el tamaño de las imagenes es relativamente pequeño (entre 300 y 500 MB).

```
$ podman images 
```

Con el siguiente comando puede listar todos los contenedores que se encuentran en ejecución. Valide los nombres de los contenedores en la columna "NAME" y trate de relacionar algunos de ellos con la funcionalidad que proporciona al cluster de OpenShift. Identifique principalmente los siguientes:
* etcd
* kube-scheduler
* kube-controller-manager
* kube-apiserver
* openshift-apiserver  

```
$ crictl ps 
```

Puede inspeccionar los logs de los contenedores con el comando crictl. Ejecute el siguiente comando proporcionando como parámetro el ID (valor de 13 caracteres que aparece en la primera columna) del contenedor que quiera visualizar sus logs. Reemplaza ID por el valor correspondiente:

```
$ crictl logs ID
```

Puede visualizar logs en tiempo real adicionando "-f" al comando:

```
$ crictl logs -f ID
```

El comando anterior finaliza presionando Crtl + c.

Finalice la sesión haciendo click sobre el nombre del usuario en la esquina superior derecha de la pantalla, y luego "Log out".
