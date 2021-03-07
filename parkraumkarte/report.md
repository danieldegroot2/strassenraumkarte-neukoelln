---
title: Methodenbericht
layout: page
social_sharing:
  title:
  description:
  image: images/report/social-sharing.jpg
  image_alt:
show_legend: true
menu_highlight: report
---

# Parkraumanalyse für den Berliner Ortsteil Neukölln – Methoden- und Ergebnisbericht

Stand: März 2021

## Autoren

Alexander Seidel, M.A. und OpenStreetMap-Beitragende

## TL/DR

Diese Parkraumanalyse entstand im Rahmen einer Mobilitäts- und Verkehrswende-Initiative der Berliner OpenStreetMap-Community (OSM) und wurde als ehrenamtliches Projekt durchgeführt. Ein großer Teil der Datenauswertung und Datenerhebung geht auf Alexander Seidel, Sozial- und Stadtgeograf und OSM-Beitragender, zurück und mündete gemeinsam mit den Beiträgen vieler anderer OSM-Beitragender in den hier vorgestellten Ergebnissen.




## Einführung

Daten über die Anzahl und Verteilung von Kfz-Parkplätzen im Stadtraum stellen eine wertvolle Ressource dar. So wird der Verkehrsraum im Zuge der Verkehrswende zunehmend neu verteilt oder zumindest politisch darüber gestritten und die Reduzierung des ruhenden Verkehrs in diesem Zusammenhang als wichtiger Ansatzpunkt für mehr Flächengerechtigkeit identifiziert. Gleichzeitig finden Verkehr und Mobilität unter Einbeziehung geographischer Daten immer zielgerichteter statt, sodass beispielsweise unnötige Wege oder innenstädtischer Verkehr verhindert werden können – auch hier können Parkplatz- und Stellplatzdaten einen Beitrag leisten.

Vielerorts gibt es jedoch noch gar kein systematisches Wissen, wo es wie viele Parkplätze gibt. In aufwendigen Studien müssen diese Daten bei Bedarf erfasst werden – und meist sind diese Daten anschließend nicht für die Öffentlichkeit zugänglich. Im Gegensatz dazu stellt die freie Geodatenbank OpenStreetMap (OSM) eine optimale Umgebung dar, in der solche Daten frei zugänglich erfasst und analysierbar gemacht werden können.

Diese Parkraumanalyse demonstriert am Beispiel des Berliner Ortsteils Neukölln, wie urbaner Parkraum systematisch auf OSM-Basis kartiert und mit Geoinformationssystemen (GIS) und unter Einbezug weiterer offener Daten hochaufgelöst ausgewertet werden kann. Ziel des Projektes ist es,

* eine Methode zur Erhebung und Verarbeitung parkraumbezogener Geodaten zu demonstrieren,
* Standorte und Stellplatzzahlen aller Parkmöglichkeiten -- sowohl im öffentlichen Straßenraum als auch im privaten Raum -- zu ermitteln,
* Stellplatzdichten unter Einbeziehung von Kfz- und Bevölkerungsdaten zu berechnen,
* Angaben zum Flächenverbrauch durch geparkte Fahrzeuge zu machen,
* die Daten für das Untersuchungsgebiet zur freien Verwendung bereit zu stellen.

Der vorliegende Bericht stellt die Herangehensweise und Methodik der Parkraumanalyse dar und geht kurz auf zentrale Ergebnisse ein.

### Ergebnisse, Daten und weiterführende Informationen

<div class="row">
<div class="col-5">

<img src="{{ '/images/report/parkraumanalyse-neukoelln-grafik.jpg' | relative_url }}" alt="" class="img-fluid" />

</div>
<div class="col-7">

