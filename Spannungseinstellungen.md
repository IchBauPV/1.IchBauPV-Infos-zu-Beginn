# Setup der Spannungen: #    
Die Komponenten Laderegler und Wechselrichter sollten so eingestellt sein, dass diese VOR dem BMS (Battery-Management-System) abschalten. Der Wechselrichter sollte also vor  der unteren Grenze des BMS und der Laderegler vor der oberen abschalten.  

## Hintergrund: ##    
Beim Überspannungs-Abschalten des BMS geht der Strombezug schlagartig auf Null und der Laderegler "pumpt" ggf. ins „Leere“, was zu Spannungsspitzen (>>70V) führt / führen kann. Diese können ggf. andere Komponenten, insbesondere den Wechselrichter schädigen/zerstören (ist bei mir passiert, wenngleich wohl ein Vordefekt/Abnutzung vorlag). Dieses ist somit die kritischere Abschaltung, die unbedingt wirken sollte.
Beim Unterspannungs-Abschalten des BMS geht der Strom aus und der EASUN- Laderegler auch. Somit kann der Laderegler die Batterie nicht mehr laden, selbst wenn wieder PV Spannung anliegt ("Dead-lock"). Die Batterie muss manuell wieder auf Mindestspannung gebracht werden, damit sie wieder einschaltet. Alternativ könnte man notfalls im BMS Setup kurz die Abschaltspannung absenken, wenn wieder PV Leistung kommt, damit die Batterie wieder kurz "erwacht" und der Laderegler sie wieder laden kann.

## Meine Spannungseinstellungen im System: ##  

![grafik](https://user-images.githubusercontent.com/125013125/233797451-fd6ab893-eb3f-47ea-b70e-7bc07158c84e.png)

Die Voltzahlen des EASUN 6048 beziehen sich immer auf ein 12V System, auch wenn eine andere Spannung gewählt ist. Es muss dann (im Kopf) mit den Faktoren 2, 3 bzw 4 für 24, 36 bzw 48V System gerechnet werden, um die tatsächliche Schaltspannung zu erhalten, bei der er regelt.
