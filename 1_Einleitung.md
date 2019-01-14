# 1. Einleitung

Da sich die Anforderungen im Big-Data-Bereich stetig verändern, müssen Datenbanken in der Lage sein, sowohl kleinere Datenmengen in Echtzeit als auch große Datenmengen zuverlässig zu verarbeiten. Dabei müssen die Systeme auch verteilt, skalierbar, verfügbar und fehlertolerant sein.  

Vor allem in Bereichen mit kontinuierlichem Datenstrom, zu finden in Internet of Things, eCommerce, Online Advertising, ist eine derartige Verarbeitung notwendig. Sie benötigen genaue und umfassende Views der großen Datenmengen, aber auch niedrige Latenz, Durchsatz und hohe Fehlertoleranz. [2, 4]

Da klassische Datenbanken auf diese Anforderungen nicht flexibel genug reagieren, hat der Softwareentwickler Nathan Marz im Jahr 2012 die Lambda-Architektur entwickelt. Dabei handelt es sich mehr um eine Spezifikation, die einen allgemeinen Ansatz für den Systementwurf liefert. Sie gibt keine bestimmte Technologie vor und hat das Ziel, Batch- und Echtzeit-Views zu kombinieren und die Ergebnisse mit geringer Latenz zurückzugeben. Außerdem beschäftigt sie sich mit den drei Vs des Big-Data-Problems: Volume, Velocity, Variety. [4]  

Dabei ist sie so aufgebaut, dass sie generisch, skalierbar und tolerant gegenüber Hardwareausfällen und menschlichen Fehlern sein soll. Sie findet Verwendung in BigData-Systemen, wo es erforderlich ist, die Latenz bei Aktualisierungsvorgängen möglichst gering zu halten.
 [3]  

Die Bezeichnung stammt vom Lambda-Kalkül, was zu den Grundlagen der funktionalen Programmierung gehört. Ein wesentliches Merkmal dabei sind die __immutable data__, also unteränderliche Daten, welche in der Lambda-Architektur so umgesetzt sind. [1]

[**[Beam18a]**](10_Literaturverzeichnis.md)

------------

[☜ vorheriges Kapitel](README.md)
   |   [nächstes Kapitel ☞](2_Grundlagen.md)