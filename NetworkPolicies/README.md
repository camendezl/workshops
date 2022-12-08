# Taller de creación de NetworkPolicies 

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. Autentiquese con el usuario que se le asigno en etherpad (perfil desarrollador) con la contraseña "r3dh4t1!" (sin incluir las comillas). Si le muestra una ventana de bienvenida, cierrela u omitala.

Ingrese a la opción "+Add", y en la selección del proyecto, pulse el boton "Create Project", y nombre el proyecto userXX-networkpolicy tal como se muestra en la siguiente imagen:

![alt text](images/create_project.png?raw=true)

Luego ingrese a la opcion "All services" dentro del catálogo del desarrollador, y busque una aplicación llamada "CakePHP + MySQL (Ephemeral)". Instalela aceptando todas las opciones por defecto.

![alt text](images/install.png?raw=true)

Espere a que se termine de desplegar la applicación por completo (cuando los dos DeploymentConfig se encuentren rodeados de la franja azul oscura), lo cual puede tardar un par de minutos.

![alt text](images/success.png?raw=true)

Abra la URL de la ruta en una nueva pestaña para verificar que la aplicación web se esta ejecutando correctamente. No cierre esta pestaña, dado que la necesitaremos mas adelante.

![alt text](images/app.png?raw=true)

Vuelva a la consola web de OpenShift, y cambie a la perspectiva de administrador (sin cambiar de usuario). Luego seleccione Networking > NetworkPolicies. Asegure que se encuentre seleccionado el proyecto que creo hace unos instantes.

![alt text](images/np.png?raw=true)

Allí podra identificar dos networkpolicies creados por defecto, los cuales son nombrados como allow-from-all-namespaces y allow-from-ingress-namespace. Estos se crean con la creación del proyecto y se puede eliminar debido a que no son necesarios (se permite todo el trafico por defecto si no hay un networkpolicy). Para eliminarlos, seleccione los 3 puntos de la derecha, y pulse "Delete NetworkPolicy". Repita el procedimiento con el segundo NetworkPolicy.

![alt text](images/delete.png?raw=true)

Vuelva a la pestaña donde tiene la aplicación web, y refresque con F5 para garantizar que la aplicación continua respondiendo peticiones.

Para crear los NetworkPolicies es necesario tener presente lo siguiente:

* Tener claro el nombre de los DeploymentConfig de cada microservicio desplegado en el proyecto.
* Tener claro el puerto por el que escuchan los servicios asociados a cada DeploymentConfig.
* Tener claro como es el flujo de la información.

Ingrese a Workloads > DeploymentConfig y a Networking > Services para obtener la información correspondiente, y la siguiente grafica lo guiará con el flujo de la información:

![alt text](images/flow_app.png?raw=true)

Antes de generar los NetworkPolicies para limitar el trafico al extrictamente necesario, realicemos una prueba de conectividad que no es necesaria y será bloqueada por la creación de los NetworkPolicies. Dicha conección es desde el POD de mysql hacia el frontend. Para ello, pulse en Workloads > Pods, y luego sobre el POD de mysql que se encuentra en estado Running. Luego pulse sobre la pestaña terminal para conectarse a dicho POD. En la terminal que se despliegua, consulte el puerto del servicio del frontend con el comando curl, tal cual se visualiza en la imagen. Observe que el servicio responde:

![alt text](images/curl_ini.png?raw=true)

Ahora procederemos a bloquer el trafico innecesario. Vuelva a Networking > NetworkPolicies y pulse en el botón "Create NetworkPolicy". Dado que inicialmente vamos a proteger el backend (la base de datos), llene el formulario como se muestra en la imagen siguiente:

![alt text](images/1_podselec.png?raw=true)
![alt text](images/1_ingress.png?raw=true)
![alt text](images/1_ports.png?raw=true)

Vuelva a Networking > NetworkPolicies y pulse en el botón "Create NetworkPolicy". Esta vez vamos a proteger el backend, por lo que deberá llenar el formularion como se muestra a continuación.

![alt text](images/2_podselec.png?raw=true)
![alt text](images/2_ingress.png?raw=true)
![alt text](images/2_ports.png?raw=true)

En este punto, debera tener 2 NetworkPolicies tal como se muestra a continuación:

![alt text](images/nps.png?raw=true)

Vuelva a la pagina web de la aplicación y verifique que ésta siga operando. Luego, vuelva a conectarse al POD de mysql y verifique que este POD ya no puede conectarse con el puerto de servicio del frontend. Para ello, pulse en Workloads > Pods, y luego sobre el POD de mysql que se encuentra en estado Running. Luego pulse sobre la pestaña terminal para conectarse a dicho POD. En la terminal que se despliegua, consulte el puerto del servicio del frontend con el comando curl, tal cual se visualiza en la imagen. Observe que el servicio que antes respondia, ua no lo hace:

![alt text](images/no_con.png?raw=true)

Finalice la sesión haciendo click sobre el nombre del usuario en la esquina superior derecha de la pantalla, y luego "Log out".
