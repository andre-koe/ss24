
## Einleitung

### Was ist KI?

#### Definitionsversuch

- *Künstliche Intelligenz ist die Fähigkeit einer Maschine, menschliche Fähigkeiten wie logisches Denken, Lernen, Planen und Kreativität zu imitieren*
- *KI ermöglicht es technischen Systemen, ihre Umwelt wahrzunehmen, mit dem Wahrgenommenen umzugehen und Probleme zu lösen um ein bestimmtes Ziel zu erreichen. Der Computer empfängt Daten (die bereits über eigene Sensoren, zum beispiel eine Kamera, vorbereitet oder gesammelt wurden), verarbeitet sie und reagiert.*
- *KI-Systeme sind in der Lage, ihr Handeln anzupassen, indem sie die Folgen früherer Aktionen analysieren und autonom arbeiten.*

#### Schematische Darstellung eines KI-Systems

![[Pasted image 20240425172449.png]]

#### Viele Fallstricke bei Definitionsversuchen von KI

![[Pasted image 20240425172546.png]]

#### Gebiete der KI

![[Pasted image 20240425172616.png]]

#### Schwache vs. Starke KI

**Schwache KI**
- Systeme, die spezielle Aufgaben, die Intelligenz erfordern, ebenso gut oder besser als ein Mensch ausführen.
- Beispiele:
	- Schachcomputer
	- Sprachübersetzer
- Alle gegenwärtigen KI-Systeme sind schwache KI-Systeme!

**Starke KI**
- Systeme, die jedes Problem, das Menschen lösen können, ebenfalls auf gleichem oder höherem Niveau lösen können.
- Starke KI-Systeme gibt es bisher nur in Scirence-Fiction bspw. HAL 9000
- Viele noch ungelöste Probleme:
	- Freier Wille
	- Bewusstsein
	- Gefühle
	- Verschiedene Formen von Intelligenz:
		- soziale, emotionale, künstlerische, ...

### Kann man KI messen?

#### Turing Test

Versuchsaufbau:

![[Pasted image 20240425173911.png]]

Menschlicher Fragesteller A versucht durch Fragen herauszufinden, ob B oder C ein Computer oder ein Mensch ist.

B und C versuchen A zu überzeugen, dass sie Menschen sind.

Kommunikation über Tastatur und Bildschirm.

Kann A nach einer gewissen Zeit nicht entscheiden, wer der Computer ist, dann hat B den Test bestanden und es kann B eine KI zugesprochen werden.

Turing-Tests sind im Internet allgegenwärtig:
CAPTCHA-Tests:

(Completly Automated Public Turing test to tell Computers and Humans apart)
![[Pasted image 20240425173847.png]]

#### Winograd Schema Challenge

Alternative zum Turing-Test

Benannt nach Terry Winograd, Informatikprofessor und einer der Begründer der KI

Winograd-Schemas sind kurze Multiple-Choice-Fragen mit mehrdeutigen pronomialen Bezügen, deren Auflösung "wirkliches Verstehen und gesunden Menschenverstand" vorraussetzt.

GPT-3 von Open-AI (ein mit 570 Gigabyte an Text vortrainiertes tiefes Netzwerk) erreichte 2020 bereits eine Trefferquote von knapp 90%

Beispiele:

Der Pokal passt nicht in den braunen Koffer, weil er zu groß ist. 
Was ist zu groß? 
1) der Pokal 
2) der Koffer

Der Pokal passt nicht in den braunen Koffer, weil er zu klein ist. 
Was ist zu klein? 
1) der Pokal 
2) der Koffer

#### Abstraction and Reasoning Corpus (ARC)

Visueller Test, eine Testfrage besteht aus Demos und einer Frage. Der Fokus liegt hierbei auf Abstraktion und Schlussfolgerung.

![[Pasted image 20240425175009.png]]

![[Pasted image 20240425175043.png]]

### Erfolge und Geschichte

#### Geburt der KI: Darthmouth (1956)

Begriff KI (AI) wurde bei dieser Konferenz begründet

Initiatoren der Konferenz:
- John McCarthy (Erfinder LISP)
- Marvin Minsky (Pionier für künstliche neuronale Netze)
- Nathaniel Rochester (IBM 701)
- Claude Shannon (Begründer der Informationstheorie)

