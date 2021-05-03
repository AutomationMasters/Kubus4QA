# Kubus4QA

Free Version (30 Tage Testversion)

<pre>
     __ __ __
   /__/__/__/\    KUBUS 4 QA
  /__/__/__/\/\   -------------------------------------------------------
 /__/__/__/\/\/\  Stand:     15.03.2021
 \__\__\__\/\/\/  Lizenz:    
  \__\__\__\/\/   Version:   5.0.120
   \__\__\__\/    (c)Copyright 1999-2021
</pre>

## Über das Programm
 KUBUS4QA ist ein kleines Hilfe-Tool welches erlaubt, dass öffnen von Porgrammen,
 Ordner und Scripte, wie Vorlagen unter eine einfachen Auswahl einer Liste 
 auszuführen.

### Installation
 Das Programm installiert sich einfach durch das erste mal Starten. Dabei werden 
 einige Dateien in das lokale Temp-Verzeichnis abgelegt. Andere wie etwas Demo 
 Dateien werden im Hauptordner "app" abgelegt.

 In der Programm INI-Datei "app\app.ini" wird beim ersten Start, der verwendete Pfad 
 zu den Datensatz (INI-Dateien) festgelegt. Dieser absolute Pfad wird in der Section 
 [Data] hinterlegt und kann damit jederzeit geändert werden. 

##### Beispiel:
<pre>
[Data]
  Dir=D:\Development\AutoIt\K4QA\app\data
</pre>
 Der Ordner welcher über den Schlüssel "DIR" hinterlegt wurde (Standard: "app\data")
 wird untersucht, ob Datensätze in Form einer INI-Datei hinterlegt wurden. Diese 
 sind im Programm später auswählbar und deren Listeneiträge ausführbar. In einem 
 Datensatz (INI-Datei) werden dabei die Grundbefehle und Pfade zum Ausführen
 hinterlegt:

##### Beispiel:
<pre>
  [Scripts]
  s1=1: Öffne einen Ordner|FOLDER|C:\Users
  s2=2: Öffne ein Programm|OPEN|calc.exe
  s3=3: Lade aus dem Zwischenspeicher|CLIP|E:\Tools\Kubus4QA\app\scripts\code.txt
</pre>
 Es können bis zu 20 Einträge pro Datensatz in folgendem Schema hinterlegt werden:
 <Script-Nummer mit "s" vor der Zahl>=<Zeilenzahl>:<Information>|<Funktion>|<Pfad>

 INFO: Die Nummern dürfen nicht vertauscht werden, da sonst ein andere Befahl aus der 
       Liste ausgeführt werden würde!

##### Beispiel:
<pre>
  s1=1: 
  s2=2: 
  s3=3: 
</pre>

## Funktionen
Zum Ausführen gibt es mehrere Funktionen:

### Öffnen von Datei und Ordnern - mit und ohne Dialog
<pre>
 - OPEN                       öffnet den im <Pfad> hinterlegten Ordner oder ein Programm.
Bsp.1: s1=1: Öffne Ordner 2|OPEN|C:\Folder1\Folder2
Bsp.2: s2=2: Öffne Programm|OPEN|C:\PlugPlay\tool.exe

 - OPENDIALOG                 öffnet eine Datei in einem Programm durch ein Auswahl-Dialog.
                               Pfadangaben: <Pfad zum Programm>
Bsp.: s1=1: Öffne Notepad++ und wähle Datei|OPENDIALOG|notepad++.exe

 - OPENFILE                   öffnet eine festgelegte Datei oder Angaben über ein Programm.
                               Pfadangaben: <Pfad zum Programm>;<Pfad zur Datei>
                               Es können auch URL oder Schlagwörter in Browsern übergeben werden:
Bsp.1: s1=1: Öffne Browser|OPENFILE|chrome.exe;https://www.domain.tld
Bsp.2: s2=2: Öffne Datei|OPENFILE|notepad++.exe;C:\files\meintext.txt

 - OPENREGISTRY               öffnet Registry mit hinterlegten Pfad.
                               Pfadangaben: <Pfad zum Programm>;<Pfad zur Datei>
                               Es können auch URL oder Schlagwörter in Browsern übergeben werden:
