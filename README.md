# Net Practice

## Introducción a las Redes

En términos simples, una red en informática es un conjunto de dos o más dispositivos que pueden comunicarse entre sí. Por comunicación nos referimos a la posibilidad de enviar y recibir datos (o paquetes) entre diferentes dispositivos (o nodos).

Internet es uno de los muchos ejemplos de red. Probablemente sea la red más grande del mundo y conecta muchos nodos diferentes, permitiendo la compartición de datos entre dispositivos ubicados en cualquier parte del planeta.

Internet se considera una **Red Pública**. Una Red Pública permite la transferencia de datos entre cualquier dispositivo conectado a ella, con poco o ningún control de acceso. Generalmente, es operada por una compañía de telecomunicaciones con el propósito específico de proporcionar servicios de transmisión de datos al público.

Por otro lado, también existen las **Redes Privadas**. Una Red Privada permite la comunicación entre dispositivos que están restringidos a una ubicación o dominio específico. La transferencia de datos no está permitida para usuarios no registrados, creando un entorno mucho más seguro y controlado. Un ejemplo de red privada es la **Red Doméstica**. En ella, puedes conectarte a tu impresora personal mientras que nadie que no esté conectado al Wi-Fi de tu casa podría hacerlo.

## ¿Qué es TCP y la Dirección IP?

Para transferir datos de un punto a otro a través de una red, existen muchos tipos diferentes de **protocolos** que aseguran el acceso, transporte, seguridad y estabilidad. Todos estos protocolos trabajan juntos, cada uno responsable de lo que llamamos una "capa" en el proceso de comunicación.

**Transmission Control Protocol (TCP)** es un protocolo de comunicación estándar que permite que los nodos se comuniquen entre sí. TCP se encarga de "dividir" los datos en pequeñas piezas (o paquetes), enviarlos a través de la red y luego "reconstruirlos" de nuevo, asegurando que no se pierda información en el proceso.

¿Y cómo sabe TCP a dónde enviar estos paquetes? Lo hace utilizando una **Dirección de Protocolo de Internet (IP)**, que es una serie de números usada para identificar cualquier dispositivo conectado a una red, ya sea pública o privada.

TCP e IP **no son lo mismo**, sino dos protocolos separados que trabajan juntos para asegurar la transferencia de datos entre diferentes dispositivos.

Existen dos versiones diferentes de Direcciones IP: **IPv4** e **IPv6**. Para el propósito de este proyecto, solo necesitamos conocer IPv4, el modelo de protocolo más antiguo y ampliamente utilizado. A partir de ahora, en esta guía, utilizaremos los términos **IP** e **IPv4** de manera intercambiable.

## Ejemplos de Direcciones IP y Máscaras de Subred

Veamos un ejemplo práctico:

```bash
IP Address:		153.172.250.12
Subnet Mask:	255.255.255.0
CIDR:			/24
```

En binario, tendríamos:

```bash
IP Address:		10011001.10101100.11111010.00001100
Subnet Mask:	11111111.11111111.11111111.00000000
```

De acuerdo con la máscara, los primeros 24 bits se consideran parte de la Dirección de Red. Eso significa que los primeros 24 bits de la Dirección IP representan la Dirección de Red.

```bash
Network Address:	10011001.10101100.11111010.????????
or:					153.172.250.?
IP/CIDR:			153.172.250.12/24
```

En términos prácticos, podemos decir que cualquier dispositivo con IPs que van desde 153.172.250.0 hasta 153.172.250.255 pertenece a la misma red y, por lo tanto, puede comunicarse entre sí libremente.

```bash
IP Address:		153.172.175.12
Subnet Mask:	255.255.240.0
CIDR:			/20
```

Otro ejemplo con máscara diferente

```bash
IP Address:		153.172.175.12
Subnet Mask:	255.255.240.0
CIDR:			/20
```

En binario:

```bash
IP Address:		10011001.10101100.10101111.00001100
Subnet Mask:	11111111.11111111.11110000.00000000
```

Ahora, los primeros 20 bits son la Dirección de Red:

```bash
Network Address:	10011001.10101100.1010????.????????
or:					153.172.(160-175).(0-255)
IP/CIDR:			153.172.175.12/20
```

En la práctica, cualquier dispositivo con IPs de 153.172.160.0 a 153.172.175.255 pertenece a la misma red y puede comunicarse libremente.

### Nota importante sobre las máscaras

Cuando leemos la máscara de red de izquierda a derecha, una vez que aparece un cero, los bits restantes deben completarse con ceros.

