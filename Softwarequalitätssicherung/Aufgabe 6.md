
## User Stories

### Epic: Tunierverwaltung

```txt
Um Turniere verwalten zu können, muss man in ClubPro die Rolle „Spielführer“ haben. (implizit check)

Ein Spielführer ist auch ein Mitglied im Golfclub und kann in ClubPro neue Turniere mit Namen und Datum anlegen. (check)

Für Turniere können sich sowohl Mitglieder des eigenen Clubs als auch Gäste aus anderen Golfclubs anmelden.
Dies ist online über ClubPro möglich. (check)

Wenn sich Gäste in ClubPro für Turniere anmelden, wird ihr Name, ihr Handicap und der Name ihres Heimatclubs gespeichert. (implizit check)

Sowohl Mitglieder als auch Gäste gelten in ClubPro als Personen, die grundsätzlich an Turnieren teilnehmen können. (check)

Eine Online-Abmeldung von Turnieren ist in ClubPro nur für Mitglieder möglich. Gäste müssen sich telefonisch im Golfclub melden und den Spielführer um eine Abmeldung bitten. (check, für externe irrelevant da nicht Teil der Anwendung)

Golfturniere laufen in der Regel so ab, dass Gruppen von jeweils 2 bis 4 Teilnehmern im Abstand von 10 Minuten auf Bahn 1 starten.
Es werden so viele Gruppen gebildet, dass alle Teilnehmer des Turniers in irgendeiner Gruppe untergekommen sind
Die Gruppen heißen in der Golfsprache „Flights“. 
In ClubPro legt der Spielführer die Flights eines Turnieres mit den jeweiligen Startzeiten und den zugeordneten Teilnehmern fest. (check)

Immer dann, wenn alle Flights eines Turniers festgelegt sind, informiert ClubPro automatisch alle Teilnehmer per E-Mail darüber, mit welchen anderen Teilnehmern Sie in einem Flight spielen und zu welcher Uhrzeit sie auf Bahn 1 starten. (check)

Am Ende eines Turniers muss der Spielführer für jeden Teilnehmer eingeben, wie viele Schläge er auf jeder Bahn benötigt hat. Wenn ein Turnier bspw. über 18 Bahnen ausgetragen wird, dann muss der Spielführer in ClubPro pro Teilnehmer und pro Bahn die benötigte Anzahl an Schlägen speichern.
Das bedeutet, dass bei einem 18-Loch-Turnier genau 18 Datensätze pro Teilnehmer gespeichert werden.(check)

Wenn der Spielführer für alle Teilnehmer alle benötigten Schläge eingetragen hat, kann er in ClubPro das Turnier auswerten.
Hierbei berechnet ClubPro für jeden Teilnehmer die Summe aller Schläge und leitet daraus die Platzierung im Turnier ab.
Dabei gilt: Je weniger Schläge ein Teilnehmer benötigt, desto höher ist seine Platzierung. 
Es gewinnt der Teilnehmer mit den wenigsten Schlägen. (check)

Immer dann, wenn ClubPro die Platzierungen berechnet hat, informiert das System die Teilnehmer automatisch per E-Mail über ihre Platzierung. (check)

Manchmal kommt es vor, dass der Spielführer ein Turnier stornieren muss, beispielsweise wenn ein Unwetter aufzieht. 
ClubPro bietet hierfür eine entsprechende Funktion. (Check)

ClubPro kann ein Turnier auch automatisch stornieren, wenn der Anmeldezeitraum abgelaufen ist und sich nicht genügend Teilnehmer angemeldet haben.
```
---

Technologiestack:
- NestJS (Backend)
- Vite (Frontend)
- MongoDB (Datenbank)

Es wird bei der Schätzung davon Ausgegangen, dass das Grundgerüst der Anwendung bereits existiert.

Aufwand fürs Testen wurde in der Schätzung außen vor gelassen.

---
#### User Story: 1

##### Titel: Tunierverwaltung

**Als** Mitglied 

**Will ich** in der Lage sein Tuniere zu Verwalten, d.h. diese mit Datum und eigenem Namen anzulegen und ggf. zu stornieren.

**Damit ich** für kompetitive und unterhaltsame Momente unter den Mitgliedern sorgen kann

##### Akzeptanzkriterien

- **Tunierverwaltung:**
	- Tuniere werden innerhalb von Club Pro als unabhängige Entitäten verwaltet.
		- Tuniere haben einen Namen und ein Startdatum.
	- Tuniere können von Spielführern angelegt, verwaltet und storniert werden.
- **Rollen**:
	- Rolle *Spielführer* mit entsprechenden Berechtigungen hinzugefügt

##### Schätzung: 3 Tage

---

#### User Story: 2

##### Titel: Tunieranmeldung

**Als** ein Mitglied  

**Will ich** mich über die Anwendung zu Tunieren Anmelden können.

**Damit ich** in einem kompetitiven Umfeld meine Fähigkeiten unter Beweis stellen kann.

