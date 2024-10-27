
## Einführung un Motivation

## Quellkodierung

## Kanalkodierung

### 3.1 Prinzip der Kanalkodierung
#### 3.1.1 Ein erstes Beispiel

##### Beispiel Fehlererkennung: IBAN

**IBAN**: DE 32 69050001 0123456789

**Aufbau**:
- Ländercode (CC, 2 Zeichen) -> DE
- Prüfziffer (CS, 2 Zeichen) -> 32
- Bankleitzahl (BLZ, 8 Zeichen) -> 69050001
- Kontonummer (KTN, 10 Zeichen) -> 0123456789

**Validierung** (mittels MOD97 Algorithmus)
1. Umgruppieren (BLZ + KTN + CC + CS): 690500010123456789DE32
2. Ländercode in Zahlen (A=10, B=11, ...): 690500010123456789**1314**32
3. Checksumme (Zahl mod 97): 1
4. Korrekt, wenn Checksumme=1

**Generierung**: Algorithmus wie oben mit Chesumme 00
1. Berechne: BLZ + KTN + CC + "00"
2. Konvertiere Ländercode und wende die Modulo-97-Operation an
3. Subtrahiere das Ergebnis von 98 -> liefert Checksumme

**Restfehler**:
Die Fehlererkennung mittels MOD97-Algorithmus ist sehr effektiv. Der Restfehler, also die Wahrscheinlichkeit, dass eine fehlerhafte IBAN als korrekt erkannt wird, ist sehr gering:

- kein Fehler bei einer falschen Stelle
- ca 1% bei mehr als einer falschen Stelle

##### Beispiel Kanalkodierung: Prüfmatrix

