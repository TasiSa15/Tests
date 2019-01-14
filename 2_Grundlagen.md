## 2. Grundlagen
Während andere Architekturen wie SQL- und NoSQL-Datenbanken bei Aktualisierungen ihre Master-Daten manipulieren, sind diese bei der Lambda-Architektur nicht veränderlich. Stattdessen wird bei jeder Aktualisierung ein neuer Datensatz erstellt und mit einem Zeitstempel versehen. [3]  

Hier sieht man, wie alte DBs aufgebaut sind:  
![Alt-Text](/images/normaleDBs.png)[3]  

Bei relationalen Datenbanken werden bei Aktualisierungen die betroffenen Zeilen in der Datenbank blockiert, sodass diese aus anderer Stelle nicht gleichzeitig bearbeitet werden können. Diese Funktionsweise verschlechtert die Verfügung der Anwendung und dessen Performance.[1]  

Und hier die Lambda-DB:  
![Alt-Text](/images/lambdaDB.png)[3]  

Bei jeder Veränderung wird eine Kopie der Master-Daten erzeugt. Die vorhandenen Daten werden niemals aktualisiert. Der veränderte Datensatz wird als Faktum bezeichnet und gilt zu einem bestimmten Zeitpunkt, gezeichnet durch einen Zeitstempel, als wahr. (append-only)  
Aus den Berechnungen der einzelnen Fakten werden Informationen abgeleitet, wobei die Informationen als eine Funktion der Fakten definiert werden. Es gilt:  

Information = Funktion (Fakten)

Mit dieser Architektur kann nicht nur auf den letzten Stand des Datensatzes, sondern auf alle Werte und Veränderungen des Datensatzes zugegriffen werden. Da die Fakten von den Informationen getrennt werden, wird das System fehlertoleranter. Bei enstehenden Fehlern kann das Ergebnis einfach verworfen und mit Hilfe der Fakten neu berechnet werden.[1]

[☜ vorheriges Kapitel](1_Einleitung.md)
   |   [nächstes Kapitel ☞](3_Architektur.md)