##### Akzeptanzkriterien

- **Tunieranmeldung**
	- Tuniere sind sichtbar und den Mitgliedern zugänglich
	- Die Tunieranmeldung zu einem ausgewählten Tunier funktioniert über einen Button schnell und unkompliziert.
- Tuniere besitzen Referenzen auf teilnehmende Spieler
##### Schätzung: 2 Tage

---

#### User Story: 3

##### Titel: Tunierabmeldung

**Als** ein spontanes Mitglied  

**Will ich** mich möglichst unkompliziert über die Anwendung von Tunieren abmelden können.

**Damit ich** stets spontan bin falls mal was dazwischen kommt

##### Akzeptanzkriterien

- **Tunierabmeldung**
	- Tuniere sind sichtbar und den Mitgliedern zugänglich
	- Die Tunierabmeldung zu einem ausgewählten Tunier funktioniert über einen Button schnell und unkompliziert.
		- Der Button wird nur für Tuniere angezeigt für die das Mitglied angemeldet ist.
- Tuniere besitzen Referenzen auf teilnehmende Spieler
##### Schätzung: 1 Tage

---

#### User Story: 4

##### Titel: Tunieranmeldung (extern)

**Als** Gast mit Freunden im Golfclub  

**Will ich** mich auch zu Tunieren des Clubs anmelden können.

**Damit ich** mich mit meinen Freunden im Club messen kann

##### Akzeptanzkriterien

- Tunieranmeldung
	- Tuniere sind sichtbar öffentlich zugänglich
	- Die Tunieranmeldung für nicht in der Anwendung angemeldete Spieler erfolgt mit folgenden Daten:
		- Name
		- Handicap
		- Golfclub
- Tuniere besitzen Referenzen auf teilnehmende Spieler
##### Schätzung: 1 Tage

---
#### User Story: 5

##### Titel: Tunierabmeldung

**Als** ein spontanes Mitglied  

**Will ich** mich möglichst unkompliziert über die Anwendung von Tunieren abmelden können.

**Damit ich** stets spontan bin falls mal was dazwischen kommt

##### Akzeptanzkriterien

- **Tunierabmeldung**
	- Tuniere sind sichtbar und den Mitgliedern zugänglich
	- Die Tunierabmeldung zu einem ausgewählten Tunier funktioniert über einen Button schnell und unkompliziert.
		- Der Button wird nur für Tuniere angezeigt für die das Mitglied angemeldet ist.
- Tuniere besitzen Referenzen auf teilnehmende Spieler
##### Schätzung: 3 Tage

---

#### User Story: 6

##### Titel: Spieler - bzw. Flight-Verwaltung im Rahmen eines Tuniers

**Als** Spielführer 

**Will ich** im Rahmen der Tunierverwaltung die angemeldeten Spieler in Flights gruppieren sowie deren Startzeiten konfigurieren.

**Damit ich** einen fairen und reibungslosen Tunierablauf gewähren kann.
##### Akzeptanzkriterien

- **Gruppieren**
	- Innerhalb eines Tuniers werden Spieler in Flights organisiert.
	- Flights werden innerhalb eines Tuniers als eigenständige Entität bestehend aus 2-4 Spielern behandelt.
	- Flights haben Startzeiten und ihnen zugeordnete Spieler.
##### Schätzung: 1 Tage

---

#### User Story: 7

##### Titel: Spielerbenachrichtigung über Flightzuteilung

**Als** Spielführer 

**Will ich** das Spieler des Tuniers, nach Abschluss der Spielerzuweisungen über diese Benachrichtigt werden.

**Damit ich** einen reibungslosen Tunierablauf gewähren kann.
##### Akzeptanzkriterien

- Benachrichtigung
	- Sobald die Zuweisungen des Spielführers abgeschlossen sind (Bestätigung durch Klick auf einen Button) sollen sämtliche zu diesem Zeitpunkt angemeldeten Spieler darüber und ihre Zuordnung sowie Startzeit benachrichtigt werden.
##### Schätzung: 1 Tage

---

#### User Story: 8

##### Titel: Eingabe und Auswertung der Tunierergebnisse und Resultate

**Als** Spielführer 

**Will ich** die jeweiligen Leistungen Spieler im Tunier, in einer Maske eingeben können. Die Auswertung dieser Ergebnisse sowie die Platzierung im Tunier soll dann automatisch erfolgen. Darüberhinaus soll nach Abschluss der Auswertung jeder Spieler über seine Erreichte Platzierung per Mail informiert werden.

**Damit ich** die Platzierung anhand der Tunierergebnisse stets korrekt berechnet wird und alle Spieler Feedback erhalten.
##### Akzeptanzkriterien

