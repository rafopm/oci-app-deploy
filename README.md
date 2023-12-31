# oci-app-deploy

1. Crear compartimento
   Identity & Security / Compartments
   
    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1b22bf2f-5c33-462f-9684-619dad48a610)
  
   Seleccionar Create Compartment

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/d92011b1-0153-452a-91a9-6e54ce0f6d18)

   Ingresar informacion necesaria y presionar el boton Create Compartment

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1d283e69-ba9e-4cdd-a8d9-7c83593cc9bd)

   
2. Crear usuario en la siguiente ruta: Identity / Domains / Default domain

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/759c2bf1-851f-4c5d-b235-a5da8e7028be)

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/0155a8b3-8d8f-411a-a812-974b7014c208)

   Crear usuario sin seleccionar grupo pues lo asignaremos posteriormente.
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/e67ff540-fa08-4de1-be09-08f4c51b2fb3)

3. Creamos un grupo

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1ab2f3fb-c6c6-4f1b-95ef-f6a70a0d43a3)


4. Asignamos permisos

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/c366e369-29a1-40fb-8f34-9ecda30388b8)

   Registramos el nombre y seleccionamos las opciones:

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/677b2fec-01bf-43b1-a1a0-69bc328e8fed)

   Luego seleccionamos el switch "Show manual editor" y corregimos la linea

   De:
   Allow group 'Default'/'DeveloperGroup' to manage compute-management-family in compartment Desarrollo

    A:
    Allow group 'Default'/'DeveloperGroup' to manage all-resources in compartment Desarrollo

   Modificamos políticas para permitir el acceso a shell del nuevo usuario o grupo:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/e4eb8404-e926-47fe-bf3f-4bc8ff76c0dd)

   Agregamos la siguiente sentencia (sin comillas de inicio y fin): "Allow group 'Default'/'DeveloperGroup' to use cloud-shell in tenancy"
   Recuerda que debes cambiar el nombre del grupo en caso el tuyo sea diferente
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/724d761a-6f6f-4915-8817-243d371fafd6)


5. Nos logueamos con el nuevo usuario. Generalmente no se tiene la contraseña inicial así que lo que queda es restablecer la contraseña y luego activar el login de 2 factores.

   
6. fdsf
   Seleccionamos Shell

   Creamos la carpeta .ssh con "mkdir .ssh"

   Accedemos a la carpeta con "cd .ssh/"
   
   Creamos la llave pública y privada:
   ssh-keygen -b 2048 -t rsa -f cloudshellkey

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1301562b-4a0f-4726-96fc-108402ede421)

   No ingresamos ninguna información cuando nos pide passphrase 
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/96e149fb-e2a8-4c27-a522-17bb4c588ef6)

   Escribimos "ls -a" para verificar que se hayan creado las keys, estas llaves nos servirán para hacer una conección de una forma segura y la utilizaremos más adelante.

7. Vamos a usar el asistente para crear una VCN

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/473ebc79-721e-4769-ab0a-a0f049daa74e)

   Dejamos los valores por defecto y creamos nuestra VCN
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/34a474b0-525d-434b-b151-37cf61d0dc0f)

8. Creamos una instancia:

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/570d7c34-16db-492e-a4aa-35bbda0f2e3d)

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/78dd0bf9-d12e-40dd-9799-8828b9529d9a)

   Colocamos el nombre y dejamos todos las opciones por defecto exepto el área en el que nos permite elegir la Key SSH
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/3c5854a5-2d35-43d4-994e-cfcf58bb9d04)

   Seleccionamos la opción: "Paste public keys" y abrimos el shell
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/77352b6c-8bb3-4b0f-8076-79f0acccd0de)

   Tener en cuenta que debes ubicarte dentro de la carpeta .shh

   Copiamos las dos líneas siguientes luego de escribir: "cat TUCLAVE.pub"
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/4b4e8f80-ee26-4cf4-92df-ed168c42860b)

   Finalmente seleccionamos el botón Create:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/6a4a7dc1-13f6-462e-b37c-a6534feb10e3)


   Finalmente ya tenemos creada nuestra instancia en la que unos de los datos más importantes es el número de IP y el usuario que por defecto es opc:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/af5c0b45-5763-4567-93a9-1bfccfccf30b)

   Abrimos shell y escribimos: "ssh opc@TUIPPUBLICA -i cloudshellkey" y luego escribimos "yes" cuando el sistema lo solicita
   Para confirmar que ya estamos dentro de la instancia podemos ver que la última línea tiene el nombre de nuestro usuario y podemos hacer un ping para conectarnos hacía afuera, por ejemplo: "ping www.google.com"

9. Ahora vamos a realizar algunas configuraciones para que podamos acceder desde internet a nuestra ip pública.
    Escribimos: "sudo yum -y install httpd"
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/fbfd8467-f011-4cca-b1b5-c68e776a905f)


   Vamos a agregar el puerto 80  al firewall:
   "sudo firewall-cmd --permanent --add-port=80/tcp"
   "sudo firewall-cmd --reload"
   "sudo systemctl start httpd"

   Agregamos un archivo para mostrar un html para mostrar en nuestra ip publica
   "sudo su"
   "echo "<h1>Hola Mundo</h1>" >> /var/www/html/index.html"

   Vamos a agregar una regla de entrada:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/a9b17806-59ea-4dde-ba9e-3c774ce48a04)

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/2016e63c-ab30-41ef-8649-50034a90e891)

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/a55e299e-9a7c-434d-bb27-eb8f71c9b8e9)

