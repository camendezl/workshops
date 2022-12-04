# Taller de uso basico de OCP
## Despliegue de aplicación web
Ingrese al servidor bastión via SSH:
ssh userX@bastion.7z6mg.example.opentlc.com

Inicie sesión en OpenShift mediante la CLI (comando oc). Debido a que la plataforma cuenta con certificados autofirmados, la CLI preguntará si se debe usar una conexión insegura, por lo que ebe responder con "y" y luego enter:
oc login -u  ${USER} -p r3dh4t1! https://api.cluster-7z6mg.7z6mg.example.opentlc.com:6443'

Luego de la confirmación del login, cree un nuevo proyecto utilizando el siguiente comando:
oc new-project myapp-${USER}

Por ultimo, ejecute el siguiente comando para desplegar una aplicaion web contenerizada en OpenShift:
oc new-app httpd~http://git.apps.cluster-7z6mg.7z6mg.example.opentlc.com/${USER}/myapp

Puede visualizar los logs del proceso de construcción de la imagen (build) ejecutando el siguiente comando:
oc logs -f buildconfig.build.openshift.io/myapp

Para visualizar todos los recursos de OpenShift generados por el comando anterior, ejecute:
oc get all

Cree la ruta para exponer su aplicación en internet:
oc expose service myapp

Consulte la ruta que se creo previamente:
oc get routes

Y acceda a la URL anteponiendo http://. Puede accederla tambien mediante un navegador web, pero recuerde reemplazar la variable ${USER} por el nombre de su usuario.
curl http://myapp-myapp-${USER}.apps.cluster-7z6mg.7z6mg.example.opentlc.com

## Actualice el nombre del autor de la aplicación web
Clone el codigo fuente del repositorio GIT que utilizo para el despliegue de la aplicación, e ingrese al directorio:
git clone http://git.apps.cluster-7z6mg.7z6mg.example.opentlc.com/${USER}/myapp
cd myapp

Sustituya el valor "Desconocido" en el archivo index.html por su nombre:
sed -i 's/Desconocido/REEMPLACE_CON_SU_NOMBRE/g' index.html

Puede ejecutar el siguiente comando para verificar que el reemplazo se ha realizado exitosamente:
cat index.html

Verifique es estado del repositorio git:
git status

Adicione los cambios realizados al archivo index.html al área de staging:
git add index.html

Nuevamente verifique es estado del repositorio git:
git status

Luego confirme los cambios para aplicarlos en el repositorio local:
git commit -m "Campo de autor configurado"

Ahora debe actualizar el repositorio remoto con los cambios efectuados localmente. Para ello, ejecute el siguiente comando:
git push

Se le preguntará por los datos de su usuario, los cuales deberá ingresar.

Luego debe generar un nuevo build para actualizar su aplicación web en OpenShift. Para ello ejecute el siguiente comando:
oc start-build myapp

Puede visualizar los logs del proceso de construcción de la imagen (build) ejecutando el siguiente comando:
oc logs -f buildconfig.build.openshift.io/myapp

Una vez terminado el proceso anterior, verifique que la versión del BuildConfig se haya cambiado a 2, se haya generado un segundo un segundo pod del build y se haya actualizado el POD de la aplicación:

![alt text](images/build2.png?raw=true)