Newell und Simon stellen das erste Schlussfolgerungsprogramm Logic Theorist vor, das der Lage war "nichtnumerisch zu denken" und einfache mathematische Theoreme zu beweisen.

Keine großen Durchbrüche. Dafür lernten sich die Personen kennen, die die KI prägen sollten
(vor allem am MIT, an der CMU, in Stanford und bei IBM)

#### Menschliches Gehirn als Vorbild

Ein grober Vergleich der Leistungsfähigkeit eines Computers mit einem menschlichen Gehirn.

![[Pasted image 20240425182843.png]]

Menschliches Gehirn besteht aus ca. 100 Mrd. Neuronen die jeweils über durchschnittlich 1000 Synapsen verbunden sind.

![[Pasted image 20240425182813.png]]

### Die frühen Zeiten der neuronalen Netze

- McCulloch-Pitts-Zelle (1943)
- Hebbsche Lernregel (1949)
- Perzeptron:
	- Rosenblatt (1958)
	- Modell eines einzelnen Neurons
	- Mit einfacher Lernregel
	- Theoretisch untersucht von Minsky und Papert (1969)
- ...
- Mehrschichtige Netze mit Backpropagation als Lernverfahren

![[Pasted image 20240425183429.png]]

### Deep Neural Networks (Durchbruch seit ca. 2010)

Neuronale Netze mit zahlreichen versteckten Schichten
Durchbruch vor allem aufgrund massiv parallel arbeitender Grafikprozessoren, so dass komplexe Netze mit riesigen Datenmengen trainiert werden können.

**Recurrent Neural Networks** (insbesondere **Long short-term memory**) sehr erfolgreich bei Sprachverarbeitung (speech recognition und language processing)

**Convolutional Neural Networks (CNN)** besonders geeignet für Bildverarbeitung

![[Pasted image 20240425184455.png]]

### Transformer-Netze (2017)

Bis 2017 waren bei der Sprachverarbeitung (Sprachübersetzer, Dialogsysteme, ...) rekurrente Netze und LSTM-Netze (Long Short-Time Memory)
vorherrschend.

Natürlichsprachliche Texte werden dabei sequentiell in das Netz eingespeist. Kontextbezüge werden durch ein internes Gedächtnis der Neuronalen Netze modelliert.

2017 wurde von google-Forschern Transformer-Netze mit dem sogenannten Attention-Mechanismus vorgeschlagen. Siehe Paper Attention Is All You Need von Vaswani et al, 2017.

Transformer sind besser geeignet für die Auflösung von Kontextbezügen und lassen sich besser parallelisieren und damit effizienter trainieren.

![[Pasted image 20240425190312.png]]

### Transformer-Netze im Detail

![[Pasted image 20240425190512.png]]

![[Pasted image 20240425190535.png]]

### Training von ChatGPT

**Pre-Training**: Training eines Sprachmodells (wahrscheinlichstes nächstes Wort bei einer Wortfolge)
Datenbasis: 570GB bestehend aus Websites, Büchern, Artikeln, u.a.

**Fine-Tuning**: mit überwachtem Lernen mit vorgegebenen Fragen-Antworten

Weitere Verbesserungen durch Reinforcement-Learning

![[Pasted image 20240425193537.png]]


## Problemlösung durch Suchen

### Formulierung von Suchproblemen

#### Flussüberquerungsproblem

Bauer möchte Ziege, Wolf und Kohl mit Boot auf die andere Seite bringen

Bauer kann maximal ein Objekt transportieren

Wolf frisst Ziege und Ziege frisst Kohl falls Bauer nicht anwesend.

Suche möglichst kurze Folge von Aktionen, um Ziel zu erreichen?

#### Allgemeine Formulierung des Suchproblems (1)

![[Pasted image 20240425194216.png]]

**Zustände (evtl. unendlich viele)**
![[Pasted image 20240425194121.png]]

**Ausgangszustand**
![[Pasted image 20240425194144.png]]

**Zielzustände (evtl. Prüfbedingung)**
![[Pasted image 20240425194238.png]]

**Aktionen mit Zustandsübergängen und ihren kosten**

$\{l,r\}\times\{Z,W,K,-\}$ 
l bzw. r = an das linke bzw. rechte Ufer fahren 
"-" = leere Fracht.
Einheitskosten: jede Aktion hat gleiche Kosten

![[Pasted image 20240425194432.png]]
Bauer fährt mit Ziege ans rechte Ufer.

