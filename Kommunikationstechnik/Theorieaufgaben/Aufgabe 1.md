
### Allgemeine Definitionen

##### Information

"*Eine Aussage oder Beobachtung ist dann informativ, wenn sie und etwas mitteilt, das uns vorher nicht bekannt war. Nur über solche Dinge können wir jedenfalls Informationen gewinnen, über die bei uns ein gewisses Maß an Nichtwissen oder Ungewissheit besteht. In der Tat lässt sich Information als dasjenige erklären, dass Ungewissheit beseitigt oder reduziert.*" - (Fred Attneave)

##### Shannon'sche Kommunikationsmodell

![[Pasted image 20240405224157.png]]

- Überlegungen zur Kanalkapazität *C* 
	- Allgemein: Übertragung von codierten Symbolen von einer Informationsquelle über einen gestörten Übertragungskanal zu einer Informationssenke
	- Speziell: Übertragung von Bitsequenzen
- Sender:
	- In einer Zeitspanne *T* werden *n* bits in den Kanal eingespeist
	- damit können $2^n$ Bitsequenzen konstruiert werden [[Warum können mit n in einer Zeitspanne T übertragenen Bits 2 hoch n  Bitsequenzen konstruiert werden?]]
- Kanal:
	- Wenn *n* Bits an Information übertragen werden, muss der Empfänger nach *T* Zeitschritten $2^n$ verschiedene Signale unterscheiden können [[Warum muss der Empfänger nach T Zeitschritten 2 hoch n  verschiedene Signale unterscheiden können?]]
	- Eine Halbierung der Signalzahl bedeutet die Übertragung von einem Bit

###### Mathematische Definition

$$N(T) = \textrm{Anzahl der Signale der Länge T}$$

Ist $N(T) = 2^n$, dann können $n$ Bits übertragen werden und damit überträgt der Kanal 
$$\frac{log_2N(T)}{T}$$
Informations-Bits pro Zeiteinheit

Definition der Kapazität *C* eines diskreten Kanals von Claude Shannon (1948):
$$C = \lim_{T\rightarrow \infty} \frac{log_2N(T)}{T}$$


### Terminologie

| Term                    | Bedeutung                                                                                                                                                                                                                                                                                         | Berechnungsvorschrift |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Entropie                | Durchschnittlicher Informationsgehalt einer Nachricht.<br>Wird aus der Auftrittswahrscheinlichkeit und dem Informationsgehalt berechnet                                                                                                                                                           |                       |
| Information             | Information beseitigt oder reduziert Ungewissheit                                                                                                                                                                                                                                                 |                       |
| Kodierung               | Dient der verlustfreien (hinsichtlich der in der Nachricht enthaltenen Information) Komprimierung einer Nachricht                                                                                                                                                                                 |                       |
| Quelle                  | Quelle der Information                                                                                                                                                                                                                                                                            |                       |
| Informationsgehalt      | Die Menge an Information die die Nachricht transportiert, wird aus den Anzahlen der sich wiederholenden                                                                                                                                                                                           |                       |
| Huffman                 | Kodierungsverfahren nach Huffman, basiert auf der Konstruktion sogennanter Huffman-Trees, dabei wird jeweils die Wurzel rekursiv durch die Fusion zweier Nodes mit den kleinsten Werten erzeugt.<br><br>Die Kodierungsvorschrift, wird dann durch rekursives durchlaufen durch den Baum gebildet. |                       |
| Shannon-Fano            | Kodierungsverfahren nach Shannon und Fano, basiert auf der rekursiven Unterteilung einer Nachricht auf Basis der relativen Häufigkeit ihrer einzelnen Bestandteile, durch diese Unterteilung werden dann die Präfixe gebildet.                                                                    |                       |
| Arithmetische Kodierung | Proprietäres? Kodierungsverfahren von IBM,                                                                                                                                                                                                                                                        |                       |
| Redundanz               |                                                                                                                                                                                                                                                                                                   |                       |
| Mittlere Codewort Länge |                                                                                                                                                                                                                                                                                                   |                       |



---


### Entropie



### Kodierung

#### Huffman

#### Shannon-Fano

#### Arithmetische Kodierung