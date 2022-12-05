# Taller de navegación por el dashboard de OpenShift Data Foundation (antigualmente OpenShift Container Storage)

## Navegación por el dashboard de ODF

Ingrese a la consola web de OpenShift en la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com/

![alt text](images/ocp_login.png?raw=true)

En el campo de usuario, coloque el usuario asignado + 100. Por ejemplo, si su usuario es user18, entonces ingrese con el usuario user118. El password es el mismo "r3dh4t1!". **IMPORTANTE: Este usuario tiene permisos de administrador del cluster, por lo tanto se ruega no realizar alguna operación no especificada en éste taller. Recuerde que este laboratorio lo requerimos para los futuros talleres.** 

Una vez dentro, expanda la opción "Storage" en el arbol de navegación de la izquierda. Ingrese a la opción OpenShift Data Foundation, en donde vera algo como lo siguiente:

![alt text](images/odf_dashboard.png?raw=true)

Ingrese a la pestaña "Storage Systems" y luego haga click en el nombre "ocs-storagecluster-storagesystem" que aparece en la tabla:

![alt text](images/ss.png?raw=true)

En la ventana que cargo, intente responder las siguientes preguntas:
* ¿Puede identificar rapidamente cual es el estado del cluster de ODF? (Recuerde que ODF se basa en el software open source Ceph Storage)
* ¿Puede determinar cuando espacio disponible tiene ODF?
* ¿Y cuanto tiene ocupado?
* ¿Puede encontrar en el dashboard los tipos de almacenamiento que proporciona ODF? (¿Block,File System and object storage?)
* ¿Puede identificar que proyectos esta consumiendo almacenamiento de ODF?
* ¿Puede identificar cuantos PersistentVolumeClaims (PVCs) y PersistentVolumes (PVs) ODF tiene desplegado? (Revise la sección "Inventory")
* ¿Puede identificar en cuantos nodos esta desplegado ODF, y cuales son esos nodos y que rol tienen en OpenShift?

En la sessión "Used Capacity Breakdown", seleccione "Pods" en lugar de "Projects". Identifique el nombre del POD que esta consumiendo espacio de ODF.

![alt text](images/pod_used.png?raw=true)

Luego cambie a la pestaña "BlockPools" e identifique la cantidad de replicas. En pocas palabras, el valor de las replicas indica la cantidad copias de la información que hace ODF en su instalación por defecto.

![alt text](images/blockpools.png?raw=true)

## Crear un PVC en OpenShift, proporcionado por ODF.
Verifique los StorageClasses que el cluster de laboratorio proporciona. Un StorageClass representa un tipo de almacenamiento que OpenShift puede proporcionar de manera dinamica o "automatica". Para ello, ingrese a la opción StorageClasses en el arbol de la izquierda de la consola web de OpenShift. 
* Cuantos StorageClasses visualiza?
* Puede identificar quien o que proporciona el almacenamiento en cada StorageClass?

Luego, ingrese a la opción PersistentVolumeClaims en el arbol de la izquierda de la consola web de OpenShift. Haga click en el boton "CreatePersistentVolumeClaim" para crear un nuevo PVC.

![alt text](images/create_pvc.png?raw=true)

Seleccione "ocs-storagecluster-ceph-rbd" como StorageClass, nombre el PVC igual que el nombre de su usuario y configure size al valor de 1. No modifique mas opciones y luego presione el boton "Create.

![alt text](images/new_pvc.png?raw=true)
 
Por ultimo deberá observar que su PVC ha sido correctamente creado, mediante la etiqueta de color verde "Bound".

![alt text](images/verify_pvc.png?raw=true)

Para finalizar, cierre la sesión web haciendo click sobre el nombre del usuario en la parte superior derecha de la pantalla, y luego "Log out".
