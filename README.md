# Daitsu (aerotermia) (heat to water) Modbus-RTU to Home Assistant 
**Para aerotermias Daitsu distribuidas por Eurofredd - similares a Gree**

[![license](https://img.shields.io/badge/Licence-GNU%20v3.0-green)](https://github.com/desktop/desktop/blob/master/LICENSE)
![ESP32 Architecture](https://img.shields.io/badge/Architecture-ESP32-blue)



Este proyecto describe como comunicarse por Modbus con una aerotermia Daitsu con un ESP826 y enviar los datos a Home Asiistant.  


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

Breakout boards
There are many RS485-to-TTL modules, aka breakout boards, available. They may work or not. You should have attention on the operation voltage. The ESP-devices work with 3 volts. Because of that be careful experimenting with 5 volts. In the best case nothing works. In the worst case it will destroy your ESP or breakout board. Here are two examples of tested breakout boards. Recommended is a board with a SP3485 chip, because it is designed for operating at 3 volts.

Board HW-0519
The HW-0519 breakout board does not need a separate RTS-pin, because it automatically switches between sending and receiving. The recommended voltage is 5 volts, but it should also work with 3 volts.
![image](https://github.com/user-attachments/assets/ae71de71-d1b1-449d-aa63-36632c428429)



Board HW-97
This board is a standard TTL zu RS485 Module with MAX485. It runs per default with 5VDC, but it works with 3.3VDC too. It is a halfdublex Board and has 2 separates RTS-pins (DI/RO) which have to connect together to 1 RTS-Pin.



Board SP3485
The SP3485 breakout board is specially made to work with only 3 volts. It is a halfdublex Board and has a separate RTS-pin. It works with a voltage from 3 to 5 volts.



ESP ⬌ breakout board
The schematic is very simple. Just connect the ESP32 with RS-485 TTL Adapter by RX/TX 2. Its important that you are using HardwareSerial 1 or 2 GPIO´s.

ESP32   HW-0519     HW-97     SP3485
--------------------------------------
D16  ->  RX     -> RO      -> TX
D17  ->  TX     -> DI      -> RX
GND  ->  GND    -> GND     -> GND
3V3  ->  VCC    -> VCC     -> VCC
D5              -> DE+RE   -> RTS
Most of ESP32 have a crosswiring of RX/TX already implemented, so you only need to connect RX with RX and TX with TX. If it doesn´t work properly, try to exchange both.

Breakout board ⬌ Inverter
The RS485 interface is a 2-wire-connection. The wires are called A+ and B-. The big advantage of the interface is, beside of needing only two wires, that it can reach a length up to 1200 meters. The inverter should has a modbus jack connection port where the interface is accessible. Its sufficient to connect the Inverter by 2 wires at specified Modbus Jack connector. You can use a standard NetworkCable and cut it at one end.

In many cases two wires are enough to keep it working without errors. When your environment has electrical interferences or your cable is quiet long, you should use a third wire to establish a common signal reference. This wire has to be connected to the Ground pins.

Solax-X1 G4 Inverter
at Solax-X1 Version G4 Inverter the RJ45-jack connection port is called "COM", you can use this schematic

RS485    Inverter
-----------------
  A   ->  Pin 4
  B   ->  Pin 5
  G   ->  Pin 6 (Ground is optional)
See into the manual if you are using another Inverter.
