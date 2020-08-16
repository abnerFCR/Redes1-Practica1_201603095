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
|Máquina Virtual  |TinyLinuxVM-1|SW1          |192.168.15.15 |
|VPC              |PC2          |SW1          |192.168.15.30 |
|VPC              |PC3          |SW2          |192.168.19.30 |
|VPC              |PC4          |SW2          |192.168.19.15 |


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
# ip [direccion/mascara]
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

Una vez, conectado y configurado de la forma anteriormente descrita, 





