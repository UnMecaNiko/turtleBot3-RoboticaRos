
# Primeras configuraciones

## PC Setup

> Verifficar siempre que se siguen las instrucciones para ROS Noetic
En el pc se debe instalar ROS NOETIC, todos los pasos están en el primer link de las fuentes de información.

### Trabajo en laboratorio

En red cel de nico:

ip de trutlebot:
ipaddress = '192.168.43.126'

ip de pcRemote:  192.168.43.154

ip de 3B+ nico: 192.168.43.234

nombre de red : habitacion97

constraseña : contrasena

Configurar archivos ~/.bashrc

![configuracion de ips](https://emanual.robotis.com/assets/images/platform/turtlebot3/software/network_configuration.png)


### Trabajo en nitrolas linux

ip de pcRemote:  192.168.0.13

ip de trutlebot: 192.168.0.12


## Paquetes y depenencias en el turtlebot

Se deben seuir todos los pasos de la guía, tnato los de la secciń SBC tup, como los de OpenCR setup


## Bring up

Los siguientes comando son necesarios cada vez que se requiera iniciar el robot, se debe tener en cuenta que ya se debe contar con la raspberry pi conectada 
//(contraseña: turtlebot)
```bash
ssh ubuntu@192.168.0.12
```
si la ip del turtlebot cambia no es necesario hacer cambios en el pc
los cambios se deben hacer en el móvil

En turtlebot a través de ssh:
```bash
sudo nano ~/.bashrc
source ~/.bashrc
```
Si ya están configuradas las ips se puede hacer el bringup
```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_bringup turtlebot3_robot.launch
```
en pc remote
```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Luego, para operar el robot con el teclado
```bash 
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

Los comando que sí permiten el uso del Lidar son:
(en burger) se deben iniciar dos ventanas de comandos, desde remote pc, dos conexiones ssh
```bash
roslaunch turtlebot3_bringup turtlebot3_core.launch
roslaunch turtlebot3_bringup turtlebot3_lidar.launch
```

# Conexión con matlab

[*source*](https://la.mathworks.com/help/ros/ug/get-started-with-a-real-turtlebot.html)

Para este método se debe configurar las dos opciones de ip en la turtlebot como su propia ip:

en el archivo '~/.bashrc'

ROS_MASTER_URI=http://IP_OF_TURTLEBOT:11311
ROS_HOSTNAME=IP_OF_TURTLEBOT

Accedemos por ssh y ejecutamos en el turtlebot:
```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_bringup turtlebot3_core.launch
roslaunch turtlebot3_bringup turtlebot3_lidar.launch
```

Las toolbox de ROS y de support turtlebot deben ser instaladas

en MATLAB
```matlab
ipaddress = 'IP_OF_TURTLEBOT'
tbot = turtlebot(ipaddress,11311); %192.168.43.126
tbot.Velocity.TopicName = '/cmd_vel';
setVelocity(tbot,0.25,0,'Time',0.1)
```

para desconectar:
```matlab
clear tbot %elimina todas las variables
rosshutdown
```

#Tuturial de uso paso a paso

Al momento de hacer uso del robot por pirmera vez se tiene que seguir los siguientes pasos para configurar la red a la cual elo robot se va a conectar

1. Conectar el robot via hdmi a una pantalla para realizar la configuracion inicial
2. Ingresar al robot
    Usuario: ubuntu
    Contraseña: turtlebot
3. ingresar al archivo bash con el siguiente comando
    sudo nano /etc/netplan/50-cloud-init.yaml
4. colocar el nombre de la red y la contraseña como se ve en la imagen

//falta colocar la imagen

5. salir del archivo y guardar los cambios hechos

En siguiente lugar para comenzar a hacer uso del robot se puede hacer la conexion desde otro dispositivo (computador) conectado a la misma red que el robot a traves del comando ejecutado desde un cmd o un powershell

```bash
ssh ubuntu@192.168.__.___
```
donde la direccion ip que esta colocada luego del simbolo @ es la ip de la red

Con esto se ingresara usuario y contraseña del robot y se tendra acceso al robot

Y para finalizar la configuracion del robot y tener uso de ete via matlab se accedera al archvio bas con el siguiente comando:

```bash
sudo nano ~/.bashrc
```

donde en las ultimas lineas del archivo se encontrara dos direcciones ip las cuales se les colocara la misma direccion ip de la red a la que esta conectado el robot, se saldra del archivo guardando los cambios y se ejecutara el siguiente comando para que active los cambios de las direcciones ip.

```bash
source ~/.bashrc
```

Finalmente para ya activar el funcionamiento del robot se colocaran los siguientes dos comandos:

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_bringup turtlebot3_core.launch
```

Y con esto se termina la configuracion del robot para uso a traves de matlab.

#Modo de uso a traves de matlab

Inicialmente es importante tener las librerias correspndientes a ros y al turtulebot en si las cuales se encuentran en el Add-Ons de matlab 

En siguiente lugar se creara un objeto de tipo turtlebot con la siguiente funcion y se le activara asi mismo el movimiento con las siguientes lineas de codigo.

```bash
tbot = turtlebot(ipaddress)
tbot.Velocity.TopicName = '/cmd_vel';
```

y ya con esto creado solo queda movier el robot con la siguiente linea de codigo de forma que se le dara la velocidad lineal, angular y tiempo del movimiento

```bash
setVelocity(tbot, VelocidadLineal, VelocidadAngular, 'Time', Tiempo);
```

# Issues

## La red WIFI no funciona

Cuando ya se haya instalado la imagen en la micro sd card puede que el wifi no funcione:

Para esto primero se verifica si el módulo está deshabilitado y se reinicia
```bash
sudo lshw -C network
sudo ifconfig wlan0 down
sudo ifconfig wlan0 up
```
También es útil probar con:
```bash
sudo nmcli networking off
sudo nmcli networking on
```

## No se puede instalar una toolbox en matlab linux

`sudo chown -R <username>:<username> /usr/local/MATLAB/R***`

## instalamos mal una versión de ROS o hay un problema con la versión

Para desinstalar todo:
```bash
sudo apt-get purge ros-*
sudo apt-get autoremove

sudo nano ~/.bashrc
```
Se borra todo registro de ROS

## Problemas al instalar ROS en WSL

Luego de desinstalar ROS:

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
```

Luego, desintalar conda, si se ha instalado

Luego se sigue con instalación normal **NOETIC**

> No he podido instalar esta distribución en mi pc

# Tips

- Si deseas saber la versión de tu ubuntu: `lsb_release -a`

# Fuentes de información

- [Quick start guide TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)
- [Ubuntu install of ROS Noetic](http://wiki.ros.org/noetic/Installation/Ubuntu)
- [Get Started with a Real TurtleBot](https://la.mathworks.com/help/ros/ug/get-started-with-a-real-turtlebot.html)
- [Communicate with the TurtleBot](https://la.mathworks.com/help/ros/ug/communicate-with-the-turtlebot.html)
- [Explore Basic Behavior of the TurtleBot](https://la.mathworks.com/help/ros/ug/explore-basic-behavior-of-the-turtlebot.html)
- [Control the TurtleBot with Teleoperation](https://la.mathworks.com/help/ros/ug/control-the-turtlebot-with-teleoperation.html)
- [Obstacle Avoidance with TurtleBot and VFH](https://la.mathworks.com/help/ros/ug/obstacle-avoidance-with-turtlebot-and-vfh.html)
- [Uninstalling Anaconda Distribution](https://docs.anaconda.com/anaconda/install/uninstall/)
- [ROS Toolbox Support Package for TurtleBot-Based Robots](https://la.mathworks.com/help/supportpkg/turtlebotrobot/index.html)
- [Create a UI for TurtleBot](https://la.mathworks.com/help/supportpkg/turtlebotrobot/ug/create-a-ui-for-turtlebot.html)
