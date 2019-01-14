## 3. Architektur
Auf der technischen Ebene besteht die Lambda-Architektur aus den drei Schichten: Batch Layer, Serving Layer und Speed Layer. Abbildung x zeigt deren Zusammenspiel.  

![Alt-Text](/images/layers.png)[3]  

1. Im ersten Schritt werden alle eingehenden Daten sowohl zum Batch Layer als auch zum Speed Layer geschickt.
2. Im Batch Layer wird der Master-Dataset verwaltet, das heißt die eingehenden Daten werden hier an den Master-Datensatz drangehängt. Weiterhin werden hier die Batch Views vorberechnet und an den Serving Layer weitergeleitet.
3. Im Serving Layer werden die Batch Views indiziert und können so mit niedriger Latenz angefragt werden.
4. Der Speed Layer behandelt nur die neuesten Daten. Hier wird die hohe Latenzzeit der Aktualisierungen ausgeglichen. So entstehen die Real-Time Views.
5. Eingehende Anfragen werden beantwortet, indem die Ergebnisse aus Batch Views und Real-Time-Views zusammengeführt werden. [3]


Im Folgenden werden die genauen Funktionsweisen der einzelnen Schichten beschrieben.

### 3.1 Batch Layer
Der Batch Layer hält sämtliche Fakten in redundanter Ausführung. Bei Aktualisierungen werden neue zusätzliche Daten an den entsprechenden Master-Datensatz drangehängt und beim nächsten Durchlauf berücksichtigt. Berechnungen können uneingeschränkt stattfinden und es ist keine Normalisierung notwendig. Außerdem sind sie horizontal skalierbar und die Berechnungen sind idempotent (liefert bei gleichem Input immer dieselben Ergebnisse). Aufgrund der hohen Faktenmenge können Berechnungen zu hoher Latenz führen. [1][3]  

- Views-Generierung  
- Map-Reduce  
- Serialisierung und Schema  
- Batch View Database

### 3.2 Server Layer
Im Serving Layer werden die Ergebnisse der Berechnungen gespeichert und die Informationen können von externen Systemen abgefragt werden. Wenn eine Berechnung beendet wird, werden die entsprechenden Daten im Layer durch die neuen ersetzt. So entfallen komplexe Aktualisierungsmechanismen und die Latenz wieder gesenkt. [1]  
Weiterhin fragt der Layer die Batch Views aus dem Batch Layer und die Real-Time-Views aus dem Speed Layer ab und vereinigt sie als Antwort auf Abfragen. [3]  

- Durchschnitt abfragen mit CQRS

### 3.3 Speed Layer
Da der Serving Layer durch die hohe Latenz des Batch Layers womöglich nicht den aktuellen Stand hält, wird der Speed Layer benötigt. Wie beim Batch Layer werden hier die neuen Daten empfangen und darauf die Berechnungen ausgeführt, allerdings wird nur ein begrenztes Datenfenster gespeichert. Somit zeigt er lediglich die letzten wenigen Stunden, während der Batch Layer alle Daten hält. Nach der Berechnung werden die Ergebnisse ebenfalls temporär gespeichert und gewähren wegen der niedrigen Latenz eine aktuellere Sicht auf die Daten. Holt der Batch Layer in der Aktualität auf und reicht die Informationen an den Serving Layer weiter, werden diese Informationen im Speed Layer gelöscht. Die Ergebnisse aus Serving Layer und Speed Layer werden durch ein externes System kombiniert und erlaubt es somit Ergebnisse in Real-Time zu bekommen.  

Dafür hält der Layer die ganze Komplexität. Hier wird mit Hilfe von verschiedenen __Strategien__ entschieden, wie neue Ergebnisse mit bereits vorhandenen Informationen kombiniert werden können. Die Komplexität erlaubt es auch, bei Fehlern direkt eine automatische Korrektur auszuüben.  

- Strategien  
- Real Time Views

[☜ vorheriges Kapitel](2_Grundlagen.md)
   |   [nächstes Kapitel ☞](4_Praxis.md)