**Codewort**:
$$
\underbrace{x_1\quad x_2 \quad x_3 \quad x_4}_{X}\quad\underbrace{y_5\quad y_6\quad y_7}_Y
$$
**Codierungsvorschrift**: 
$$Y = \Gamma[X]  \left\{\begin{array}{l}
y_5 = x_1 \oplus x_2 \oplus x_3 \\
y_6 = x_1 \oplus x_2 \oplus x_4 \\
y_7 = x_1 \oplus x_3 \oplus x_4
\end{array}\right.$$ **Matrixdarstellung**:

| $x_1$ | $x_2$ | $x_3$ | $x_4$ |     | $y_5$ | $y_6$ | $y_7$ |
| :---: | :---: | :---: | :---: | :-: | :---: | :---: | :---: |
|   1   |   1   |   1   |   0   |     |   1   |   0   |   0   |
|   1   |   1   |   0   |   1   |     |   0   |   1   |   0   |
|   1   |   0   |   1   |   1   |     |   0   |   0   |   1   |

**Gesendetes Codewort ($Y^*$):** $1\quad 0 \quad 1 \quad 1$ -> ($\Gamma$) $0\quad 0\quad 1$ 

(Störung der Übertragungsschritte sorgt für fehlerhaft empfangenes Codewort **$Y'$**)

**Empfangenes Codewort (Y')**: $1\quad 0 \quad 1 \quad 0$ -> ($\Gamma$) $0\quad 1 \quad 0$

**Fehlerkorrektur** durch stellenweise Addition von $Y^*$ und $Y'$ 

Fehlersyndrom
$$\overbrace{\left(\begin{array}{l}0\\0\\1\end{array}\right)}^{Y^*}\oplus 
\overbrace{\left(\begin{array}{l}0\\1\\0\end{array}\right)}^{Y}=\left(\begin{array}{l}0\\1\\1\end{array}\right)$$
-> Spalte 4, 4. Stelle gestört!
#### 3.1.2 Fehlererkennung und Fehlerkorrektur

##### Prinzip der Kanalcodierung
![[Pasted image 20240424220855.png]]

$X$: Quellcodewort (bestehend aus Nutzinformation)
$\Gamma()$: Vorschrift zur Berechnung der nützlichen Redundanz
$Y$: nützliche Redundanz (in Form von Prüfbits oder Kontrollstellen)
$X,Y$: gesendetes Codewort
$X^*,Y^*$: empfangenes, evtl. störungbehaftetes Codewort
$Y'$: vom Empfänger neu berechnete, nützliche Redundanz

##### Kanalcodierung

Unter Kanalcodierung versteht man das hinzufügen von zusätzlichen Bits (**nützlicher Redundanz**) zu einem **Nutzwort**, um eventuell auftretende **Bitfehler erkennen oder korrigieren** zu können.

Das Nutzwort inklusive der zusätzlichen Bits wird als **Codewort** bezeichnet.

Notation:
- K: Länge eines Nutzwortes, Anzahl der Nutzbits
- N: Länge eines Codeworts
- N-K: Anzahl der zusätzlichen Bits (bei systematischen Codes: Prüfbits)
- K/N: Coderate

##### Anwendungsgebiete

**Datenübertragung:**
- Datensicherungsprotokolle in Rechnernetzen
	- fast alle Datenübertragungen in Rechnernetzen werden mit Prüfsummen (engl. Checksum) abgesichert, um das Weiterleiten von fehlerhaften Daten zu vermeiden
		- DSL, CAN-Bus, Ethernet, Bluetooth, Mobilfunk, TCP, IP, UDP, etc.
- Fehlerreduzierung durch **Forward Error Correction (FEC)** bei Funkübertragungen
	- bei der drahtlosen Übertragung treten häufig Fehler auf
	- eine sehr niedrige Bitfehlerwahrscheinlichkeit kann nur auf Kosten von Datenrate und Reichweite erzielt werden
	- stattdessen werden relativ hohe Bitfehlerwahrscheinlichkeiten durch effiziente Kanalcodierungsverfahren akzeptabel.
- Datenspeicherung:
	- **Fehlerreduzierung** in Massenspeichern (Band, Platte, CD, DVD, Flash) und hochintegrierter Halbleiter-Speicher (RAM, ROM)

##### Codes zur Fehlererkennung und Fehlerkorrektur

**Fehlererkennung:**
- Empfänger erkennt Übertragungsfehler typischerweise durch 
	- einfache Paritätsprüfung
	- Zyklische Redundanz Prüfung (**Cyclic Redundancy Check, CRC**)
- Fehlerkorrektur (Foward Error Correction, FEC):
	- Empfänger korrigiert Übertragungsfehler typischerweise durch
		- Block-Codes
			- Hamming-Code, Golay-Code, Reed-Muller-Code
			- Reed-Solomon Codes (z.B. DVB, CD)
			- Low Density Parity Check-Codes, LDPC (DVB-S2, IEEE 802.11n)
			- Repetition Coding, mehrfaches Übertragen von Bits (Mobilfunk)
		- basierend auf Faltungscodes (Convolutional Codes)
			- einfache Faltungscodes (Mobilfunk, IEEE 802.11)
			- iterative Faltungscodes, Turbo Codes (Mobilfunk)

##### Betriebsarten

**"Reine" Wiederholungsaufforderung**
- nach der Erkennung eines Fehlers wird eine Übertragungswiederholung angefordert
- geringe Restfehlerwahrscheinlichkeit
	- Trade-Off zwischen Code-Overheads und Restfehlerwahrscheinlichkeit
- aufwändigere Übertragungsprotokolle und zusätzlicher Delay
- Einsatz in Systemen mit geringer Bitfehlerwahrscheinlichkeit
	- Bus-Systeme (CAN, Ethernet, etc.)

**Mischbetrieb (Fehlerkorrektur und Wiederholungsaufforderung)**
- zweistufiges Verfahren: Fehlererkennung findet nach der Fehlerkorrektur statt
	- Wiederholungsaufforderung (Acknowledged Mode)
	- Verwerfen/Akzeptanz des fehlerhaften Pakets (Unacknowledged Mode)
- Einsatz in Systemen mit signifikanter Bitfehlerwahrscheinlichkeit
	- Funkübertragung, DSL

**Unüblich: automatische Fehlerkorrektur**
- gewisse Restfehlerwahrscheinlichkeit muss akzeptabel sein
- möglich z.B. bei Übertragung von analogen Signalen (Sprache), wenn kleinere Verfälschungen akzeptabel sind.

##### Beispiel Funkübertragung (Mischbetrieb)

![[Pasted image 20240424225219.png]]

##### Wiederholungsaufforderung: Send-And-Wait

**Send-and-Wait Protokoll**:
- Sender überträgt ein Paket und wartet auf eine Bestätigung
- nach korrektem Empfang eines Datenpakets sendet der Empfänger eine Bestätigung (Acknowledgement, ACK)
- nach Erhalt der Bestätigung überträgt der Sender das nächste Datenpaket
- falls nach einiger Zeit keine Bestätigung eintrifft (Timeout), wiederholt der Sender die Übertragung des Datenpakets

![[Pasted image 20240424225702.png]]
#### 3.1.3 Grundlagen

##### Beispiel: Einfache Paritätskontrolle

**Codierung**:

Hinzufügen eines Paritätsbits
- "0": gerade Anzahl von "1"en
- "1": ungerade Anzahl von 1"en

Codierung für Nachricht mit 2 Bits:

| $x_1$ | $x_2$ | $y_1$ |
| :---: | :---: | :---: |
|   0   |   0   |   0   |
|   0   |   1   |   1   |
|   1   |   0   |   1   |
|   1   |   1   |   0   |
![[Pasted image 20240424230153.png]]

**Welche Fehler können erkannt werden? Welche Fehler können korrigiert werden?**

##### Code und Korrekturbereich

**Code**: Ein Code ist definiert als die Menge aller benutzten Codeworte
- benutztes Codewort: $y=\Gamma(x)$
- Code: $C = \{y\ |\ \exists x:\ y = \Gamma(x)\}$ 

**Korrekturbereich** eines benutzten Codeworts:
- Menge der unbenutzten Codeworte, deren Distanz zu diesem benutzten Codewort am kleinsten ist
- Codeworte innerhalb eines Korrekturbereichs können einem benutzen Codewort zugeordnet werden
- **Korrekturkugel:** symmetrischer Korrekturbereich
- **dichtgepackter Code:** es existieren keine Codewörter außerhalb der Korrekturbereiche

##### Hamming-Distanz

**Hamming-Distanz** $h(x,y)$ von zwei Codeworten $x,y$:
- Anzahl der verschiedenen Bits

**Minimale Hamming-Distanz** $h_C$ eines Codes $C:$
- kleinste Distanz zwischen zwei benutzten Codeworten
$$h_c =\min_{x,y\ \in\ C} h(x,y)$$
Anzahl sicher **erkennbarer Fehler**:
$$\overline\eta_C = h_C -1$$
Anzahl sicher **korrigierbarer Fehler**:
$$\eta_C = \left\lfloor\frac{h_C-1}{2}\right\rfloor$$

##### Beispiel Hamming-Distanz

Was ist die minimale Hamming-Distanz dieser drei Codeworte?
$01010$, $10011$, $00111$

$01010$ <-> $10011$ => h = 3
$01010$ <-> $00111$ => h = 3
$00111$ <-> $10011$ => h = 2

Was ist die maximale minimale Hamming-Distanz bei drei Codeworten mit 5 Bits?

$00000$ <-> $00111$ => h = 3
$00000$ <-> $11001$ => h = 3
$11001$ <-> $00111$ => h = 4

=> Maximale minimale Hamming-Distanz $h_C$ = 3
=> Bei drei Codeworten mit 5 Bits können maximal 2 Bitfehler erkannt und ein Bitfehler sicher korrigiert werden

Rechnung:
- $h_C = 3$
- $\eta_C = \left\lfloor\frac{h_C-1}{2}\right\rfloor =  \left\lfloor\frac{2}{2}\right\rfloor = 1$
- $\overline{\eta}_C = h_C - 1 = 3 - 1 = 2$  

##### Beispiel Repetition-Coding

Repetition-Coding (Codierung durch Bitwiederholung):

- übertrage ein Bit nicht 1-mal sondern n-mal

**Beispiel: n=2**

![[Pasted image 20240425144638.png]]

Hamming-Distanz: 2
Anzahl erkennbarer Fehler: 1
Anzahl korrigierbarer Fehler: 0

**Beispiel: n=3**

![[Pasted image 20240425145319.png]]

Hamming-Distanz: 3
Anzahl erkennbarer Fehler: 2
Anzahl korrigierbarer Fehler: 1

**Allgemein**:
Hamming-Distanz: n
Anzahl erkennbarer Fehler: n-1
Anzahl korrigierbarer Fehler: $\left\lfloor(n-1)/2\right\rfloor$

##### Beispiel: Korrekturbereiche und Hamming-Distanz

**Codewort:**
$$\underbrace{x_1\quad x_2 \quad x_3 \quad x_4}_{X}\quad \underbrace{y_5\quad y_6\quad y_7}_{Y}$$

**Codierungsvorschrift:**
$$Y=\Gamma[X] \left\{\begin{array}{l}
y_5 = x_1 \oplus x_2 \oplus x_3\\
y_6 = x_1 \oplus x_2 \oplus x_4\\
y_7 = x_1 \oplus x_3 \oplus x_4\\
\end{array}\right.$$
**Matrixdarstellung**

| $x_1$ | $x_2$ | $x_3$ | $x_4$ |     | $y_5$ | $y_6$ | $y_7$ |
| :---: | :---: | :---: | :---: | :-: | :---: | :---: | :---: |
|   1   |   1   |   1   |   0   |     |   1   |   0   |   0   |
|   1   |   1   |   0   |   1   |     |   0   |   1   |   0   |
|   1   |   0   |   1   |   1   |     |   0   |   0   |   1   |

**Code:**
- Anzahl Nutz-Bits: $K = 4$; Anzahl benutzter Codeworte: $2^K = 16$
- Codewortlänge: $N=7$; Anzahl Codeworte: $2^N = 128$
- Anzahl korrigierbarer Fehler: $\eta = 1$

**Größe des Korrekturbereich eines benutzten Codeworts:**
- Der Korrekturbereich umfasst alle Codeworte, sie sich um höchstens $\eta = 1$ Bit von einem benutzten Codewort unterscheiden. Es gibt $N = 7$ benachbarte Codeworte, die sich um ein bit unterscheiden. Das benutzte Codeworte zählt auch zum Korrekturbereich.
	- Anzahl Codeworte pro Korrekturbereich: 1 + 7 = 8
	- Anzahl Codeworte in allen Korrekturbereichen: $16\cdot (1+7) = 128$
- Es handelt sich um dichtgepackten Code, da alle Codeworte in einem Korrekturbereich liegen
	- zwei Fehler werden immer erkannt und immer falsch korrigiert
	- drei Fehler können nicht sicher erkannt werden
- Hamming Distanz: 3
	- 1 Fehler korrigierbar, 2 Fehler erkennbar
### 3.2 Blockcodes
#### Übersicht Blockcodes

![[Pasted image 20240427090300.png]]

##### Blockcode
Ein Blockcode ist ein Kanalkodierungsverfahren, bei dem aus einem Nutzwort mit einer festen Länge von *K* Bits (einem Block) ein Codewort mit *N* Bits berechnet wird.

Ein *(N,K)-Code* funktioniert genau für diese eine feste Kombination aus *N* und *K* und weißt dann bestimmte Eigenschaften hinsichtlich Fehlererkennung und Fehlerkorrektur auf.

##### Faltungscodes
Sind eine andere große Gruppe von codes, sind flexibler und der Code (die Hardware) arbeitet unabhängig von der Anzahl der Nutzbits. Faltungscodes werden daher nur über ihre *Coderate* **K/N** beschrieben. In der Praxis werden aber innerhalb einer Übertragungstechnologieauch Faltungscodes meist für wenige feste Blockgrößen eingesetzt

#### Binäre Block-Codes

**Encoder** für (N,K)-Block-Code *C* = $\{\overline{x}_0, \overline{x}_1,\cdots,\overline{x}_{2^K-1}\}$

![[Pasted image 20240427091018.png]]

**Systematischer** (N,K) Block-Code C
- K Info-Bits $\overline{u}$ erscheinen im Codewort $\overline{x}$
	- einfache 

#### 3.2.1 Linear-systematische Blockcodes

##### Codierungsvorschrift für lineare Codes: Generator Matrix

- Codeworte werden aus Nutzworten durch Multiplikation mit einer Generator-Matrix G erzeugt
  
  In Matrixschreibweise $\overline{x} = \overline{u}\cdot G$
$$(x_0, x_1, \cdots, x_{N-1}) = (u_0, u_1, \cdots, u_{K-1}) \cdot \begin{pmatrix} g_{0,0} & \cdots & g_{0,N-1} \\ \vdots & \ddots & \vdots \\ g_{K-1,0} & \cdots & g_{K-1,N-1} \end{pmatrix}$$

- Linear-systematischer Code:
	- Die Generator-Matrix G hat die Form $G = [P\quad I_K]$, wobei $I_K$ die $K\times K$ Einheitsmatrix ist
	- Dadurch stehen die Nutzbits an den letzten K stellen des Codeworts
- **WICHTIG**:
	- alle Berechnungen werden "modulo 2" gerechnet
	- bei Additionen gibt es KEINEN Übertrag:
	  $1101+1010=0111$

##### Beispiel: (7,4) Hamming Code

Code ist durch die Generator Matrix G beschrieben

$$G = \begin{pmatrix}
1&1&0&1&0&0&0\\
0&1&1&0&1&0&0\\
1&1&1&0&0&1&0\\
1&0&1&0&0&0&1
\end{pmatrix}$$

Codierung des Nutzwortes $\overline{u} = (0\quad 1\quad 1\quad 0)$
$$\overline{x} = (0\quad 1\quad 1\quad 0) \cdot \begin{pmatrix}
1&1&0&1&0&0&0\\
0&1&1&0&1&0&0\\
1&1&1&0&0&1&0\\
1&0&1&0&0&0&1
\end{pmatrix} = (1\quad 0\quad 0\quad 0\quad 1\quad 1\quad 0)$$
$$\begin{align}
x_0 &= u_0 + u_2 + u_3\\
x_1 &= u_0 + u_1 + u_2\\
x_2 &= u_1 + u_2 + u_3\\
x_3 &= u_0\\
x_4 &= u_1\\
x_5 &= u_2\\
x_6 &= u_3
\end{align}$$

##### Parity-Check-Matrix

Jeder lineare (N,K) Code hat eine (N,K) x N Parity-Check-Matrix *H* mit

$$(x_o, x_1,\cdots x_{N-1})\cdot H^T=(0,\cdots,0)$$
da $\overline{x}\cdot H^T = \overline{0}$

Ergibt also ein empfangenes Codewort bei Multiplikation mit $H^T$ nicht 0, dann muss ein Bitfehler vorliegen.

Bei linear-systematischen Codes lässt sich die Parity-Check-Matrix direkt aus der Generator-Matrix konstruieren:
$$G = [P\quad I_K]\Rightarrow H=[I_{N-K}\quad P^T]$$

Beispiel: **Hamming-Code**

$$G=\begin{pmatrix}
1&1&0&1&0&0&0\\
0&1&1&0&1&0&0\\
1&1&1&0&0&1&0\\
1&0&1&0&0&0&1
\end{pmatrix} \Rightarrow H = \begin{pmatrix}
1&0&0&1&0&1&1\\
0&1&0&1&1&1&0\\
0&0&1&0&1&1&1
\end{pmatrix}$$

##### Fehlererkennung und Fehlerkorrektur

Beispiel:
- Nutzwort: $\overline{u} = (0\quad 1 \quad 1\quad 0)$
- Codewort: $\overline{x} = (1\quad 0\quad 0\quad 0\quad 1\quad 1 \quad 0)$
- Fehlervektor: $\overline{e} = (0\quad 1\quad 0\quad 0\quad 0 \quad 0 \quad 0)$
- empfangenes Codewort: $\overline{y} = \overline{x} + \overline{e} = (1 \quad 1\quad 0\quad 0 \quad 1\quad 1\quad 0)$
	- 2. Bit durch Übertragung gekippt
- Fehlersyndrom: $$\overline{s} = \overline{y}\cdot H^T = (1\quad 1\quad 0\quad 0\quad 1\quad 1\quad 0)\cdot \begin{pmatrix}1&0&0\\0&1&0\\0&0&1\\1&1&0\\0&1&1\\1&1&1\\1&0&1\end{pmatrix} = (0\quad 1\quad 0)$$
	- Fehlersyndrom $\overline{s}$ ist identisch mit verfälschter Spalte der Parity-Check-Matrix

##### Mathematischer Background

Fehlersyndrom:
$$\overline{s} = \overline{y}\cdot H^T = (\overline{x} + \overline{e}) \cdot H^T = \overline{x}\cdot H^T + \overline{e} \cdot H^T = \overline{e} \cdot H^T$$
- Fehlersyndrom entspricht der Summe der "fehlerbehafteteten Spalten" der Parity-Check-Matrix

- Warum gilt $\overline{x} \cdot H^T = \overline{0}_n?$

$$\overline{x}\cdot H^T = (\overline{u}\cdot G) \cdot H^T = \overline{u}\cdot(G\cdot H^T)=\overline{u}\cdot 0_{k,n-k} = \overline{0}_n$$
![[Pasted image 20240427113814.png]]

##### Eigenschaften

Fehlererkennung:
- Fehlersyndrom: $\overline{s} \neq \overline{0}$
- unerkannter Fehler: Summe der "fehlerbehafteten Spalten" der Parity-Check-Matrix ergibt $\overline{0}$
	- Beispiel: $\overline{e} = (1\quad 1\quad 0\quad 1\quad 0\quad 0\quad 0)$

Fehlerkorrektur:
- Fehlersyndrom muss eindeutige Linearkombination aus Spalten der Parity-Check-Matrix sein
- Fehlerhafte Fehlerkorrektur bei 2 Fehlern:
	- Beispiel: $\overline{e} = (1\quad 1\quad 0\quad 0\quad 0\quad 0\quad 0)$

Hamming-Distanz h:
- $h-1$ = Anzahl der linear-unabhängigen Spalten der Prüfmatrix
- im Beispiel: Hamming-Distanz=3

##### Dekodierung über Syndrom-Tabelle

Die Fehlerkorrektur wird über eine Syndrom-Tabelle durchgeführt

Die Syndrom-Tabelle bildet jedes Fehlersyndrom auf den Fehlervektor ab
- dabei wird das Fehlersyndrom in einen Integerwert umgewandelt, so dass sich eine liste (ein Array) von Fehlervektoren ergibt
- die Syndrom-Tabelle kann enthalten
	- alle Fehlersyndrome
		- evtl. auch nicht-eindeitige, eine Fehlerkorrektur ist besser als keine, da auf jeden Fall ein Fehler vorliegt
	- alle eindeutigen Fehlersyndrome
	- alle Fehlersyndrome bis zu 

Die Fehlerkorrektur wird dann wie folgt implementiert
- berechne Fehlersyndrom $\overline{s} = \overline{y} \cdot H^T$
- wandle Fehlersyndrom in einen Integerwert $s=int(\overline{s})$ um
- bestimme Fehlervektor $\overline{e} =$ $syndrom$\_$table[s]$
- korrigiere Bitfehler: $\overline{y}_{korr} = (\overline{y}+\overline{e})\  mod\ 2$

##### Beispiel für Syndrom-Tabelle

$$H = \begin{pmatrix}
1&0&0&1&0&1&1\\
0&1&0&1&1&1&0\\
0&0&1&0&1&1&1
\end{pmatrix}$$
Beispiel:
- Nutzwort: $\overline{u} = (0\quad 1\quad 1\quad 0)$
- Codewort: $\overline{x} = (1\quad 0\quad 0\quad 0\quad 1\quad 1\quad 0)$
- Fehlervektor: $\overline{e} = (0\quad 1\quad 0\quad 0\quad 0\quad 0\quad 0)$ 
- empf. Codewort: $\overline{y} = (1\quad 1\quad 0\quad 0\quad 1\quad 1\quad 0)$
- Fehlersyndrom: $\overline{s} = (0\quad 1\quad 0)$
- Fehlersyndrom (Integer): $s=2$


| Syndrom | Fehlervektor                                  |
| ------- | --------------------------------------------- |
| 0       | $0\quad 0\quad 0\quad 0\quad 0\quad 0\quad 0$ |
| 1       | $0\quad 0\quad 1\quad 0\quad 0\quad 0\quad 0$ |
| 2       | $0\quad 1\quad 0\quad 0\quad 0\quad 0\quad 0$ |
| 3       | $0\quad 0\quad 0\quad 0\quad 1\quad 0\quad 0$ |
| 4       | $1\quad 0\quad 0\quad 0\quad 0\quad 0\quad 0$ |
| 5       | $0\quad 0\quad 0\quad 0\quad 0\quad 0\quad 1$ |
| 6       | $0\quad 0\quad 0\quad 1\quad 0\quad 0\quad 0$ |
| 7       | $0\quad 0\quad 0\quad 0\quad 0\quad 1\quad 0$ |

##### Konstruktion von Codes

Bei der Konstruktion von linear-systematischen Codes bietet es sich an, zunächst die Parity-Check-Matrix zu generieren.

zur Korrektur von einem Fehler -> Hamming-Distanz: 3
- alle Spalten der Prüfmatrix müssen paarweise linear unabhängig sein
- einfach: alle Spalten der Parity-Check-Matrix müssen verschieden ungleich dem Nullvektor sein

zur Erkennung von drei Fehlern -> Hamming-Distanz: 4
- je drei beliebige Spalten der Prüfmatrix müssen linear unabhängig sein
- die Summe von drei (oder weniger) beliebigen Spalten darf nie den Nullvektor ergeben

zur Korrektur von zwei Fehlern -> Hamming-Distanz: 5
- je vier beliebige Spalten der Prüfmatrix müssen linear unabhängig sein
- die Summe von vier (oder weniger) beliebigen Spalten darf nie den Nullvektor ergeben

##### Konstruktion Hamming-Code

gewünschte Codeeigenschaften:
- $\eta = 1$ Fehler korrigierbar
- $N-K$ = 4 Prüfbits

Frage: Was ist die maximale Anzahl Nutzbits?
- $2^{4+K} \geq 2^K(k+4+1) \leftrightarrow 2⁴ \geq K+4+1\leftrightarrow K \leq 11$

Benötigen Parity-Check-Matrix $H = [I_{N-K}\quad P^T]$ mit maximal $2^{N-K}-1 = 15$
- 4 Spalten für Identitätsmatrix => 11 weitere Prüfspalten => 11 Nutzbits

$$H = \begin{bmatrix} 1 & 0 & 0 & 0 & 1 & 1 & 1 & 1 & 0 & 1 & 1 & 1 & 1 & 0 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 & 1 & 1 & 0 & 0 & 1 & 1 & 0 \\ 0 & 0 & 1 & 0 & 1 & 1 & 0 & 0 & 0 & 1 & 1 & 0 & 0 & 1 & 1 & 0 & 1 \\ 0 & 0 & 0 & 1 & 1 & 0 & 1 & 1 & 0 & 1 & 0 & 0 & 1 & 1 & 0 & 1 & 1 \end{bmatrix}$$

## Leitungskodierung

### Übersicht
### Basisband
### Trägerfrequenz

## WLAN
### Basics
### Multiple Access

### Channelcoding
