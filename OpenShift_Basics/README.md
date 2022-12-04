# Taller de uso basico de OCP
## Preparación de herramientas GIT
Mediante un navegador web, acceda a la URL http://git.apps.cluster-7z6mg.7z6mg.example.opentlc.com/user/login e identifiquese con sus credenciales.

![alt text](images/git_login.png?raw=true)

Luego cree un nuevo repositorio haciendo click en el simbolo "+" indicado en la imagen:

![alt text](images/new_repo.png?raw=true)

Luego digite el nombre de "myapp" en el campo "Repository Name", y luego haga click en el boton verde "Create Repository":

![alt text](images/create_repo.png?raw=true)

Ahora genere el codigo que se almacenará en el repositorio web. Para ello, sebera ingresar al servidor bastión que contiene todas las herramientas necesarias, tales como la CLI de OpenShift y la herramienta git:

Ingrese al servidor bastión via SSH. En el siguiente comando debe reemplazar el valor de <userX> por el valor de usuario asignado:
```
$ ssh <userX>@bastion.7z6mg.example.opentlc.com
```
Cree una carpeta para almacenar el codigo, y luego inicialice el repositorio git creado anteriormente:
```
$ mkdir myapp
$ cd myapp
$ cat <<EOF >> index.html
<html>
<body lang="es-MX" dir="ltr">
<p align="center" style="margin-bottom: 0cm; line-height: 100%"> 
<img src="https://www.redhat.com/cms/managed-files/Logo-redhat-color-375.png" name="Image1" align="bottom" width="399" height="116" border="0"/>
</p>
<p align="center" style="margin-bottom: 0cm; line-height: 100%"><br/>

</p>
<p align="center" style="margin-bottom: 0cm; line-height: 100%"><font size="6" style="font-size: 26pt">WorkShop OpenShift v4 - Claro Ecuador - Diciembre 2022</font></p>
<p align="center" style="margin-bottom: 0cm; line-height: 100%"><br/>

</p>
<p align="center" style="margin-bottom: 0cm; line-height: 100%"><font size="6" style="font-size: 26pt">Autor: Desconocido.</font></p>
<p align="center" style="margin-bottom: 0cm; line-height: 100%"><br/>

</p>
</body>
</html>
EOF
$ git init
```

Inicie sesión en OpenShift mediante la CLI (comando oc). Debido a que la plataforma cuenta con certificados autofirmados, la CLI preguntará si se debe usar una conexión insegura, por lo que ebe responder con "y" y luego enter:
```
$ oc login -u  ${USER} -p r3dh4t1! https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443'
```

## Despliegue de aplicación web

Cree un nuevo proyecto utilizando el siguiente comando:
```
$ oc new-project myapp-${USER}
```

Por ultimo, ejecute el siguiente comando para desplegar una aplicaion web contenerizada en OpenShift:
```
$ oc new-app httpd~http://git.apps.cluster-7z6mg.7z6mg.example.opentlc.com/${USER}/myapp
```

Puede visualizar los logs del proceso de construcción de la imagen (build) ejecutando el siguiente comando:
```
$ oc logs -f buildconfig.build.openshift.io/myapp
```

Para visualizar todos los recursos de OpenShift generados por el comando anterior, ejecute lo siguiente. Note que no existe una ruta (recurso route)  generada para acceder a la aplicación desde internet:
```
$ oc get all
```

![alt text](images/build1.png?raw=true)

Cree la ruta para exponer su aplicación en internet:
```
$ oc expose service myapp
```

Consulte la ruta que se creo previamente:
```
$ oc get routes
```

Y acceda a la URL anteponiendo http://. Puede accederla tambien mediante un navegador web, pero recuerde reemplazar la variable ${USER} por el nombre de su usuario.
```
$ curl http://myapp-myapp-${USER}.apps.cluster-7z6mg.7z6mg.example.opentlc.com
```

## Actualice el nombre del autor de la aplicación web
Clone el codigo fuente del repositorio GIT que utilizo para el despliegue de la aplicación, e ingrese al directorio:
```
$ cd ~
$ git clone http://git.apps.cluster-7z6mg.7z6mg.example.opentlc.com/${USER}/myapp
$ cd myapp
```

Sustituya el valor "Desconocido" en el archivo index.html por su nombre:
```
$ sed -i 's/Desconocido/REEMPLACE_CON_SU_NOMBRE/g' index.html
```

Puede ejecutar el siguiente comando para verificar que el reemplazo se ha realizado exitosamente:
```
$ cat index.html
```

Verifique es estado del repositorio git:
```
$ git status
```

Adicione los cambios realizados al archivo index.html al área de staging y nuevamente verifique el estado del repositorio:
```
$ git add index.html
$ git status
```

Luego confirme los cambios para aplicarlos en el repositorio local:
```
$ git commit -m "Campo de autor configurado"
```

Ahora debe actualizar el repositorio remoto con los cambios efectuados localmente. Para ello, ejecute el siguiente comando:
```
$ git push
```

Se le preguntará por los datos de su usuario, los cuales deberá ingresar.

Luego debe generar un nuevo build para actualizar su aplicación web en OpenShift. Para ello ejecute el siguiente comando:
```
$ oc start-build myapp
```

Puede visualizar los logs del proceso de construcción de la imagen (build) ejecutando el siguiente comando:
```
$ oc logs -f buildconfig.build.openshift.io/myapp
```

Una vez terminado el proceso anterior, verifique que la versión del BuildConfig se haya cambiado a 2, se haya generado un segundo un segundo pod del build y se haya actualizado el POD de la aplicación:
```
$ oc get all
```

![alt text](images/build2.png?raw=true)

Para finalizar el ejercicio, elimine la aplicación de OpenShift y realice limpieza de los archivos generados ejecutando el siguiente comando:
```
$ oc delete project myapp-${USER}
$ cd ~/
$ rm -rf myapp/
```

