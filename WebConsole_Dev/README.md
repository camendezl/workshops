# Navegación de la consola web de OpenShift - Perspectiva Developer

## Navegación por la topologia de una aplicación generada previamente.

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. Autentiquese con el usuario que se le asigno en etherpad con la contraseña "r3dh4t1!" (sin incluir las comillas). Si le muestra una ventana de bienvenida, cierrela u omitala. 

![alt text](images/all_projects.png?raw=true)

¿Cuantos proyectos o namespaces puede visualizar? note que la consola web solo le muestra los proyectos a los cuales su usuario tiene permisos de acceso.

Haga click en la opción "Topology" del panel izquierdo, y luego click sobre el nombre del proyecto que le muestra (topology-example). Este proyecto cuenta con 2 aplicaciones desplegadas, cada una compuesta de 2 microservicios (un frontend y una base de datos de backend). Cada aplicación se encuentra agrupada bajo los nombres siguientes:
* dancer-example.
* django-example. 

Identifique en el dashboard cuales deploymentConfig (circulos de la topologia marcados con el label DC) corresponde a las agrupaciones mencionadas.

![alt text](images/topology.png?raw=true)

Haga click sobre el DC llamado django-psql-example. Observe la barra que se despliega a la derecha de la pantalla he identifique la siguiente información:
1. Nombre y estado del POD que se esta ejecutando.
2. El puerto TCP por el cual atiende peticiones el servicio y el POD. Note que son diferentes los puertos, debido a que los contenedores en OpenShift por defecto no pueden exponer servicios en puertos reservados de 1 a 1024.
3. URL de la ruta.

Luego haga click sobre la URL de la ruta. Se debe abrir la pagina donde esta publicada la aplicación.

![alt text](images/app_example.png?raw=true)

## Creación de una aplicación web a partir del codigo fuente

Ingrese a la opción "+Add" del panel izquierdo, y luego  

![alt text](images/create_project.png?raw=true)
![alt text](images/new_project.png?raw=true)