##### Allgemeine Formulierung des Suchproblems (2)

Alle Zustände mit ihren Übergängen bilden den Zustandsraum (= gerichteter Graph)

Beachte, dass zulässige Aktionen vom Zustand abhängen.

**Suchproblem**:
Suche im Zustandsraum eine Folge von Aktionen, die den Ausgangszustand in einen Zielzustand kostenoptimiert überführt.

![[Pasted image 20240430001112.png]]

### Beispiele

#### Staubsaugerwelt

![[Pasted image 20240430001427.png]]

- Zustandsraum für eine Staubsaugerwelt mit 2 Zellen
- Zelle kann schmutzig oder nicht schmutzig sein
- Es gibt 8 Zustände mit den Aktionen L = links, R = rechts und S = Saugen

#### 15-Puzzle

![[Pasted image 20240430001618.png]]

- $16!/2 \approx$ 10 Billionen viele Zustände, die sich in Zielzustand überführen lassen
- Aktionen: freie Stelle nach links, rechts oben oder unten bewegen
- Kürzeste Lösung braucht maximal 80 Aktionen.

#### Sudoku

![[Pasted image 20240430001901.png]]

- Sudoku-Rätsel mit seiner eindeutigen Lösung
- Als Problem unter Randbedingungen lösen (Constraint Satisfaction Problem, CSP)
- Späteres Kapitel

#### Färbung von Landkarten

![[Pasted image 20240430002019.png]]

- Ordne jedem Land eine Farbe zu:
	- Rot, Gelb, Grün oder Blau
- Benachbarte Länder müssen unterschiedlich gefärbt sein
- Aufgabe: Formuliere als Suchproblem
- Bemerkung:
	- nach dem Vier-Farben-Satz (Appel und Haken, 1976) genügen grundsätzlich 4 Farben.
	- Annahme: keine Exklaven
- Als Problem unter Randbedingungen lösen
	- (Constraint Satisfaction Problem, CSP)
- Späteres Kapitel

#### Hamilton-Tour

![[Pasted image 20240430002535.png]]

- Die Altstadt von Venedig, besteht aus 118 Inseln, die durch ca. 400 Brücken verbunden sind.
- Finde eine Rundtour, so dass alle mit Brücken erreichbaren Inseln genau einmal besucht werden.
- Problem ist NP-vollständig
- Aufgabe: formuliere Problem als Suchproblem

#### Klausuraufgabe:

##### Aufgabe 1 Problemlösen durch Suchen (12 Punkte) 

Ein Gefäß, das 8 Liter fasst, ist bis zum Rand mit Wasser gefüllt. Daneben stehen zwei weitere noch leere Gefäße, die 3 bzw. 5 Liter fassen. 
Mit Hilfe eines Suchverfahrens soll eine möglichst kurze Folge von Umfüllaktionen gefunden werden, so dass sich danach sowohl im 5- als auch im 8-Liter-Gefäß jeweils 4 Liter Wasser befinden?

Die Zustände des Suchraums lassen sich als Triple (x, y, z) beschreiben, wobei x, y bzw. z die Füllmenge des 8-, 5- bzw. 3-Liter-Gefäßes angibt. 

a) Geben Sie den Ausgangszustand S und den Endzustand Z an. (1 Punkt) 

S = (8, 0, 0), Z = (4, 0, 4)

b) Geben Sie den Suchbaum bis zur Tiefe 2 einschließlich an. Berücksichtigen Sie auch redundante Pfade und umranden Sie die redundanten Zustände. Zyklen werden vermieden. (2 Punkte) 


c) Welche Aktionen sind prinzipiell in einem Zustand möglich? (1 Punkt) 
(l,r,x), (r,l,x), (l,m,x), (m,l,x), (r,m,x), (m,r,x) -> x ist Menge Wasser in Behälter

d) Eine Analyse des Problems zeigt, dass es insgesamt 24 zulässige Zustände gibt. Wieviel Elemente wird die ClosedList in der Breitensuche maximal enthalten? Begründen Sie Ihre Antwort. (2 Punkte) 

|ClosedList| <= 24 da die ClosedList keine bereits besuchten Zustände enthält 

