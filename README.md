## Realización de ejercicios para practicar

Use este conjunto de ejercicios para obtener experiencia práctica en Azure. Se requiere una suscripción a Azure individual para realizar las tareas del ejercicio. Para suscribirse, vaya a https://www.azure.microsoft.com/free.

https://learn.microsoft.com/es-mx/training/modules/network-security/1-introduction?source=learn

## Tarea 1: Grupos de seguridad de red

Esta tarea requiere una máquina virtual Windows asociada a un grupo de seguridad de red (NSG). El NSG debe tener una regla de seguridad de entrada que permita RDP. La máquina virtual debe estar en estado de ejecución y tener una dirección IP pública.

En esta tarea, revisaremos las reglas de red, confirmaremos que la página de IP pública no se muestra, configuraremos una regla de NSG entrante y confirmaremos que se muestra la página de la IP pública.


### Revisión de las reglas de red

1. En el Portal, vaya a su máquina virtual.

![image](https://user-images.githubusercontent.com/110675810/193300098-e328b4b2-d06c-409f-8f78-67adf7c4ce12.png)

2. En Configuración, haga clic en Redes.

![image](https://user-images.githubusercontent.com/110675810/193300209-39b58ac4-ffaa-4c43-884d-b32ac9d5e5d0.png)

3. Analice las reglas de entrada y salida predeterminadas.

![image](https://user-images.githubusercontent.com/110675810/193300289-1a41f79e-d048-4c7c-be42-639c8e6157ee.png)

4. Revise las reglas de entrada y asegúrese de que se permite RDP.

![image](https://user-images.githubusercontent.com/110675810/193300209-39b58ac4-ffaa-4c43-884d-b32ac9d5e5d0.png)

5. Anote la dirección IP pública.

IP pública de NIC: 20.169.55.26

### Conexión a la máquina virtual y prueba de la dirección IP pública

1. En el panel Información general, haga clic en Conectar y acceda mediante RDP a la máquina virtual.

![image](https://user-images.githubusercontent.com/110675810/193300684-c6633ea7-2904-4886-b990-9adec582587a.png)

2. En la máquina virtual, abra un explorador.

![image](https://user-images.githubusercontent.com/110675810/193304316-86994648-99d0-4575-af44-c87b6b664979.png)

3. Pruebe la página HTML predeterminada de IIS de localhost: http://localhost/default.htm. Debería aparecer esta página.

![image](https://user-images.githubusercontent.com/110675810/193305216-57dff120-46f1-44eb-8d43-03e7d95e9236.png)

4. Pruebe la página HTML predeterminada de IIS de la IP pública: http://public_IP_address/default.htm. Esta página no debe mostrarse.

![image](https://user-images.githubusercontent.com/110675810/193305935-067b6ec2-9b76-4420-93fe-87f368a2ec91.png)

### Configuración de una regla de entrada para permitir el acceso público en el puerto 80

1. Vuelva al Portal y a la hoja Redes.

![image](https://user-images.githubusercontent.com/110675810/193306081-d9af7441-4d5f-4d10-89ac-424d17db5765.png)

2. Anote la dirección IP privada de la máquina virtual.

IP privada de NIC: 10.0.0.4

3. En la pestaña Reglas de puerto de entrada, haga clic en Agregar regla de puerto de entrada. Esta regla solo permitirá ciertas direcciones IP en el puerto 80. A medida que avance por los valores de configuración, asegúrese de analizar cada uno de ellos.

- Origen: Etiqueta de servicio
- Etiqueta de servicio de origen: Internet
- Destino: Direcciones IP
- Intervalos de direcciones IP de destino y CIDR: private_IP_address/32
- Intervalo de puertos de destino: 80
- Protocolo: TCP
- Acción: Permitir
- Nombre: Allow_Port_80
- Haga clic en Agregar.

![image](https://user-images.githubusercontent.com/110675810/193306667-5d79fae0-6799-42e9-80e0-455cef719489.png)

4. Espere a que se agregue la nueva regla de entrada.

![image](https://user-images.githubusercontent.com/110675810/193306944-af500eeb-7f01-4e3c-87d0-55c907f39464.png)

### Nueva prueba de la dirección IP pública

1. En la máquina virtual, vuelva al explorador.

![image](https://user-images.githubusercontent.com/110675810/193307310-dfdfca10-7555-48fa-8eab-b8bbdb2f8d79.png)

3. Actualice la página HTML predeterminada de IIS de la IP pública: http://public_IP_address/default.htm. Ahora debería verse esta página.

![image](https://user-images.githubusercontent.com/110675810/193307250-37cc14a5-70c2-4029-97fc-c173af5850b0.png)


## Tarea 2: Grupos de servicios de aplicaciones
Esta tarea requiere una máquina virtual de Windows con IIS instalado. En estos pasos se usa VM1. El nombre de su máquina puede ser diferente.

En esta tarea, nos conectaremos a una máquina virtual, crearemos una regla de denegación de entrada, configuraremos un grupo de seguridad de aplicaciones y probaremos la conectividad.

### Conexión a la máquina virtual

1. En el Portal, vaya a VM1.

![image](https://user-images.githubusercontent.com/110675810/193316044-131f88ce-daed-4f07-a1d6-968aeae55641.png)

2. En la hoja Redes, anote la dirección IP privada.

IP privada de NIC: 10.0.0.4

3. Asegúrese de que hay una regla de puerto de entrada que permite RDP.

![image](https://user-images.githubusercontent.com/110675810/193316127-f119d80b-0f4a-4395-8f02-01089bde2033.png)

4. En la hoja Información general, asegúrese de que VM1 esté en ejecución.

![image](https://user-images.githubusercontent.com/110675810/193321425-b41e18d4-9ae4-49ae-b177-80b86499ca53.png)

5. Haga clic en Conectar y acceda mediante RDP a VM1.

6. En VM1, abra un explorador.

7. Asegúrese de que se muestra la página predeterminada de IIS para la dirección IP privada: http://private_IP_address/default.htm.

![image](https://user-images.githubusercontent.com/110675810/193321740-4eb7d809-5178-4e36-8b9f-7bc6edd4292e.png)

### Adición de una regla de denegación de entrada y prueba de la regla

1. Continúe en el Portal desde la hoja Redes.

![image](https://user-images.githubusercontent.com/110675810/193322030-7e0ab676-4120-4873-b99b-35cc6d558bcf.png)

2. En la pestaña Reglas de puerto de entrada, haga clic en Agregar regla de puerto de entrada. Agregue una regla que deniegue todo el tráfico entrante.

- Intervalos de puertos de destino: *
- Acción: Denegar
- Nombre: Deny_All
- Haga clic en Agregar.
- Espere a que se agregue la nueva regla de entrada.

![image](https://user-images.githubusercontent.com/110675810/193322328-72b6b5de-76b2-4cbe-a73e-b2a456e4ac54.png)

![image](https://user-images.githubusercontent.com/110675810/193324961-2a05bab1-ec1a-4992-83b6-de02c6ac03a3.png)

3. En VM1, actualice la página del explorador:

4. Compruebe que la página no se muestra.

![image](https://user-images.githubusercontent.com/110675810/193325400-f6fb8ddb-3396-4fc8-a964-d942e421d7cf.png)

### Configuración de un grupo de seguridad de aplicaciones

1. En el Portal, busque y seleccione Grupos de seguridad de aplicaciones.

![image](https://user-images.githubusercontent.com/110675810/193328465-524b21c6-0c71-4714-8d5b-bc64be9877cb.png)

2. Cree un nuevo grupo de seguridad de aplicaciones.

3. Proporcione la información necesaria: suscripción, grupo de recursos, nombre y región.

![image](https://user-images.githubusercontent.com/110675810/193328791-3530b29a-1f29-4ee1-bb12-01f309378dd8.png)

4. Espere a que se implemente el grupo.

![image](https://user-images.githubusercontent.com/110675810/193329016-211bfa59-e819-4d46-981d-698837bb7825.png)

5. En el Portal, vuelva a VM1.

6. En la hoja Redes, seleccione la pestaña Grupos de seguridad de aplicaciones.

![image](https://user-images.githubusercontent.com/110675810/193329151-75c9e639-f8e9-4295-886d-b8bdbb210878.png)

7. Haga clic en Configurar grupos de seguridad de aplicación.

![image](https://user-images.githubusercontent.com/110675810/193332710-b4e5b5b1-a905-4bfd-9e42-6038eb5df447.png)

8. Seleccione el nuevo grupo de seguridad de aplicaciones y guarde los cambios.

![image](https://user-images.githubusercontent.com/110675810/193332818-8cd6b142-7c30-4b29-ba18-6bf30cfd7216.png)

9. En la pestaña Reglas de puerto de entrada, haga clic en Agregar regla de puerto de entrada. De este modo, se permitirá el grupo de seguridad de aplicaciones.

- Origen: grupo de seguridad de aplicaciones
- Grupo de seguridad de aplicaciones de origen: your_ASG
- Destino: Direcciones IP
- Direcciones IP de destino: private_IP_address/32
- Intervalo de puertos de destino: 80
- Prioridad: 250
- Nombre: Allow_ASG
- Haga clic en Agregar.

![image](https://user-images.githubusercontent.com/110675810/193333271-d10db3dc-4642-4cbb-9b4d-3180677c59f5.png)

10. Espere a que se agregue la nueva regla de entrada.

![image](https://user-images.githubusercontent.com/110675810/193333377-7a067306-18ba-40ca-9216-465d91e63f20.png)

### Prueba del grupo de seguridad de aplicaciones

1. En VM1, actualice la página del explorador:

2. Compruebe que ahora se muestra la página.

![image](https://user-images.githubusercontent.com/110675810/193341196-4db428de-b4a6-428f-8d0d-29df3bac670b.png)