Die Ergebnisse dieses Projekts sind kartographisch in der [Neuköllner Parkraumkarte](https://supaplexosm.github.io/strassenraumkarte-neukoelln/?map=parkingmap#18/52.48150/13.43571) aufbereitet. Darüber sind auch die [zugrunde liegenden Datensätze frei verfügbar](https://supaplexosm.github.io/strassenraumkarte-neukoelln/data). Weiterführende Informationen finden sich darüber hinaus [im OpenStreetMap-Wiki](https://wiki.openstreetmap.org/wiki/Berlin/Verkehrswende/Parkraumanalyse_Neuk%C3%B6lln).

</div>
</div>


## Methodik

### Allgemeine Herangehensweise

Die dieser Auswertung zugrunde liegenden Parkplatzdaten wurden systematisch für dieses Projekt in der **OSM-Datenbank** erfasst bzw. vervollständigt, mit offenen Daten aus weiteren Quellen angereichert und mit der Software QGIS ausgewertet. Zwar umfasst OSM immer umfangreichere und zunehmend hochspezialisierte Geoinformationen und bietet insbesondere in Mitteleuropa einen nahezu lückenlosen Datensatz zum Straßennetz, die Detailtiefe der Informationen ist jedoch regional unterschiedlich ausgeprägt und abhängig von den Aktivitäten und Interessen lokaler Communities und ihren Beitragenden. So gehören Daten zu straßenbegleitendem Parken beispielsweise derzeit noch nicht zu den „Standardinformationen" und sind vielerorts lediglich rudimentär erfasst. Eine Übertragung der hier demonstrierten Analyse auf andere Orte wird daher zur Zeit meist an die Bedingung geknüpft sein, die notwendigen Daten zuvor zu erheben bzw. zu vervollständigen. Darüber hinaus stellt die angewandte Methodik hohe Ansprüche an die Präzision und Lagegenauigkeit der Daten, da aus diesen Geometrien weitere Werte wie Stellplatzkapazitäten oder Halteverbote abgeleitet werden. Je genauer und vollständiger die Daten dabei vorliegen, desto präzisere Ergebnisse können anschließend daraus ermittelt werden[^1].

[^1]: Welchen Einfluss eine geringere Genauigkeit und Vollständigkeit der OSM-Daten auf die Qualität des Ergebnisses insbesondere in Bezug auf das Straßenparken hätte, soll Gegenstand späterer Auswertungen sein, die [auf der Projektseite im OSM-Wiki dokumentiert](https://wiki.openstreetmap.org/wiki/Berlin/Verkehrswende/Parkraumanalyse_Neuk%C3%B6lln) werden.

Die Auswertung berücksichtigt verschiedene Arten von Park- und Stellplätzen, die auf unterschiedliche Weise erfasst und interpretiert werden. Den überwiegenden Anteil am Kfz-Parkraumangebot stellt in der Berliner Innenstadt das **Straßenparken** dar, also Parken im öffentlichen Straßenraum auf Parkstreifen am Fahrbahnrand. Basis des Datenmodells dieser Parkraumanalyse ist es, die Anzahl und Lage dieser Stellplätze aus der (geomterisch linienhaft erfassten) Information abzuleiten, auf welchen Abschnitten und mit welcher Ausrichtung (Längs, Schräg, Quer) entlang einer Straße geparkt werden kann. Streckenabschnitte, an denen nicht geparkt werden darf (Einfahrten, abgesenkte Bordsteine, Kreuzungsbereiche, Gehwegübergänge, Park- und Halteverbote etc.), werden automatisiert ermittelt und aus der Auswertung ausgeschlossen. Vergleiche zwischen berechneten/interpolierten und realen/gezählten Werten zeigen, dass diese Methode bei ausreichender Qualität der Datengrundlage präzise Ergebnisse liefert (vgl. Kapitel 3).

Darüber hinaus wurden Informationen zu (meist privaten) **Stellplätzen abseits des Straßenraums** erhoben und einbezogen, die geometrisch in flächenhafter Form vorliegen. Dazu zählen:
* allgemeine, meist ebenerdige Park- und Stellplätze,
* Tiefgaragen,
* Garagen und Carports,
* Parkhäuser.

Diese Objekte sind häufiger mit einer genauen Stellplatzzahl erfasst, da diese oft markiert und abzählbar sind. Aus ihrer Grundfläche (und, bei mehrstöckigen Objekten, ggf. unter Berücksichtigung ihrer horizontalen Ausdehnung) kann die Stellplatzkapazität aber auch abgeschätzt werden.

Die Stellplatzdaten enthalten zusätzliche Attribute wie zu Beschränkungen der Nutzung oder Zugänglichkeit (öffentlich/privat/Kunden etc., Gebühren, zeitliche Beschränkungen) und können auf dieser Grundlage gezielt ausgewertet werden.

### Untersuchungsgebiet

Die vorliegende Parkraumanalyse bezieht sich auf den Berliner Ortsteil Neukölln. Das gesamte Untersuchungsgebiet, für das Parkplatzdaten erhoben wurden, umfasst das Gebiet innerhalb der Ortsteilgrenzen Neuköllns sowie einen Pufferbereich von 500 Metern außerhalb der Ortsteilgrenze, um insbesondere bei Aussagen zur Stellplatzdichte Verzerrungen an den Randbereichen zu vermeiden. Der Ortsteil Neukölln umfasst eine Fläche von 11,7 km² (gesamtes Untersuchungsgebiet: 20,6 km²).

Der Ortsteil Neukölln ist ein überwiegend von Wohnquartieren geprägter, dicht besiedelter und eng bebauter urbaner Raum mit 165.000 Einwohnerinnen und Einwohnern. Er ist durch eine vergleichsweise geringe Motorisierungsquote geprägt: Pro 1.000 Personen sind hier 219 Kraftfahrzeuge zugelassen[^2]. Das Gebiet des Ortsteils umfasst zwei Gewerbegebiete, die bei einigen Auswertungen nicht berücksichtigt wurden. Die in diesem Fall berücksichtigten Wohnquartiere erstrecken sich über eine Fläche von 7,4 km² (Kfz-Quote: 206 pro 1.000 Personen) und können für genauere Datenauswertungen in 16 Teilgebiete untergliedert werden, die den lokalen „Kiezen“ bzw. lebensweltlich orientierten Räumen entsprechen (vgl. Anhang A).

[^2] Berechnet nach Amt für Statistik Berlin-Brandenburg: „Melderechtlich registrierte Einwohnerinnen und Einwohner am Ort der Hauptwohnung in Berlin am 30.06.2020 nach Planungsräumen und KfZ-Bestand", verfügbar auf der [Datenseite zu dieser Parkraumanalyse](https://supaplexosm.github.io/strassenraumkarte-neukoelln/data)._

In Bezug auf die Parkraumsituation spielen zwar tagsüber insbesondere entlang der Hauptstraßen einzelhandelsbezogen vielerorts Lieferverkehr und Kurzzeitparken eine zentrale Rolle, in den Kiezen (und außerhalb der Geschäftszeiten) wird die lokale Parkraumsituation jedoch vom Parkverhalten der Anwohnenden bestimmt. Um die Parkraumsituation zu bewerten, sind daher vor allem Parkmöglichkeiten relevant, die sich zum dauerhaften Parken eignen. Kunden- oder Mitarbeiterparkplätze sind zwar im Datensatz enthalten, wurden aber bei der Ermittlung des regulären Stellplatzangebots und von Stellplatzdichten ausgeschlossen. Aufgrund ihrer teils großen Kapazitäten (insbesondere von Supermarkt-Parkplätzen) stellen sie dennoch eine wichtige Größe dar, die in der Diskussion um die zukünftige Gestaltung des Parkraums nicht vernachlässigt werden darf und in Modellen wie Anwohner-Nachtparken mancherorts bereits Berücksichtigung findet.

Gewerblich genutzte Parkplätze (z.B. für Transportfahrzeuge des Handwerks) sind in die Auswertungen eingeflossen, da die herangezogenen Vergleichsdaten zum tatsächlichen Fahrzeugbestand auch gewerbliche Fahrzeuge enthalten. Insgesamt spielen Stellplätze dieser Art in den Wohnquartieren – also außerhalb der Gewerbegebiete – aber nur eine geringe Rolle.

### Datenerhebung, Datenquellen und Datensätze

Der überwiegende Anteil der Park- und Stellplatzdaten wurde durch systematische Begehungen des Untersuchungsgebiets zwischen Frühjahr und Herbst 2020 erfasst. Gegenstand dieser Kartierung war vor allem die Erhebung des Straßenparkens im Verlauf des etwa 170 km umfassenden Straßennetzes (davon 104 km im Ortsteil Neukölln) und die Vervollständigung von etwa 2.200 Gebäude- und Grundstückseinfahrten (davon etwa 1.400 im Ortsteil Neukölln), da vor diesen nicht geparkt werden darf[^3]. Darüber hinaus wurden Daten zu anderen Parkmöglichkeiten wie Garagen und Stellplätzen erhoben, soweit diese erreichbar oder sichtbar waren.

[^3]: Gebäudeeinfahrten wurden dann in die Auswertung einbezogen, wenn sie an der Fahrbahneinmündung eine Bordsteinabsenkung besitzen und als Einfahrt erkennbar oder ausgeschildert sind. Das ist in der überwiegenden Mehrheit der baulich angelegten Einfahrten der Fall. In selteneren Fällen werden solche Einfahrten trotz Bordsteinabsenkung aber offensichtlich nicht mehr genutzt (weder für Fahrzeuge noch bspw. für die Müllabfuhr) und sind auch nicht als Einfahrt gekennzeichnet, möglicherweise auch rechtlich nicht mehr als solche gewidmet.

Die Erhebungen vor Ort wurden durch weitere Auswertungen und Recherchen ergänzt:

* Auswertung von Luftbildern, um Stellplätze in nicht öffentlich zugänglichen Bereichen, insbesondere Hinterhöfen, zu ermitteln. Im Berliner Geoportal stehen jährlich erzeugte, meist im Frühjahr aufgenommene Orthophotos zur Verfügung; einbezogen wurden Aufnahmen von 2016 bis 2019.

* Ermittlung von Tiefgaragengrundflächen auf Grundlage des Amtlichen Liegenschaftskatasterinformationssystems (ALKIS) und Plausibilitätsprüfung mit Kartendaten und Luftbildern sowie vor Ort.[^4]

[^4]:	Da die ALKIS-Daten in manchen Fällen offensichtlich fehlerhaft sind oder Tiefgaragenteile fehlen, wurden einige Geometrien auf Grundlage von Kartendaten und Luftbildern korrigiert (insbesondere unter Berücksichtigung von Gebäudegrundflächen oder darüber liegenden Strukturen wie ebenerdigen Parkplätzen, Hängen und Eingängen). Drüber hinaus wurden vor Ort die Zufahrtswege zu den Tiefgaragen erfasst und Standorte ausgeschlossen, wenn keine Zufahrtswege aufgefunden werden konnten bzw. in selteneren Fällen Tiefgaragen mit geschätzten Grundflächen einbezogen, wenn diese vollständig in den ALKIS-Daten fehlten.

* Überprüfung von Gebäuden, die im ALKIS als Garage kategorisiert sind, auf ihren faktischen Status als Garage bzw. ihre Tauglichkeit zum Abstellen von Kraftfahrzeugen (vor Ort sowie auf Luft- und Schrägluftbildern).

* Recherche von Stellplatzkapazitäten von Parkhäusern und Tiefgaragen aus online zugänglichen Dokumenten (Websites, Berichte und Planungsunterlagen zu Bauprojekten, Bebauungspläne...) oder vereinzelt durch Nachfrage bei Vermietern und Eigentümern.

Für die anschließende Analyse wurden weitere Daten aufbereitet und einbezogen:

* Kfz-Bestand auf Ebene der LOR-Planungsräume (Lebensweltlich orientierte Räume) zur Ermittlung der Stellplatzdichte: „Melderechtlich registrierte Einwohnerinnen und Einwohner am Ort der Hauptwohnung in Berlin am 30.06.2020 nach Planungsräumen und KfZ-Bestand", auf Nachfrage zur Verfügung gestellt durch das Amt für Statistik Berlin-Brandenburg.

* Einwohnerdichte auf Ebene der Block- und Blockteilflächen (Stand 31.12.2019, verfügbar im Berliner Geoportal/Umweltatlas) und Gebäudedatensatz (ALKIS) zur Generierung eines gebäudebezogenen Bevölkerungsmodells (vgl. Kapitel 2.6).

* Die Blockflächen wurden außerdem herangezogen, um unter Einbeziehung von OSM-Daten die Fläche öffentlicher Verkehrsräume als Grundlage von Flächenverbrauchsberechnungen zu ermitteln (öffentliche Fahrbahn- und Gehwegbereiche, also der Raum zwischen den Gebäudefassaden bzw. Grundstücksgrenzen).

Generierung eines Bordsteinkanten- bzw. Fahrbahn-Datensatzes aus OSM- und ALKIS-Daten (Datensatz „Bauwerke, Anlage und Einrichtung in Siedlungsflächen und für den Verkehr"), um eine exakte Lagegenauigkeit der Parkstreifen zu erreichen. Dieser Bordsteinkanten- bzw. Fahrbahndatensatz bildet außerdem eine Grundlage für die Visualisierung der [Straßen- und Parkraumkarte](https://supaplexosm.github.io/strassenraumkarte-neukoelln/?map=parkingmap).

### Datenverarbeitung zur Modellierung des Straßenparkens

Das OSM-Datenschema zur Erfassung von Parkstreifen („parking:lane"-Schema) sieht vor, einem Straßensegment jeweils Informationen zum Parken am linken und rechten Fahrbahnrand zuordnen zu können. Dazu gehören in erster Linie:

* Art des Parkens: Entweder Park- oder Halteverbote, oder die Anordnung/Ausrichtung der geparkten Fahrzeuge (insbes. Längs, Schräg, Quer).
* Position des Parkens: Die Fahrzeuge können auf der Fahrbahn, in einer Parkbucht, auf dem Gehweg, halb auf dem Gehweg oder auf dem Seitenstreifen stehen.
* Bedingungen und Einschränkungen: Stellplätze können insbesondere für bestimmte Nutzergruppen reserviert, zeitlich begrenzt nutzbar oder gebührenpflichtig sein.

Die Straßensegmente liegen geometrisch als Linienobjekte vor, die geteilt werden können, wenn sich Attribute im Straßenverlauf ändern. Besteht entlang eines Teilabschnitts einer Straße beispielsweise ein Parkverbot, kann dieses direkt über ein eigenes Straßensegment differenziert werden. Kleinteilige Einschränkungen wie Einfahrten oder Gehwegübergänge müssen (und sollen) nicht gesondert segmentiert werden, da sie aus den entsprechenden Daten im späteren Verlauf abgeleitet werden können. Abweichungen von signifikanter Länge, wie im Bereich längerer Gehwegvorstreckungen, wurden bei der Datenerfassung jedoch durch Teilung der Straßensegmente berücksichtigt.

Die eigentliche Datenverarbeitung fand weitestgehend automatisiert über Python-Scripte[^5] und Geoverarbeitungswerkzeuge in QGIS statt, wobei in groben Zügen diese Arbeitsschritte erfolgten:

[^5]: Online verfügbar auf der [Projektseite der Parkraumanalyse](https://github.com/SupaplexOSM/strassenraumkarte-neukoelln).

(1.) Entsprechend der Fahrbahnbreite, die entweder direkt am Straßenobjekt hinterlegt ist oder aus seinen Attributen abgeschätzt werden kann, können die räumlichen Verläufe der jeweils linken und rechten Parkstreifen abgeleitet werden.

(2.) Bereiche, in denen sich aus der Straßenverkehrsordnung (StVO) ein Park- bzw. Halteverbot ergibt oder die sich entsprechend ihrer baulichen Anlage nicht zum Parken eignen, und die nicht bereits durch beschilderte Park- und Halteverbote abgebildet sind, können anschließend aus den Daten ausgeschlossen werden, in dem dort Abschnitte mit einer vorbestimmten Länge abgetrennt werden. Die Länge ergibt sich aus der StVO, Richtwerten oder der typischen baulichen Anlage im Untersuchungsgebiet:

<div class="table-responsive">
<table class="table table-hover table-bordered table-sm caption-top">
  <caption>Tabelle 1: Abstandsdefinitionen zum Parken an verschiedenen baulichen Anlagen.</caption>
  <thead class="table-secondary">
    <tr>
        <th class="w-50">Objekt / bauliche Anlage</th>
        <th class="w-50">Länge / Abstand</th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td>Kreuzung</td>
        <td>
        je 5 Meter vor Schnittpunkt der Bordsteinkanten
        <div class="text-muted"><small>Seit der StVO-Novelle aus dem Jahr 2020 erhöht sich dieser Abstand auf 8 Meter, wenn sich neben der Fahrbahn ein baulich angelegter Radweg befindet, was im Datenmodell jedoch noch nicht berücksichtigt wird – im Untersuchungsgebiet aber auch nur an vergleichsweise wenigen Kreuzungen der Fall ist.</small></div>
        </td>
    </tr>
    <tr>
        <td>Grundst&uuml;cks- und Gebäudeeinfahrten,abgesenkte Bordsteine</td>
        <td>Breite der Einfahrt, wenn bekannt, aber mindestens 4 Meter</td>
    </tr>
    <tr>
        <td>
          &Uuml;bergänge f&uuml;r andere Verkehrsteilnehmer:
          <ul>
            <li>Fu&szlig;gänger&uuml;berwege (Zebrastreifen)</li>
            <li>randseitige Markierungen oder Gehwegvorstreckungen</li>
            <li>Fu&szlig;gängerfurten und sonstige Markierungen</li>
          </ul>
        </td>
        <td>4 Meter und je 5 Meter davor6 Meter4 Meter und evtl. Ampeln</td>
    </tr>
    <tr>
        <td>Ampeln (nicht klar geregelt, faktisch kaum eingehalten)</td>
        <td>10 Meter davor</td>
    </tr>
    <tr>
        <td>Bushaltestellen</td>
        <td>15 Meter davor und dahinter</td>
    </tr>
  </tbody>
</table>
</div>


(3.) Objekte, die das Parken im Parkstreifenbereich verhindern, wurden vor der Auswertung systematisch erfasst bzw. vervollständigt und in einem separaten Arbeitsschritt mit Sicherheitsabständen von den Parkbereichen abgezogen. Dazu gehören Fahrradabstellanlagen, Straßenbäume, Laternen, Poller, Bordsteinstrukturen, Straßenschilder sowie insbesondere beim (halben) Parken auf Gehwegen auch Straßenmöbel und Gehweg-Einbauten (z.B. Verteilerkästen). Insgesamt betrifft das aber nur einen kleinen Anteil aller Straßen.

(4.) Die berechneten Parkstreifensegmente wurden anschließend einer (zum Teil manuell gesteuerten) Nachbearbeitung unterzogen: So wurden kurze Segmente und Artefakte entfernt und Fehler- und Plausibilitätsprüfungen durchgeführt (z.B. Korrektur von überlappenden oder angrenzenden, aber nicht verbundenen Segmenten).

(5.) Für die vorliegende Parkraumanalyse wurde zudem zusätzlich eine aufwendige manuelle Nachbearbeitung vorgenommen, insbesondere um die Parkstreifen an die exakten, realen Bordsteinkanten anzupassen.[^7] Die Präzision wurde dadurch zwar erheblich erhöht, da dieser Schritt lagegenaue Aussagen ermöglicht, die allgemeine Aussagekraft der Ergebnisse wäre ohne eine solche Nachbearbeitung jedoch kaum beeinträchtigt und ist bei Übertragung der Parkraumanalyse auf andere Orte daher verzichtbar.[^8]

(6.) Abschließend wurden Stellplatzkapazitäten für zusammenhängende Parkstreifensegmente berechnet (Quotient aus der Länge eines Segments und dem Abstand der dort geparkten Fahrzeuge, vgl. nachfolgender Abschnitt).

[^7]: Dafür wurde zunächst ein automatisiertes „Snapping“ und anschließend eine systematische Fehlerkorrektur und Nachkontrolle für jedes Einzelsegment vorgenommen, teils unter Verwendung von aktuellen Straßenfotos (Mapillary) und anderen Daten wie dem Verkehrszeichen- und Gehwegüberfahrten-Layer der Berliner Straßenbefahrung 2014 zur präziseren Ausrichtung von Park- und Halteverboten oder Einfahtsbereichen.
[^8]: Die Abweichung zwischen den rein automatisiert ermittelten Stellplatzzahlen und den nachbearbeiteten Daten beträgt für das Straßenparken lediglich 0,6 Prozent und ist damit geringer als die anderer Unsicherheitsfaktoren (vgl. Kapitel 3).


### Interpolation von Stellplatzkapazitäten

#### Straßenparken

Für 5,5 Prozent aller Parkstände im Straßenbereich des Untersuchungsgebiets lagen bereits in den OSM-Daten Kapazitätsangaben vor, insbesondere bei markierten Parkständen und Parkbuchten. Die fehlenden Werte mussten aus der Länge der Parkstreifensegmente abgeleitet werden.

Beim Parallelparken sind einzelne Stellplätze meist nicht markiert; die Anzahl der Fahrzeuge, die entlang eines Streckenabschnitts geparkt werden können, richtet sich vielmehr nach der Fahrzeuglänge und einem Rangier-/Sicherheitsabstand. Dabei wird in der Verkehrsplanungsliteratur ein mittlerer Abstand von 5,2 Metern zwischen den Fahrzeugen angenommen, der sich bei Zählungen im Untersuchungsgebiet weitestgehend bestätigen lässt (vgl. auch Anhang B). Beim Schräg- und Querparken richtet sich die Anordnung der einzelnen Parkstände üblicherweise nach den Empfehlungen für Anlagen des ruhenden Verkehrs (EAR)[^9]. Beim Schrägparken sind dabei verschiedene Aufstellwinkel möglich, die in verschiedenen Parkstandsbreiten resultieren -- hier wurde ein konstanter Aufstellwinkel von 60 gon (54 Grad) angenommen.[^10] Daraus ergeben sich folgende Abstände zwischen jeweils zwei geparkten Fahrzeugen:

[^9]:	Forschungsgesellschaft für Straßen- und Verkehrswesen e.V. (FGSV) (Hrsg.): Empfehlungen für Anlagen des ruhenden Verkehrs EAR 05, Ausgabe 2005. Köln: FGSV-Verlag.
[^10]: Dieser Wert entspricht dem Winkel, der bei den meisten Parkständen dieser Art aus Stichproben im Untersuchungsgebiet aus Orthophotos ermittelt werden konnte. Bei davon abweichenden Winkeln ist insgesamt nur eine marginale Abweichung in Bezug auf das Gesamtergebnis zu erwarten, daher wurde dieser Wert zur Vereinfachung der Berechnungen als konstant angenommen.


* Längsparken:  5,2 Meter,
* Schrägparken:  3,1 Meter,
* Querparken:  2,5 Meter.

Die Stellplatzkapazität ergibt sich aus dem Quotienten der Länge eines Parkstreifensegments und dem entsprechenden Abstand, abgerundet auf eine ganze Zahl.

<div class="bg-info">

**Ergebnis:**

Für den Ortsteil Neukölln ergeben sich insgesamt 27.335 Kfz-Stellplätze im öffentlichen Straßenraum. In den Wohnquartieren des Ortsteils, also abzüglich der Gewerbegebiete Ederstraße und Köllnische Heide, sind es 24.403 (vgl. ausführlicher Anhang A).

Die [Parkraumkarte](https://supaplexosm.github.io/strassenraumkarte-neukoelln/?map=parkingmap) stellt die Stellplätze in verschiedenen Zoomstufen in unterschiedlichen Formen dar -- von einer straßenzugsorientierten Zählung bis zum einzelnen Stellplatz.

</div>

#### Park- und Stellplätze abseits des Straßenbereichs

Für die geometrisch flächenhaft vorliegenden Park- und Stellplätze abseits des öffentlichen Straßenraums liegen häufiger genaue Stellplatzangaben vor, da diese oft markiert und abzählbar sind. Für etwa die Hälfte der Parkplätze liegen jedoch keine Angaben vor (vgl. 2); diese Stellplatzkapazitäten werden aus der Grundfläche der geometrischen Objekte abgeleitet (sowie bei mehrgeschossigen Objekten in einigen Fällen aus der Anzahl der Parkebenen). Dies betrifft vor allem Tiefgaragen: Für diese lagen auf Grund der eingeschränkten Zugänglichkeit nur für 36 von 221 einbezogenen Objekten genaue Stellplatzzahlen vor.[^11] Da das Daten- bzw. Interpolationsmodell hier nur an den wenigen realen, bekannten Fällen validiert werden konnte, unterliegen diese Daten auch einer größeren Unsicherheit (vgl. Kapitel 3).

[^11]: Die bekannten Stellplatzinformationen für Tiefgaragen basieren auf online zugänglichen Dokumenten wie Berichten und Planungsunterlagen zu Bauprojekten oder Inseraten auf Vermietungsportalen, Zählungen vor Ort sowie vereinzelt erfolgreichen Nachfragen bei Vermietern oder Eigentümern (vgl. auch Kapitel 2.3).

Aus den Objekten mit bekannten Stellplatzangaben wurde der Median der mittleren Fläche pro Stellplatz ermittelt – differenziert für verschiedene Stellflächentypen und unter Berücksichtigung evtl. mehrstöckiger Stellplatzobjekte (Geschossfläche). Die geschätzte Kapazität eines Stellplatzobjekts ergibt sich aus dem Quotienten der Geschossfläche der Objektgeometrie und diesem Medianwert. Die Differenzierung nach Stellflächentypen ist notwendig, da diese sich im Flächenbedarf pro Fahrzeug und der baulichen Gestalt unterscheiden: Beispielsweise enthalten Garagengeometrien üblicherweise keine Zufahrtswege, während diese bei Tiefgaragen ebenso wie Stützelemente, Ausgänge etc. in der Grundfläche enthalten sind. Ebenerdige Park- und Stellplätze wurden in eine kleinere und eine größere Kategorie geteilt, da kleinere Stellflächen meist ohne, größere überwiegend mit Zufahrtswegen in den OSM-Daten enthalten sind.[^12]

[^12]: Kleinere Parkplätze umfassen dabei weniger als acht Stellplätze, größere mindestens acht. Diese Grenze wurde aus den vorhandenen Objekten mit genauen Angaben zur Stellplatzkapazität abgeleitet, da in diesem Bereich ein signifikanter Sprung im Quotienten aus Fläche und Stellplatzanzahl zu beobachten war.

<div class="table-responsive">
<table class="table table-hover table-bordered table-sm caption-top">
  <caption>Tabelle 2: Berechnungsgrundlage für die Interpolation von Stellplatzkapazitäten geometrisch flächenhafter Parkraumobjekte.</caption>
  <thead class="table-secondary">
    <tr>
      <th rowspan=2>Stellfl&auml;chentyp</th>
      <th rowspan=2>Fl&auml;che pro Stellplatz [m&sup2;]</th>
      <th colspan=2>Anzahl Objekte im Datensatz</th>
      <th rowspan=2>Anteil gesch&auml;tzter Stellpl&auml;tze</th>
    </tr>
    <tr>
      <th>gesamt</th>
      <th>mit bekannter Stellplatzzahl</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Carports</td>
      <td>14,9</td>
      <td>46</td>
      <td>38</td>
      <td>14 %</td>
    </tr>
    <tr>
      <td>Garagen</td>
      <td>16,8</td>
      <td>789</td>
      <td>578</td>
      <td>34 %</td>
    </tr>
    <tr>
      <td>Parkh&auml;user</td>
      <td>28,2</td>
      <td>9</td>
      <td>5</td>
      <td>8 %</td>
    </tr>
    <tr>
      <td>Parkpl&auml;tze (klein)</td>
      <td>14,5</td>
      <td>537</td>
      <td>327</td>
      <td>42 %</td>
    </tr>
    <tr>
      <td>Parkpl&auml;tze (gro&szlig;)</td>
      <td>21,7</td>
      <td>472</td>
      <td>247</td>
      <td>48 %</td>
    </tr>
    <tr>
      <td>Tiefgaragen</td>
      <td>31,3</td>
      <td>221</td>
      <td>36</td>
      <td>81 %</td>
    </tr>
    <tr class="table-light">
      <td><strong>Summe</strong></td>
      <td><strong>-</strong></td>
      <td><strong>2074</strong></td>
      <td><strong>1231</strong></td>
      <td><strong>47 %</strong></td>
    </tr>
  </tbody>
</table>
</div>

_Legende:_

* _"Anzahl Objekte im Datensatz"_: Die Anzahl bezieht sich auf die Gesamtzahl der Objekte eines Stellflächentyps im Untersuchungsraum, also im Berliner Ortsteil Neukölln sowie einer Pufferzone von 500 Metern um dessen Ortsteilgrenzen.
* _"Parkplätze (klein)"_:	Die Kategorie „Parkplätze“ umfasst überwiegend klassische ebenerdige Park- und Stellplätze (N = 994), aber auch vereinzelt vorkommendes Dachparken (N = 6) und Parkdecks/Parkflächen im Erdgeschoss unter Gebäuden (N = 9).

<div class="bg-info">

**Ergebnis:**

Für den Ortsteil Neukölln ergeben sich daraus 12.226 (in den Wohnquartieren: 11.044) Stellplätze abseits des Straßenraums, die sich dauerhaft bzw. über Nacht zum Parken für Anwohnende eignen. Zusammen mit dem Straßenparken stehen somit insgesamt 39.561 (Wohnquartiere: 35.447) Stellplätze zur Verfügung, denen 36.266 (33.513) angemeldete Kfz gegenüber stehen, was einer theoretischen Stellplatzauslastung von 91,7 Prozent (94,5 Prozent) entspricht.

Darüber hinaus gibt es im Ortsteil Neukölln 8.105 (Wohnquartiere: 1.940) nicht zum dauerhaften Parken geeignete Stellplätze (insbesondere Mitarbeiter- und Kundenparkplätze), sowie 428 (219) ungenutzte Stellplätze, beispielsweise in leerstehenden Tiefgaragen.

Die [Parkraumkarte](https://supaplexosm.github.io/strassenraumkarte-neukoelln/?map=parkingmap) stellt auch diese Stellplätze abseits des Straßenparkens dar, differenziert nach Stellflächentypen und Eignung zum Dauerparken.

</div>

### Ermittlung von Stellplatzdichten mit gebäudegenauem Bevölkerungsmodell

Ein Ziel der Auswertung ist es, kleinräumige Stellplatzdichteverteilungen zu berechnen, also die Anzahl von Kfz-Stellplätzen in einem Gebiet mit der Anzahl der Einwohnerinnen und Einwohner bzw. der Anzahl der zugelassenen Kfz zu vergleichen. Dabei wird angenommen, dass die Anzahl der zugelassenen Fahrzeuge an einem Ort ein Indikator für tatsächlich an einem Ort geparkte Fahrzeuge ist, was zumindest für Wohngebiete naheliegt (vgl. Kapitel 3). Das Verhältnis von verfügbaren Stellplätzen zur Anzahl zugelassener Kraftfahrzeuge wird im Folgenden als „Stellplatzdichte" bezeichnet.

Für kleinräumige Aussagen, beispielsweise zur Bestimmung der Stellplatzdichte für einen bestimmten Straßenzug oder im Umfeld eines bestimmten Ortes, sind entsprechend hoch aufgelöste, adress-genaue Kfz-Daten notwendig, die im Rahmen dieses Projekts jedoch nicht zur Verfügung standen. Abhilfe schafft ein eigenes Datenmodell auf Grundlage von Bevölkerungsdaten auf Blockebene (323 Teilräume allein im Ortsteil Neukölln mit durchschnittlich je etwa 500 Einwohnerinnen und Einwohnern) und Kfz-Daten auf LOR-Planungsraumebene (18 Teilräume im Ortsteil Neukölln mit durchschnittlich je knapp 10.000 Einwohnerinnen und Einwohnern; zu den Datensätzen vgl. Kapitel 2.3).

Für das Bevölkerungsmodell wurde zunächst jedem Gebäude die statistisch erwartbare Anzahl von Bewohnenden zugeordnet. Dafür müssen zunächst Wohngebäude von anderen Gebäuden unterschieden[^15] und die jeweils zum Wohnen genutzten Gebäudestockwerke ermittelt werden.[^16] Die Gesamtbevölkerung einer Blockteilfläche wurde schließlich anteilig dieser „Wohngeschossflächenzahl" auf die Gebäude verteilt. Jede Bewohnerin und jeder Bewohner lässt sich auf diese Weise statistisch individuell am Wohnort darstellen und kann auf Basis der Kfz-Anmeldedaten mit einer entsprechenden Wahrscheinlichkeit als Kfz-Halter/in eingestuft werden.

[^15]: Die ALKIS-Gebäudedaten enthalten für jedes Gebäude eine Klassifikation seiner Funktion, sodass Wohngebäude beispielsweise von Büro-, Gewerbe- oder Industriegebäuden unterschieden werden können oder Mischnutzungen erkennbar sind.
[^16]: Für reine Wohngebäude wurden dabei alle Obergeschosse einbezogen. Für Gebäude der Kategorie „Wohngebäude mit Gewerbenutzung“ ist anzunehmen, dass ein Geschoss (Erdgeschoss) nicht zum Wohnen genutzt wird. Für die eher seltene Kategorie „Gewergegebäude mit Wohnnutzung“ wurde angenommen, dass die Hälfte aller Geschosse als Wohngeschosse genutzt werden.

Die resultierenden Kfz-Halterdaten lassen sich auf diese Weise -- ebenso wie die verfügbaren Stellplätze -- in Form von Punktwolken abbilden, wobei jeder Punkt einem Stellplatz bzw. einem zugelassenen Kfz entspricht. Für ein bestimmtes Gebiet lässt sich auf diese Weise leicht das Verhältnis aus verfügbaren Stellplätzen und angemeldeten Kfz ermitteln. Die [Parkraumkarte](https://supaplexosm.github.io/strassenraumkarte-neukoelln/?map=parkingmap) stellt diese Stellplatzdichte auf niedrigeren Zoomstufen für das Nahumfeld eines Wohnortes dar, wobei eine fußläufige Distanz von 350 Metern (3 Minuten zu Fuß bei einer Laufgeschwindigkeit von 7 km/h bzw. knapp über 4 Minuten bei 5 km/h) zugrunde liegt. Die Stellplatzdichte für diese Distanz wurde jeweils für den Gittermittelpunkt eines 25 Meter großen hexagonalen Gitters berechnet auf Basis von Isochronen[^17] berechnet.

[^17]: Isochronen sind räumliche Linien gleicher Zeit, umgrenzen in diesem Fall also einen Raum, der innerhalb der angegebenen Zeit zu Fuß erreicht werden kann und sich dabei bis zu 350 Meter entfernt vom Ausgangspunkt erstreckt. Das Routing erfolgte über das OSM-Straßen- und Wegenetz.


<div class="bg-info">

**Ergebnis:**

Im Durchschnitt (Median) ergibt sich für die Neuköllner Wohnquartiere im Umkreis von 350 Metern Laufdistanz um einen Ort eine Anzahl von 835 Stellplätzen, eine Zahl von 759 zugelassenen Kraftfahrzeugen und eine theoretische Verfügbarkeit von 1,08 Stellplätzen pro Fahrzeug. Wird nur das Straßenparken berücksichtigt, stehen in diesem Umkreis 604 Stellplätze zur Verfügung (Median: 0,81 pro Fahrzeug).

Wie viele finden im Nahumfeld einen Parkplatz, wie viele müssen im Mittel weiter fahren?

Bei der Interpretation dieser Darstellung ist zu berücksichtigen, dass Räume und Objekte mit größerem Stellplatzüberangebot -- wie dünn besiedelte Gebiete oder Parkhäuser, die einen wichtigen Beitrag zur Stellplatzversorgung eines größeren Umfelds leisten können -- sich nur innerhalb dieser Nahdistanz auf das Ergebnis auswirken.

</div>

### Flächenverbrauch

Aus der Lage und Länge der Parkstreifen im Straßenraum kann -- abhängig von der Ausrichtung der dort geparkten Fahrzeuge -- auf die Fläche geschlossen werden, die direkt von stehenden bzw. geparkten Fahrzeugen in Anspruch genommen wird. Die Breite eines Parkstreifens entspricht dabei:

* 2 Meter bei Längsparken,
* 4,5 Meter bei Schrägparken,
* 5 Meter bei Querparken.

Diese Fläche kann in Relation zur Fläche des öffentlichen Straßen- bzw. Verkehrsraumes gesetzt werden, also der Fläche zwischen den Gebäudefassaden oder Grundstücksgrenzen inklusive aller Straßenbestandteile wie Fahrbahnen, Mittelstreifen oder Geh- und Radwegen. Berechnungsgrundlage dafür ist die Einteilung der Blockflächen, wie sie im Berliner Geoportal beispielsweise für die Wiedergabe der Bevölkerungsdichte verwendet wird (vgl. Kapitel 2.3). In unbewohnten Räumen hat diese Blockflächeneinteilung Lücken, die auf Basis von OSM-Daten gefüllt wurden.

<div class="bg-info">

**Ergebnis:**

Allein für die Neuköllner Wohnquartiere ergibt sich daraus, dass Parkstreifen im öffentlichen Straßenraum eine Fläche von insgesamt 327.000 m² in Anspruch nehmen, was 19 Prozent des öffentlichen Verkehrsraumes und 4,4 Prozent der Gesamtfläche entspricht. Parkflächen und Stellplätze abseits des Straßenraumes beanspruchen darüber hinaus zusätzlich 171.000 m², ein Gesamtflächenanteil von 2,3 Prozent.

</div>

## Bewertung von Unsicherheitsfaktoren

Die vorliegende Parkraumanalyse basiert auf einem interpolativen Datenmodell und beruht damit auf Annahmen und Vereinfachungen, um die (komplexe) Realität modellhaft abzubilden und „berechenbar" zu machen. Während sich viele der zu Grunde liegenden Annahmen in der tatsächlichen Realität überprüfen, zählen oder messen lassen, unterliegen die Ergebnisse in ihrer Interpretation kleineren Unsicherheiten, die sich kaum oder nur mit erheblichem empirischen Aufwand quantifizieren lassen. Wie viele Garagen werden beispielsweise tatsächlich zum Abstellen von Kfz genutzt, wie viele Falschparker gibt es oder wie viele Dienst- und Mietwagen bleiben in der Kfz-Statistik für das Untersuchungsgebiet unberücksichtigt? Unsicherheitsfaktoren wie diese sollen in diesem Abschnitt einer groben Schätzung unterzogen werden.

Das Kernstück des Datenmodells ist die Abbildung des Straßenparkens, das die Parkraumsituation wesentlich prägt. Um diesen Aspekt des Datenmodells zu prüfen, wurden in zwei Testgebieten willkürlich XXX Straßenteilstücke abgelaufen und und die dort geparkten Fahrzeuge bzw. verfügbaren Stellplätze[^20] mit dem Datenmodell verglichen, um seine Aussagekraft zu belegen (vgl. Anhang B). Der Vergleich zeigt eine hohe Übereinstimmung zwischen interpolierten und vor Ort gezählten Werten mit einer Abweichung von weniger als einem Prozent -- die Zählung ergab eine leicht höhere Anzahl tatsächlich geparkter Fahrzeuge, wobei der Unterschied eher vernachlässigbar bleibt. [... evtl. kurz auf Unterschiede im Längs-/Schräg-/Querparken eingehen.]

[^20]: Gezählt wurden Fahrzeuge und Parklücken mit ausreichender Größe für einen Pkw, soweit ein ordnungskonformes Parken eingehalten wird, also insbesondere unter Einhaltung des 5-Meter-Abstands zu Kreuzungen und der Freihaltung von Einfahrten.

Die automatisiert erzeugten Parkstreifendaten der vorliegenden Parkraumanalyse wurden einer aufwendigen manuellen Nachbearbeitung unterzogen, wodurch ebenfalls eine (quantitativ jedoch ebenfalls eher vernachlässigbare) Fehlerkorrektur erfolgte: Die Stellplatzzahlen des Rohdatensatzes lagen 0,6 Prozent über denen des nachbearbeiteten Datensatzes (vgl. Kapitel 2.4).

Darüber hinaus gibt es eine Reihe anderer Faktoren, die zu einer Über- oder Unterschätzung der realen Parkraumsituation im Vergleich zum Datenmodell führen können. Sie lassen sich nur schwer bemessen und können daher nicht oder nur eingeschränkt in einem numerischen Datenmodell abgebildet werden. Für die Interpretation der Ergebnisse der Parkraumanalyse sind insbesondere diese Faktoren zu berücksichtigen:

* Das Datenmodell des Straßenparkens bildet eine juristische, StVO-konforme Situation ab; in der Realität ist im Untersuchungsraum jedoch häufiges Falschparken zu beobachten bis hin zu faktischen Parkstreifen in verkehrsberuhigten Bereichen, in denen dauerhaft falsch geparkt wird (z.B. Isar-/Neckarstraße). Darüber hinaus gibt es Graubereiche wie Diagonal- und Querparken, das eigentlich durch Beschilderung oder Markierungen angeordnet sein müsste, was vor Ort in manchen Fällen nicht (mehr) erkennbar ist -- in diesem Fall gibt das Modell die Situation wieder, wie sie vor Ort und in der Vergangenheit (Luftbildaufnahmen) dauerhaft zu beobachten war.

* Für zwei Szenarien wurde der Einfluss durch Falschparkverhalten quantifiziert:

  * Wird der mittlere Abstand geparkter Fahrzeuge zum Kreuzungsbereich von 5 auf 2,5 Meter halbiert, erhöht sich die Anzahl geparkter Fahrzeuge im Straßenraum um 3,3 Prozent.

  * Wird vor jeder zweiten Einfahrt geparkt, erhöht sich die Anzahl geparkter Fahrzeuge im Straßenraum um 2,6 Prozent.

* Bei der Berechnung von Stellplatzdichten unter Verwendung von Kfz-Anmeldedaten wird angenommen, dass die Anzahl angemeldeter Fahrzeuge an einem Ort ein Indikator für tatsächlich dort geparkte Fahrzeuge ist (vgl. Kapitel 2.6). Insbesondere in Wohnquartieren dürfte hier zumindest eine starke Korrelation bestehen -- die tatsächliche Anzahl geparkter Fahrzeuge könnte allerdings höher sein, insbesondere da:

  * Firmen-/Dienstwagen von einem Teil der Bevölkerung privat, also auch an ihrem Wohnort genutzt werden, die Fahrzeuge dort jedoch meist nicht angemeldet sind und daher statistisch unsichtbar bleiben. Dieser Wert lässt sich nur schwer quantifizieren, dürfte im Untersuchungsgebiet aber in einer Größenordnung von höchstens vier Prozent aller Kfz liegen.[^21]

  * Zunehmend sind in diesem Zusammenhang auch Fahrzeuge von Carsharing-Anbietern zu berücksichtigen, von denen in Berlin derzeit etwa 6.000 im Free-Floating-Segment bereitstehen. Im Untersuchungsgebiet dürfte der Anteil dieser Fahrzeuge etwa in einer Größenordnung von einem Prozent liegen.[^22] Zusätzlich beanspruchen stationsbasierte Anbieter vereinzelt Stellplätze beispielsweise in Tiefgaragen.

[^21]: Etwa vier Prozent der Autofahrer:innen in Deutschland geben an, dass ihr Erstfahrzeug ein Dienstwagen ist (vgl. Statista: [„Anzahl der Personen in Deutschland, deren Erstwagen ein Privat- bzw. Dienstwagen ist"](https://de.statista.com/statistik/daten/studie/172094/umfrage/dienstwagen-oder-privatwagen-als-erstwagen/)). Inwieweit sich diese Angaben auf die sozioökonomischen und geografischen Bedingungen des Untersuchungsgebiets übertragen lassen und wie Zweitwagen etc. und andere Faktoren diesen Wert beeinflussen, kann an dieser Stelle nicht bewertet werden.
[^22]: 	Unter der Annahme, dass diese 6.000 Fahrzeuge alle innerhalb des S-Bahn-Rings abgestellt würden, wo es etwa 350.000 zugelassene Kfz gibt, ergäbe sich ein Anteil von 1,7 Prozent der dort zugelassenen Fahrzeuge. Der Geschäftsbereich vieler Anbieter erstreckt sich aber auch darüber hinaus.

* In Gebieten mit geringem Parkdruck kommen außerdem Fahrzeuge dazu, die dort auf Grund der günstigen Parkraumsituation länger und in größerer Entfernung zu ihrem eigentlichen Meldeort abgestellt werden (beispielsweise sporadisch genutzte Transporter oder Wohnmobile) -- dafür aber am eigentlichen Meldeort keinen Stellplatz in Anspruch nehmen. Phänomene wie Besuchsverkehr dürften dagegen bei der Bewertung der dauerhaften Parkraumsituation nur einen geringen Einfluss haben.

* Stellplatzangaben, die neben dem Straßenparken im öffentlichen Raum auch die (meist privaten) Stellplätze abseits des Straßenraums berücksichtigen, müssen als potentielle Aussagen verstanden werden, da die tatsächliche Auslastung von Stellplätzen unbekannt bleibt. Vor allem Garagen werden beispielsweise häufig anders genutzt als zum Abstellen eines Kfz. Unter der Annahme, dass jede zweite Garage nicht zum Abstellen eines Kfz genutzt wird, reduziert sich das Gesamt-Stellplatzangebot im Datenmodell um 3 Prozent. In Nachbarschaften mit hohem Garagenanteil, insbesondere dem Rollbergkiez, kann das im Einzelfall zu größeren Unsicherheiten führen.

* Alle Parkhäuser im Untersuchungsgebiet können auch von Anwohnerinnen und Anwohnern genutzt werden; sie tragen insgesamt fast 4 Prozent der Gesamtstellplatzkapazitäten im Datenmodell bei. Faktisch wird dieses Potential jedoch offenbar nicht ausgeschöpft, da ein großer Leerstand beobachtet werden kann. Zum Teil trifft dies auch auf andere, dauerhaft gering ausgelastete Stellplätze, Tiefgaragen etc. zu.

* Tiefgaragen tragen 7 Prozent aller verfügbaren Stellplätze bei, 81 Prozent dieser Tiefgaragenstellplätze basieren allerdings auf geschätzten Werten (vgl. Kapitel 2.5.2). Läge die tatsächliche Anzahl der geschätzten Tiefgaragenplätze 10 Prozent über oder unter den ermittelten Werten, würde sich das Gesamt-Stellplatzangebot im Datenmodell um 0,6 Prozent erhöhen bzw. reduzieren. Dieser Wert ist vergleichsweise gering; im Einzelfall könnten jedoch größere Abweichungen auftreten. So wird die Parkraumsituation rund um den Mariendorfer Weg im Datenmodell von zwei sehr großen Tiefgaragen dominiert, die zu einem großen Überangebot von Stellplätzen führen. Die reale Stellplatzzahl könnte hier unter Umständen erheblich geringer sein oder nicht für alle Anwohnenden zur Verfügung stehen.

* Baustellen und andere temporäre Halte- und Parkverbote finden keine Wiedergabe im Datenmodell, führen in der Realität aber permanent zu einer leichten Reduktion der tatsächlich nutzbaren Stellplatzkapazitäten.

Darüber hinaus gibt es weitere Faktoren, die im konkreten Fall zu Unsicherheiten führen können, in Relation zur Gesamtheit der Daten aber nur einen sehr geringen Teil betreffen und bei denen daher ein eher vernachlässigbarer Einfluss auf die allgemeine Aussagekraft angenommen werden kann:

* Es muss davon ausgegangen werden, dass nicht alle parkplatzrelevanten Objekte kartiert wurden und einige falsch oder nicht mehr aktuell klassifiziert sind. Fehlen dürften vor allem kleinere Stellplätze in schattigen Hinterhöfen oder auch Parkgaragen im Erdgeschoss von Gebäuden, die schwer aus dem öffentlichen Raum aus zugänglich oder einsehbar sind und auf Luftbildaufnahmen nicht erkennbar sind.

* Das Datenmodell umfasst nur Parkstreifen sowie Park- und Stellplätze, vernachlässigt jedoch beispielsweise das (teils ordnungswidrige) Parken auf Einfahrten, Wegen oder anderen nicht dafür angelegten Flächen.

* Den Stellplatzkapazitäten für Parkstreifen liegt eine pauschale Fahrzeuglänge bzw. ein fester Abstand zwischen zwei geparkten Fahrzeugen zu Grunde, basierend auf einer gemittelten Fahrzeuglänge. Tatsächliche Fahrzeuglängen sind natürlich variabel; es gibt zudem Fahrzeuge mit größerem (z.B. Transporter) oder kleinerem (z.B. Motorräder) Raumbedarf. Der für die Stellplatzdichte berücksichtigte Kfz-Datensatz umfasst zu 80 Prozent Pkw, der Rest teilt sich vor allem zu etwa gleichen Teilen auf Krafträder und Lastkraftwagen (wozu auch die meisten Kleintransporter zählen) auf.[^23]

[^23]: Für Berlin vgl. Amt für Statistik Berlin-Brandenburg: Kraftfahrzeugbestand im Land Berlin, hier online verfügbar.

* Die Abgrenzung von gewerblich genutzten Stellplätzen, beispielsweise für (meist an diesem Ort angemeldete) Transportfahrzeuge des Handwerks, und Mitarbeiter- oder Kundenparkplätzen, die nicht zum Dauerparken angelegt sind (und daher in einigen Auswertungen nicht berücksichtigt werden), ist im Einzelfall schwer oder durch Mischnutzung unmöglich, daher können diese teils falsch zugeordnet sein.

Einfahrten bzw. abgesenkte Bordsteine, für die in den OSM-Daten keine Breiten vermerkt sind, gehen mit einer pauschalen Breite von 4 Metern[^24] in das Datenmodell ein. Im Einzelfall können diese schmaler oder breiter sein, auch wenn besonders breite Einfahrten während der Datenerhebungsphase meist mit einer Breitenangabe versehen wurden oder die Parkstreifen in diesem Bereich in der manuellen Nachbearbeitung der Daten korrigiert wurden.

[^24]:  In der Rechtsprechung wird teils eine Breite von 3 Metern als ausreichend angesehen, was im Datenmodell insgesamt eine um 0,7 Prozent höhere Stellplatzzahl ergeben würde. Das einzelne Einfahrten breiter sind, aber nicht mit ihrer tatsächlichen Breite in das Modell einfließen, ist dabei jedoch noch nicht berücksichtigt.

## Anhang A: Verfügbare Stellplatzkapazitäten in verschiedenen Teilräumen

<div class="table-responsive">
<table class="table table-hover table-bordered table-sm caption-top">
  <thead class="table-secondary">
    <tr>
      <th></th>
      <th>Bevölkerung</th>
      <th>Kfz</th>
      <th colspan=6>Verfügbare Stellplätze (zum Anwohner-/Nachtparken geeignet)</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th>Gesamt</th>
      <th><span class="text-muted">davon</span><br>Straßenparken</th>
      <th><span class="text-muted">davon</span><br>Park-/Stellplätze</th>
      <th><span class="text-muted">davon</span><br>Tief-garagen</th>
      <th><span class="text-muted">davon</span><br>Garagen/Carports</th>
      <th><span class="text-muted">davon</span><br>Parkhäuser</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Untersuchungsgebiet gesamt</th>
      <td>245870</td>
      <td>59718</td>
      <td>64973</td>
      <td>43161<br><small class="text-muted">66,4%</small></td>
      <td>9654<br><small class="text-muted">14,9%</small></td>
      <td>4697<br><small class="text-muted">7,2%</small></td>
      <td>4551<br><small class="text-muted">7,0%</small></td>
      <td>2910<br><small class="text-muted">4,5%</small></td>
    </tr>
    <tr>
      <th>…davon Ortsteil Neukölln</th>
      <td>165702</td>
      <td>36266</td>
      <td>39561</td>
      <td>27335<br><small class="text-muted">69,1%</small></td>
      <td>5285<br><small class="text-muted">13,4%</small></td>
      <td>2782<br><small class="text-muted">7,0%</small></td>
      <td>2360<br><small class="text-muted">6,0%</small></td>
      <td>1799<br><small class="text-muted">4,5%</small></td>
    </tr>
    <tr>
      <th>…davon Wohnquartiere</th>
      <td>162841</td>
      <td>33513</td>
      <td>35447</td>
      <td>24403<br><small class="text-muted">68,8%</small></td>
      <td>4375<br><small class="text-muted">12,3%</small></td>
      <td>2718<br><small class="text-muted">7,7%</small></td>
      <td>2206<br><small class="text-muted">6,2%</small></td>
      <td>1745<br><small class="text-muted">4,9%</small></td>
    </tr>
    <tr>
      <th>Bouchéstraße</th>
      <td>3852</td>
      <td>1023</td>
      <td>1212</td>
      <td>690<br><small class="text-muted">56,9%</small></td>
      <td>103<br><small class="text-muted">8,5%</small></td>
      <td>71<br><small class="text-muted">5,9%</small></td>
      <td>5<br><small class="text-muted">0,4%</small></td>
      <td>343<br><small class="text-muted">28,3%</small></td>
    </tr>
    <tr>
      <th>Donaukiez</th>
      <td>8306</td>
      <td>1632</td>
      <td>1015</td>
      <td>721<br><small class="text-muted">71,0%</small></td>
      <td>124<br><small class="text-muted">12,2%</small></td>
      <td>108<br><small class="text-muted">10,6%</small></td>
      <td>62<br><small class="text-muted">6,1%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Flughafenkiez</th>
      <td>9824</td>
      <td>1792</td>
      <td>2758</td>
      <td>1315<br><small class="text-muted">47,7%</small></td>
      <td>247<br><small class="text-muted">9,0%</small></td>
      <td>208<br><small class="text-muted">7,5%</small></td>
      <td>38<br><small class="text-muted">1,4%</small></td>
      <td>950<br><small class="text-muted">34,4%</small></td>
    </tr>
    <tr>
      <th>Glasower Straße</th>
      <td>8570</td>
      <td>2066</td>
      <td>2062</td>
      <td>1580<br><small class="text-muted">76,6%</small></td>
      <td>160<br><small class="text-muted">7,8%</small></td>
      <td>140<br><small class="text-muted">6,8%</small></td>
      <td>182<br><small class="text-muted">8,8%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Hertzbergkiez</th>
      <td>8894</td>
      <td>1845</td>
      <td>1931</td>
      <td>1560<br><small class="text-muted">80,8%</small></td>
      <td>206<br><small class="text-muted">10,7%</small></td>
      <td>28<br><small class="text-muted">1,5%</small></td>
      <td>137<br><small class="text-muted">7,1%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Körnerkiez</th>
      <td>12248</td>
      <td>2405</td>
      <td>2352</td>
      <td>1986<br><small class="text-muted">84,4%</small></td>
      <td>176<br><small class="text-muted">7,5%</small></td>
      <td>55<br><small class="text-muted">2,3%</small></td>
      <td>135<br><small class="text-muted">5,7%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Reuterkiez</th>
      <td>27355</td>
      <td>5426</td>
      <td>5780</td>
      <td>4334<br><small class="text-muted">75,0%</small></td>
      <td>628<br><small class="text-muted">10,9%</small></td>
      <td>430<br><small class="text-muted">7,4%</small></td>
      <td>388<br><small class="text-muted">6,7%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Richardkiez</th>
      <td>23143</td>
      <td>4669</td>
      <td>4655</td>
      <td>3455<br><small class="text-muted">74,2%</small></td>
      <td>351<br><small class="text-muted">7,5%</small></td>
      <td>337<br><small class="text-muted">7,2%</small></td>
      <td>512<br><small class="text-muted">11,0%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Rollbergkiez</th>
      <td>7397</td>
      <td>1497</td>
      <td>2158</td>
      <td>1234<br><small class="text-muted">57,2%</small></td>
      <td>157<br><small class="text-muted">7,3%</small></td>
      <td>418<br><small class="text-muted">19,4%</small></td>
      <td>349<br><small class="text-muted">16,2%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Schillerkiez</th>
      <td>15798</td>
      <td>2848</td>
      <td>2953</td>
      <td>2742<br><small class="text-muted">92,9%</small></td>
      <td>105<br><small class="text-muted">3,6%</small></td>
      <td>47<br><small class="text-muted">1,6%</small></td>
      <td>43<br><small class="text-muted">1,5%</small></td>
      <td>16<br><small class="text-muted">0,5%</small></td>
    </tr>
    <tr>
      <th>Schulenburgpark</th>
      <td>9226</td>
      <td>2331</td>
      <td>2568</td>
      <td>1670<br><small class="text-muted">65,0%</small></td>
      <td>799<br><small class="text-muted">31,1%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
      <td>99<br><small class="text-muted">3,9%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Silbersteinstraße</th>
      <td>5045</td>
      <td>966</td>
      <td>1298</td>
      <td>413<br><small class="text-muted">31,8%</small></td>
      <td>172<br><small class="text-muted">13,3%</small></td>
      <td>641<br><small class="text-muted">49,4%</small></td>
      <td>72<br><small class="text-muted">5,5%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>TreptowerStraße Nord</th>
      <td>7073</td>
      <td>1544</td>
      <td>1671</td>
      <td>964<br><small class="text-muted">57,7%</small></td>
      <td>413<br><small class="text-muted">24,7%</small></td>
      <td>160<br><small class="text-muted">9,6%</small></td>
      <td>134<br><small class="text-muted">8,0%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Warthekiez</th>
      <td>6762</td>
      <td>1136</td>
      <td>1214</td>
      <td>1155<br><small class="text-muted">95,1%</small></td>
      <td>48<br><small class="text-muted">4,0%</small></td>
      <td>3<br><small class="text-muted">0,2%</small></td>
      <td>8<br><small class="text-muted">0,7%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
    <tr>
      <th>Weiße Siedlung</th>
      <td>5734</td>
      <td>1638</td>
      <td>1301</td>
      <td>643<br><small class="text-muted">49,4%</small></td>
      <td>205<br><small class="text-muted">15,8%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
      <td>17<br><small class="text-muted">1,3%</small></td>
      <td>436<br><small class="text-muted">33,5%</small></td>
    </tr>
    <tr>
      <th>Wissmannstraße</th>
      <td>3614</td>
      <td>695</td>
      <td>519</td>
      <td>370<br><small class="text-muted">71,3%</small></td>
      <td>52<br><small class="text-muted">10,0%</small></td>
      <td>72<br><small class="text-muted">13,9%</small></td>
      <td>25<br><small class="text-muted">4,8%</small></td>
      <td>-<br><small class="text-muted">0%</small></td>
    </tr>
  </tbody>
</table>
</div>

_Fußnoten:_

* _"Untersuchungsgebiet gesamt":_ Das gesamte Untersuchungsgebiet umfasst den Ortsteil Neukölln sowie zusätzlich eine angrenzende Pufferzone von 500 Metern um dessen Ortsteilgrenzen, vgl. Kapitel X.
* _"davon Wohnquartiere":_ Die Einteilung der Wohnquartiere entspricht den LOR-Planungsräumen, mit der Ausnahme, dass der Warthekiez aus dem Planungsraum „Silbersteinstraße“ in einen eigenständigen Teilraum herausgelöst wurde.

## Anhang B: Vergleich interpolierter und gezählter Stellplätze (Straßenparken)

<div class="table-responsive">
<table class="table table-hover table-bordered table-sm caption-top">
  <thead class="table-secondary">
    <tr>
      <th>Straßenbschnitt</th>
      <th></th>
      <th></th>
      <th>Seite</th>
      <th>Ausrichtung</th>
      <th colspan=2>Stellplatzzahl</th>
      <th colspan=2>Abweichung</th>
    </tr>
    <tr>
      <th>Name</th>
      <th>von</th>
      <th>bis</th>
      <th></th>
      <th></th>
      <th>gezählt</th>
      <th>berechnet</th>
      <th>absolut</th>
      <th>relativ</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Schillerkiez</th>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <th>Allerstr.</th>
      <td>Lichtenrader Str.</td>
      <td>Oderstr.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>18</td>
      <td>18</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Allerstr.</th>
      <td>Oderstr.</td>
      <td>Lichtenrader Str.</td>
      <td>Süd</td>
      <td>Schräg</td>
      <td>30</td>
      <td>30</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Allerstr.</th>
      <td>Schillerprom.</td>
      <td>Weisestr.</td>
      <td>Süd</td>
      <td>Längs</td>
      <td>18</td>
      <td>17</td>
      <td>-1</td>
      <td>-5,9%</td>
    </tr>
    <tr>
      <th>Allerstr.</th>
      <td>Weisestr.</td>
      <td>Schillerprom.</td>
      <td>Nord</td>
      <td>Schräg</td>
      <td>33</td>
      <td>30</td>
      <td>-3</td>
      <td>-10,0%</td>
    </tr>
    <tr>
      <th>Herrfurthstr.</th>
      <td>Oderstr.</td>
      <td>Lichtenrader Str.</td>
      <td>Süd</td>
      <td>Quer</td>
      <td>34</td>
      <td>33</td>
      <td>-1</td>
      <td>-3,0%</td>
    </tr>
    <tr>
      <th>Herrfurthstr.</th>
      <td>Weisestr.</td>
      <td>Hermannstr.</td>
      <td>Süd</td>
      <td>Längs</td>
      <td>20</td>
      <td>17</td>
      <td>-3</td>
      <td>-17,6%</td>
    </tr>
    <tr>
      <th>Kienitzer Str.</th>
      <td>Lichtenrader Str.</td>
      <td>Schillerprom.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>20</td>
      <td>18</td>
      <td>-2</td>
      <td>-11,1%</td>
    </tr>
    <tr>
      <th>Kienitzer Str.</th>
      <td>Oderstr.</td>
      <td>Lichtenrader Str.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>17</td>
      <td>17</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Kienitzer Str.</th>
      <td>Schillerprom.</td>
      <td>Weisestr.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>17</td>
      <td>18</td>
      <td>+1</td>
      <td>+5,6%</td>
    </tr>
    <tr>
      <th>Leinestr.</th>
      <td>Schillerprom.</td>
      <td>Lichtenrader Str.</td>
      <td>Nord</td>
      <td>Schräg</td>
      <td>34</td>
      <td>34</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Herrfurthstr.</td>
      <td>Selchower Str.</td>
      <td>Ost</td>
      <td>Quer</td>
      <td>62</td>
      <td>62</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Herrfurthstr.</td>
      <td>Kienitzer Str.</td>
      <td>West</td>
      <td>Längs</td>
      <td>26</td>
      <td>26</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Kienitzer Str.</td>
      <td>Herrfurthstr.</td>
      <td>Ost</td>
      <td>Schräg</td>
      <td>44</td>
      <td>42</td>
      <td>-2</td>
      <td>-4,8%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Kienitzer Str.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Längs</td>
      <td>15</td>
      <td>15</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Leinestr.</td>
      <td>Okerstr.</td>
      <td>Ost</td>
      <td>Längs</td>
      <td>14</td>
      <td>14</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Mahlower Str.</td>
      <td>Herrfurthstr.</td>
      <td>West</td>
      <td>Längs</td>
      <td>48</td>
      <td>52</td>
      <td>+4</td>
      <td>+7,7%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Okerstr.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Längs</td>
      <td>16</td>
      <td>14</td>
      <td>-2</td>
      <td>-14,3%</td>
    </tr>
    <tr>
      <th>Lichtenrader Str.</th>
      <td>Selchower Str.</td>
      <td>Mahlower Str.</td>
      <td>Ost</td>
      <td>Quer</td>
      <td>31</td>
      <td>32</td>
      <td>+1</td>
      <td>+3,1%</td>
    </tr>
    <tr>
      <th>Oderstr.</th>
      <td>Kienitzer Str.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Schräg</td>
      <td>27</td>
      <td>22</td>
      <td>-5</td>
      <td>-22,7%</td>
    </tr>
    <tr>
      <th>Oderstr.</th>
      <td>Okerstr.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Schräg</td>
      <td>24</td>
      <td>26</td>
      <td>+2</td>
      <td>+7,7%</td>
    </tr>
    <tr>
      <th>Okerstr.</th>
      <td>Hermannstr.</td>
      <td>Weisestr.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>25</td>
      <td>25</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Okerstr.</th>
      <td>Lichtenrader Str.</td>
      <td>Oderstr.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>15</td>
      <td>18</td>
      <td>+3</td>
      <td>+16,7%</td>
    </tr>
    <tr>
      <th>Okerstr.</th>
      <td>Lichtenrader Str.</td>
      <td>Schillerprom.</td>
      <td>Süd</td>
      <td>Schräg</td>
      <td>31</td>
      <td>31</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Okerstr.</th>
      <td>Schillerprom.</td>
      <td>Lichtenrader Str.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>18</td>
      <td>18</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Okerstr.</th>
      <td>Weisestr.</td>
      <td>Schillerprom.</td>
      <td>Nord</td>
      <td>Längs</td>
      <td>19</td>
      <td>19</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Schillerprom.</th>
      <td>Kienitzer Str.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Schräg</td>
      <td>25</td>
      <td>24</td>
      <td>-1</td>
      <td>-4,2%</td>
    </tr>
    <tr>
      <th>Schillerprom.</th>
      <td>Okerstr.</td>
      <td>Leinestr.</td>
      <td>West</td>
      <td>Längs</td>
      <td>15</td>
      <td>15</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Weisestr.</th>
      <td>Allerstr.</td>
      <td>Kienitzer Str.</td>
      <td>West</td>
      <td>Schräg</td>
      <td>27</td>
      <td>27</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <th>Weisestr.</th>
      <td>Herrfurthstr.</td>
      <td>Kienitzer Str.</td>
      <td>West</td>
      <td>Längs</td>
      <td>27</td>
      <td>26</td>
      <td>-1</td>
      <td>-3,8%</td>
    </tr>
    <tr>
      <th>Weisestr.</th>
      <td>Kienitzer Str.</td>
      <td>Allerstr.</td>
      <td>Ost</td>
      <td>Längs</td>
      <td>16</td>
      <td>14</td>
      <td>-2</td>
      <td>-14,3%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>766</td>
      <td>754</td>
      <td>-12</td>
      <td>-1,6%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Längs</td>
      <td>364</td>
      <td>361</td>
      <td>-3</td>
      <td>-0,8%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Schräg</td>
      <td>275</td>
      <td>266</td>
      <td>-9</td>
      <td>-3,4%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Quer</td>
      <td>127</td>
      <td>127</td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <td colspan=4>normiert auf reale Häufigkeit der Ausrichtungskategorie:</td>
      <td>Längs</td>
      <td></td>
      <td></td>
      <td>0,0</td>
      <td>0,0%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Schräg</td>
      <td></td>
      <td></td>
      <td>0,0</td>
      <td>0,0%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Quer</td>
      <td></td>
      <td></td>
      <td>0</td>
      <td>0%</td>
    </tr>
    <tr>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>gesamt</td>
      <td></td>
      <td></td>
      <td></td>
      <td>0,0%</td>
    </tr>
  </tbody>
</table>
</div>