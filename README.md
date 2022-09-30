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
