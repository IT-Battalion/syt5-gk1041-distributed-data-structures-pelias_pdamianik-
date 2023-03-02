# GK1041 Datenmanagement "Distributed Data Structures"

## von Philip Damianik und Patrick Elias

### Apache Spark, Atomix, Hadoop und Storm

Apache Spark, Atomix (wenig Doku), und Storm sind alle Frameworks, die für verteiltes Rechnen in der Cloud-Umgebung ausgelegt sind, während Hadoop eine Sammlung an Technologien für distrubuted computing ist, unter anderem einem verteiltem Dateisystem HDFS (Hadoop Distrubted File System), einer Framework, für verteiltes Rechnen MapReduce und einem Scheduler und Monitor von verteilten Applikationen und Resourcen YARN. Hier sind einige Vergleiche zwischen diesen Frameworks:

**Architektur:**

- Apache Spark und Hadoop verwenden ein Master/Worker-Modell, bei dem ein zentraler Master-Knoten die Arbeit an die einzelnen Worker-Knoten verteilt.
- Die Grundstruktur in Apache Storm ist die sog. "Topology". Diese Topology ist praktisch ein gerichteter Graph bestehend aus Spouts, Bolts (Nodes) und Streams Edges. Spouts sind Datenquellen, die Daten von externen Quellen in eine von Storm verarbeitbare Form umwandeln oder selbst Daten generieren. Streams bilden die Edges in dem Graph und sind eine kontinuierliche Folge an Tuples (gruppierte, benannte Daten) die von einer Edge an eine andere übertragen werden. Bolts kümmern sich um die Verarbeitung der Daten und liefern aus einem oder mehreren Eingabe-Streams die verarbeiteten Daten in Form von einem oder mehreren Ausgabe-Streams. [4]

**Programmiersprachen:**

- Apache Spark unterstützt eine Vielzahl von Programmiersprachen, darunter Java, Scala, Python und R.
- Hadoop ist in Java geschrieben und bietet APIs für andere Programmiersprachen.
- Atomix ist in Go geschrieben und bietet mittels gRPC eine API [5] für eine Vielzahl an Programmiersprachen [6] und SDKs für sowohl Go als auch Java.
- Ähnlich ist Storm, welches in Java geschrieben ist. Mit einer zentralen Thift Definitionsdatei bietet Storm die Möglichkeit von verschiedensten Programmiersprachen aus mit Storm zu arbeiten.

**Datenverteilung und gemeinsamer Speicher:**

- In Hadoop ist die grunsätzliche Form von Daten die RDDs welche eine Datenstruktur darstellt, welche auf die Nodes des Clusters verteilt werden. Eine der Quellen dieser RDDs und gleichzeitig die Speicherung der Ergebnisse der Berechnungen übernimmt ein verteiltes Filesystem, standardmäßig HDFS. [6] Apache Spark läuft im Normalfall auf Hadoop und hat daher die gleichen Basiselemente. Storm verwendet Tupel (eine Sammlung von benannten Daten), deren Einzige Anforderung die Serialisierung ist, zur Datenverteilung und Speicherung.

**Performance:**

- Spark ist bekannt für seine schnelle Verarbeitung großer Datenmengen und ist daher bei Anwendungen mit hohen Anforderungen an paralleles Rechnen und Datenverarbeitung sehr beliebt. Hadoop hat ähnliche Leistungsmerkmale, obwohl es oft als langsamer als Spark angesehen wird. Atomix und Storm sind im Allgemeinen nicht so schnell wie Spark oder Hadoop.

**Notifikation von Master oder anderen Slaves:**

- Spark und Hadoop verfügen über Mechanismen zur Benachrichtigung von Master-Knoten und anderen Worker-Knoten. Storm verwendet eine ereignisbasierte Architektur, bei der Knoten auf Ereignisse und Nachrichten reagieren.

Zusammenfassend lässt sich sagen, dass alle Frameworks in der Cloud-Umgebung einsetzbar sind und für verteiltes Rechnen ausgelegt sind. Spark und Hadoop sind besonders gut geeignet für Anwendungen mit hohen Anforderungen an paralleles Rechnen und Datenverarbeitung, während Storm besser für Anwendungen geeignet ist, die Daten in Echtzeit verarbeiten. Die Auswahl eines Frameworks hängt von den spezifischen Anforderungen der Anwendung ab. [1][2][3]

**RDD ->** steht für "Resilient Distributed Datasets" und ist ein zentraler 
Bestandteil des Apache Spark-Frameworks. RDDs sind eine 
Abstraktionsebene, die es ermöglicht, große Datenmengen in einem Cluster
 parallel zu verarbeiten. Sie sind resilient, da sie automatisch auf 
fehlgeschlagene Knoten im Cluster reagieren und ihre Daten replizieren 
können, um sicherzustellen, dass die Datenverarbeitung fehlertolerant 
und skalierbar bleibt. [1]

#### Tasks
Tasks sind Einheiten von Aufgaben oder Prozessen, die von einem 
Computersystem ausgeführt werden können. In der Regel bestehen sie aus 
einer Reihe von Schritten oder Algorithmen, die eine bestimmte Funktion 
erfüllen oder ein bestimmtes Ziel erreichen sollen. Tasks können 
unterschiedliche Komplexitätsstufen aufweisen, von einfachen Operationen 
wie das Sortieren einer Liste bis hin zu komplexen Verarbeitungsprozessen 
wie die Analyse von großen Datensätzen.

Beispiele für einfache Tasks sind:

   - Das Sortieren einer Liste von Zahlen in aufsteigender oder 
