
# Primeras configuraciones

## PC Setup

> Verifficar siempre que se siguen las instrucciones para ROS Noetic
En el pc se debe instalar ROS NOETIC, todos los pasos están en el primer link de las fuentes de información.

### Trabajo en laboratorio


ip de trutlebot: 192.168.43.126

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
(el burger)
```bash
roslaunch turtlebot3_bringup turtlebot3_core.launch
roslaunch turtlebot3_bringup turtlebot3_lidar.launch
roslaunch turtlebot3_bringup turtlebot3_rpicamera.launch
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

# Fuentes de información


- [Quick start guide TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)