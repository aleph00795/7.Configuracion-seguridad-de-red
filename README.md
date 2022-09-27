## Realización de ejercicios para practicar

Use este conjunto de ejercicios para obtener experiencia práctica en Azure. Se requiere una suscripción a Azure individual para realizar las tareas del ejercicio. Para suscribirse, vaya a https://www.azure.microsoft.com/free.

https://learn.microsoft.com/es-mx/training/modules/network-security/1-introduction?source=learn

## Tarea 1: Grupos de seguridad de red

Esta tarea requiere una máquina virtual Windows asociada a un grupo de seguridad de red (NSG). El NSG debe tener una regla de seguridad de entrada que permita RDP. La máquina virtual debe estar en estado de ejecución y tener una dirección IP pública.

En esta tarea, revisaremos las reglas de red, confirmaremos que la página de IP pública no se muestra, configuraremos una regla de NSG entrante y confirmaremos que se muestra la página de la IP pública.

### Revisión de las reglas de red

En el Portal, vaya a su máquina virtual.
En Configuración, haga clic en Redes.
Analice las reglas de entrada y salida predeterminadas.
Revise las reglas de entrada y asegúrese de que se permite RDP.
Anote la dirección IP pública.

### Conexión a la máquina virtual y prueba de la dirección IP pública

En el panel Información general, haga clic en Conectar y acceda mediante RDP a la máquina virtual.
En la máquina virtual, abra un explorador.
Pruebe la página HTML predeterminada de IIS de localhost: http://localhost/default.htm. Debería aparecer esta página.
Pruebe la página HTML predeterminada de IIS de la IP pública: http://public_IP_address/default.htm. Esta página no debe mostrarse.

### Configuración de una regla de entrada para permitir el acceso público en el puerto 80

1. Vuelva al Portal y a la hoja Redes.

2. Anote la dirección IP privada de la máquina virtual.

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

4. Espere a que se agregue la nueva regla de entrada.

### Nueva prueba de la dirección IP pública

1. En la máquina virtual, vuelva al explorador.
2. Actualice la página HTML predeterminada de IIS de la IP pública: http://public_IP_address/default.htm. Ahora debería verse esta página.