Bsp.1: s1=1: Öffnet Registry mit Pfad|OPENREGISTRY|HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Word\InstallRoot
</pre>

### Öffnen von Datei und Ordnern
<pre>
 - START                      startet ein im <Pfad> hinterlegtes Programm per ShellExecute().
                               !Der Befehl unterstützt keine MagicWords und dient zum aufrufen,
                               Windows eigene Programme:
Bsp.: s1=1: Ereignisanzeige|START|eventvwr.exe
</pre>

### AU3 Script direkt ausführen
<pre>
 - AU3                        startet ein im <Pfad> hinterlegtes Au3-Script direkt als ausfürbares Programm.
Bsp.: s1=1: Demo au3-Script ausführen|AU3|C:\scripts\demo.au3
</pre>

### Systemsterungs - Dialoge
<pre>
 - CPL                        öffnet eines der Systemeinstellungen zugeordneten Dialoge per Run()
                               Der Befehl unterstützt keine {MagicWord}!
Bsp.: s1=1: Programme löschen|CPL|appwiz.cpl
</pre>

### Speichern in Clipboard (Zwischenspeicher)
<pre>
 - CLIPPATH                   speichert ein durch den <Pfad> hinterlegtes Script oder Vorlage
                               in den Zwischenspeicher. Es können {MagicWord} in der Vorlage 
                               verwendet werden. 
Bsp.: s1=1: Aus Vorlage in Clipboard|CLIPPATH|C:\scripts\clip.txt

 - CLIPSTRING                 speichert den im <Pfad> hinterlegte einen String in die Zwischenablage. 
                               Es können dabei {MagicWord} verwendet werden. 
Bsp.: s1=1: String in Clipboard|CLIPSTRING|Ich bin {@UserName}
</pre>

### Kopieren von Ordnern und Dateien
<pre>
 - COPYFILE                   kopiert eine Datei aus einem festgelegten Ordner und legt sie auf einem 
                               Zielsystem ab. Wird kein Endpfad nach dem ; angegeben wird die Kopie auf dem  
                               Desktop abgelegt. Ansonsten am angegebenen Pfad. Es können dabei {MagicWord} 
                               verwendet werden. 
Bsp.1: s1=1: Datei kopieren auf den Desktop|COPYFILE|{@GlobalDir}\template.docx
Bsp.2: s2=2: Datei aun Platz kopieren|COPYFILE|{@ScriptDir}\template.docx;{@DesktopDir}\Ordnername

 - COPYFOLDER                 kopiert einen Ordner an einem anderen Platz. Wurde kein ; gesetzte wird der Ordner 
                               auf den Desktop abgelegt. Ansonsten am angegebenen Pfad. Es können dabei {MagicWord} 
Bsp.1: s1=1: Ordner auf den Dektop kopieren|COPYFOLDER|{@GlobalDir}\Data
Bsp.2: s2=2: Ordner zu Pfad kopieren|COPYFOLDER|{@GlobalDir}\Data;{@DesktopDir}\MyFolder_{@UserName}-{HEUTE}

 - COPYFOLDERDIALOG           kopiert einen Ordner per Dialoge. Es können dabei {MagicWord} Dabei wird
                               in vier unterschiedliche Möglichkeiten unterschieden:
                           (1) Ohne Angaben im Pfad: Auswahl des Ordners per Dialog; wird auf dem Desktop gespeichert.
                           (2) Mit ; ohne Angaben: Auswahl des Ordners per Dialog; Dialog zur Auswahl um Kopie zu gespeichern.
                           (3) Mit Pfadangabe: Nur Dialog zur Auswahl um Kopie zu speichern wird geöffnet.
                           (4) Mit ; und Pfadangabe: Nur Dialog zur Auswahl des Ordners wir geöffnet; wird über Pfadangabe nach ; gespeichert.
Bsp.1: s1=1: Dialog Starten und auf Desktop ablegen|COPYFOLDERDIALOG|
Bsp.2: s2=2: Dialoge zur Auswahl eines Ordner und zum speichern|COPYFOLDERDIALOG|;
Bsp.3: s3=3: Dialog zum speichern der Kopie (mit Ausgangspfad)|COPYFOLDERDIALOG|{@ScriptDir}\app\templates
Bsp.4: s4=4: Dialog zur Auswahl des Ordners (mit Zielpfad)|COPYFOLDERDIALOG|;{@DesktopDir}\MyFolder_{@UserName}-{HEUTE}

