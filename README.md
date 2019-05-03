# Datenintensive und datenfokussierte Aktivitäten in der ULB Münster

## Einleitung

In dieser Arbeit werden zunächst zahlreiche datenbasierte Prozesse und Aktivitäten innerhalb der ULB Münster aufgelistet und darin jeweils kurz beschreiben, welche Daten in welcher Reihenfolge und in welcher Art und Weise in den Arbeitsprozessen fließen. Anschließend sollen anhand zweier Beispiele Optimierungspotentiale dieser Prozesse beleuchtet werden.

## Datenflüsse und -aktivitäten im ULB-Kerngeschäft

1. Online-Katalog + Discovery-System

Als einer der ältesten und wichtigsten datenbasierten Systeme ist der bereits in den 1990er entwickelte Online-Katalog (damals noch OPAC) zu nennen. In diesem Katalog kann man alle Bücher, Zeitschriften und sonstige Medien der ULB-Zentralbibliothek, der Zweigbibliotheken und aller Institutsbibliotheken der WWU Münster recherchieren. Als Sammelstelle dieser Katalogdaten dient eine zentrale Datenbank (= PostgresSQL), in welche alle benötigten Katalogdaten aus den kooperierenden Bibliotheken migriert werden. In den meisten Fällen über den bibliothekarischen Standard MARC21XML. Solche MARC21XML-Packages werden per FTP-Server in den Index der zentralen Datenbank gespielt und dahingehend interpretiert, d.h. so gemappt, dass sie als brauchbare Katalogdaten im Online-Katalog angezeigt werden. In die zentrale Datenbank gehen ebenso alle Katalogdaten aus dem Discovery-System der ULB ein (= Primo Central der Fa. *Exlibris*). Diese Katalogdaten kommen allerdings aus dem Discovery-System selbst und werden per OAI-Schnittstelle in die zentrale Datenbank gespeist und verarbeitet. Sämtliche Daten aus der zentralen Datenbank werden zweifach abgesichert: Zum einen durch einen dreimal pro Woche automatisiert stattfindenden Backup auf einem externen Backup-Server, der den Katalogbestand auf dem Stand des zurückliegenden Monats absichert, zum anderen durch einen Backup Slave, der als immerwährende Kopie der zentralen Datenbank den aktuellen Zustand dupliziert und für den Fall eines plötzlichen (physischen) Verlustes der Datenbank gedacht ist. Im Hinblick auf den Online-Katalog sei noch erwähnt, dass hier persönliche Daten der Angehörigen der WWU verwaltet werden. Diese Daten stammen aus dem Identitätsmanagement der WWU Münster, verwaltet im hiesigen Rechenzentrum (ZIV), und werden mittels eines standardisierten Netzwerkprotokolls (LDAP) für die Nutzung der persönlichen ULB-Konten verwendet.   

2. Backup, Statistik

3. (Retro)digitalisierung