e) Warum findet die Breitensuche eine Lösung mit möglichst wenig Umfullaktionen? Warum findet die Tiefensuche zwar eine Lösung aber nicht notwendigerweise eine kürzeste? Hinweis: Skizzieren Sie einen Suchbaum und begründen Sie damit. (3 Punkte) 


f) Die iterativ vertiefende Tiefensuche findet ebenfalls eine kurzeste Lösung. Sie besteht aus 7 Umfullaktionen. Beschreiben Sie mit Hilfe einer Formel (keine O-Notation), wie oft die rekursive Funktion depthFirstSearch höchstens aufgerufen wird. Verwenden Sie die Antwort aus c). (3 Punkte)


### Suche nach Lösungen

#### Beispiel: Kürzeste Routen

![[Pasted image 20240430002914.png]]

- Eine vereinfachte Straßenkarte von Rumänien mit Entfernungsangaben in Meilen.
- Problem: finde eine kürzeste Route von Arad nach Bucharest.
- Zustände = Orte
- Aktion: fahre zum nächsten erreichbaren Ort
- Straßenkarte stellt Zustandsraum dar

#### Suche ergibt einen Suchbaum

- Starte mit Ausgangszustand

![[Pasted image 20240430075315.png]]

- Expandiere Knoten und generiere neue Knoten indem alle möglichen Aktionen angewandt werden
- ...
- Ergibt Suchbaum

![[Pasted image 20240430075506.png]]

##### Zyklen im Suchbaum

- Ein Zyklus ist ein Pfad der zu sich selbst führt
- Ein Vollständiger Suchbaum würde daher unendlich werden.

![[Pasted image 20240430221555.png]]

#### Redundante Pfade im Suchbaum

- Redundante Pfade sind unterschiedliche Pfade, die zum selben Zustand (hier: Oradea) führen
- Der blaue Pfad ist teuerer als roter Pfad und daher überflüssig

![[Pasted image 20240430221742.png]]

#### OpenList und ClosedList

**Closed List (Blau)**:
- Knoten, die bereits expandiert wurden
- Werden auch untersuchte Knoten (explored nodes) genannt

**Open List (Türkis):**
- Knoten, die generiert aber noch nicht expandiert wurden
- Werden auch Grenzknoten (frontier nodes) genannt

![[Pasted image 20240430222423.png]]

#### Suchalgorithmus

```java
Function search(problem) {
	// return Lösung oder null (keine Lösung)
	
	openList = {problem.state()}; // initialisiere openList mit Ausgangszustand aus problem;
	closedList = {} // initialisiere closedList als leer;
	
	while (!openList.isEmpty()) {
	  // wähle Knoten n aus openList und entferne n aus openList;
	  if (Knoten n ist ein Zielzustand) {
		  return lösung;
	  }
	  füge n zu closedList dazu;
	  expandiere n und füge die generierten Knoten, die nicht in 
	  closedList und nicht in openList sind zu openList dazu;
	}
	
	 return null; // Keine Lösung
}
```

#### Suchbaum und Zustandsbaum

- Suchalgorithmus vermeidet Zyklen und redundante Pfade
- Suchbaum ist ein Teil des Zustandsraum

![[Pasted image 20240430223551.png]]

#### Suchalgorithmus - Datenstrukturen

- closedList:
	- Üblich: HashSet
	- add(x) und contains(x) sollten effizient sein.
- openList:
	- Datenstruktur hängt von der Suchstrategie ab.
	- Üblich:
		- Stack
		- Queue
		- PriorityQueue
	- add(x), contains(x) und remove() sollten effizient sein.

#### Suchalgorithmus - Datenstrukturen (2)

- Lösung:
	- Pfad zu einem Zielzustand (inklusive Zielzustand selbst)

#### Suchalgorithmus - Datenstrukturen (3)

Für jeden Knoten n im Suchbaum speichere ab:
- Zeiger auf Elternknoten (als Map oder Feld) - blau
- Evtl. Aktion, um vom Elternknoten Knoten n zu erreichen.
- Kosten um Knoten n zu erreichen - rot
- Evtl. Tiefe im Suchbaum

![[Pasted image 20240430225132.png]]

#### Suchstrategie

Suchstrategie:
- Legt fest, welcher Knoten als nächstes expandiert wird.
- Die verschiedenen Suchverfahren unterscheiden sich im Wesentlichen in der Suchstrategie
- Suchstrategie hat einen wesentlichen Einfluss auf die Leistungsfähigkeit des Suchverfahrens.

