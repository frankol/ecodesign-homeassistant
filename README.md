# ecodesign-homeassistant
Home Assistant + EcoDesign Brauchwasserwärmepumpe

Dokumentation über die Integration einer EcoDesign Warmwasserwärmepumpe in Home Assistant

Voraussetzungen:
- Modbus zu Ethernet Adapter (z.B. Waveshare RS485 to RJ45)
- Home Assistant

Konfiguration EcoDesign
- 5 Sekunden Wahlregler gedrückt halten
- Werte ablesen für die Modbuskonfiguration
  - Baudrate: 19200
  - Databits: 8
  - Stopbits: 1
  - Flow control: none
  - Parity: Even
  - Modbus: 3 #< in meinem Fall habe ich 3. Wenn das bei dir anders ist, muss die slave-Variable in allen yaml-Dateien angepasst werden.
 
Rest folgt