Die ULB digitalisiert bereits seit einigen Jahre ihre historischen Bestände systematisch bzw. nach bestimmten strategischen Kriterien (Westfalica, Historische Drucke, Nachlässe) und verwendet hierfür die Software [Visual Library (VL)](https://www.semantics.de/visual_library/) der Aachener Fa. *semantics*. Die VL ist eine speziell für Bibliotheken un Informationseinrichtungen entwickelte Visualisierungssoftware u.a. im Bereich Retrodigitalisierung. In Verbindung mit der Software [Multidotscan](http://www.walternagel.de/multidotscan) der mit *semantics* kooperierenden Bielefelder Fa. *Walter Nagel* lässt sich der gesamte Prozess von der Digitalisierung bis hin zur Präsentation im Portal der ULB durchautomatisiert abbilden. Zunächst wird am jeweiligen Buchscanner ein Scan-Job eingerichtet, der für den Job eine eindeutige Id generiert (= HT-Nummer) und per nächtlichem Import automatisch auf dem VL-Server abgelegt wird. Anschließend werden die Titeldaten über eine Abfrage der HT-Nummer aus dem Verbundkatalog des hbz in Köln importiert und gemeinsam mit den Images in der VL angezeigt. Nachdem anschließend die sog. VL-Manager den Titel inhaltlich strukturiert haben (Inhaltsverzeichnis, Buchkapitel etc.), wird der Titel freigegeben, mit einer Nutzungslizenz versehen und in den [Digitalen Sammlungen der ULB](https://sammlungen.ulb.uni-muenster.de/) angezeigt.  

4. Elektronischer Semesterapparat (ESA)

siehe Beispiel 1

5. Forschungsdatenmanagement

Ein weiteres Feld, in welchem ebenfalls zahlreiche Daten fließen, ist der Bereich Forschungsdatenmanagement innerhalb der ULB. Hier tritt die ULB gemeinsam mit dem zentralen Rechenzenrum (ZIV) als Servicedienstleister für die Wissenschaftler der WWU Münster auf, um die im Rahmen ihrer Forschungen auftretenden Daten aufzubereiten und langfristig zu speichern (max. 10 Jahre). In Form eines [Servicepunkts Forschungsdaten](https://www.uni-muenster.de/Forschungsdaten/angebote/ansprechpartner/) hilft die ULB den Wissenschaftlern bei forschungsdatenrelevanten Themen wie Antragstellung, Rahmenbedingungen, Datenmanagementplan, Datenschutz, Werkzeuge, Publizieren, Open Access und Langzeitarchivierung. Wenn man sich allein die im Forschungsdatenmanagement auftretenden Phasen als [Datenlebenszyklus](https://www.uni-muenster.de/Forschungsdaten/information/lebenszyklus/) vergegenwärtigt, wird klar, dass hier große Datenmengen und viele verschiedene Arten von Daten anfallen, und zwar bei der Erzeugung, Verarbeitung, Analyse, Archivierung, Zugang, Nachnutzung (und dann wieder) Erzeugung der Daten etc. Hierfür stellt die ULB gemeinsam mit dem ZIV die nötige IT-Infrastruktur und -software bereit und informiert auch im Rahmen von Schulungen und Workshops.

## Datenintensive Projekte mit ULB-Beteiligung

1. Linked Open Data (LODUM)

2. Opening Reproducible Research (O2R)

3. sciebo-research Data Services (sciebo-RDS)

4. Digitales Archiv NRW (DA NRW)

Das [Landesprojekt Digitales Archiv NRW](https://www.danrw.de/ueber-das-da-nrw/die-nrw-loesung/) hat sich auf ihrer Webseite Folgendes  auf ihre Fahnen geschrieben: „Das DA NRW ist ein informationstechnisches Angebot für alle Einrichtungen, die ihr elektronisches Kulturgut nach dem Archivgesetz und Pflichtexemplargesetz sicher und auf Dauer speichern müssen. Zur Nutzung von Synergieeffekten wird die Dienstleistung in einem Verbund verschiedener Dienstleister des Landes und der Kommunen bereitgestellt.“ Zudem sollen die Daten nicht nur langzeitarchiviert bzw. -gespeichert werden, sondern auch für die Zulieferung in weitere Portal dienen (DDB, Europeana). Als Testpartner der ersten Stunde hat die ULB Münster bereits Erfahrungen mit dem Workflow gesammelt, wie und auf welchen Wegen die Daten ins DA NRW migriert werden können. Für die Migration der Daten ins DA NRW spielt die Fa. *semantics* insofern eine Rolle, als sie für VL-Bibliotheken die vorhandenen Daten aus den jeweiligen Portalen in sog. Submission Information Packages (SIP) automatisiert zusammenfasst und per rsync-Netwerkprotokollen sowie einer Authentifizierung per SSH-keys ins DA NRW hochgeladen werden können. Hierfür muss die VL in einem automatisierten Serverjob die besagten SIP-Kapseln erstellen und in das Incomingverzeichnis des hbz in Köln transferieren. Für später veränderte Objekte werden Delta-Kapseln erstellt, damit auch die Veränderungen an Objekten und ihren Metadaten erfasst werden. Die Verwaltung der SIP-Kapseln selbst erfolgt im VL-Manager. Hier können die MitarbeiterInnen der jeweiligen Einrichtung verfolgen, ob eine SIP-Kapsel erfolgreich erstellt, übertragen und archiviert worden ist. Außerdem gibt es im VL-Manager Such- und Filtermöglichkeiten (VL-ID, URN, HBZ-ID) sowie eine Archivierungshistorie. Die Datenübertragungsstraßen von der VL ins DA NRW werden zurzeit eingerichtet und voraussichtlich im Sommer 2019 zur Nutzung freigegeben.

5. Digitalisierung Historischer Zeitungen NRW

siehe Beispiel 2

6. FID Benelux

Der Fachinformationsdienst (FID) Benelux ist ein DFG-gefördertes Projekt im Rahmen des Förderprogramms [Fachinformationsdienste für die Wissenschaft](https://www.dfg.de/foerderung/programme/infrastruktur/lis/lis_foerderangebote/fachinfodienste_wissenschaft/index.html) und ist das Nachfolgeformat der 2015 ausgelaufenen Sondersammelgebiete (SSG), hier des SSG Niederländischer Kulturkreis. Damit der FID seinem Selbstverständnis als „zentrale Anlaufstelle für forschungsrelevante Literatur und Informationen über die Kultur und Gesellschaft der Beneluxländer sowie für forschungsunterstützende Services“ gerecht werden kann, gibt es neben zahlreichen Services in der ULB das [Rechercheportal FID Benelux](https://www.fid-benelux.de/literatur-recherche/suche/) als zentrale Suchmaschine für forschungsrelevante Literatur über die Kultur und Gesellschaft der Beneluxländer. Um diese spezielle Literatur in einem eigenen Portal suchbar machen zu können, werden Benelux-relevante Titel von einschlägigen liefernden Bibliotheken entweder über MARC21XML-Exporte über einen FTP-Server in die zentrale Datenbank der ULB importiert, um von dort aus in den Online-Katalog und in das Discovery-System zu gelangen. Ein anderer Weg, um an relevante Literatur für das Rechercheportal zu gelangen, ist das Harvesten (Einsammeln) relevanter Literatur über offene OAI-Schnittstellen, die den offenen Austausch von Metadaten zum Ziel haben. Hierfür kommen zumeist sog. „OAI-Harvester“ zum Einsatz, wie etwa auch in der [Deutschen Nationalbibliothek (DNB)](https://www.dnb.de/DE/Service/DigitaleDienste/OAI/oai_node.html). Um die eingesammelten Metadaten nun mit dem genannten FTP-Server und der zentralen Datenbank der ULB zu synchronisieren und semantisch verstehbar zu machen, werden spezielle Computerprogramm namens Parser eingesetzt. 


## Beispiel 1: Elektronischer Semesterapparat (ESA)

- Projektskizze mit Workflow

## Beispiel 2: Digitalisierung Historischer Zeitungen NRW

- Projektskizze mit Workflow