#### Leistungsbewertung für Suchalgorithmen

- **Vollständigkeit**:
	- Findet der Algorithmus eine Lösung, falls es eine gibt?
- **Optimalität**:
	- Findet die Suchstrategie die (genauer: eine) optimale Lösung?
- **Zeitkomplexität**: 
	- Wie lange dauert es, bis eine Lösung gefunden wird?
- **Speicherkomplexität**
	- Wie viel Speicher benötigt die Suche?

#### Wichtige Größen für die Leistungsbewertung

- **Verzweigungsfaktor** (branching factor) b:
	- maximale Anzahl der Nachfolger für einen Knoten
- **Tiefe** (depth) d des flachsten Ziels:
	- Tiefe eine flachsten Zielknotens im Suchbaum
- **Maximale Pfadlänge** m:
	- maximale Länge eines beliebigen Pfades im Suchbaum
- Beachte, dass bei einem unendlich großen Suchraum b und d dennoch endlich groß sein können.

### Uninformierte Suche

Bei der uninformierten Suche handelt es sich um eine "blinde Suche", d.h. der Suchalgorithmus hat keine Information, die über die Problemdefinition hinausgeht!

#### Breitensuche und uniforme Kostensuche

##### Breitensuche (Breadth-First Search) für einen einfachen Binärbaum

![[Pasted image 20240430232433.png]]

- Knoten werden in der Reihenfolge expandiert, in der sie generiert werden. (OpenList als FIFO-Liste, Queue)
- Suche ist vollständig, vorausgesetzt Verzweigungsfaktor b ist endlich.
- Suche ist optimal, falls jede Aktion gleiche positive Kosten hat (Einheitskosten)

##### Breitensuche

- openList als FIFO-Liste (Queue) mit effizienten Operationen:
	- add(x)
	- x = remove()
	- contains(x)
- closedList mit effizienten Operationen:
	- add(x)
	- contains(x)
- child wird bereits vor dem Einfügen in die openList auf Zielzustand geprüft. -> Bessere Laufzeit

```java
Function breathFirstSearch(problem) {
  start = Ausgangszustand aus problem;
  if (start ist Zielzustand) {
    return lösung;
  }
  initialisiere openList als FIFO-Liste mit start;
  initialisiere closedList als leer;

  while (!openList.isEmpty()) {
	n = openList.remove();
	closedList.add();
	for (jeden Knoten child, der sich mit einer Aktion aus n erreichen lässt) {
		if (child ist in closedList oder openList) {
			continue;
		}
		if (child ist ein Zielzustand) {
			return Lösung;
		}
		openList.add(child);
	}  
  }
  return null;
}
```


##### Komplexität der Breitensuche

**Zeit-Komplexität**:
- Falls Verzweigungsgrad b und Lösung in Tiefe d ist, dann ist die Gesammtzahl der generierten Knoten:
	$1+b+b²+b³+\dots+b^d=O(b^d)$
- Würde der Algorithmus den Zieltest auf Knoten erst anwenden, wenn sie expandiert werden und nicht wenn sie generiert werden, dann wäre die zeitkomplexität um den Faktor b größer

**Speicher-Komplexität**:
- Jeder expandierte oder generierte Knoten wird gespeichert:
	- Closed-List (expandierte Knoten): $O(b^{d-1})$
	- Open-List (nur generierte Knoten): $O(b^d)$
	
![[Pasted image 20240430235528.png]]

##### Zeit- und Speicheranforderungen für die Breitensuche

![[Pasted image 20240430235627.png]]

#### Uniforme Suche (Uniform Cost Search)

Bei der Uniformen Suche handelt es sich ebenso um eine blinde Suche, d.h. der Suchalgorithmus hat keine Information, die über die Problemdefinition hinausgeht!

- Die Breitensuche ist nicht optimal, falls Aktionen unterschiedliche Kosten haben.
- Dagegen expandiert die uniforme Kostensuche immer den Knoten n mit den geringsten Pfadkosten g(n)
- Realisiere dazu openList als Prioritätsliste, wobei die Prioritätswerte die Pfadkosten sind.
- Damit Optimalität gewährleistet ist, müssen Kosten positiv sein.
- Entspricht dem Dijkstra-Algorithmus.

![[Pasted image 20240501005158.png]]

**Uniforme Kostensuche (Uniform Cost Search)**

