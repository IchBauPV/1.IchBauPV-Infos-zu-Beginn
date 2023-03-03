Hier gibt es allgemeine Infos zu meinem Projekt für eine DIY PV Anlage mit Nulleinspeisung via IR Schnittstelle vom Einheitenzähler.
Ihr könnt mehr über das Projekt auf Youtube erfahren: https://www.youtube.com/@ichbaupv8402  
Am besten vorne starten: https://www.youtube.com/watch?v=iOFwGEbs9Tw

An dieser stelle findet Infos wie Bauplan, Tipps, etc.  

Die Hardware kann stückweise erweitert werden. Für den ersten Test reicht der Controller + Fototransistor.

INSTALLATION:  
1. Binary aus Repositiory laden (https://github.com/IchBauPV/ESP32-PV-Controller-Binaries).  
2. Mit Flashtool flashen (https://www.espressif.com/en/support/download/other-tools?keys=&field_type_tid%5B%5D=13), 0x10000 als Adresse einstellen und natürlich den richtigen COM Port.  
3. Nach dem Start baut der ESP einen Accesspunkt für eine Minute auf. Einwählen, Heimnetz eintragen. Dann starter er neu und meldet sich an.  
4. Im Router ESP eintragen als: esp32-pv-anlage  (zunächst nicht zwingend notwendig, aber da man eh nach der IP-Adresse schauen muss, ist das aber ein Abwasch)  
5. Um die IR-Verbindung zum Einheitenzähler zu prüfen, ist ein Serieller Monitor sehr nützlich (z.B Coolterm oder HTerm) 115200 Baud 8N1. Hier werden auch Debug Informationen und der komplette SML Datensatz des Zählers ausgeben sowie der ggf gefundene Gesamtverbrauch und die Wirkleistung.  
6. Browser öffnen und esp32-pv-anlage eintragen. Nun kann man die Webseite mit den Werte sehen (sofern welche vorhanden)
7. Das Exceltool für die Visualisierung funktioniert nun ebenfalls, da es esp32-pv-anlage aufruft und die Daten abholt (https://github.com/IchBauPV/Zusatzsoftware).  
8. Thats all!!! Have fun!!!