Por ejemplo, 255.255.240.0 es válida, pero 255.255.240.128 no lo es.

Solo existen nueve posibles valores para un bloque de 8 bits en la máscara:

```bash
0 0 0 0 0 0 0 0 ->	0 
1 0 0 0 0 0 0 0 ->	128
1 1 0 0 0 0 0 0 ->	192
1 1 1 0 0 0 0 0 ->	224
1 1 1 1 0 0 0 0 ->	240
1 1 1 1 1 0 0 0 ->	248
1 1 1 1 1 1 0 0 ->	252
1 1 1 1 1 1 1 0 ->	254
1 1 1 1 1 1 1 1 ->	255
```

Direcciones reservadas en cada subred

Al dividir una red grande en subredes más pequeñas, debemos reservar 2 IPs que no pueden usarse en dispositivos:

Primera IP de la subred: identifica la subred.

Última IP de la subred: usada para enviar mensajes de broadcast a todos los dispositivos de la subred.

Por ejemplo, en la primera red /24 (153.172.250.0/24):

IPs reservadas: 153.172.250.0 y 153.172.250.255

IPs disponibles para dispositivos: 153.172.250.1 a 153.172.250.254

⚠️ Esto significa que debemos elegir cuidadosamente la máscara de red según la cantidad de dispositivos que queremos conectar a nuestra red.

## Conexión de Múltiples Dispositivos

Como se mencionó anteriormente, las **Redes Públicas**, como Internet, son establecidas por proveedores de telecomunicaciones con el objetivo de **conectar dispositivos de todo el mundo**.

Una **Dirección IP Pública** es asignada por tu **Proveedor de Servicios de Internet (ISP)** directamente a tu router personal, y permite la conectividad hacia tu red privada personal.

Tu **red privada** se establece mediante un **switch** ubicado dentro del router proporcionado por tu ISP. El router se encarga de asignar **Direcciones IP Privadas** a cada dispositivo conectado a tu red privada, siguiendo las reglas previamente mencionadas sobre máscaras de subred y rangos de IPs.

Existen algunas **Direcciones IP reservadas** para usos específicos. Por lo tanto, al asignar una IP dentro de una red conectada a Internet, debes prestar atención a la siguiente lista:

### Direcciones IP Reservadas

A continuación se muestran los rangos de Direcciones IP que están reservadas para usos específicos:

| Rango de Dirección IP | Uso Reservado |
|----------------------|---------------|
| 10.0.0.0 - 10.255.255.255 | Reservadas para IPs privadas (Clase A) |
| 127.0.0.0 - 127.255.255.255 | Reservadas para loopback y pruebas internas |
| 172.16.0.0 - 172.31.255.255 | Reservadas para IPs privadas (Clase B) |
| 192.168.0.0 - 192.168.255.255 | Reservadas para IPs privadas (Clase C) |
| 224.0.0.0 – 239.255.255.255 | Reservadas para multicast |
| 240.0.0.0 – 255.255.255.255 | Reservadas para uso experimental e investigación |

## Switch, Router y Tabla de Enrutamiento

### Switch
Un **switch de red** es responsable de **distribuir paquetes entre dispositivos dentro de la misma red**, usualmente una red local (**LAN**).  
Un switch **no tiene interfaces** para comunicarse con redes externas y **no puede conectarse a redes fuera de la suya propia**.

---

### Router
Un **router** es responsable de **conectar múltiples redes entre sí**. Cada router tiene **una interfaz para cada red** a la que está conectado.

Dado que conecta varias redes, el **rango de IPs de una interfaz nunca debe superponerse con el rango de otra interfaz**.  
Si hubiera superposición de rangos, significaría que las interfaces pertenecen a la misma red, lo cual genera conflictos de enrutamiento.

---

### Tabla de Enrutamiento
Una **Tabla de Enrutamiento** es una tabla de datos almacenada en un router o en un host de red que lista todas las rutas hacia una **destinación de red particular**.

En *Net Practice*, una tabla de enrutamiento consiste en **solo dos informaciones básicas**:

1. **Destino (izquierda):**  
   La dirección IP a la que deseas enviar un paquete, combinada con el **CIDR** de esa red.  
   Ejemplo: `190.3.2.252/30`.  
   Si no quieres especificar un destino particular, o quieres que la ruta sea válida para **toda la red**, puedes usar `default` o `0.0.0.0/0`.

2. **Siguiente Salto / Next Hop (derecha):**  
   La dirección IP del **siguiente router** al que debes enviar los paquetes para alcanzar la red de destino.