</pre>

### Komprimieren oder Entpacken von Dateien
<pre>
 - ZIP                        Zipt den Inhalt eines über den Pfad festgelegten Ordner uns speichert die 
                               Datei, mit Datum und Uhrzeit im Namen auf dem Desktop. 
Bsp.1: s1=1: Ordner zippen (auf den Desktop ablegen)|ZIP|{@ScriptDir}\MyFolder
Bsp.2: s2=2: Ordner zippen (an anderen Ort ablegen)|ZIP|{@ScriptDir}\MyFolder;{@DesktopDir}\test.zip

 - UNZIP                      Entpackt den Inhalt einer über den Pfad festgelegten Zip-Datei uns speichert 
                               sie in einem Ordner mit Datum und Uhrzeit auf dem Desktop. 
Bsp.1: s1=1: Zip (auf den Desktop entpacken)|UNZIP|{@ScriptDir}\test.zip
Bsp.2: s2=2: Zip (an anderen Ort entpacken)|UNZIP|{@ScriptDir}\test.zip;{@DesktopDir}\MyFolder
</pre>

### Öffnen von Systemvariablem / MagicPath
<pre>
 - MAGICPATH                  öffnet ein {@MagicWordPath} welcher im Feld <Pfad> hinterlegt wurde:
Bsp.: s1=1: Öffne MagicWord Pfad|MAGICPATH|{@AppDataDir}
</pre>

### Zusammenführen von mehreren Dateien (txt)
<pre>
 - MERGE                      verbindet Inhalte unterschiedlicher Dateien (txt) miteinander. Dabei kann gewählt werden
                               ob der Merge in den Zwischenspeicher geschrieben werden soll, ober als Datei auf den Rechner. 
Bsp.1: s1=1: Merge an Ort|MERGE|{@ScriptDir}\app\scripts\today.txt,{@ScriptDir}\app\scripts\magicwords.txt
Bsp.2: s2=2: Merge in Zwischenspeicher|MERGE|{@ScriptDir}\app\scripts\today.txt,{@ScriptDir}\app\scripts\magicwords.txt;{@DesktopDir}\MyMerge-{HEUTE}.txt
</pre>

### Auslesen eines Registry-Pfad
<pre>
 - REGISTRY                   Auslesen der Registry
Bsp.1: s1=1: Lese Registry|REGISTRY|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer;svcVersion
</pre>

## Anpassen (app.ini)
 Nach der "Installation" wird ein Ordner app angezeigt. Dieser enthält die app.ini 
 Datein mit der, Kubus4QA individuell angepasst werden kann:
 
