### ESP8266 ## Programación del ESP8266

De entre las diferentes opciones una de las más sencillas es la utilización de ESPHome para la programación del ESP8266
De este modo en Home Assistant aparecen automáticamente las variables modbus
Otras opciones es programar el ESP8266 "a pelo" para por un lado ller los datos de modbus de la aerotermia y por otro lado enviar los datos leidos por protocolo MQTT a Home Asiistant

### Ejemplo de Modbus con ESP8266 : MQTT + Nodered
MAX485 or MAX3485 TTL to RS485 board
ESP8266 Microcontroller
(en este ejemplo se leen los datos de un inversor FV por modbus, se envían a home assistant por mqtt y se leen los registros modbus con nodered)

https://github.com/cliffdude/SofarCtrl

### Con ESPHome
ESPhome se usa para programar el ESP8266, se puede hacer desde Home Asisistan y temabién directamente desde cualquier ordenador con linus o windows
Toda la documentación disponible en:
https://esphome.io/

Instalación de ESPHome: https://esphome.io/guides/installing_esphome
Resumen: 
1. en un ordenador windows se installa python
2. desde comandos se ejecuta:
> pip3 install wheel
> pip3 install esphome
3. Se puede crear un proyecto, por ejemplo llamado "daitsu.yaml"
> esphome wizard livingroom.yaml
Hay que responder a una serie de preguntas sobre la configuración que estamos usando (fácil)
4. con un editor (ejemplo notepad++ o similar) se crea un fichero daitsu.yaml (ver el ejemplo)
  en este fichero .yaml se configuran los registros modbus que se desean leer
5. en la linea de comando se ejecuta
> esphom run daitsu.yaml
se ve cómo se carga el código al ESP8266 que está conectado al ordenador por el puesto USB. a partir de la primera carga ya se puede actualizar el software vía WIFI (a través de OTA)
el programa, después de compilar, ya pregunta cómo se desea actualizar (vía wifi -OTA o vía puerto USB)
> 


## ESPhome MODBUS
https://esphome.io/components/modbus_controller.html
en está página está la información para la programación modbus a incluir en el fichero datisu.yaml