![[Pasted image 20240501005258.png]]

![[Pasted image 20240501005324.png]]

![[Pasted image 20240501005337.png]]

![[Pasted image 20240501005351.png]]

![[Pasted image 20240501005408.png]]

![[Pasted image 20240501005420.png]]

##### Algorithmus für Uniforme Kostensuche

- openList als Prioritätsliste.
  Elemente sind über Pfadkosten geordnet
- Effiziente Operationen:
	- add(x, g)
	- x = removeMin()
	- contains(x)
	- change(x,g)
- Zielzustand wird bei Knoten n geprüft, sobald er expandiert werden soll.
- Ist ein erzeugter Knoten child bereits in der openList, so muss geprüft werden, ob sich die Pfadkosten g(child) verbessern:
  change(x, g)

```java
Function uniformCostSearch(problem) {
  start = Ausgangszustand aus problem;
  if (start ist Zielzustand) {
    return Lösung;
  }
  initialisiere openList als Prioritätsliste geordnet nach Pfadkosten;
  openList.add(start);
  initialisiere closedList als leer;

  while (openList nicht leer) {
    n = openList.removeMin();
    if (n ist ein Zielzustand) {
      return lösung;
    }
    closedList.add(n);
    for (jeden Knoten child, der sich mit einer Aktion aus n erreichen lässt) {
	    if (child ist nicht in openList und nicht in closedList) {
	      openList.add(child);
	    } else if (child ist in openList) {
	      überprüfe ob sich Pfadkosten g(child) verbessern lassen;
	    }
    }
  }
  return null;
}
```


#### Tiefensuche und Tiefenbeschränkte Suche

##### Tiefensuche (Depth-First-Search)

![[Pasted image 20240501010614.png]]

![[Pasted image 20240501010631.png]]

![[Pasted image 20240501010651.png]]

![[Pasted image 20240501010709.png]]

![[Pasted image 20240501010720.png]]

![[Pasted image 20240501010735.png]]
##### Eigenschaften der Tiefensuche

**Vollständigkeit**
- Die Tiefensuche ist nur vollständig in einem endlichen Zustandsraum, vorausgesetzt Endlosschleifen in einem Pfad werden abgefangen.
- In einem unendlichen Zustandsraum terminiert die Tiefensuche evtl. nicht und ist daher nicht vollständig.

**Die Tiefensuche ist nicht optimal**

Vorteil ggü. der Breitensuche ist der wesentlich geringere Speicherplatzbedarf:
- Speicherung der generierten Knoten (Stack) und des aktuellen Pfads: O(bm).
  (b = Verzweigungsfaktir (branching factor) und m = Höhe des Suchbaums)

In der Praxis Tiefensuche rekursiv und mit Tiefenbeschränkung. (Tiefenbeschränkte Suche, depth-limited search)

##### Tiefenbeschränkte rekursive Suche (Depth-Limited Search)

- Beschränkung der Rekursionstiefe auf *limit* um Terminierung zu erzwingen.
- Liste *path* speichert aktuellen Pfad und dient zum Prüfen von Zyklen. Prüfung kann den Suchraum erheblich verkleinern.
- Operationen für Liste path:
	- path.add(child)
	  hängt Knoten child an
	- path.removeLast():
	  entfernt letzten Knoten (Backtrack-Schritt)
- Keine ClosedList (Speicherplatzgründe!).
- Rückgabewert von depthFirstSearch:
	- Lösung
	- failure: es gibt keine Lösung!
	- bei gegebenem Rekursionstiefenlimit gibt es keien Lösung (in größerer Tiefe jedoch Lösung möglich)
  
```java
Function depthFirstSearch(problem, limit) {
  s = Ausgangszustand aus Problem;
  return depthFirstSearch(problem, [s], s, limit);
}

Function depthFirstSearch(problem, path, node, limit) {
  if (node ist ein Zielzustand) {
    return path;
  } 
  else if (limit == 0) {
    return cutOff;
  }
  else {
    cutOffOccurred = false;
    for (jede Aktion a auf node) {
      child = wende a auf node an;
      if (child kommt in path vor) {
        continue;
      }
      path.add(child);
      result = depthFirstSearch(problem, path, child, limit - 1);
      if (result ist eine Lösung then return result);
      if (result == cutOff) then cutOffOccurred = true;
      path.removeLast();
    }
    if (cutOffOccurred return cutOff else return failure);
  }
}
```

