# Datenintensive und datenfokussierte Aktivitäten in der ULB Münster

## Einleitung

In diesem Papier werden zunächst die wichtigsten datenbasierten Prozesse und Aktivitäten innerhalb der ULB Münster aufgelistet und darin jeweils kurz beschreiben, welche Daten in welcher Reihenfolge und in welcher Art und Weise in den Arbeitsprozessen fließen. Anschließend sollen anhand zweier Beispiele Optimierungspotenziale dieser Prozesse beleuchtet werden.

## Datenflüsse und -aktivitäten im ULB-Kerngeschäft

### 1. Online-Katalog + Discovery-System

Als eines der ältesten und wichtigsten datenbasierten Systeme ist der bereits in den 1990er Jahren entwickelte [Online-Katalog](https://katalogix.uni-muenster.de/Katalog/start.do) (damals noch OPAC) zu nennen. In diesem Katalog kann man alle Bücher, Zeitschriften und sonstigen Medien der ULB-Zentralbibliothek, der Zweigbibliotheken und aller Institutsbibliotheken der WWU Münster recherchieren.

Als Sammelstelle dieser Katalogdaten dient eine zentrale Datenbank (= [PostgresSQL](https://www.postgresql.org/)), in welche alle benötigten Katalogdaten aus den kooperierenden Bibliotheken migriert werden; in den meisten Fällen über den für den bibliothekarischen Kontext entwickelten Standard MARC21XML. MARC21XML-Datenpakete werden per [FTP-Server](https://de.wikipedia.org/wiki/File_Transfer_Protocol) in den Index der zentralen Datenbank gespielt und im Rahmen dieses Datenaustausches so interpretiert und verstehbar gemacht (= Datenmapping), dass sie als brauchbare Katalogdaten im Online-Katalog angezeigt werden können. In die zentrale Datenbank gehen ebenso alle Katalogdaten aus dem Discovery-System der ULB ein (= [Primo Central der Fa. *Exlibris*](https://de.wikipedia.org/wiki/Primo_Central)). Diese Katalogdaten stammen allerdings aus dem Index des Discovery-Systems und werden per [OAI-Schnittstelle](http://www.openarchives.org/) in die zentrale Datenbank gespeist und verarbeitet.

Sämtliche Daten aus der zentralen Datenbank werden zweifach abgesichert: Zum einen durch einen dreimal pro Woche automatisiert stattfindenden Backup auf einem externen Backup-Server, der den Katalogbestand auf dem Stand des zurückliegenden Monates absichert, zum anderen durch einen sog. Backup [Slave](https://www.itwissen.info/Master-Slave-Betrieb-master-slave-operation.html), der als immerwährende Kopie der zentralen Datenbank (= Master) den aktuellen Zustand dupliziert und für den Fall eines plötzlichen (physischen) Verlustes der Datenbank gedacht ist.

Im Hinblick auf den Online-Katalog sei noch erwähnt, dass hierin auch persönliche Daten der Angehörigen der WWU verwaltet werden. Diese Daten stammen aus dem Identitätsmanagement des hiesigen Rechenzentrums (ZIV) und werden mittels eines standardisierten [Netzwerkprotokolls (LDAP)](https://de.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) für die Nutzung der persönlichen ULB-Konten verwendet.   

### 2. Retrodigitalisierung

Die ULB digitalisiert bereits seit einigen Jahren ihre historischen Bestände systematisch bzw. nach bestimmten strategischen Kriterien ([Westfalica](https://www.ulb.uni-muenster.de/sammlungen/westfalica/), [Historische Drucke](https://www.ulb.uni-muenster.de/sammlungen/historisch/index.html), [Nachlässe](https://www.ulb.uni-muenster.de/sammlungen/nachlaesse/index.html)).

Sie verwendet hierfür die Software [Visual Library (VL)](https://www.semantics.de/visual_library/) der Aachener [Fa. *semantics*](https://www.semantics.de/). Die VL ist eine speziell für Bibliotheken und Informationseinrichtungen entwickelte Visualisierungssoftware u.a. im Bereich Retrodigitalisierung. In Verbindung mit der Software [Multidotscan](http://www.walternagel.de/multidotscan) der mit [*semantics*](https://www.semantics.de/) kooperierenden Bielefelder [Fa. *Walter Nagel*](http://www.walternagel.de/) lässt sich der gesamte Prozess von der Digitalisierung bis hin zur Präsentation im Portal der ULB durchautomatisiert abbilden. Zunächst wird am jeweiligen Buchscanner ein Scan-Job eingerichtet, der für den Job eine eindeutige ID generiert (= sog. HT-Nummer) und per nächtlichem Import automatisch auf dem VL-Server abgelegt wird. Anschließend werden die Titeldaten über eine Abfrage der HT-Nummer aus dem Verbundkatalog des hbz in Köln importiert und gemeinsam mit den Images in der VL angezeigt. Nachdem anschließend die VL-Manager den Titel inhaltlich strukturiert haben (Inhaltsverzeichnis, Buchkapitel etc.), wird der Titel freigegeben, mit einer Nutzungslizenz (z.B. mit [Creative Commons Lizenzen](https://creativecommons.org/)) versehen und in den [Digitalen Sammlungen der ULB](https://sammlungen.ulb.uni-muenster.de/) angezeigt.  

### 3. Elektronischer Semesterapparat (ESA)

Dozenten der WWU Münster haben seit 2010 die Möglichkeit, im [Learnweb](https://www.uni-muenster.de/LearnWeb/learnweb2/) (Moodle) [einen elektronischen Semesterapparat](https://www.ulb.uni-muenster.de/service/esa/dozenten-info.html) für ihre Studierenden zu erstellen und (selbst Teile urheberrechtlich geschützter) Literatur von Mitarbeitern der ULB digitalisieren zu lassen.

Die ULB Münster verwendet für diesen Workflow das eigens für solche Zwecke entwickelte [ESA-Modul](http://www.walternagel.de/elektronischer-semesterapparat) der schon in Punkt 2. genannten [Fa. *Walter Nagel*](http://www.walternagel.de/). Der Dozent recherchiert also im Moodle im lokalen Bestand der ULB die relevante Literatur und erteilt einen Digitalisierungsauftrag. Sobald der Auftrag im ESA-System eingegangen ist, prüft das Team Fernleihe zunächst den Auftrag. Die Prüfung bezieht sich vor allem auf urheberrechtliche Fragen, wenn der Dozent etwa mehr als 15 % eines Werkes digitalisiert haben möchte oder auch auf konservatorische Aspekte, die gegen eine Digitalisierung besonders von älteren beeinträchtigten Werken sprechen könnten. Fällt die Prüfung positiv aus, druckt das Team Fernleihe den Auftragsschein aus, der im ESA-System automatisch generiert wird und alle wichtigen Metadaten inkl. einer Auftragsnummer enthält. Im Rahmen von täglichen Routinegängen holt das Team ESA in der Fernleihe vorhandene Auftragszettel inkl. der dazugehörigen Bücher ab und stellt am Scanner einen speziellen ESA-Scanjob mithilfe der Auftragsnummer ein. Letzteres ist besonders wichtig, damit der Scanjob später dem richtigen Dozenten und dem richtigen Kursraum zugeordnet werden kann. Nach Abschluss des Scanjobs legt das Team ESA die erstellte Bilddatei in einen Importordner ab, in welchem daraus automatisch ein PDF erzeugt wird. Nach der automatischen PDF-Generierung der Datei erscheint (ebenfalls automatisiert) im Kursraum des Dozenten das betreffende PDF und der Dozent eine E-Mail, dass er ab sofort Zugriff auf die Datei hat.

### 4. Forschungsdatenmanagement

Ein weiteres Feld, in welchem in der ULB zahlreiche Daten fließen, ist der Bereich Forschungsdatenmanagement. Hier tritt die ULB gemeinsam mit dem [Zentrum für Informationsverarbeitung](https://www.uni-muenster.de/ZIV/) (ZIV) als Servicedienstleister für die Wissenschaftler der WWU Münster auf, um die im Rahmen ihrer Forschungen auftretenden Daten aufzubereiten und langfristig zu speichern (max. 10 Jahre).

In Form eines [Servicepunkts Forschungsdaten](https://www.uni-muenster.de/Forschungsdaten/angebote/ansprechpartner/) hilft die ULB den Wissenschaftlern bei forschungsdatenrelevanten Themen wie Antragstellung, Rahmenbedingungen, Datenmanagementplan, Datenschutz, Werkzeuge, Publizieren, Open Access und Langzeitarchivierung. Wenn man sich allein die im Forschungsdatenmanagement auftretenden Phasen als [Datenlebenszyklus](https://www.uni-muenster.de/Forschungsdaten/information/lebenszyklus/) vergegenwärtigt, wird klar, dass hier große Datenmengen und viele verschiedene Arten von Daten anfallen, und zwar bei der Erzeugung, Verarbeitung, Analyse, Archivierung, Zugang, Nachnutzung (und dann wieder) Erzeugung der Daten etc. Hierfür stellt die ULB gemeinsam mit dem ZIV die nötige IT-Infrastruktur und -software bereit und informiert auch im Rahmen von Schulungen und Workshops.

## Datenintensive Projekte mit ULB-Beteiligung

### 1. Fachinformationsdienst (FID) Benelux

Der Fachinformationsdienst (FID) Benelux ist ein DFG-gefördertes Projekt im Rahmen des Förderprogramms [Fachinformationsdienste für die Wissenschaft](https://www.dfg.de/foerderung/programme/infrastruktur/lis/lis_foerderangebote/fachinfodienste_wissenschaft/index.html) und ist das Nachfolgeformat der 2015 ausgelaufenen Sondersammelgebiete (SSG), hier des SSG Niederländischer Kulturkreis.

Damit der FID seinem [Selbstverständnis](https://www.fid-benelux.de/der-fid/ueber-uns/#profil) als
>zentrale Anlaufstelle für forschungsrelevante Literatur und Informationen über die Kultur und Gesellschaft der Beneluxländer sowie für forschungsunterstützende Services<sup>[1]

gerecht werden kann, gibt es neben zahlreichen Services in der ULB das [Rechercheportal FID Benelux](https://www.fid-benelux.de/literatur-recherche/suche/) als zentrale Suchmaschine für forschungsrelevante Literatur über die Kultur und Gesellschaft der Beneluxländer. Um diese spezielle Literatur in einem eigenen Portal suchbar machen zu können, werden Benelux-relevante Titel von einschlägigen liefernden Bibliotheken entweder über MARC21XML-Exporte über einen FTP-Server in die zentrale Datenbank der ULB importiert, um von dort aus in den Online-Katalog und in das Discovery-System zu gelangen. Ein anderer Weg, um an relevante Literatur für das Rechercheportal zu gelangen, ist das Harvesten (Einsammeln) relevanter Literatur über offene [OAI-Schnittstellen](http://www.openarchives.org/), die den offenen Austausch von Metadaten zum Ziel haben. Hierfür kommen zumeist sog. „OAI-Harvester“ zum Einsatz, wie etwa auch in der [Deutschen Nationalbibliothek (DNB)](https://www.dnb.de/DE/Service/DigitaleDienste/OAI/oai_node.html). Um die eingesammelten Metadaten nun mit dem genannten FTP-Server und der zentralen Datenbank der ULB zu synchronisieren und semantisch verstehbar zu machen, werden spezielle Computerprogramm namens [Parser](https://de.wikipedia.org/wiki/Parser) eingesetzt. 

### 2. Digitalisierung Historischer Zeitungen NRW

*siehe Beispiel*

### 3. Digitales Archiv NRW (DA NRW)

Das Landesprojekt Digitales Archiv NRW hat sich auf ihrer [Webseite](https://www.danrw.de/ueber-das-da-nrw/die-nrw-loesung/) Folgendes auf ihre Fahnen geschrieben:
> Das DA NRW ist ein informationstechnisches Angebot für alle Einrichtungen, die ihr elektronisches Kulturgut nach dem Archivgesetz und Pflichtexemplargesetz sicher und auf Dauer speichern müssen. Zur Nutzung von Synergieeffekten wird die Dienstleistung in einem Verbund verschiedener Dienstleister des Landes und der Kommunen bereitgestellt.<sup>[2]

Zudem sollen die Daten nicht nur langzeitarchiviert bzw. -gespeichert werden, sondern auch für die Zulieferung in weitere Portal dienen ([DDB](https://www.deutsche-digitale-bibliothek.de/), [Europeana](https://www.europeana.eu/portal/de)). Als Testpartner der ersten Stunde hat die ULB Münster bereits Erfahrungen mit dem Workflow gesammelt, wie und auf welchen Wegen die Daten ins DA NRW migriert werden können.

Für die Migration der Daten ins DA NRW spielt die Fa. *semantics* insofern eine wichtige Rolle, als sie für VL-Bibliotheken die vorhandenen Daten aus den jeweiligen Portalen in sog. [Submission Information Packages (SIP)](https://documents.clockss.org/index.php?title=Definition_of_SIP#OAIS_Submission_Information_Package_.28SIP.29) automatisiert zusammenfasst und per [rsync-Netwerkprotokollen](https://de.wikipedia.org/wiki/Rsync) sowie einer Authentifizierung per [SSH-keys](https://wiki.archlinux.org/index.php/SSH_keys) ins DA NRW hochgeladen werden können. Hierfür muss die VL in einem automatisierten Serverjob die besagten SIP-Kapseln erstellen und in das Incomingverzeichnis des hbz in Köln transferieren. Für später veränderte Objekte werden Delta-Kapseln erstellt, damit auch die Veränderungen an Objekten und ihren Metadaten erfasst werden. Die Verwaltung der SIP-Kapseln selbst erfolgt im VL-Manager. Hier können die MitarbeiterInnen der jeweiligen Einrichtung verfolgen, ob eine SIP-Kapsel erfolgreich erstellt, übertragen und archiviert worden ist. Außerdem gibt es im VL-Manager Such- und Filtermöglichkeiten (VL-ID, [URN](https://de.wikipedia.org/wiki/Uniform_Resource_Name), HBZ-ID) sowie eine Archivierungshistorie.

Die Datenübertragungsstraßen von der VL ins DA NRW werden zurzeit eingerichtet und voraussichtlich im Sommer 2019 zur Nutzung freigegeben.

### 4. Linked Open Data University of Münster (LODUM)

[LODUM](https://www.uni-muenster.de/LODUM/) ist die Open Data Initiative an der WWU Münster. Sie hat sich zum Ziel gesetzt, alle öffentlichen Information über die Universität in maschinenlesbaren Formaten für den einfachen Zugang und zur einfachen Wiederverwendung zur Verfügung zu stellen. LODUM möchte einen One-Stop Shop für alle Daten der WWU voranbringen, indem Daten von unterschiedlichen Informationssystemen geöffnet und kreuzreferenziert werden.

Schon jetzt können die [ULB-Daten](https://www.uni-muenster.de/LODUM/data/ulb/) des Online-Kataloges, der Digitalen Sammlungen, der Lynda-Video-Trainings, des Open Journal Systems (OJS), historischer Musiknoten und des Publikationsservers miami tagesaktuell als [zip](https://de.wikipedia.org/wiki/ZIP-Dateiformat)-Exporte heruntergeladen werden. Auch wenn bislang noch recht wenige Institutionen der WWU ihre Daten über den LODUM-Server bereitstellen, bildet die Initiative einen wichtigen Baustein in der Open Data Strategie der WWU Münster.

### 5. Opening Reproducible Research (O2R)

Das Projekt [Opening Reproducible Research (O2R)](https://o2r.info/) ist ein DFG-gefördertes Projekt vom Münsteraner Institut für Geoinformatik und der ULB Münster. Es lief in einer ersten Phase von 2015 bis 2018 und hat erste Strukturen geschaffen, um die in Publikationen entstandenen Forschungsergebnisse reproduzierbar zu machen.

Auf der [Projekt-Webseite](https://www.uni-muenster.de/Geoinformatics/research/projects/O2R.html) heißt es: Mit dem Projekt
>zielen wir direkt auf zentrale Aspekte von Open Access ab, indem wir den Austausch von online veröffentlichten Forschungsergebnissen verbessern, die produktive Aneignung ermöglichen und deren Wiederverwendung vereinfachen.<sup>[3]

Im April 2019 hat die DFG das Folgeprojekt „O2R2“ für weitere 30 Monate bewilligt. In dieser zweiten Phase soll es nun darum gehen, die entwickelten Prototypen aus der ersten Phase mit existenten Artikeln zu testen und auf einer gemeinsam entwickelten Plattform die Forschungsergebnisse dieser Artikel reproduzierbar zu machen.

### 6. sciebo-research Data Services (sciebo-RDS)

Ebenfalls in den Bereich Forschungsdatenmanagement zielt das auf drei Jahre von der DFG geförderte Projekt „sciebo-research Data Services (sciebo-RDS) – Forschungsdatenmanagementdienste und -werkzeuge für Wissenschaftler“.

Es handelt sich um ein [Kooperationsprojekt](https://www.forschungsdaten.info/praxis-kompakt/fdm-in-den-bundeslaendern/nordrhein-westfalen/projekte/sciebords/) der ULB Münster, dem Rechenzentrum (ZIV) der WWU Münster und der Abteilung Informatik und Angewandte Kognitionswissenschaft der Universität Duisburg Essen. Als Kooperationspartner konnte die Universität Bielefeld gewonnen werden. In diesem Projekt geht es darum, ein niederschwelliges Angebot für das Management von Forschungsdaten zu entwickeln. Auf der Basis des Cloudspeicherdienstes sciebo, den das ZIV bereitstellt, sollen Werkzeuge, Workflows und Services entwickelt werden, um den Forschenden bei der Durchführung eines strukturierten Forschungsdatenmanagements zu helfen. 

## Beispiel: Digitalisierung Historischer Zeitungen NRW

Im Rahmen eines vom Land Nordrhein-Westfalen zunächst für drei Jahre (2017–2019) geförderten Projekts zur „Digitalisierung historischer Zeitungen in Nordrhein-Westfalen“ wird gemeinsam mit der ULB Bonn ein repräsentativer Querschnitt der historischen nordrhein-westfälischen Zeitungen aus dem Erscheinungszeitraum 1801 bis 1945 digitalisiert und sowohl für die Forschung als auch für die interessierte Öffentlichkeit kostenfrei und komfortabel im Zeitungsportal [zeit.punktNRW](https://zeitpunkt.nrw/) zur Verfügung gestellt.

Auf dieser Plattform, die vom hbz in Köln gehostet wird, werden mit Hilfe der Visual Library (VL) differenzierte Such- und Präsentationsmöglichkeiten geschaffen, die optimal auf die speziellen Objekte sowie auf die Fragestellungen verschiedener Nutzergruppen zugeschnitten sind.

Da sich das Projekt als Massendigitalisierungsprojekt versteht, werden historische Zeitungen in der ersten (und auch in einer möglichen zweiten Förderphase ab 2020) vornehmlich von Master-Mikrofilmen digitalisiert. Hierfür wurde ein bestimmter technischer Workflow entwickelt, der im Folgenden dargestellt und mit einer Idee zur Optimierung des Workflows endet:

Im ersten Schritt werden die Mikrofilme mit dem Mikrofilmscanner OM 1600 der [Fa. *Zeutschel*](https://www.zeutschel.de/de/) digitalisiert und damit die Rohdaten für die weitere Verarbeitung erzeugt. Diese Roh-Digitalisate werden zunächst auf einer lokalen Festplatte gespeichert und anschließend weiter bearbeitet. Dies ist notwendig, da die Zeitungsseiten in Form von sog. Strips noch unbeschnitten und entsprechend noch nicht präsentabel sind. Die Bearbeitung dieser Rohdaten erfolgt anhand der Software [Quantum Process (Scan Version 1.02.26)](http://www.acmisgroup.com/en/scanners/detail/mekel-quantum-process-software) der [Fa. *acmisgroup*](http://www.acmisgroup.com/en). Über ein lokales Netzlaufwerk werden die Rohdaten nun in den Quantum Process geladen und dort bearbeitet. Dazu gehört die korrekte Rahmensetzung (Frames), ggf. die Drehung sowie die Trennung vorhandener Doppelseiten. Das Ergebnis wird in einer [.qpf-Datei](https://www.reviversoft.com/de/file-extensions/qpf) gespeichert, mit der die Einstellung und die Parameter zu einem späteren Zeitpunkt wieder aufgerufen werden können. Anschließend werden mit Hilfe dieser .qpf-Dateien die sog. Outputdateien im [TIFF-Format](https://de.wikipedia.org/wiki/Tagged_Image_File_Format) erstellt. Diese TIFF-Dateien werden auf dem lokalen Server mittels einer Batch-Datei als ZIP-Datei verpackt:

![Verpackung ZIP-Datei](https://user-images.githubusercontent.com/49555636/57213930-8e2e3700-6fe8-11e9-9e41-3392864e5749.jpg) *aus internem ULB-Dokument*

Wichtig hierbei ist, dass die Batch-Datei zip.bat zusammen mit den Outputdatei-Verzeichnissen liegen müssen:

![Verzeichnis Struktur](https://user-images.githubusercontent.com/49555636/57214056-0268da80-6fe9-11e9-9e17-0f28862fc152.png)

*aus internem ULB-Dokument*

Alle ZIP-Dateien werden nun über einen [SFTP](https://de.wikipedia.org/wiki/SSH_File_Transfer_Protocol)-Server manuell mittels Log-Dateien und dem Programm [FileZilla](https://filezilla-project.org/) in das Upload-Verzeichnis „ULB MS“ des hbz hochgeladen. Hier wird eine Verbindung zu zdiginrw.hbz.nrw.de aufgebaut, anschließend in das Verzeichnis zdiginrwulbms gewechselt und die Dateien hochgeladen:

![ZIP-Upload](https://user-images.githubusercontent.com/49555636/57214423-3abce880-6fea-11e9-9ca2-057c11ae3f6d.png)
*aus internem ULB-Dokument*

In einem nächtlich stattfindenden VL-Batchprozess werden die Daten automatisch entpackt und in die VL importiert:

![Batch-Import](https://user-images.githubusercontent.com/49555636/57214432-3f819c80-6fea-11e9-90c7-762af6a5ef50.png)
*aus internem ULB-Dokument*

Am folgenden Tag kann dann die Bearbeitung der hochgeladenen Images durch die VL-Manager erfolgen:

![Ordner Struktur](https://user-images.githubusercontent.com/49555636/57214437-427c8d00-6fea-11e9-8f0f-e341eeb26029.png)

*aus internem ULB-Dokument*

### Optimierungspotenzial im Workflow

Der drittletzte Schritt des beschriebenen Datenfluss-Workflows bietet aus Sicht des Autors eine Möglichkeit, den Prozess dahingehend zu optimieren, dass man den bislang manuell durchgeführten Vorgang, die ZIP-Dateien in das Upload-Verzeichnis hochzuladen, automatisiert. Hierfür könnte man eine weitere Batch-Datei schreiben, die genau diesen Vorgang initiiert, sobald ZIP-Dateien auf dem lokalen Server generiert worden sind (ggf. mit einem Watch-Skript). In dieser Batch-Datei müsste außerdem programmiert werden, dass ZIP-Dateien nur in den Upload-Server hochgeladen werden können, solange dort genügend Speicher vorhanden ist, um diesen nicht „volllaufen“ zu lassen. Sobald der Speicher des Servers ausgereizt ist, wird der Uploadvorgang (der dann als zu groß erkannten zip-Datei) blockiert und erst dann wieder fortgesetzt, wenn wieder genügend Speicher vorhanden ist. Es ist noch zu klären, ob der Speicher manuell oder auch automatisiert durch Löschen vorhandener zip-Dateien freigegeben werden kann. Schließlich muss noch getestet werden, wie groß die Datenmenge in einem Upload-Vorgang sein darf, damit der Upload in einem nächtlichen Prozess durchgelaufen ist. Die täglichen Arbeitsprozesse in der VL dürfen durch einen fortdauernden Upload am nächsten Morgen auf keinen Fall behindert werden.

## Quellen

1. Persönliche Gespräche mit zwei IT- und Datenexperten der ULB Münster (Dez. Digitale Dienste)

2. Interne ULB-Dokumente

3. Webquellen:

* Acmisgroup. URL: http://www.acmisgroup.com/en (zuletzt abgerufen am 20.05.2019).
* Acmisgroup, Mekel Quantum Process Software. URL: http://www.acmisgroup.com/en/scanners/detail/mekel-quantum-process-software (zuletzt abgerufen am 20.05.2019).
* Creative Commons. URL: https://creativecommons.org/ (zuletzt abgerufen am 20.05.2019).
* Digitales Archiv NRW (DA NRW): URL: https://www.danrw.de/ueber-das-da-nrw/die-nrw-loesung/ (zuletzt abgerufen am 20.05.2019).
* Deutsche Digitale Bibliothek (DDB). URL: https://www.deutsche-digitale-bibliothek.de/ (zuletzt abgerufen am 20.05.2019).
* Deutsche Forschungsgemeinschaft (DFG), Fachinformationsdienste für die Wissenschaft. URL: https://www.dfg.de/foerderung/programme/infrastruktur/lis/lis_foerderangebote/fachinfodienste_wissenschaft/index.html (zuletzt abgerufen am 20.05.2019).
* Deutsche Nationalbibliothek (DNB), OAI-Schnittstelle. URL: https://www.dnb.de/DE/Service/DigitaleDienste/OAI/oai_node.html (zuletzt abgerufen am 20.05.2019).
* Europeana. URL: https://www.europeana.eu/portal/de (zuletzt abgerufen am 20.05.2019).
* FID Benelux Low Countries Studies, Profil. URL: https://www.fid-benelux.de/der-fid/ueber-uns/#profil (zuletzt abgerufen am 20.05.2019).
* FID Benelux Low Countries Studies, Rechercheportal. URL: https://www.fid-benelux.de/literatur-recherche/suche/ (zuletzt abgerufen am 20.05.2019).
* FileZilla. URL: https://filezilla-project.org/ (zuletzt abgerufen am 20.05.2019).
* Open Archives Initiative. URL: http://www.openarchives.org/ (zuletzt abgerufen am 20.05.2019).
* Opening Reproducible Research. URL: https://o2r.info/ (zuletzt abgerufen am 20.05.2019).
* PostgreSQL. URL: https://www.postgresql.org/ (zuletzt abgerufen am 20.05.2019).
* Seite „File Transfer Protocol“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 18. Mai 2019, 22:40 UTC. URL: https://de.wikipedia.org/w/index.php?title=File_Transfer_Protocol&oldid=188716771 (zuletzt abgerufen am 20.05.2019).
* Seite „Lightweight Directory Access Protocol“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 7. Mai 2019, 06:53 UTC. URL: https://de.wikipedia.org/w/index.php?title=Lightweight_Directory_Access_Protocol&oldid=188315409 (zuletzt abgerufen am 20.05.2019). 
* Seite „Master-Slave-Betrieb“. In: ITWissen.info. URL: https://www.itwissen.info/Master-Slave-Betrieb-master-slave-operation.html (zuletzt abgerufen am 20.05.2019).
* Seite „Parser“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 13. Juni 2018, 17:09 UTC. URL: https://de.wikipedia.org/w/index.php?title=Parser&oldid=178286070 (zuletzt abgerufen am 20.05.2019).
* Seite „Primo Central“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 8. Mai 2019, 04:48 UTC. URL: https://de.wikipedia.org/w/index.php?title=Primo_Central&oldid=188346136 (zuletzt abgerufen am 20.05.2019).
* Seite „.QPF Dateierweiterung". In: ReviverSoft. URL: https://www.reviversoft.com/de/file-extensions/qpf (zuletzt abgerufen am 20.05.2019).
* Seite „Rsync“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 7. Januar 2019, 13:50 UTC. URL: https://de.wikipedia.org/w/index.php?title=Rsync&oldid=184489056 (zuletzt abgerufen am 20.05.2019).
* Seite „sciebo.RDS“. In: forschungsdaten.info. URL: https://www.forschungsdaten.info/praxis-kompakt/fdm-in-den-bundeslaendern/nordrhein-westfalen/projekte/sciebords/ (zuletzt abgerufen am 20.05.2019).
* Seite „SSH keys“. In: archlinux. URL: https://wiki.archlinux.org/index.php/SSH_keys (zuletzt abgerufen am 20.05.2019).
* Seite „SSH File Transfer Protocol“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 11. Mai 2019, 13:51 UTC. URL: https://de.wikipedia.org/w/index.php?title=SSH_File_Transfer_Protocol&oldid=188459540 (zuletzt abgerufen am 20.05.2019).
* Seite „Submission Information Package (SIP)“. In: CLOCKSS Archive. URL: https://documents.clockss.org/index.php?title=Definition_of_SIP#OAIS_Submission_Information_Package_.28SIP.29 (zuletzt abgerufen am 20.05.2019).
* Seite „Tagged Image File Format“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 14. Mai 2019, 08:41 UTC. URL: https://de.wikipedia.org/w/index.php?title=Tagged_Image_File_Format&oldid=188558470 (zuletzt abgerufen am 20.05.2019).
* Seite „Uniform Resource Name“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 7. Mai 2019, 22:21 UTC. URL: https://de.wikipedia.org/w/index.php?title=Uniform_Resource_Name&oldid=188341453 (zuletzt abgerufen am 20.05.2019).
* Seite „ZIP-Dateiformat“. In: Wikipedia, Die freie Enzyklopädie. Bearbeitungsstand: 25. März 2019, 21:07 UTC. URL: https://de.wikipedia.org/w/index.php?title=ZIP-Dateiformat&oldid=186925117 (zuletzt abgerufen am 20.05.2019).
* semantics. URL: https://www.semantics.de/ (zuletzt abgerufen am 20.05.2019).
* semantics, Visual Library. URL: https://www.semantics.de/visual_library/ (zuletzt abgerufen am 20.05.2019).
* ULB Münster, Digitale Sammlungen. URL: https://sammlungen.ulb.uni-muenster.de/ (zuletzt abgerufen am 20.05.2019).
* ULB Münster, Elektronischer Semesterapparat (ESA). URL: https://www.ulb.uni-muenster.de/service/esa/dozenten-info.html (zuletzt abgerufen am 20.05.2019).
* ULB Münster, Online-Katalog. URL: https://katalogix.uni-muenster.de/Katalog/start.do (zuletzt abgerufen am 20.05.2019).
* ULB Münster, Westfalica. URL: https://www.ulb.uni-muenster.de/sammlungen/westfalica/ (zuletzt abgerufen am 20.05.2019).
* ULB Münster, Historische Drucke. URL: https://www.ulb.uni-muenster.de/sammlungen/historisch/index.html (zuletzt abgerufen am 20.5.2019).
* ULB Münster, Nachlässe. URL: https://www.ulb.uni-muenster.de/sammlungen/nachlaesse/index.html (zuletzt abgerufen am 20.05.2019).
* Walter Nagel. URL: http://www.walternagel.de/ (zuletzt abgerufen am 20.05.2019).
* Walter Nagel, Elektronischer Semesterapparat (ESA). URL: http://www.walternagel.de/elektronischer-semesterapparat (zuletzt abgerufen am 20.05.2019).
* Walter Nagel, Multidotscan. URL: http://www.walternagel.de/multidotscan (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Linked Open Data University of Münster (LODUM). URL: https://www.uni-muenster.de/LODUM/ (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Linked Open Data University of Münster (LODUM), ULB Data. URL: https://www.uni-muenster.de/LODUM/data/ulb/ (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Projekt Open Reproducible Research (O2R). URL: https://www.uni-muenster.de/Geoinformatics/research/projects/O2R.html (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Servicepunkt Forschungsdatenmanagement. URL: https://www.uni-muenster.de/Forschungsdaten/angebote/ansprechpartner/ (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Servicepunkt Forschungsdatenmanagement, Lebenszyklus. URL: https://www.uni-muenster.de/Forschungsdaten/information/lebenszyklus/ (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Learnweb. URL: https://www.uni-muenster.de/LearnWeb/learnweb2/ (zuletzt abgerufen am 20.05.2019).
* WWU Münster, Zentrum für Informationsverarbeitung (ZIV). URL: https://www.uni-muenster.de/ZIV/ (zuletzt abgerufen am 20.05.2019).
* zeit.punktNRW. URL: https://zeitpunkt.nrw/ (zuletzt abgerufen am 20.05.2019).
* Zeutschel. URL: https://www.zeutschel.de/de/ (zuletzt abgerufen am 20.05.2019).

<div class="footnotes">
[1]: https://www.fid-benelux.de/der-fid/ueber-uns/#profil (zuletzt abgerufen am 20.05.2019).
[2]: https://www.danrw.de/ueber-das-da-nrw/die-nrw-loesung/ (zuletzt abgerufen am 20.05.2019).
[3]: https://www.uni-muenster.de/Geoinformatics/research/projects/O2R.html (zuletzt abgerufen am 20.05.2019).