absteigender Reihenfolge
   - Das Durchsuchen einer Textdatei nach einem bestimmten Wort oder 
Ausdruck
   - Die Berechnung der Summe oder des Durchschnitts einer Liste von 
Zahlen
   - Die Generierung eines zufälligen Passworts
   - Das Laden von Daten aus einer Datenbank

Beispiele für komplexe und aufteilbare Tasks sind:

    - Die Analyse großer Datensätze, z.B. zur Erstellung von 
Vorhersagemodellen in der künstlichen Intelligenz oder Machine Learning
    - Die Erstellung von Grafiken oder Diagrammen aus großen Datenmengen
    - Die Simulation von physikalischen Prozessen oder komplexen Systemen
    - Die Aufteilung von Daten in kleinere Teilmengen, die von mehreren 
Rechenknoten gleichzeitig verarbeitet werden können, um die 
Verarbeitungsgeschwindigkeit zu erhöhen.

Diese komplexen und aufteilbaren Tasks erfordern häufig eine Aufteilung in 
mehrere Teilaufgaben, die parallel auf verschiedenen Rechenknoten 
ausgeführt werden können. Dies kann durch das Master/Worker Pattern oder 
das Map-Reduce Pattern erreicht werden.

Beim Master/Worker Pattern ist ein zentraler Master-Server für die 
Aufteilung und Koordination der Aufgaben zuständig. Der Master-Server 
teilt den Tasks die verfügbaren Worker-Knoten zu und sammelt die 
Ergebnisse wieder ein, wenn die Verarbeitung abgeschlossen ist. Das 
Map-Reduce Pattern ist eine spezielle Form des Master/Worker Patterns, bei 
dem die Daten automatisch in kleine Teilmengen aufgeteilt werden und 
parallel von mehreren Worker-Knoten verarbeitet werden können, bevor sie 
wieder zusammengeführt werden.

Ein Beispiel für den Einsatz des Master/Worker Patterns ist die Analyse 
großer Datenmengen in der Wissenschaft oder im Geschäftsumfeld. Hier 
können die Daten in kleinere Teilmengen aufgeteilt und von mehreren 
Rechenknoten gleichzeitig verarbeitet werden, um die 
Verarbeitungsgeschwindigkeit zu erhöhen und die Ergebnisse schneller zu 
erhalten.

#### Atomix

Ich habe mich dazu entschieden erstmal Atmoix [7] zu testen. Hierfür habe ich mir das verlinkte Repository angesehen und nachgebaut. 

Anschließend habe ich mir von Mavencentral den standalone atomix server heruntergeladen und ihn wie im Tutorial beschrieben versucht zu starten.

`java -jar atomix-standalone-server-1.0.8.jar -address 127.0.0.1:8700 -bootstrap -config atomix.properties`

Dabei habe ich jedoch immer wieder den selben Fehler bekommen:
`kein Hauptmanifestattribut, in atomix-standalone-server-1.0.8.jar`

Außerdem bin ich auf ein weiteres Problem gestoßen: Was gehört in die atomix.properties? Ich habe intensive nach einer Lösung gesucht doch für beide Probleme keine gefunden: Der Manifest Error kommt daher, dass in der Manifest Datei keine main Class angegeben wurde, das konnte ich bestätigen, indem ich die jar dekompiliert habe. 

Weiteres ist im übrigen die Dokumentation auf der Website nicht vollständig und teilweise fehlen Abschnitte.

#### Spark

Da Atomix leider wirklich überhauptnicht funktioniert hat, haben wir uns an Spark herangewagt. Dazu haben wir uns wie auch bei Atomix erstmal examples angeschaut und das repository geklont. Anschließend habe ich mithilfe von `./build/mvn -DskipTests clean package` Spark und vorallem die Examples gebuildet. 

Dann habe ich mittels `./bin/run-example SparkPi` das Pi example ausgeführt.

Das hat funktioniert !!! :D

#### RMI

Da Prof. Roschger der Überzeugung war, das unser RMI Beispiel vom letzten Semester eine akzeptable Abgabe für diese Übung ist, haben wir auch unseren RMI Code hinzugefügt. :)

## Quellen

[1] ChatGPT; 

[2] "Apache Storm Vs Apache Spark [Comparison]"; [Apache Storm Vs Apache Spark [Comparison] - Whizlabs Blog](https://www.whizlabs.com/blog/apache-storm-vs-apache-spark/); zuletzt besucht am 16.02.2023

[3] "Understanding Hadoop v/s Spark v/s Storm"; [Understanding Hadoop v/s Spark v/s Storm | Cognixia](https://www.cognixia.com/blog/understanding-hadoop-vs-spark-vs-storm/); zuletzt besucht am 16.02.2023

[4] "Apache Storm - Concepts"; https://storm.apache.org/releases/2.4.0/Concepts.html; zuletzt besucht am 16.02.2023;

[5] "Atomix User Guide - Architecture"; https://atomix.io/user-guide/architecture/; zuletzt besucht 16.02.2023

[6] "gRPC Languages"; https://grpc.io/docs/languages/; zuletzt besucht 16.02.2023

[6] "Apache Spark RDD Programming Guide"; https://spark.apache.org/docs/latest/rdd-programming-guide.html#resilient-distributed-datasets-rdds; zuletzt besucht 16.02.2023

[7] "Introduction to Atomix"; [Introduction to Atomix | Baeldung](https://www.baeldung.com/atomix); zuletzt besucht am 16.02.2023

