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

## Self-service - Creación de una aplicación web a partir del codigo fuente.

Ingrese a la opción "+Add" del panel izquierdo, y luego haga click en el menú desplegable "Project". Seleccione la opción "Create Project" para crear un nuevo projecto, y nombrelo como newapp-"userXX". Ej: newapp-user50. Luego click en el botón crear.

![alt text](images/create_project.png?raw=true)
![alt text](images/new_project.png?raw=true)

En la casilla del catalogo de desarrollador (Catalog Developer), pulse sobre "All services" para acceder al catalogo de aplicaciones de OpenShift.

![alt text](images/catalog.png?raw=true)

Navegue por el catalogo e identifique algunas de las aplicaciones que pueden ser desplegadas a modo Self Service por parte de los desarrolladores.

Busque dentro del catalogo una aplicación llamada "CakePHP + MySQL" (seleccione la que NO dice "Ephemeral"), y haga click sobre ella. Asegurese de leer la descripción para entender el tipo de aplicación que desplegará en OpenShift. Luego pulse el botón "instantiate Template".

![alt text](images/instantiate.png?raw=true)

Note el formulario que se despliega con las opciones disponibles. Intente identificar los siguiente datos:
1. El proyecto donde se desplegará la app.
2. La versión de la imagen PHP que se usará para construir la app.
3. El limite de memoria que se asignará al POD del frontend y al pod de la BD MySQL.
4. El tamaño del volumen que se creará para alojar la base de datos.
5. La URL del repositorio git que contiene el codigo fuente de la app. Opcional: copie la URL y abrala. El codigo fuente esta alojado en un repositorio publico en internet de GitHub.

No realice cambios y dirijase al final del formulario, luego presione el botón "Create".

Luego, haga click sobre el DC llamado cakephp-mysql-persistent, y luego click en la opción "View logs" tal cual se muestra en la imagen siguiente:

![alt text](images/view_logs.png?raw=true)

Observe el proceso de "Build" de la imagen (proceso donde se compila el codigo fuente extraido de GitHub, y se inyecta en una imagen que posteriormente es almacenada en el Registry de OpenShift).

![alt text](images/logs.png?raw=true)

Regrese a la pantalla de "Topology", y luego pulse el botón Open URL que se muestra en la imagen. Se abrira la aplicación WEB que ha desplegado.

![alt text](images/open_url.png?raw=true)

Regrese a la consola web de OpenShift y pulse sobre la opción "Project" en el panel izquierdo. En el recuadro del inventario, identifique todos los recursos que se desplegaron con la aplicación. Ingrese a cada uno de los recursos he identifiquelos. Note que junto con la base de datos se desplego un volumen persistente de 1GiB.

Por ultimo, cierre la sesión web pulsando sobre el nombre de usuario en la esquina superior derecha de la consola web, y luego Log out.
