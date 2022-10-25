
# Primeras configuraciones

## PC Setup

> Verifficar siempre que se siguen las instrucciones para ROS Noetic
En el pc se debe instalar ROS NOETIC, todos los pasos están en el primer link de las fuentes de información.

ip de trutlebot: 192.168.43.126

ip de pcRemote:  192.168.43.154

nombre de red : habitacion97

constraseña : contrasena

Configurar archivos ~/.bashrc

![configuracion de ips](https://emanual.robotis.com/assets/images/platform/turtlebot3/software/network_configuration.png)

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

# Fuentes de información


- [Quick start guide TurtleBot3](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/#pc-setup)