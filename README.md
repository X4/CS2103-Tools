# Compilerbau Tools (CB)

## Um die Fehlersuche angenehmer zu machen
Sicher habt Ihr schon eine parser.out generiert und euch die Grammatik eurer Sprache zu Gemüte geführt, nebenbei den abstrakten Syntaxbaum eures SPL-Compilers und die der Referenzimplementierung in einem Anderen Tab zu vergleichen versucht. Nach kurzer Zeit verliert man dann den Überblick und errinnert sich nicht mehr welchen Fehler man eigentlich suchte. Kommt das bekannt vor?
Wenn euch Bison noch erzürnt schaut euch 'man bison' bzw. 'info bison' für detailiertere Angaben an. Wer mehr will und Beispiele sucht findet diese in 'bison.pdf'.

## Ein schnellerer Buildvorgang
Ich nutze während der Entwicklung TCC und für Releases GCC. Es ist schneller und ich probiere gerne neues. ↪ [TCC](http://bellard.org/tcc/) ist vielen nicht bekannt, aber tcc hat nahezu alle features die auch gcc hat, außer der Platform Portabilität. Linux kernel compilierung ist 30% schneller (10 seconds @2.4 GHz Intel P4) siehe: ↪ [TCC vs GCC](http://bellard.org/tcc/#speed)
Optional: Durch den parameter -j könnt ihr mehr Prozessoren/Cores zur compilirung nutzen. Bsp: make -j6 macht in diesem fall keinen sinn da die Compilierung selten lange dauert und race-conditions auftreten können.

## Makefile Targets
make run → Führt einfach alle SPL Programm unter Tests/ aus

make ast → Führt ./spl --absyn aus für all eure SPL Programme in Tests/

make fast → Compiliert mit TCC statt GCC

make verify → Zeigt welche Dateien noch nicht mit eurem Compiler laufen.

make tests → Führt einfach alle SPL Programme in Tests/ beginnend mit test?? aus. (original)

make scannerTest → Führt den SPL-Compiler interaktiv mit dem flag --tokens flag aus und gibt erkannte token an (HU1).

make scannerTest2 → Führt den SPL-Compiler interaktiv mit dem flag --tokens flag aus und gibt erkannte token an (HU2).

make scannerRef → Führt den Referenzcompiler interaktiv mit dem flag --tokens flag aus und gibt erkannte token an (HU2).

make parserTest → Führt den SPL-Compiler interaktiv aus und gibt die Ausgabe zurück (HU1).

make parserTest2 → Führt den SPL-Compiler interaktiv aus und gibt die interpretierte Ausgabe zurück (HU2).

make parserRef → Führt den Referenzcompiler interaktiv aus und gibt die interpretierte Ausgabe zurück (HU1).

make astTest → Führt den SPL-Compiler interaktiv mit dem flag --absyn aus und gibt den AST aus (HU1).

make astTest2 → Führt den SPL-Compiler interaktiv mit dem flag --absyn aus und gibt den AST aus (HU2).

make astRef → Führt den Referenzcompiler interaktiv mit dem flag --absyn aus und gibt den AST aus (HU1).

Details zu verify:
Erzeugt euch einen AST cache zu euren SPL Programmen aus der Referenzimplementierung (Tests/*.absyn) und jeweils eine Datei mit allen Parserbäumen eurer Testprogramme unter nutzung des Referenzcompilers (parser_referenz.txt) und eurem Programm (parser_test.txt). Anschließend wird ein diff aus diesen beiden Dateien erstellt und in parser_unterschiede.txt abgelegt. Das nützlichste Feature allerdings ist, dass auf der Konsole visuell gezeigt wird Welche SPL Prgrammme vermutlich auf eurem SPL-Commpiler nicht funktionieren. Das ist keine Garantie!! Wenn Ihr die Semantische Analyse noch nicht gemacht habt, ist es absolut logisch das zum Beispiel eine leere SPL Datei nicht Kompiliert in der Referenzimplementierung aber in eurer Version schon.

### Warum geht 'make fast' nicht?
sudo apt-get install tcc

### Warum läuft verify nicht unter Mac OSX?
Tut mir leid, habe momentan keine Referenzimplementierung die auf Mac compiliert wurde, aber werde sobald möglich eine hinzufügen.
Ich denke manches wird bei Mac nicht funktionieren wie zum beispiel die Bash Farben, wenn Ihr einen Mac habt, schickt mir einen pull request bzw. fix. und ich kümmer mich drum, bzw lege eine OSX branch an.

### Fragen?
RTFM und README_SPL
Happy Hacking :)

### Credits: Herr Ulbrich für tricks in verify, Marcel für den ansatz in verify, Herr Geisse für die Referenzimplementierung
