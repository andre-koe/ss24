
## Einführung

## 3D-Reconstruction Pipeline

### Die 3D-Rekonstruktions Pipeline

#### Datenakquise:

![[Pasted image 20240426161234.png]]

#### Datenakquise und 3D Rekonstruktion

**Kernfrage:** Welche Scantechnologie und welche Sensoren werden verwendet?

Die Datenaquise liefert oft mehrere Datensätze aus verschiedenen Perspektiven, Messungen oder Einstellungen.

Hierfür verwendete Algorithmen sind unteranderem:
- Stereo Triangulation (Aufgabe 2)
- Time-of-flight
- Laser-Triangulation
- Shape-from-X

#### Datenrepräsentation

![[Pasted image 20240426161846.png]]

**Kernfrage:** Wie reprensentieren wir die Daten im Computer?

Die Datenrepräsentation hängt von der verwendeten Scantechnologie ab.

**Dimensionalität der Daten**: 2d vs. 2.5d vs. 3d vs kd
- 2d:    Bilder
- 2.5d: Höhenfeld (Height Field)
- 3d:    3d Punkte
- kd:    Vektor/Tensor Felder

**Struktur**: Grid (Regulär) vs. Space Partition vs. Unstrukturiert (Irregulär)
- Grid:                    Array, Matrix, Voxels
- Space Partition: Octree, kd-Tree, bsp-Tree
- Unstrukturiert:   Halbkanten, etc.

**Verbundenheit (Connectivity)**: Punktwolke vs. Punktmesh
- Punktwolke: Topologyinformationen nur implizit
- Punktmesh:  Topologyinformationen sind explizit gespeichert

#### Clean Up

![[Pasted image 20240426163949.png]]

**Kernfrage:** Was sind die relevanten Daten?

**Clean Up**:
Entferne Artefakte und unnötige bzw. ungewollte Daten aus den Datensätzen
- De-Noising, Smoothing (Glätten)
- Hole-Filling
- Outlier Entfernung
- Freistellen (Background Removal)
- Analyse der Datenqualität

**Vereinfachung**

**Objekterkennung**

#### Registrierung

![[Pasted image 20240426172510.png]]

**Kernfrage:** Was ist die räumliche relative Pose (Position + Ausrichtung/Richtung) der Datensätze?

**Ausrichtung** der Datensätze, d.h. was ist ihre räumliche relative Pose?
- **Grobe Registrierung**: Bringe die Datensätze *näher* zueinander
	- Was ist mit *näher* gemeint? -> Das sich die übereinstimmenden Datenpunkte der jeweiligen Datensätze, in räumlicher Nähe zueinander befinden.
	- Techniken: Hauptkomponentenanalyse (Principal Component Analysis (PCA)), Unabhängigkeitsanalyse (Independent Component Analysis (ICA)), vier kongruente Punkte (Four Congruent Points (4CP))
- **Feine Registrierung**: Überlagere die Datensätze so präzise wie möglich
	- Techniken: Iterative engste Punkte (iterative closest points (ICP)), fMerkmalsabgleich (feature matching), Verteilungsabgleich (distribution matching)

**Fusion** der Datensätze in einen einzigen Datensatz
**Sensorfusion**: Fusion der rohen Daten verschiedener Sensoreinstellungen.

#### Konvertierung

![[Pasted image 20240426174405.png]]

**Kernfrage**: Welche Datenrepräsentation ist für die folgenden Schritte am geeignetsten?

![[Pasted image 20240426174708.png]]

**Verbessern** der Repräsentation
- Re-meshing, decimation, sub-sampling
- Super-sampling, refinement, subdivision
- Hierarchische Modellierung
- Qualitätsoptimierung

**Konvertierung** der Repräsentation
- CAD-Modell, Parametrisches Modell (Rekonstruktion)
- Meshing (Triangulation)

#### Segmentierung

![[Pasted image 20240426174958.png]]

**Kernfrage**: Was sind die relevanten semantischen Komponenten?

![[Pasted image 20240426180614.png]]

**Klassifiziere** den Datensatz:
-  Was sind gute semantische Maßstäbe?
	- (Diskrete) differential Geometrie: Diederwinkel, Krümmungsfluss usw.
	- k-nearest Neighbour
	- DNN-Merkmale

**Es handelt sich bei der Segmentierung um einen optionalen Schritt**

#### Klassifizierung

![[Pasted image 20240426180808.png]]

**Kernfrage**: Welche realen Objekte sehen wir?

![[Pasted image 20240426181257.png]]

**Interpretation** der Daten
- Formabgleich
	- Abgleich über Registrieren
	- Abgleich über trainierte DNNs
- 3d-Daten  Abruf
- Fehlererkennung
- Novelty detection
**Erkennung**
- Haben wir das Objekt bereits zuvor gesehen?
- Wo und in welcher Pose haben  wir das Objekt bereits gesehen?

#### Visualisierung

