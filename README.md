# Daitsu (aerotermia) (heat to water) Modbus-RTU to Home Assistant 
**Para aerotermias Daitsu distribuidas por Eurofredd - similares a Gree**

[![license](https://img.shields.io/badge/Licence-GNU%20v3.0-green)](https://github.com/desktop/desktop/blob/master/LICENSE)
![ESP32 Architecture](https://img.shields.io/badge/Architecture-ESP32-blue)



Este proyecto describe como comunicarse por Modbus con una aerotermia Daitsu con un ESP826 y enviar los datos a Home Asiistant.  
https://daitsu.es/

### Supported Datisu
Creo que puede comunicarse con las aertotermias Daistu distribuidas en España por Eurfreed:
*
* 
* 
* 
* 
* 
* 



### What you need
* ESP32, Esp8266 NodeMCU
* RS-485 TTL UART Module with MAX485 Semiconductor 

An ESP8266 is sufficient for Modbus communication 

### How to start
It´s recommend to start with one example to check wiring works correctly. Both LED´s (TX and RX) on your RS-485 module should blink. If only TX-LED blinks, please check: 
* wiring
* baud rate


## please refer full documentation and How-To´s in our )

#wiring the circuit
tobiasfaust edited this page on Jan 27, 2023 · 12 revisions
To connect the inverter to the ESP32, you have to use a breakout board to adapt the RS485 interface of the inverter to serial interface of the ESP.

Please note: Basis for this article came from Tasmota wiki, thanks to those authors.

#Breakout boards
There are many RS485-to-TTL modules, aka breakout boards, available. They may work or not. You should have attention on the operation voltage. The ESP-devices work with 3 volts. Because of that be careful experimenting with 5 volts. In the best case nothing works. In the worst case it will destroy your ESP or breakout board. Here are two examples of tested breakout boards. Recommended is a board with a SP3485 chip, because it is designed for operating at 3 volts.

#Board HW-0519
The HW-0519 breakout board does not need a separate RTS-pin, because it automatically switches between sending and receiving. The recommended voltage is 5 volts, but it should also work with 3 volts.
![image](https://github.com/user-attachments/assets/ae71de71-d1b1-449d-aa63-36632c428429)

![image](https://github.com/user-attachments/assets/645b0a99-bd2a-4e4d-b6e3-7d1b906e40fa)


#Board HW-97
This board is a standard TTL zu RS485 Module with MAX485. It runs per default with 5VDC, but it works with 3.3VDC too. It is a halfdublex Board and has 2 separates RTS-pins (DI/RO) which have to connect together to 1 RTS-Pin.
![image](https://github.com/user-attachments/assets/008e1d61-6e66-4bd0-a3ea-99628d209b49)

![image](https://github.com/user-attachments/assets/d4354c2a-6329-496e-82a3-4ce7bf79a81e)


#Esp8266 - NodeMcu

![image](https://github.com/user-attachments/assets/0b39a1de-8e3b-42e4-b5ee-591e69c331b4)

# Datisu Control Panel - Panel de control tactil
En la parte posterior del panel de control tactil de la aerotermai Daitsu hay un conector que está comunicando con la aerotermia. Ha dos Salidas (marcadas como A y B) que se conectan al convertidor Rs484-TTL elegido (en mi caso el HW-97, pero debería funcionar con otros modelos)
![image](https://github.com/user-attachments/assets/ba17d97a-597e-4323-8382-91a1d301313c)

# ESP8266 ⬌ breakout board
The schematic is very simple. Just connect the ESP8266 with RS-485 TTL Adapter by RX/TX 2. 

ESP8266   HW-0519     HW-97   
------------------------------
GPIO13 -D7     ->  RX     -> RO      
GPIO14 - D8    ->  TX     -> DI      
GND            ->  GND    -> GND    
3V3            ->  VCC    -> VCC     
D5                        -> DE+RE   



RS485    Daitsu panel de control
-----------------
  A   ->  Pin A
  B   ->  Pin B
  G   ->  Pin 6 (Ground is optional)


## Referencias:
https://github.com/tobiasfaust/SolaxModbusGateway/wiki/wiring-the-circuit


