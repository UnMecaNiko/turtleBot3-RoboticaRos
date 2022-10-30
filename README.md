
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
(en burger) se deben iniciar dos ventanas de comandos, desde remote pc, dos conexiones ssh
```bash
roslaunch turtlebot3_bringup turtlebot3_core.launch
roslaunch turtlebot3_bringup turtlebot3_lidar.launch
```

# Conexión con matlab

[*source*](https://la.mathworks.com/help/ros/ug/get-started-with-a-real-turtlebot.html)

para este método se debe configurar las dos opciones de ip en la turtlebot como su propia ip




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
```

## Problemas al instalar ROS en WSL

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt install curl # if you haven't already installed curl
curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
sudo apt update
```
Luego se sigue con instalación normal **NOETIC**

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