##### Iterativ vertiefende Suche (iterative deepening depth-first search)

Tiefenbeschränkte Suche terminiert zwar, ist aber nicht vollständig, da lösungstiefe d > Tiefenbeschränkung limit sein kann.

Daher: Führe tiefenbeschränkte Suche durch für schrittweise erhöhte Tiefenbeschränkungen: 1, 2, 3, ...

```java
Function iterativeDeepingSearch(problem) {
  for (depth = 1 to Integer.MAX_VALUE) {
    result = depthFirytSearch(problem, depth);
    if (result != cutoff) {
      result;
    }
  }
}
```

![[Pasted image 20240501101136.png]]

##### Eigenschaften der iterativ vertiefenden Tiefensuche

- Verfahren ist vollständig
- Suche ist optimal, falls jede Aktion gleiche positive Kosten aufweist
- Speicherplatz: $O(bd)$
- Zeitkomplexität: $O(b^d)$
	- Anzahl der generierten Knoten = $1\cdot b^d + 2\cdot b^{d-1} + \dots + d\cdot b¹ = O(b^d)$
	- Zeitkomplexität hat dieselbe Größenordnung wie die Breitensuche.
	- Vergleich mit Breitensuche an einem Beispiel mit b = 10 und d = 5:
		- Breitensuche: 10 + 10² + 10³ +10⁵ = 111,110
		- iterativ vertiefende Suche: $10⁵ + 2\cdot 10^4 + 3\cdot 10³ + 4 \cdot 10^ + 5\cdot 10^1 = 123,450$ 

##### Vergleich uninformierter Suchalgorithmen

![[Pasted image 20240501110848.png]]

#### Informierte (heuristische) Suchmethoden

Nächster Knoten n wird auf Basis einer Evaluierungsfunktion f(n) ausgewählt.

Evaluierungsfunktion f(n) schätzt die Kosten eines Lösungspfads ab, der über Knoten n geht.

Wichtige Komponente von f(n) ist oft eine Heuristik h(n)

h(n) schätzt die Kosten von Knoten n zu einem Zielknoten ab.

Heuristik (altgr. heuriskein = auffinden, entdecken) bezeichnet eine Methode, um möglichst schnell zu einer Lösung zu kommen.

Wichtige Einschränkung für h:
h(n) = 0, falls n Zielknoten ist

![[Pasted image 20240501111838.png]]


##### Algorithmus für Informierte (heuristische) Suche

- openList als Prioritätsliste. Elemente x sind mit Evaluierungsfunktion f(x) geordnet.
- Algorithmus ansonsten wie bei uniformer Kostensuche.

```java
Function heuristicSearch(problem) {
  start = Ausgangszustand aus problem;
  if (start ist ein Zielzustand) {
    return lösung;
  }
  initialisiere openList als Prioritätsliste geordnet mit Evaluierungsfunktion f;
  openList.add(start);
  initialisiere closedList als leer;

  while (openList nicht leer) {
    n = openList.removeMin();
    if (n ist ein Zielzustand) {
      return lösung;
    }
    closedList.add(n);
    for (jeden Knoten child, der sich mit einer Aktion aus n erreichen lässt) {
      if (child ist nicht in openList und nicht in closedList) {
        openList.add(child);
      } else if (child ist in openList) {
        überprüfe ob sich Evaluierungswert f(child) verbessern lässt;
      }
    }
  }
  return null; // keine Lösung
}
```

##### Gierige Breitensuche

- Wähle immer den Knoten, der dem Ziel am nächsten liegt, wähle dazu
	- f(n) = h(n)
- h(n) = geschätzte Kosten von Knoten n zu einem Zielknoten
- Beispiel: Finde kürzeste Route in einer Straßenkarte
  h(n) = Luftliniendistanz von n zum Ziel

![[Pasted image 20240501112837.png]]

##### Beispiel zur gierigen Breitensuche mit Ziel = Bukarest

![[Pasted image 20240501114938.png]]

![[Pasted image 20240501115034.png]]

![[Pasted image 20240501115046.png]]

##### Eigenschaften der gierigen Breitensuche

- Eine gute Heuristik reduziert die benötigte Zeit für die Lösungssuche dramatisch.
- Suche ist nicht optimal (siehe Beispiel eben).
- Suche ist vollständig nur bei einem endlichen Zustandsraum.

