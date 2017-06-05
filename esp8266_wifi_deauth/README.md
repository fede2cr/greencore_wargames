# Ataque de desautenticación de Wifi con ESP8266

La gran mayoría de las redes Wifi que encontramos en la calle y en nuestras empresas, son vulnerables a un ataque de desautenticación.

En este ejercicio vas a construir uno, utilizando la microcontroladora ESP8266. De esta micro hay muchas versiones, por lo que recomendaremos el ESP8266 Feather Huzzah de Adafruit.

## Materiales

Para realizar este laboratorio necesita:

- [Microcontroladora ESP8266](http://www.crcibernetica.com/adafruit-feather-huzzah-with-esp8266-wifi/) Feather Huzzah de Adafruit
- [Cable micro USB](http://www.crcibernetica.com/usb-microb-cable-6-foot/)
- (Opcional) [Batería Lipo pequeña](http://www.crcibernetica.com/lithium-ion-polymer-battery-3-7v-350mah/) o [Adaptador micro USB](http://www.crcibernetica.com/wall-adapter-power-supply-5v-dc-2-5a-usb-micro-b/)

## Atribución

El proyecto que hace este nivel posible es el [esp8266_deauther](https://github.com/spacehuhn/esp8266_deauther) de [spacehuhn](https://github.com/spacehuhn). Se incluye un excelente README con instrucciones y capturas de pantalla.

Este nivel es solamente un tutorial introduciendo de forma práctica a la instalación y uso de la micro como herramienta de serguridad.

## Subiendo la imagen a la ESP8266 con ``esptool``

Iniciamos por instalando la herramienta de ESPTool

```bash
sudo apt install python3-pip
sudo pip3 install --upgrade pip esptool
```

Luego bajamos una imagen en formato ``bin`` para la ESP8266. Esto ahorra el trabajo de bajar el IDE de Arduino, agregar librerías para la ESP8266 y luego modificarlas para agregar el comando de DeAuth en el que se basa este ataque.

```bash
wget https://github.com/spacehuhn/esp8266_deauther/releases/download/v.1.4/esp8266_deauther_1mb.bin
esptool.py --port /dev/ttyUSB0 erase_flash
esptool.py --port /dev/ttyUSB0 --baud 460800 write_flash --flash_size=detect 0 esp8266_deauther_1mb.bin 
```

## Realizando el ataque

Luego de cargar la imagen binaria, reinicie la tarjeta usando el botón de ``reset``. Luego de esto puede encontrar disponible la red inalámbrica con SSID ``pwned`` con contraseña ``deauther``. Conecte su teléfono móvil u otro dispositivo a esta red inalámbrica, y visite el sitio web ``http://192.168.4.1``.

Siga las instrucciones de la página web para escoger un Access points, luego descubra equipos conectados a este AP para luego iniciar el ataque de Desautenticación.

### Advertencia

Ejecutar este tutorial en redes inalámbricas que no sean de su pertenencia tiene serias implicaciones éticas y legales. Use solamente equipo para el que ha sido autorizado **por escrito**.
