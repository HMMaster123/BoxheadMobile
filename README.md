# Arena Survivors

Een kleine, originele top-down zombie-survivalgame voor Android, gemaakt met Godot 4 en GDScript. De code en eenvoudige vormen zijn eigen werk; dit project bevat geen Boxhead-code, levels of afbeeldingen.

## Benodigd

- Godot 4.3 of nieuwer, met de standaardeditor.
- Voor een Android-build: Android SDK, JDK en de Godot Android export templates. Stel deze in via **Editor > Editor Settings > Export > Android**.
- Voor testen van LAN: twee Android-telefoons op hetzelfde wifi-netwerk. Een router die client-isolatie toepast of UDP-broadcast blokkeert kan ontdekken/verbinden verhinderen.

## Openen en spelen

1. Clone de Git-repository of open de projectmap in Godot.
2. Importeer `project.godot` en druk op **F5** of de knop **Run Project**.
3. Kies **Alleen spelen**, of start op de ene telefoon **Host een wifi-spel**.
4. Kies op de tweede telefoon **Zoek spelers op wifi** en druk op **Meedoen** bij de host. Als automatische ontdekking niet werkt, kun je het IPv4-adres van de host handmatig invullen.
5. Gebruik de linker virtuele joystick om te bewegen en de rechter joystick om te richten. Je personage schiet automatisch in de gekozen richting; er is geen vuurknop. Op desktop beweeg je met de pijltjestoetsen en richt je met de muis. De telefoon speelt liggend en de camera volgt je door het grotere speelveld.
6. Je score verschijnt boven in het midden en stijgt met één punt per gedode zombie. Zombies komen in golven: elke nieuwe wave bevat meer zombies met meer gezondheid. Er verschijnt een vuurflits bij het pistool als je schiet. Zombies spawnen buiten beeld. Na elke kill blijft er een bloedvlek op de grond liggen. Zombies halen bij aanraking steeds 12 gezondheid weg; bij nul gezondheid is het spel voorbij. In singleplayer begin je opnieuw met **R**, een tik of een klik; in een wifi-spel kun je via **Menu** de sessie verlaten.

De host beheert de zombies en score. Er kunnen maximaal vier spelers deelnemen (host plus drie gasten). De netwerkverbinding gebruikt ENet/UDP-poort `24580`; host-ontdekking gebruikt UDP-broadcast-poort `24579`.

## Android exporteren

1. Installeer de Android SDK/JDK en export templates en stel de paden in bij de Android-exportinstellingen van Godot.
2. Kies **Project > Export**, voeg **Android** toe en geef de app een unieke package-naam.
3. Schakel in de Android-exportinstellingen de internet/netwerktoestemming in; die is nodig voor UDP-discovery en de ENet-spelsessie op het lokale netwerk.
4. Exporteer een APK voor lokaal testen. Deel geen signing-keystore of wachtwoorden via Git.

Een debug-APK voor installatie en testen staat in `build/ArenaSurvivors.apk`. Je kunt dit bestand naar een Android-telefoon kopiëren en daar openen om het te installeren. Met USB-debugging ingeschakeld kun je ook `adb install -r build/ArenaSurvivors.apk` gebruiken. Android kan vragen om installatie uit deze bron toe te staan.

Deze APK is met de Godot-debughandtekening ondertekend en bedoeld voor testen; voor publicatie via Google Play is een eigen release-keystore nodig. APK-bestanden zijn uitgesloten van Git, dus deel de APK apart van de broncode.

## Samenwerken via Git

De repository bevat `.gitignore`-regels voor editorcache, Android-builds en signing-bestanden. Commit de broncode, scènes en documentatie; commit geen APK's, `.godot/`-cache of sleutels. Een collega kan daarna clonen en `project.godot` openen in Godot.

## Projectstructuur

- `project.godot` — instellingen en startscène.
- `scenes/main.tscn` — startscène.
- `scripts/main.gd` — menu, host/join en LAN-ontdekking.
- `scripts/arena.gd` — arena, spelers, zombies en gameplay/netwerksynchronisatie.
