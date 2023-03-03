Hier gibt es allgemeine Infos zum Projekt wie Bauplan und Tipps.  
Die Hardware kann stückweise erweitert werden. Für den ersten Test reicht der Controller + Fototransistor.

INSTALLATION:  
1. Binarie aus Repositiory laden.  
2. Mit Flashtool flashen (https://www.espressif.com/en/support/download/other-tools?keys=&field_type_tid%5B%5D=13), 0x10000 als Adresse einstellen.  
3. Nach Start baut der ESP einen Accesspunkt für ein Minute auf. Einwählen, Heimnetz eintragen. Dann starter er neu und meldet sich an.  
4. Im Router ESP eintragen als: esp32-pv-anlage  (zunächst nicht zwingend notwendig, aber da man eh nach der IP-Adresse schauen muss ist das ein Abwasch)  
5. Um die Verbindung zum Einheitenzähler zu prüfen, ist ein Serieller Monitor sehr nützlich (z.B Coolterm oder HTerm) 115200 Baud 8N1. Hier werden auch Debug Informationen und der komplette SML Datensatz des Zählersausgeben sowie der ggf gefundene Gesamtverbrauch und die Wirkleistung.  
6. Browser öffnen und esp32-pv-anlage eintragen. Nun kann man die Webseite mit den Werte sehen (sofern welche vorhanden)
7. Das Exceltool für die Visualisierung funktioniert nun ebenfalls, da es esp32-pv-anlage aufruft und die Daten abholt.  
8. Thats all!!!