<pre>
 [Data]                       Sektion für Hauptdaten
 Dir=<Pfad>                    Zeigt den Pfad an, von dem aus die Datensätze
                               geladen werden sollen. Die Ini-Dateien werden 
                               automatisch erkannt und ausgelesen.
 DirGlobal=<Pfad>              Einbinden eines externer Pfad für Datensatz.ini-Dateien. 
                               So können Vorlagen gemeinsam verwendet werden.
 DirPersonalTemp=<Pfad>        Öffnet den Pfad zu einem Ordner der als Ablage unter Temp liegt.
                               Ist der Pfad in der INI-Datei leer, wird nach Ausführen der Funktion 
                               im Menü: "Ablagen > Persönlich" erst ein neuer Ordner erzeugt
                               und danach geöffnet. Es lassen sich Daten dort dauerhaft hinterlegen.
 DirGlobalTemp=<Pfad>          Pfad zu einer gemeinsam nutzbarem Ablage als Ordner. 
                               

 [Label]                      Sektion für Beschreibungen
 DatasetPrivate=<Name>         Vergabe des Namens für das Label "Privater Datensatz" 
 DatasetGlobaler=<Name>        Vergabe des Namens für das Label "Globaler Datensatz" 
 MyTool1=<Name>                Vergabe eines Namens für das eigene Menü unter "Werkzeuge" 
 MyTool2=<Name>                Vergabe eines Namens für ein eigenes Menü unter "Werkzeuge" 
 MyTool3=<Name>                Vergabe eines Namens für ein weiteres Menü unter "Werkzeuge" 
                               

 [Flags]                      Sektion zum anpassen des Programms
 HotKey=^<                     Anzeigen per Tastenkürzel (Standard: STRG+>)
 Date=dd.mm.YYYY               MagicWord Datumsausgabe
 Random=1                      Ändert bei Starten die Hintergrundfarbe (1=an(0/=aus)
 Color=00FF00                  Wenn Random aus ist, wir dieser Farbwert übergeben
 WindowType=1                  Zeigt das Hauptfenster in drei Variationen an:
                                2= leeres Fenster ohne Fenster-Funktionen
                                1= Fenster mit [x] Schließen-Button 
                                0= normales Fenster ohne Maximieren
 ShowWindowAfterStart=1        Anzeige des Fensters nach dem Start (1=an(0/=aus)
 CloseAfterRunning=1           Verstecken nach Ausführen eines Befehls
 OpenMousePosition=1           Öffne nach Tastenkürzel an Mausposition
 ShowInfoBox=0                 Zeige Informationsbox an (noch experimentell)
 SaveTemplateAboutDialog=0     Zeigt ein Speichern-Dialog bei Ausführen der Funktion: "COPYTEMP"
                               

 [MyMagicWords]               Hier lassen sich eigene (statische) Inhalte als MagicWords festlegen.
 MW1=Das
 MW2=ist
 MW3=eine
 MW4=neue
 MW5=Funktion
 MW6=für
 MW7=die
 MW8=eigenen
 MW9=Magic
 MW10=Words
</pre>



## Anpassen (nav.ini)
Nach der "Installation" wird ein Ordner app angezeigt. Dieser enthält die nav.ini. 
Damit lassen sich weitere Tools unter dem Menü "Werkzeuge" und deren Untermenüs erweitern. Dazu gehören: 
- Generatoren, Prozessoren, Archivieren, Skipte, Ablagen, Editoren, Crypto 

Über MyTools können drei eigene Untermenüs erzeugt werden. Diese benötigen vorerst ein Label unter der app.ini: 
- MyTool1, MyTool2, MyTool3 
Es können die oben beschriebenen Funktionen (FUNC) genutzt werden: 

<pre>
 [Generatoren]                Hiermit lassen sich weitere Generatoren hinzufügen. Es sind Zehn weitere Einbindungen möglich.
 link1=<name>|FUNC|<path>
 link2=<name>|FUNC|<path>
 link3=<name>|FUNC|<path>
 link4=<name>|FUNC|<path>
 link5=<name>|FUNC|<path>
 link6=<name>|FUNC|<path>
 link7=<name>|FUNC|<path>
 link8=<name>|FUNC|<path>
 link9=<name>|FUNC|<path>
 link10=<name>|FUNC|<path>
</pre>



### MagicWords im Überblick

MagicWords sind Angaben in einer Vorlage- oder Script-Datei welche ebim Ausführen 
der Funktionen "CLIPPATH" oder "CLIPSTRING" erkannt und mit entsprechenden Inhalt
gefüllt werden. Dabei handelt es sich um Kernpfade und Namen, Datum oder Uhrzeiten
wie Systemname der Nutzer usw.; so gibt es auch die Möglichkeit, einen MagicWordPath 
zu verwenden bei dem ein Script direkt eingebunden werden kann. 

### Einbinden anderer Scripts:
<pre>
{#include="C:\Meine Vorlagen\template-001.txt"}
</pre>

#### Registry:
IE: zum Beispiel
<pre>
{#registry="HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Internet Explorer;svcVersion"}
</pre>

#### Zeiten:
<pre>
 Date  / HEUTE:          {HEUTE}                 30.10.2020
 Year  / JAHR:           {JAHR}                  2020
 Month / MONAT:          {MONAT}                 10
 Day   / TAG:            {TAG}                   30
 Time  / ZEIT:           {ZEIT}                  11:55:00
 Hour  / STUNDE          {STUNDE}                11
 Min.  / MINUTE:         {MINUTE}                55
 Sec.  / SEKUNDEN:       {SEKUNDEN}              00
 </pre>

#### Infos:
<pre>
 UserName:              {@UserName}              <Benutzername>
 ComputerName:          {@ComputerName}          PC-001
 DesktopDepth:          {@DesktopDepth}          32
 DesktopHeight:         {@DesktopHeight}         1080
 DesktopWidth:          {@DesktopWidth}          1920
 DesktopRefresh:        {@DesktopRefresh}        0
 IPAddress1:            {@IPAddress1}            169.100.10.100
 IPAddress2:            {@IPAddress2}            172.021.10.100
 IPAddress3:            {@IPAddress3}            0.0.0.0
 IPAddress4:            {@IPAddress4}            0.0.0.0
 KBLayout:              {@KBLayout}              00000407
 LogonDomain:           {@LogonDomain}           Domain
 LogonServer:           {@LogonServer}           \\SRV-DCPC1
 LogonDNSDomain:        {@LogonDNSDomain}        DOMAIN.LAN
 OSArch:                {@OSArch}                X64
 OSBuild:               {@OSBuild}               18363
 OSLang:                {@OSLang}                0407
 OSServicePack:         {@OSServicePack}         1
 OSType:                {@OSType}                WIN32_NT
 OSVersion:             {@OSVersion}             WIN_10
</pre>

#### Pfade:
<pre>
 ScriptDir:             {@ScriptDir}             S:\MyTools\Kubus4QA
 GlobalDir:             {@GlobalDir}             G:\MyTools\Global\Data
 PersonalDir:           {@PersonalDir}           P:\MyTools\Global\Data
 AppDataDir:            {@AppDataDir}            C:\Users\<ich1>\AppData\Roaming
 DesktopCommonDir:      {@DesktopCommonDir}      C:\Users\Public\Desktop
 DesktopDir:            {@DesktopDir}            C:\Users\<ich1>\Desktop
 DocumentsCommonDir:    {@DocumentsCommonDir}    C:\Users\Public\Documents
 FavoritesCommonDir:    {@FavoritesCommonDir}    C:\Users\<gloabl1>\Favorites
 FavoritesDir:          {@FavoritesDir}          C:\Users\<ich1>\Favorites
 HomeDrive:             {@HomeDrive}             C:
 HomePath:              {@HomePath}              \Users\<ich1>
 HomeShare:             {@HomeShare}             \Users\<share1>
 LocalAppDataDir:       {@LocalAppDataDir}       C:\Users\<ich1>\AppData\Local
 MyDocumentsDir:        {@MyDocumentsDir}        C:\Users\<ich1>\Documents
 ProgramFilesDir:       {@ProgramFilesDir}       C:\Program Files
 ProgramsCommonDir:     {@ProgramsCommonDir}     C:\ProgramData\Microsoft\Windows\Start Menu\Programs
 ProgramsDir:           {@ProgramsDir}           C:\Users\<ich1>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs
 ScriptFullPath:        {@ScriptFullPath}        C:\MyTools\Kubus4QA\K4QA.exe
 StartMenuCommonDir:    {@StartMenuCommonDir}    C:\ProgramData\Microsoft\Windows\Start Menu
 StartMenuDir:          {@StartMenuDir}          C:\Users\<ich1>\AppData\Roaming\Microsoft\Windows\Start Menu
 StartupCommonDir:      {@StartupCommonDir}      C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
 SystemDir:             {@SystemDir}             C:\WINDOWS\system32
 TempDir:               {@TempDir}               C:\Users\<ich1>\AppData\Local\Temp
 UserProfileDir:        {@UserProfileDir}        C:\Users\<ich1>
 WindowsDir:            {@WindowsDir}            C:\WINDOWS
 WorkingDir:            {@WorkingDir}            C:\MyTools\Kubus4QA
</pre>

Eigene MagicWords: (Siehe)
<pre>
 Eigenes Word 1:        {@MW1}                   Das
 Eigenes Word 2:        {@MW2}                   ist
 Eigenes Word 3:        {@MW3}                   eine
 Eigenes Word 4:        {@MW4}                   neue
 Eigenes Word 5:        {@MW5}                   Funktion
 Eigenes Word 6:        {@MW6}                   für
 Eigenes Word 7:        {@MW7}                   die
 Eigenes Word 8:        {@MW8}                   eigenen
 Eigenes Word 9:        {@MW9}                   Magic
 Eigenes Word 10:       {@MW10}                  Words
</pre>
