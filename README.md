# GK1041 Datenmanagement "Distributed Data Structures"

## von Philip Damianik und Patrick Elias

### Apache Spark, Atomix, Hadoop und Storm

Apache Spark, Atomix, Hadoop und Storm sind alle Frameworks, die für verteiltes Rechnen in der Cloud-Umgebung ausgelegt sind. Hier sind einige Vergleiche zwischen diesen Frameworks:

**Architektur:**

- Apache Spark und Hadoop verwenden ein Master/Worker-Modell, bei dem ein zentraler Master-Knoten die Arbeit an die einzelnen Worker-Knoten verteilt. Atomix und Storm verwenden ein verteiltes Modell, bei dem alle Knoten gleichberechtigt sind.
- Atomix und Storm verwenden eine ereignisbasierte Architektur, bei der Ereignisse und Nachrichten zwischen Knoten ausgetauscht werden, während Spark und Hadoop Daten in RDDs aufteilen und auf verschiedenen Knoten verteilen.

**Programmiersprachen:**

- Apache Spark unterstützt eine Vielzahl von Programmiersprachen, darunter Java, Scala, Python und R. Hadoop ist in Java geschrieben und bietet APIs für andere Programmiersprachen. Atomix bietet APIs für Java und C++. Storm ist in Java geschrieben, bietet aber auch APIs für andere Programmiersprachen.

**Datenverteilung und gemeinsamer Speicher:**

- Spark und Hadoop verwenden RDDs, um Daten in kleine Stücke aufzuteilen und auf verschiedenen Knoten zu verteilen. Atomix verwendet ein verteiltes Konsistenzmodell, das den gemeinsamen Zugriff auf Daten ermöglicht. Storm verwendet Tupel zur Datenverteilung und Speicherung.

**Performance:**

- Spark ist bekannt für seine schnelle Verarbeitung großer Datenmengen und ist daher bei Anwendungen mit hohen Anforderungen an paralleles Rechnen und Datenverarbeitung sehr beliebt. Hadoop hat ähnliche Leistungsmerkmale, obwohl es oft als langsamer als Spark angesehen wird. Atomix und Storm sind im Allgemeinen nicht so schnell wie Spark oder Hadoop.

**Notifikation von Master oder anderen Slaves:**

- Spark und Hadoop verfügen über Mechanismen zur Benachrichtigung von Master-Knoten und anderen Worker-Knoten. Atomix und Storm verwenden eine ereignisbasierte Architektur, bei der Knoten auf Ereignisse und Nachrichten reagieren.

Zusammenfassend lässt sich sagen, dass alle Frameworks in der Cloud-Umgebung einsetzbar sind und für verteiltes Rechnen ausgelegt sind. Spark und Hadoop sind besonders gut geeignet für Anwendungen mit hohen Anforderungen an paralleles Rechnen und Datenverarbeitung, während Atomix und Storm besser für ereignisbasierte Anwendungen geeignet sind. Die Auswahl eines Frameworks hängt von den spezifischen Anforderungen der Anwendung ab. [1][2][3]

**RDD ->** steht für "Resilient Distributed Datasets" und ist ein zentraler 
Bestandteil des Apache Spark-Frameworks. RDDs sind eine 
Abstraktionsebene, die es ermöglicht, große Datenmengen in einem Cluster
 parallel zu verarbeiten. Sie sind resilient, da sie automatisch auf 
fehlgeschlagene Knoten im Cluster reagieren und ihre Daten replizieren 
können, um sicherzustellen, dass die Datenverarbeitung fehlertolerant 
und skalierbar bleibt. [1]

#### Atomix

Ich habe mich dazu entschieden erstmal Atmoix [4] zu testen. Hierfür habe ich mir das verlinkte Repository angesehen und nachgebaut. 

Anschließend habe ich mir von Mavencentral den standalone atomix server heruntergeladen und ihn wie im Tutorial beschrieben versucht zu starten.

`java -jar atomix-standalone-server-1.0.8.jar -address 127.0.0.1:8700 -bootstrap -config atomix.properties`

Dabei habe ich jedoch immer wieder den selben Fehler bekommen:
`kein Hauptmanifestattribut, in atomix-standalone-server-1.0.8.jar`

Außerdem bin ich auf ein weiteres Problem gestoßen: Was gehört in die atomix.properties? Ich habe intensive nach einer Lösung gesucht doch für beide Probleme keine gefunden: Der Manifest Error kommt daher, dass in der Manifest Datei keine main Class angegeben wurde, das konnte ich bestätigen, indem ich die jar dekompiliert habe. 

## Quellen

[1] ChatGPT; 

[2] "Apache Storm Vs Apache Spark [Comparison]"; [Apache Storm Vs Apache Spark [Comparison] - Whizlabs Blog](https://www.whizlabs.com/blog/apache-storm-vs-apache-spark/); zuletzt besucht am 16.02.2023

[3] "Understanding Hadoop v/s Spark v/s Storm"; [Understanding Hadoop v/s Spark v/s Storm | Cognixia](https://www.cognixia.com/blog/understanding-hadoop-vs-spark-vs-storm/); zuletzt besucht am 16.02.2023

[4] "Introduction to Atomix"; [Introduction to Atomix | Baeldung](https://www.baeldung.com/atomix); zuletzt besucht am 16.02.2023