10. Crear Load Balancer

    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/a21601ac-8753-4df7-af22-740f8466007e)

    Antes de crear un Load Balancer creamos otra instancia con este objetivo, la creamos de la misma forma que lo hicimos anteriormente, copiando la key publica.

    La nueva instancia va a tener otra ip
     Abrimos shell y escribimos: "ssh opc@TUIPPUBLICA -i cloudshellkey" y luego escribimos "yes" cuando el sistema lo solicita

    Realizamos los mismos procedimientos para instalar httpd con:

   "sudo yum -y install httpd"

   Luego ejecutamos los siguientes comandos para que finalmente podamos probar la segunda instancia:
   sudo firewall-cmd --permanent --add-port=80/tcp
   
   sudo firewall-cmd --reload
   
   sudo systemctl start httpd
   
   Agregamos un archivo para mostrar un html para mostrar en nuestra ip publica
   sudo su
   
   echo "<h1>Hola Mundo 2</h1>" >> /var/www/html/index.html

   Deberias tener 2 instancias corriendo:
   
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1a0aa712-ddcc-4da9-8cde-7bbf49e198be)

   Como vamos a usar los recursos gratuitos lo dejamos todos como esta y solo seleccionamos nuestra VCN:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/aab3bbd6-558b-4db5-b12a-b6bf3cd0b1ae)

   Luego agregamos Backends y seleccionamos nuestras 2 instancias creadas previamente:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/e5d3816e-146f-4349-98fd-942b594e5456)

   Luego viene la configuracion de Listener y seleccionamos HTTP
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/a385ee2b-d69b-4d65-91c3-e469bf4c871d)

   En la seccion de logs dejamos las opciones por defecto:
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/40cc950e-145e-418f-b35b-73d710d4ef52)

   Con la ip publica podemos verificar que alterna el acceso a las dos instancias de forma alterna:

   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/923ba443-0216-4065-b97b-3df4591b45b4)



11. Creamos nuestra base de datos JSON
    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/c28e9c4e-105e-4dc5-8958-930a4317005c)

    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/2b56549b-d3c6-4055-b32e-960afc3b1bd2)

    Solo sera necesario colocar el nombre, las otras configuraciones las dejamos como esta para que se mantenga siempre gratis.

    Una vez creada la base de datos se debe seleccionar la opcion "View all database actions" para revisar las opciones disponibles:
    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/1a7fbc61-0497-4a2f-8074-a412bcd72d35)

    ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/874e6361-3a1a-4119-9332-8e8810e31583)


12. Ingresamos a shell con los datos de la primera instancia:
    "ssh opc@TUIPUBLICA -i .ssh/cloudshellkey"

    Instalamos GIT
    sudo dnf install git

   Clonamos una app de git
   git clone https://tuappengit

   Instalamos node, dependiendo de la version que corresponda a tu aplicacion
   
   sudo dnf install @nodejs:16


   Ingresamos a la carpeta de la aplicacion

   cd nombreDeLaCarpeta

   Instalamos dependencias:
   
   npm install

   Instalacmos InstantClient
   
   sudo dnf list installed | grep instantclient

   sudo dnf install oracle-instantclient-release-el8

   sudo dnf install oracle-instantclient-basic

   DEscargamos el Wallet

   Vamos a panel izquierdo -> Oracle DB -> Autonomous DB -> DoguitoDB -> DB Connection -> Download wallet -> pw=LaMismaDeLaDatabase -> Download


   Salimos del usuario loqueado con "exit"


   Cargamos el archivo de Wallet

   Panel superior izquierdo o engranaje en parte superior derecha de cloudshell -> Upload -> Cargamos archivo de wallet que acabamos de descargar -> Hide


   copiamos el archivo a la raiz de opc

   scp -i .ssh/cloudshellkey Wallet_devdb.zip opc@129.151.122.13:/home/opc


   accedemos nuevamente con el usuario opc

   ssh opc@TUIP -i .ssh/cloudshellkey

   verificamos que el archivo del wallet se copio correctamente

   ls

   copiamos el wallet a una ubicacion predeterminada
   
   sudo cp Wallet_*.zip /usr/lib/oracle/21/client64/lib/network/admin
   
  nos ubicamos en la carpeta

  cd /usr/lib/oracle/21/client64/lib/network/admin

  descomprimimos
  sudo unzip -B Wallet_algunnombre.zip


agregamos las variables de entorno

export DB_USER=ADMIN export DB_PASSWORD=tuclave export CONNECT_STRING=devdb_high


Agregamos el puerto 3000 para que reciba trafico

sudo firewall-cmd --permanent --add-port=3000/tcp


reiniciamos el firewall

sudo firewall-cmd --reload

Agregamos el puerto 3000 a security list

vm1 -> public subnet VCN1 -> Default security list -> Add ingress rule -> Source CDIR=0.0.0.0/0 -> Port=3000 -> Add rule


Iniciamos el proyecto

npm start

Iniciar el servicio que tiene la siguiente estructura
--------------------------------------------------------------------
[Unit]
Description=Doguito API Service
After=network.target

[Service]
Environment="DB_USER=ADMIN"
Environment="DB_PASSWORD=???"
Environment="CONNECT_STRING=???"
Type=simple
User=opc
ExecStart=/usr/bin/node /home/opc/doguito-api-es/bin/www
Restart=on-failure

[Install]
WantedBy=multi-user.target
---------------------------------------------------------

Modificamos el archivo si es necesario con:

vim doguito-api.service

Primero copiamos el archivo a donde corresponde

sudo cp doguito-api.service /lib/systemd/system

cd /lib/systemd/system

sudo systemctl daemon-reload

sudo systemctl status doguito-api.service

sudo systemctl start doguito-api.service

sudo systemctl enable doguito-api.service





   
   
    
    

    



    


   


   




    





   





