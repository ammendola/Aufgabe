# Datenintensive und datenfokussierte Aktivitäten in der ULB Münster

## Einleitung

In dieser Arbeit werde ich zunächst zahlreiche datenbasierte Prozesse und Aktivitäten innerhalb der ULB Münster auflisten und darin jeweils kurz beschreiben, welche Daten in welcher Reihenfolge und in welcher Art und Weise in diesen Arbeitsprozessen fließen. Anschließend soll anhand zweier Beispiele der Umgang mit den Daten herausgearbeitet werden, um in einem letzten Schritt das Optimierungspotential dieser Prozesse zu beleuchten.

## Datenflüsse und -aktivitäten im ULB-Kerngeschäft

1. Online-Katalog + Discovery-System

Als einer der ältesten und wichtigsten datenbasierten Systeme ist der bereits in den 1990er entwickelte Online-Katalog (damals noch OPAC) zu nennen. In diesem Katalog kann man alle Bücher, Zeitschriften und sonstige Medien der ULB-Zentralbibliothek, der Zweigbibliotheken und aller Institutsbibliotheken der WWU Münster recherchieren. Als Sammelstelle dieser Katalogdaten dient eine zentrale Datenbank (= PostgresSQL), in welche alle benötigten Katalogdaten aus den kooperierenden Bibliotheken migriert werden. In den meisten Fällen über den bibliothekarischen Standard MARC21XML. Solche MARC21XML-Packages werden per FTP-Server in den Index der zentralen Datenbank gespielt und dahingehend interpretiert, d.h. so gemappt, dass sie als brauchbare Katalogdaten im Online-Katalog angezeigt werden. In die zentrale Datenbank gehen ebenso alle Katalogdaten aus dem Discovery-System der ULB ein (= Primo Central der Fa. *Exlibris*). Diese Katalogdaten kommen allerdings aus dem Discovery-System selbst und werden per OAI-Schnittstelle in die zentrale Datenbank gespeist und verarbeitet. Sämtliche Daten aus der zentralen Datenbank werden zweifach abgesichert: Zum einen durch einen dreimal pro Woche automatisiert stattfindenden Backup auf einem externen Backup-Server, der den Katalogbestand auf dem Stand des zurückliegenden Monats absichert, zum anderen durch einen Backup Slave, der als immerwährende Kopie der zentralen Datenbank den aktuellen Zustand dupliziert und für den Fall eines plötzlichen (physischen) Verlustes der Datenbank gedacht ist. Im Hinblick auf den Online-Katalog sei noch erwähnt, dass hier persönliche Daten der Angehörigen der WWU verwaltet werden. Diese Daten stammen aus dem Identitätsmanagement der WWU Münster, verwaltet im hiesigen Rechenzentrum (ZIV), und werden mittels eines standardisierten Netzwerkprotokolls (LDAP) für die Nutzung der persönlichen ULB-Konten verwendet.   

2. Backup, Statistik

3. (Retro)digitalisierung

Die ULB digitalisiert bereits seit einigen Jahre ihre historischen Bestände systematisch bzw. nach bestimmten strategischen Kriterien (Westfalica, Historische Drucke, Nachlässe) und verwendet hierfür die Software [Visual Library (VL)](https://www.semantics.de/visual_library/{:target="_blank"}) der Aachener Fa. *semantics*. Die VL ist eine speziell für Bibliotheken un Informationseinrichtungen entwickelte Visualisierungssoftware u.a. im Bereich Retrodigitalisierung. In Verbindung mit der Software [Multidotscan](http://www.walternagel.de/multidotscan) der mit *semantics* kooperierenden Bielefelder Fa. *Walter Nagel* lässt sich der gesamte Prozess von der Digitalisierung bis hin zur Präsentation im Portal der ULB durchautomatisiert abbilden. Zunächst wird am jeweiligen Buchscanner ein Scan-Job eingerichtet, der für den Job eine eindeutige Id generiert (= HT-Nummer) und per nächtlichem Import automatisch auf dem VL-Server abgelegt wird. Anschließend werden die Titeldaten über eine Abfrage der HT-Nummer aus dem Verbundkatalog des hbz in Köln importiert und gemeinsam mit den Images in der VL angezeigt. Nachdem anschließend die sog. VL-Manager den Titel inhaltlich strukturiert haben (Inhaltsverzeichnis, Buchkapitel etc.), wird der Titel freigegeben, mit einer Nutzungslizenz versehen und in den [Digitalen Sammlungen der ULB](https://sammlungen.ulb.uni-muenster.de/) angezeigt.  

4. Elektronischer Semesterapparat (ESA)

5. Forschungsdatenmanagement

## Datenintensive Projekte mit ULB-Beteiligung

1. Linked Open Data (LODUM)

2. Opening Reproducible Research (O2R)

3. sciebo-research Data Services (sciebo-RDS)

4. Digitales Archiv NRW (DA NRW)

5. Digitalisierung Historischer Zeitungen NRW

6. FID Benelux

## Beispiel 1: Elektronischer Semesterapparat (ESA)

- Projektskizze mit Workflow

## Beispiel 2: Digitalisierung Historischer Zeitungen NRW

- Projektskizze mit Workflow
