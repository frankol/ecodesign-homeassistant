# ecodesign-homeassistant
Home Assistant + EcoDesign Brauchwasserwärmepumpe
![homeassistant_dashboard](https://github.com/frankol/ecodesign-homeassistant/assets/28876168/42df56c0-3408-423e-8675-bdefc01adce4)

Dokumentation über die Integration einer EcoDesign Warmwasserwärmepumpe in Home Assistant

Voraussetzungen:
- Modbus zu Ethernet Adapter (z.B. Waveshare RS485 to RJ45)
- Home Assistant

Konfiguration EcoDesign
- 5 Sekunden Wahlregler gedrückt halten
- Werte ablesen für die Modbuskonfiguration (modbus.yaml)
  - Baudrate: 19200
  - Databits: 8
  - Stopbits: 1
  - Flow control: none
  - Parity: Even
  - Modbus: 3 #< in meinem Fall habe ich 3. Wenn das bei dir anders ist, muss die slave-Variable in allen yaml-Dateien angepasst werden.

 Konfiguration HomeAssistant
 - configuration.yaml mit der bestehenden Datei zusammenführen
 - modbus.yaml in das /config Verzeichnis kopieren und die IP des Modbus Konverters angeben
 - automations.yaml mit der bestehenden Datei zusammenführen
 - alle inputs über Einstellungen -> Geräte und Dienste -> Helfer anlegen (Die Vorlagen befinden sich im input Ordner hier)

Beschreibung

Die Inputs in HomeAssistant können in ein Dashboard übernommen werden. Die Automatisierungen "lauschen" auf die Änderungen bei den Inputs und schreiben die Änderungen über Modbus in die Warmwasserwärmepumpe. Außerdem werden die Inputs mit der automation.yaml in Zahlcodes übersetzt. 
Manche Sensoren müssen vom Zahlencode in eine lesbare Form gebracht werden. Das übernehmen die Template Sensoren in der configuration.yaml.

Als Beispiel z.B. sensor.ecodesign_kwl gibt einen Statuscode der Kontrollierten WohnraumLüftung von 0 (Aus) bis 3 (High) aus. Über das Template wird der Code in eine lesbare Form übersetzt und es wird ein neuer Sensor erstellt und heisst sensor.ecodesign_kwl_typ, welcher die leserlichen Angaben dazu enthält. Es gibt also zwei Sensoren. Der eine mit den Zahlencodes und der andere mit den lesbaren Inhalten

Hinweise:
Ich habe noch nicht alle Status-Codes übertragen, daher fehlen noch ein paar.
Die Dokumentation ist eigentlich nur für mich selbst gedacht. Wünsche und Anregungen gerne über die Issues einkippen.
Die Strommessung erfolgt durch einen NOUS-Zwischenstecker, den es bei Amazon mit Tasmota Firmware zu kaufen gibt. Diesen habe ich mit ESPHome geflasht