- Eingabemaske für Tunierergebnisse:
	- Für jede im Tunier bespielte Bahn ist es möglich die Leistung (#Schläge) der jeweiligen am Tunier teilnehmenden Spieler einzutragen.
- Automatische Auswertung:
	- Sind die werte jedes am Tunier teilnehmenden Spielers eingetragen soll nach den klassischen Golfregeln, vollautomatisch die Platzierung eines jeden Spielers ermittelt werden. Im Anschluss an die Auswertung sollen die Spieler per Mail, über ihre erreichte Platzierung, an die von ihnen hinterlegte Adresse benachrichtigt werden.
- Benachrichtigung
	- Basierend auf Templates, erfolgt direkt im Anschluss an die automatische Auswertung.
##### Schätzung: 3 Tage

---

#### User Story: 9

##### Titel: Automatische Tunierabsage durch die Anwendung

**Als** viel beschäftigter Spielführer 

**Will ich** das Tuniere deren Mindestspieleranzahl bis zu einem gewissen Datum vor dem Tunierstart, zu gering sind, vom System automatisch storniert werden.

**Damit ich** enttäuschung unter den Spielern vermeide falls das Tunier vor Ort doch nicht stattfinden kann.
##### Akzeptanzkriterien

- Datentypen für Tuniere: Mindestspieleranzahl, (Vorlaufdatum?)
- Tuniere deren Mindestspieleranzahl bis zu einem vorher festgelegten Datum (sinnvolle Constraints) unterschritten werden, sollen von der Anwendung automatisch storniert werden.
- Die angemeldeten Teilnehmer sollen über die Stornierung frühzeitig informiert werden.
##### Schätzung: 2 Tage

---
---


## Erster Ansatz

#### User Story: 1

##### Titel: Team Anmeldung

**Als** ein kompetitiver Tunierspieler 

**Will ich** in der Lage sein mit meinen Kollegen in einem Team an tunierübergreifend an Tunieren teilzunehmen.

**Damit ich** und meine Kollegen uns gemeinsam verbessern könnern

##### Akzeptanzkriterien

- **Teamverwaltung:**
	- Teams werden innerhalb von Club Pro als unabhängige Entitäten verwaltet.
		- Teams haben einen Namen, ein Logo, eine Historie und die Durchschnittswerte der Spieler
	- Teams können von Spielern erstellt werden
	- Spieler können sich für Teams bewerben
	- Teams können sich geschlossen zu Tunieren anmelden

##### Schätzung: 7 Tage

---
#### User Story: 2

##### Titel: Benachrichtigung über neues Tunier

**Als** ein Spielführer

**Will ich**, dass Spieler innerhalb unseres Clubs über die von mir erstellten Tuniere benachrichtigt werden.

**Damit mein** Tunier auch frühzeitig genügend Aufmerksamkeit bekommt

##### Akzeptanzkriterien

- Beim Erstellen eines neuen Tuniers soll allen Mitgliedern, die nicht das Opt-Out aktviert haben eine automatische Benachrichtigung innerhalb der Anwendung 
- Opt-Out für Mitglieder um keine automatischen Benachrichtigungen zu erhalten

##### Schätzung: 2 Tage

---

#### User Story: 3

##### Titel: Tunierübersicht

**Als** neues Mitglied und Golfeinsteiger 

**Will ich** in der Lage sein Tuniere bequem in der Tunierübersicht nach Schwierigkeit zu sortieren

**Damit** ich mich bequem zu Tuniere auf meinem Niveau anmelden kann.

##### Akzeptanzkriterien:

- Das Tunierübersichtsdashboard sollte eine Übersicht anstehender Tuniere in Form einer Liste anzeigen.
	- Diese Liste sollte nach Merkmalen eines Tuniers sortierbar sein

---
#### User Story: 4

##### Titel: Tracking von Tunieren

**Als** Profispieler und Spielführer der viele Tuniere erstellt und an vielen Tunieren teilnimmt

**Will ich** jederzeit eine klare Übersicht über meine erstellten Tuniere und meine angemeldeten Tuniere haben.

**Damit ich** auch kein Tunier verpasse und meine Tuniere effektiv verwalten kann.

##### Akzeptanzkriterien:

- Auf der Tunierübersichtsseite existieren zwei neue Reiter bzw. Tabs (Angemeldet) und (Meine Tuniere) die jeweils Tuniere anzeigen zu denen der Spieler angemeldet ist bzw. die der Spieler erstellt hat.

---

#### User Story: 5

##### Titel: Anzahl und Maximale Anzahl an Spielern anzeigen

**Als** Tunierspieler der gerne viel Action hat

**Will ich** in der Lage sein genau zu sehen wie viele Spieler sich bereits zu einem Tunier angemeldet haben und wie viele sich maximal Anmelden können.

**Damit ich** nicht zu irgendwelchen halbleeren Tunieren auftauche

##### Akzeptanzkriterien:

- Jedes Tunier hat als Eigenschaft die Anzahl angemeldeter Spieler
- Jedes Tunier hat eine Maximale Anzahl an Teilnehmern die bei der Erstellung vom Spielführer 


