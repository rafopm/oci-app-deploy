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

   Agregamos la siguiente sentencia: Allow group 'Default'/'DeveloperGroup' to use cloud-shell in tenancy
   Recuerda que debes cambiar el nombre del grupo en caso el tuyo sea diferente
   ![image](https://github.com/rafopm/oci-app-deploy/assets/5562967/724d761a-6f6f-4915-8817-243d371fafd6)




6. Nos logueamos con el nuevo usuario. Generalmente no se tiene la contraseña inicial así que lo que queda es restablecer la contraseña y luego activar el login de 2 factores.

   
4. fdf
