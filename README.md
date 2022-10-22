
# Primeras configuraciones

## PC Setup

En el pc se debe instalar ROS NOETIC, todos los pasos están en el primer link de las fuentes de información.

Cuando ya se haya instalado la imagen en la micro sd card puede que el wifi no funcione:

```
sudo lshw -C network
sudo ifconfig wlan0 down
sudo ifconfig wlan0 up
```

ip de trutlebot: 192.168.43.126
ip de pcRemote:  192.168.43.154

nombre de red : habitacion97

constraseña : contrasena

# Fuentes de información


- [Quick start guide TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)