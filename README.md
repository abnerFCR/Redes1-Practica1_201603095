# Manual de Configuración. 
Redes de Computadoras 1 - Practica 1

## Topología de Red

La topología que se implemento en esta práctica esta compuesta por:

1. **VPC**
2. **Switch**
3. **Router**
4. **Maquina Virtual**

### Configuración de Topología

En cuanto a la distribución de los equipos, las 2 interfaces del router se conectaron cada una a un switch, y en este a su vez se conectaron, en uno 2 VPC y en otro una VPC y una máquina virtual.

Las conexiones entre los equipos estan dadas de la siguiente forma. 

|Tipo de Host     |Nombre       | Conectado a       |Puerto/Interfaz  |
| --------------- | ----------- | ----------------- |---------------- |
|Máquina Virtual  |TinyLinuxVM-1|SW1-Ethernet2      |Ethernet0        |
|VPC              |PC2          |SW1-Ethernet1      |Ethernet0        |
|VPC              |PC3          |SW2-Ethernet1      |Ethernet0        |
|VPC              |PC4          |SW2-Ethernet2      |Ethernet0        |
|Switch           |SW1          |R1-FastEthernet 0/0|Ethernet0        |
|Switch           |SW1          |R1-FastEthernet 0/1|Ethernet0        |

Las configuraciones del router (tanto la dirección de red como la dirección ip de cada interfaz), se detalla en la siguiente tabla:

|Interfaz          |Dirección de Red |Direccion IP   |
| ---------------- | --------------- |-------------- |
|FastEthernet 0/0  |192.168.15.0/24  |192.168.15.254 |
|FastEthernet 0/1  |192.168.19.0/24  |192.168.19.254 |


En los host se implementaron las siguientes configuraciones:

|Tipo de Host     |Nombre       | Conectado a |Direccion IP  |
| --------------- | ----------- | ----------- |------------- |
|Máquina Virtual  |TinyLinuxVM-1|SW1          |192.168.15.30 |
|VPC              |PC2          |SW1          |192.168.15.15 |
|VPC              |PC3          |SW2          |192.168.19.15 |
|VPC              |PC4          |SW2          |192.168.19.30 |


Dando como resultado la topología de la siguiente forma:  

