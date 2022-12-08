# Taller de creación de NetworkPolicies 

Ingrese a la consola web de OpenShift desde un navegador web a la URL https://console-openshift-console.apps.cluster-7z6mg.7z6mg.example.opentlc.com. Autentiquese con el usuario que se le asigno en etherpad (perfil desarrollador) con la contraseña "r3dh4t1!" (sin incluir las comillas). Si le muestra una ventana de bienvenida, cierrela u omitala.

Ingrese a la opción "+Add", y en la selección del proyecto, pulse el boton "Create Project", y nombre el proyecto userXX-networkpolicy tal como se muestra en la siguiente imagen:

![alt text](images/create_project.png?raw=true)

Luego ingrese a la opcion "All services" dentro del catálogo del desarrollador, y busque una aplicación llamada "CakePHP + MySQL (Ephemeral)". Instalela aceptando todas las opciones por defecto.

![alt text](images/install.png?raw=true)

Espere a que se termine de desplegar la applicación por completo (cuando los dos DeploymentConfig se encuentren rodeados de la franja azul oscura), lo cual puede tardar un par de minutos.

![alt text](images/success.png?raw=true)

Abra la URL de la ruta para verificar que la aplicación web se esta ejecutando correctamente.

![alt text](images/app.png?raw=true)

Vuelva a la consola web de OpenShift, y cambie a la perspectiva de administrador (sin cambiar de usuario). Luego seleccione Networking > NetworkPolicies. Asegure que se encuentre seleccionado el proyecto que creo hace unos instantes.

![alt text](images/np.png?raw=true)

Allí podra identificar dos networkpolicies creados por defecto, los cuales son nombrados como allow-from-all-namespaces y allow-from-ingress-namespace. Estos se crean con la creación del proyecto y se puede eliminar debido a que no son necesarios (se permite todo el trafico por defecto si no hay un networkpolicy). Para eliminarlos, seleccione los 3 puntos de la derecha, y pulse "Delete NetworkPolicy". Repita el procedimiento con el segundo NetworkPolicy.

![alt text](images/delete.png?raw=true)