##### A* - Suche

Bei der Evaluierungsfunktion f(n) werden die bisherigen Kosten g(n) mitberücksichtigt, um vom Start zu Knoten n zu gelangen.

$f(n) = g(n) + h(n)$

f(n) sind damit die geschätzten Kosten für die billigste Lösung, die durch Knoten n geht.

##### Beipspiel zur A*-Suche mit Ziel = Bukarest

![[Pasted image 20240501120353.png]]

![[Pasted image 20240501120402.png]]

![[Pasted image 20240501120416.png]]

![[Pasted image 20240501120555.png]]

![[Pasted image 20240501120619.png]]

![[Pasted image 20240501120848.png]]

##### Zulässige Heuristik

- Eine Heuristik h heißt zulässig, falls $h(n) \leq h^*(n)$ 
  Dabei sind $h^*(n)$ die tatsächlichen kosten vom Knoten n bis zum Ziel.
- Eine zulässige Heuristik ist damit optimistisch
- Beispiel für zulässige Heuristik:
  Luftliniendistanz.

##### Monotone (konsistente) Heuristik

- Eine Heuristik $h$ heipt monoton, falls
	- $h(n) \leq c(n,n') + h(n')$
  Dabei sind $c(n,n')$ die Kosten um vom Knoten $n$ zu $n'$ zu kommen.

- Beispiel für monotone Heuristik: Luftliniendistanz
- Bei einer monotonen Heuristik sind die Werte von f(n) entlang eines Such-Pfades monoton steigend.
- Eine montone Heuristik ist auch zulässig (warum?)

![[Pasted image 20240501122030.png]]

##### Eigenschaften der A*-Suche

1. Bei einer monotonen Heuristik haben die von A* expandierten Knoten monoton steigende f-Werte.
   
   Damit ist für jeden expandierten Knoten n der gefundene Pfad nach n auch optimal.
   
2. A* ist mit einer monotonen Heuristik auch vollständig, sofern der Verzweigungsfaktor b endlich ist und ein $\varepsilon > 0$ existiert, s.d. alle Aktionskosten $\varepsilon$ überschritten werden.
   
3. Laufzeit- und Speicherbedarf sind weiterhin exponentiell. Jedoch hat die Heuristik einen sehr großen Einfluss auf die Komplexität.

![[Pasted image 20240501125541.png]]

##### Heuristik-Funktionen

- $h(n) = 0$ ist ebenfalls eine monotone heuristik. Knoten werden dann auf Basis von $f(n) = g(n)$ ausgewählt und expandiert (entspricht uniformer Kostensuche)
- Je schäfer die Heuristik ist (d.h. je kleiner $h^*(n)-h(n))$ desto zielgerichteter ist die Suche. Konzentrische Kreise werden schmaler.

##### Heuristik-Funktionen für das 8-Puzzle

![[Pasted image 20240501130130.png]]

- Heuristik $h_1$: Anzahl der falsch platzierten Felder.
  Im Beispiel: $h_1(Start) = 8$
  
- Heuristik $h_2$: Summe der Manhattan-Distanzen der Felder von ihren Zielpositionen.
  Im Beispiel: $h_2(Start) = 3+1+2+2+2+3+3+2 = 18
  
- $h_1$ und $h_2$ sind zulässig und monoton. Warum?

- $h_1(n) \leq h_2(n)$. Warum?

##### Beurteilung von Heuristik-Funktionen

- Ermittle empirisch die Anzahl der generierten Knoten N für verschiedene Startzustände mit einer bestimmten Lösungstiefe d.
  
- Berechne daraus den effektiven Verzweigungsfaktor $b^*$:
  $N = 1 + b^*+(b^*)^2+\dots+(b^*)^d$
  
- Für eine gute Heuristik liegt der Wert nahe bei 1.

##### Suchkosten und effektiver Verzweigungsfaktor für das 8-Puzzle

![[Pasted image 20240501131120.png]]

## Suchstrategien für Spiele

## Constraint Satisfaction Probleme

## Logikbasierte Systeme

## Schließen mit Unsicherheit

## ML Intro

### Lineare Regression
### Overfitting Regularisation Log Regression

### ML Fully Connected NN

### Faltende Neuronen

### Training von CNNs

### Deep Reinforcement Learning