![[Pasted image 20240426181520.png]]

**Kernfrage**: Welche realen Objekte sehen wir?

**Visualisierung** der Daten
- Rendering Methoden (Computergrafik)
	- Transparenz
	- Texturmapping
	- Pseudo-color Rendering

Post-Processing:
- Inspektion der Daten
- Animation
- Deformation
- Simulation

#### Anmerkungen

Es gibt **keine** standard 3D Rekonstruktions-Pipeline

Die Realisierung der verwendeten 3D-Rekonstruktions-Pipeline hängt von den verschiedenen technischen und anwendungsspezifischen Bedingungen ab.

Einige Schritte der 3D Rekonstruktionspipeline können in der finalen Umsetzung ausgelassen werden
- Insbesondere die Konvertierung der Datenrepräsentation fehlt oft

Einige Schritte werden in der Realisierung eventuell in einer anderen Reihenfolge angeordnet.

Jeder Schritt verwendet eventuell ML/DL Techniken.

### Fragen: 1

##### Was sind die typischen Schritte in einer Rekonstruktionspipeline?
1. Datenakquise & 3D Rekonstruktion
3. Repräsentation
4. Clean-Up
5. Registrierung
6. Konvertierung (Wird oft weggelassen)
7. Segmentierung (Optional)
8. Klassifizierung
9. Visualisierung

##### Welche Schritte der Rekonstruktionspipeline werden in der Vorlesung behandelt?

1. 3D Rekonstruktion

##### Was sind die typischen Kriterien bei der Auswahl der der Datenrepräsentation?

1. Sinn und Zweck der Anwendung
2. Detailgenauigkeit
3. Speicherbedarf
4. Effizienz
5. Art/Quelle der Eingabedaten
6. Folgende noch auszuführende Schritte


## Geometrische Grundlagen

### Affine Geometrie

#### 2D Affine Geometrie

Im Allgemeinen nehmen wir ein orthonormales, kartesisches Koordinatensystem (KS) an.

Gegeben:
- KS $S'$ (bspw., Weltsystem) gegeben durch $S':(O';e_1', e_2')$ oder $S':(O';e_1',e_2',e_3')$
- KS $S$ (bspw. Objektsystem) gegeben durch $S:(O;e_1,e_2)$ oder $S:(O;e_1,e_2,e_3)$

Gesucht wird:
- Die Transformation von $S$ nach $S'$
- Änderungen von Punktkoordinaten beim Wechel von $S$ nach $S'$

##### Beispiel 1: Translation

**Annahme:** Koordinatenachsen sind paarweise parallel.

Für das KS $S'$ liefert das:
- $S'$ resultiert aus $S$ durch Verschiebung um $-T$, wobei $T=(t_1, t_2)^t$ der Ursprung $O$ von $S$ im KS $S'$ ist

Der Punkt hat:
- im $S$ KS die Koordinaten: $P = (p_1, p_2)^t$
- im $S'$ KS die Koordinaten: $P' = T + P = (t_1, t_2)^t + (p_1, p_2)^t$

![[Pasted image 20240501134508.png]]

##### Beispiel 2: Rotation

**Annahme:** Beide KS haben den selben Ursprung $O = O'$

Rotation des KS $S$ relativ zu $S'$ um den Winkel $\varphi$ um $O$:
- Das KS $S'$ resultiert aus $S$ nach Rotation um $-\varphi$

Wir erhalten:
- $l/p_2 = sin(\varphi)$ und $L/p_1 = cos(\varphi)$
daher:
- $p_1' = L-l = p_1 cos(\varphi) - p_2 sin(\varphi)$
analog:
- $p_2' = \cdots = p_1 sin(\varphi) + p_2 cos(\varphi)$

![[Pasted image 20240501144238.png]]

**Kurzform**:

$$P' = \left(\begin{array}{¢}p_1'\\ p_2'\end{array}\right) = \begin{pmatrix}p_1\cos(\varphi)-p_2\sin(\varphi)\\p_1\sin(\varphi)+p_2\cos(\varphi)\end{pmatrix}\cdot \left(\begin{array}{c}p_1\\p_2\end{array}\right)$$

Dasselbe in Vektor-Matrix-Notation:

$$P' = R(\varphi)\cdot P$$
mit einer orthonormalen Rotationsmatrix: 

$R(\varphi) = \begin{pmatrix}\cos(\varphi)& -\sin(\varphi)\\ \sin(\varphi)&\cos(\varphi)\end{pmatrix}$ 

**Anmerkung:** $R$ ist orthonormal g.d.w. $R^{-1} = R^t$

##### Zu orthonormalen Matrizen



#### 3D Affine Geometrie

### Projektive Geometrie

#### Parallelprojektion

#### Perspektivische Projektion

### Die Physik von Kameraprojektion

## 3D Daten Akquise

## 3D Datenrepräsentation

## 3D-Registrierung

## Von Punktwolken zu Meshes
