# Compilerbau Tools (CB)

## Um die Fehlersuche angenehmer zu machen
Sicher habt Ihr schon eine parser.out generiert und euch die Grammatik eurer Sprache zu Gemüte geführt, nebenbei den abstrakten Syntaxbaum eures SPL-Compilers und die der Referenzimplementierung in einem Anderen Tab zu vergleichen versucht. Nach kurzer Zeit verliert man dann den Überblick und errinnert sich nicht mehr welchen Fehler man eigentlich suchte. Kommt das bekannt vor?

## Search and Destroy
Fehler finden und eliminieren, eure Hauptaufgabe solltet Ihr euch mehr widmen als manpages zu durchforstern um euer diff ordentlich zu bekommen und Compiler Flags zu suchen um mehr Debugging Ausgaben zu erhalten.

## Eure Waffe: Ein Makefile und ein Shell Script (+Docs)
Wenn euch Bison noch erzürnt schaut euch die man bison bzw. info bison für Detailiertere Angaben an. Wer mehr will und Beispiele sucht findet diese in bison.pdf

## Der Schnellste Compiler
Ich nutze während der Entwicklung TCC und für Releases GCC. Warum? Es ist schneller und warum eigentlich nicht, wenn es keine Bugs gibt? ↪ [TCC](http://bellard.org/tcc/) ist vielen nicht bekannt, aber er hat nahezu alle features die auch GCC hat, außer der Platform Portabilität. Linux kernel compilierung ist 30% schneller (10 seconds @2.4 GHz Intel P4) siehe: ↪ [TCC vs GCC](http://bellard.org/tcc/#speed)

## Makefile Targets
make run → Führt einfach alle SPL Programm unter Tests/ aus

make ast → Führt ./spl --absyn aus für all eure SPL Programme in Tests/

make fast → Compiliert mit TCC statt GCC

make verify → Zeigt welche Dateien noch nicht mit eurem Compiler laufen.

make tests → Führt einfach alle SPL Programme in Tests/ beginnend mit test?? aus. (original)

Details zu verify:
Erzeugt euch einen AST cache zu euren SPL Programmen aus der Referenzimplementierung (Tests/*.absyn) und jeweils eine Datei mit allen Parserbäumen eurer Testprogramme unter nutzung des Referenzcompilers (parser_referenz.txt) und eurem Programm (parser_test.txt). Anschließend wird ein diff aus diesen beiden Dateien erstellt und in parser_unterschiede.txt abgelegt. Das nützlichste Feature allerdings ist, dass auf der Konsole visuell gezeigt wird Welche SPL Prgrammme vermutlich auf eurem SPL-Commpiler nicht funktionieren. Das ist keine Garantie!! Wenn Ihr die Semantische Analyse noch nicht gemacht habt, ist es absolut logisch das zum Beispiel eine leere SPL Datei nicht Kompiliert in der Referenzimplementierung aber in eurer Version schon.

### Warum geht 'make fast' nicht?
sudo apt-get install tcc

### Warum läuft es unter Mac OSX läuft nicht?
Tut mir leid, habe momentan keine Referenzimplementierung die auf Mac compiliert wurde, aber werde sobald möglich eine hinzufügen.
Ich denke manches wird bei Mac nicht funktionieren wie zum beispiel die Bash Farben, wenn Ihr einen Mac habt, schickt mir nen pull request bzw. fix.

### Fragen?
RTFM und README_SPL
Happy Hacking :)