-
![image](https://user-images.githubusercontent.com/37676214/90329964-7f159300-df66-11ea-833b-db57e1dc1ce1.png)

## Configuracion de los Equipos

### VPC

Colocar una VPC y posteriormente configurarla se realizan los siguiente pasos:

 1. Se toma selecciona una imagen de VPC entre los dispositivos. 
 2. Se arrastra el dispositivo al area de trabajo.
 3. Se enciende (Click derecho -> Start).
 4. Se entra a la terminal del dispositivo (Click derecho -> Console).
 
Una vez en el terminal del dispositivo se siguen los siguientes pasos.

 1. Se le asigna una dirección IP al dispositivo, con su respectiva mascara de subred. 
```sh
# ip [direccion/mascara gateway]
```
 2. Se salvan los cambios.
```sh
# save
``` 
 3. Opcionalmente se puede visualizar si la dirección ip.
```sh
# show ip
```
 
#### Configuración de PC2

Siguiendo el algoritmo anterior dispositivo PC2 se configuró de la siguiente forma.

-
![image](https://user-images.githubusercontent.com/37676214/90329944-4fff2180-df66-11ea-97a3-f006c77e1b93.png)

#### Configuración de PC3

Siguiendo el algoritmo anterior dispositivo PC3 se configuró de la siguiente forma.

-
![image](https://user-images.githubusercontent.com/37676214/90329993-c00da780-df66-11ea-9ae2-73372043ae2f.png)

#### Configuración de PC4

Siguiendo el algoritmo anterior dispositivo PC4 se configuró de la siguiente forma.

-
![image](https://user-images.githubusercontent.com/37676214/90330039-06fb9d00-df67-11ea-8835-76076c9bd450.png)


### Configuración de la maquina virtual.

Para configurar la maquina virtual se sigue el siguiente algoritmo. 

1. Se enciende el dispositivo (Click derecho -> Start).

Nota: Esta maquina virtual debe haber sido creada previamene en VMWare o en VirtualBox y haber sido importada a GNS3.

2. Una vez encendida la maquina virtual, vamos a su configuración.

3. Abrimos Panel de control.
-
![image](https://user-images.githubusercontent.com/37676214/90329539-efbab080-df62-11ea-8366-35f1ca94eed2.png)

4. Abrimos Network
-
![image](https://user-images.githubusercontent.com/37676214/90329552-0fea6f80-df63-11ea-84f8-9efe2cf8f57a.png)

5. Ingresamos la configuración correspondiente. 

6. Damos click donde dice aplicar. 
-
![image](https://user-images.githubusercontent.com/37676214/90329568-34dee280-df63-11ea-9bd0-3ef3e875ab56.png)

7. Cerramos.

8. Opcional
- Verificamos la configuración el siguiente comando la terminal.
```sh
$ ifconfig
``` 
-
![image](https://user-images.githubusercontent.com/37676214/90329589-65bf1780-df63-11ea-8216-71a9661e9f3b.png)

### Configuración del Router

Para configurar el router, se sigue el siguente algoritmo.

1. Se arrasta el router al area de trabajo.
2. Se enciende (Click derecho -> Start).
3. Se entra al terminal (Click derecho -> console).
4. Se entra a modo privilegiado en el router.

```sh
R1 > enable
``` 

5. Opcionalmente podemos visualizar un resumen de la interfaz ip. 

```sh
R1# show ip interface brief
``` 
Obteniendo el siguiente resultado. 

-
![image](https://user-images.githubusercontent.com/37676214/90330100-88532f80-df67-11ea-8b2d-c79676b6993b.png)

6. Procedemos a ingresar en la configuración del router.

```sh
R1# configure terminal
``` 

7. Configuramos la interfaz.

```sh
R1(config)# int fastethernet 0/0
``` 

8. Insertamos la dirección IP que tendrá ese puerto.

```sh
R1(config-if)# ip address 192.168.15.254 255.255.255.0
``` 

9. Configuramos la velocidad de la interfaz.

```sh
R1(config-if)# speed auto 
``` 

10. Coguramos el modo full-duplex de la interfaz.

```sh
R1(config-if)# full-duplex
``` 

11. Encendemos la interfaz.

```sh
R1(config-if) # no shutdown
``` 

12. Salimos de la configuracion de la interfaz.

```sh
R1(config-if)# exit 
``` 

13. Repetimos del paso 7 al 12 con los siguientes valores
-Interfaz: FastEthernet 0/1 
-IP:       192.168.19.254.

14. Salimos de la configuracion del Router

```sh
R1(config)# exit 
``` 

15. Guardamos los cambios.

```sh
R1# write memory 
``` 

15. Verificamos que la configuracion este bien.  

```sh
R1# show ip interface brief
``` 
Si todo esta bien el router deberia tener este resumen de interfaz ip. 

-
![image](https://user-images.githubusercontent.com/37676214/90330150-cc463480-df67-11ea-9ba8-4af0c6ca0d2d.png)



### Verificando Conexiones

Una vez, conectado y configurado de la forma anteriormente descrita, las configuraciones ya nos deberian permitir la comunicacion entre todas las maquinas, Esto se puede corroborrar haciendo ping desde la terminal de cualquier host hacia cualquiera de las direcciones ip de los demás. 

#### TinyLinuxVM-1

- ![image](https://user-images.githubusercontent.com/37676214/90330887-75435e00-df6d-11ea-9810-86b9706126a5.png)
- ![image](https://user-images.githubusercontent.com/37676214/90330896-90ae6900-df6d-11ea-85bf-8e46ee78baa9.png)


#### PC2 

- ![image](https://user-images.githubusercontent.com/37676214/90330790-c9017780-df6c-11ea-9caf-c95dd13d718a.png)

#### PC3

- ![image](https://user-images.githubusercontent.com/37676214/90330801-dcacde00-df6c-11ea-9221-fb9d3fd0e730.png)

#### PC4

- ![image](https://user-images.githubusercontent.com/37676214/90330813-f2ba9e80-df6c-11ea-8c61-754650a731fa.png)


## Glosario

1. VPC: Es un ordenador virtual que funciona como el punto de inicio y final de las transferencias de datos. Estos poseen una única dirección IP que puede ser asignada manualmente o asignada automáticamente.

2. Router: es un dispositivo que permite interconectar computadoras que funcionan en el marco de una red. Su función: se encarga de establecer la ruta que destinará a cada paquete de datos dentro de una red informática. 

3. Switch: también llamado conmutador es el dispositivo digital lógico de interconexión de equipos que opera en la capa de enlace de datos del modelo OSI.

4. Dirección IP: es un conjunto de números que identifica, de manera lógica y jerárquica, a una Interfaz en la red de un dispositivo que utilice el protocolo o, que corresponde al nivel de red del modelo TCP/IP.

5. Interfaz de red: es una interfaz de software o hardware entre dos equipos o capas de protocolo en una red informática. Una interfaz de red generalmente tendrá algún tipo de dirección de red.

6. Host: este termino se usa en informática para referirse a las computadoras u otros dispositivos conectados a una red que proveen y utilizan servicios de ella.

7. Maquina virtual: es un software que simula un sistema de computación y puede ejecutar programas como si fuese una computadora real. 

8. Topología de red: se define como el mapa físico o lógico de una red para intercambiar datos. En otras palabras, es la forma en que está diseñada la red, sea en el plano físico o lógico. El concepto de red puede definirse como «conjunto de nodos interconectados».

9. Gateway: la pasarela o puerta de enlace es el dispositivo que actúa de interfaz de conexión entre aparatos o dispositivos, y también posibilita compartir recursos entre dos o más ordenadores. Su propósito es traducir la información del protocolo utilizado en una red inicial, al protocolo usado en la red de destino. 

10. Mascara de red: es una combinación de bits que sirve para delimitar el ámbito de una red de ordenadores. Su función es indicar a los dispositivos qué parte de la dirección IP es el número de la red, incluyendo la subred, y qué parte es la correspondiente al host.
