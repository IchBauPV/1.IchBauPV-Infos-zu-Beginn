# Allgemeine Infos zum/vor dem Start zur DIY PV-Anlage #
Hier gibt es allgemeine Infos zu meinem Projekt für eine DIY PV Anlage mit Nulleinspeisung **via IR-Schnittstelle vom Einheitenzähler**.  
Ihr könnt mehr über das Projekt auf [Youtube](https://www.youtube.com/watch?v=iOFwGEbs9Tw&list=PLFa5aG87q-WGfzpkVKIt8b8U_0DEjR42b) erfahren. Am besten Playlist vorne starten zur Einführung, was das Ganze soll, für wen es ist und wie es funktioniert.  

**An dieser Stelle findet Ihr Infos wie Verdrahtungsplan, Anleitungen, Tipps, etc.**  

Die Hardware kann stückweise erweitert werden. Für den ersten Test reicht der Controller + Fototransistor / IR-Lesekopf an PIN16/RX2.

## Bisher erfolgreich eingebundene Zähler:  ##  
|Hersteller|Bezeichnung|
|------|------|
|DZG Metering GmbH|	DVS7420.1.G2|
|ERF	|SGM-C8 |
|ISKRA	| MT175|
|EMH|	EMH iw8e2a5l0ek2p|
|EBZ	|DD3-2R10 DTA-SMZ1|
|Landis	|eBZD e320|

### Zähler, die nicht eingebunden werden können:  ###  
Zähler aus Österreich, da diese verschlüsselt senden, wie der Siemens IM350  
Zähler, die zuerst eine Abfragemessage erwarten, wie der Elster AS1440



## KURZANLEITUNG INSTALLATION:  ##  
[Videolink ESP Flashtool](https://youtu.be/iqd3WWOy71I?t=407) <-> [Videolink ESPHome Flashtool](https://youtu.be/hs3ob4z7LAg?t=78) (bei Erstintstallation ggf. besser)
1. Binary aus [Repositiory](https://github.com/IchBauPV/2.PV-Controller-Binaries-Releases)  laden. Wenn nicht anders vermerkt, neueste Version verwenden.  
2. ACHTUNG: Es gibt verschiedene ESP32 Generationen und Clone und teilweise Probleme mit der 240Mhz Standard-Version (ESP8266 geht nicht!). Daher ist für die Tests auch eine 160Mhz Version verfügbar. Meine Tests mache ich auf einem ESP32-Wroom, 30 PIN, 4MB mit 240 MHz. Weitere Tipps für eventuelle Fehlerbehebungen gibt es auf der Seite [Troubleshooting](https://github.com/IchBauPV/2.ESP32-PV-Controller-Binaries/blob/main/Troubleshooting.md).
4. Mit [Flashtool](https://www.espressif.com/en/support/download/other-tools?keys=&field_type_tid%5B%5D=13) flashen: ESP32 auswählen, Binary-Datei auwählen, 0x10000 als Adresse eingeben, Haken setzen, den richtigen COM Port einstellen - und START drücken. Funktioniert bei 4MB, solange der Bootloader noch original ist. ESPRESSIF: At a 0x10000 (64 KB) offset in the flash is the app labelled “factory”. The bootloader will run this app by default. 
Alternativ kann man den [ESPHome-Flasher](https://github.com/esphome/esphome-flasher/releases/download/1.4.0/ESPHome-Flasher-1.4.0-Windows-x64.exe) verwenden, der vorher das Flash komplett löscht und auch einen Seriellen Monitor eingebaut hat. Hiermit hatten manche mehr Erfolg, bei denen es mit dem Hersteller-Tool nicht geklappt hatte.   
6. Nach dem Start baut der ESP einen WLAN-Accesspoint für ca. 5 Minuten auf. Einwählen, Heimnetz eintragen. Dann neu starten und er meldet sich im Heimnetz an.   Wenn der ESP (irgendwann) schon einmal im Netz registriert war, sind die Credentials noch vorhanden. Er wählt sich dann damit wieder ein und das Programm startet **OHNE Accesspoint**, auch nach neuem Flashen mit neuem Binary.  Beim Start gibt der ESP seine IP-Adresse über den seriellen Monitor aus.
7. Im Router (z.B. [Fritzbox](https://github.com/IchBauPV/1.Infos-zu-Beginn/blob/main/Einstellung-Fritzbox.md)) ESP eintragen als: *esp32-pv-anlage* (zunächst nicht zwingend notwendig, aber da man eh nach der IP-Adresse schauen muss, ist das aber ein Abwasch). Alternativ wird die IP auch über den Seriellen Monitor ausgegeben.  
8. Um die IR-Verbindung zum Einheitenzähler zu prüfen, ist ein Serieller Monitor sehr nützlich (z.B Coolterm oder HTerm) 115200 Baud 8N1. Hier werden auch Debug Informationen und der komplette SML Datensatz des Zählers ausgeben sowie der ggf gefundene Gesamtverbrauch und die Wirkleistung. Beim ESP HomeFlaher ist bereits ein Serieller Monitor integriert.  
9. Browser öffnen und http://esp32-pv-anlage eintragen, alternativ die IP-Adresse. Nun kann man die Webseite mit den Werte sehen (sofern welche vorhanden)
10. Das [Exceltool](https://github.com/IchBauPV/3.Zusatzsoftware) für die Visualisierung funktioniert nun ebenfalls, da es esp32-pv-anlage aufruft und die Daten abholt.  Es müssen die Makros aktiviert werden: Im Datei Explorer Datei rechts-klicken => Eigenschaften => Sicherheit => Zulassen Haken setzen, übernehmen
11. Thats all. Have fun!!!


## PINBELEGUNG  D..   für ESP32 WROOM  ##
|PIN|Beschreibung|
|------|------|
| 1 |TX  USB                  //  1: TX von PC-USB Anschluss für serielle Kommunikation |
| 2 |OB_LED_Pin               //  2 : Built in LED für Anzeige von Datenempfang  |
| 3 |RX USB                   //  3 : PC-USB Anschluss für serielle Kommunikation |
| 4 |RS485_RX_Pin             //  4 : RX bzw RO von RS485; (Lesen wird hier nicht verwendet  |
| 5 |R5485_TX_Pin             //  5 : TX bzw DI von  RS485;  |
| 13| Buzzer_Pin              // 13 : Buzzer für Alarm keine Daten seit x sec; muss nicht eingebaut werden  |
| 15| RS485_Tog_Pin           // 15 : Pin zum Umschalten des RS485 Boards von TX (high) auf RX (Low)  |
| 16| IRHead_RX_Pin           // 16 : RX von IRHead - Eingang von Infrarottransisitor |
| 17| IRHead_TX_Pin           // 17 : TX von IRHead (wird nicht verwendet, kommt vielleicht noch  |
| 18| IR_Green_Pin            // 18 : Led Grün: erfolgreich gelesen  |
| 19| IR_Red_Pin              // 19 : Led rot: Lesefehler  |
| 21| SDA_Pin                 // 21 : SDA für 1602 Display   ; muss nicht eingebaut werden    Display:  21 = SDA; 22 = SCL  |
| 22| SCL_Pin                 // 22 : SCL für 1602 Display  |
| 27| Touch_Pin               // 27 : touch pin Taster für LCD Beleuchtung  ; muss nicht eingebaut werden  |
