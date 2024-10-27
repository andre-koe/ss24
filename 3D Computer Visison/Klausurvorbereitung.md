
# Kapitel 1: Grundlagen der Rekonstruktionspipeline


# Kapitel 2: Mathematische Grundlagen

## Homogene Koordinaten

Die serielle Anwendung von Rotation $R$ und Translation $T$ über folgende Gleichung:

$$P' = S\cdot (T+R\cdot P)$$
beinhaltet sowohl Addition als auch Multiplikation.

Um alle affinen Transformationen als Matrixmultiplikationen zu repräsentieren werden *homogene Koordinaten* eingeführt

$(x,y)\rightarrow (x, y, w)^t$ bzw. $(x,y,z)\rightarrow (x,y,z,w)$

mit $w = 1$ (typischerweise)

![[Pasted image 20240510145123.png]]


Damit ergeben sich für die affinen Transformationen folgende Repräsentationen:

#### Translation

##### 2D
$$\begin{pmatrix}1&0&t_1\\0&1&t_2\\0&0&1\end{pmatrix} \cdot \begin{pmatrix}x\\y\\1\end{pmatrix} = \begin{pmatrix}x+t_1\\y+t_2\\1\end{pmatrix}$$
##### 3D
$$\begin{pmatrix}1&0&0&t_1\\0&1&0&t_2\\0&0&1&t_3\\0&0&0&1\end{pmatrix} \cdot \begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}x+t_1\\y+t_2\\z+t_3\\1\end{pmatrix}$$

#### Skalierung

##### 2D

$$\begin{pmatrix}\lambda_1&0&0\\0&\lambda_2&0\\0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\1\end{pmatrix} = \begin{pmatrix}\lambda_1\cdot x\\\lambda_2\cdot y\\1\end{pmatrix}$$
##### 3D

$$\begin{pmatrix}\lambda_1&0&0&0\\0&\lambda_2&0&0\\0&0&\lambda_3&0\\0&0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}\lambda_1\cdot x\\\lambda_2\cdot y\\\lambda_3\cdot z\\1\end{pmatrix}$$

#### Rotation

##### 2D

$$\begin{pmatrix}\cos(\varphi)&-\sin(\varphi)&0\\\sin(\varphi)& cos(\varphi)& 0\\0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\1\end{pmatrix} = \begin{pmatrix}x\cos(\varphi)-y\sin(\varphi)\\x\cos(\varphi)+y\sin(\varphi)\\1\end{pmatrix}$$

##### 3D

###### Elementar-Rotation um z

![[Pasted image 20240510162658.png]]

$$\begin{pmatrix}\cos(\varphi)&-\sin(\varphi)&0&0\\\sin(\varphi)&\cos(\varphi)&0&0\\0&0&1&0\\0&0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}x\cos(\varphi)-y\sin(\varphi)\\x\cos(\varphi)+y\sin(\varphi)\\z\\1\end{pmatrix}$$
###### Elementar-Rotation um x
![[Pasted image 20240510163122.png]]

$$\begin{pmatrix}1&0&0&0\\0&\cos(\varphi)&-\sin(\varphi)&0\\0&\sin(\varphi)&\cos(\varphi)&0\\0&0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}x\\y\cos(\varphi)-z\sin(\varphi)\\y\sin(\varphi)+z\cos(\varphi)\\1\end{pmatrix}$$
###### Elementar-Rotation um y
$$\begin{pmatrix}\cos(\varphi)&0&\sin(\varphi)&0\\
0&1&0&0\\
-\sin(\varphi)&0&\cos(\varphi)&0\\
0&0&0&1\end{pmatrix}\cdot \begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}x\cos(\varphi)+z\sin(\varphi)\\y\\-x\sin(\varphi)+z\cos(\varphi)\\1\end{pmatrix}$$


### Allgemeiner Fall der Rotation: Rotation um eine bel. Achse G

**Ziel**: Rotation $R_G(\psi)$ eines Punktes um eine beliebig ausgerichtete Achse $G$ um den Winkel $\psi$

**Spezialfall**: Die Rotationsachse $G$ passiert den Ursprung des KS und wird durch den Vektor $b = (b_x, b_y, b_z)^t$ mit ||$b$|| = 1 aufgespannt. $\rightarrow$ $G = \{\lambda \cdot b:\lambda \in \mathbb{R}\}$

![[Pasted image 20240510164358.png]]


##### Rotation um beliebige Achse G

Jede Rotation um eine beliebige Achse kann als Kombination aus drei Rotationen um die einzelnen Koordinatenachsen beschrieben werden.

Wir unterscheiden zwischen:

**Intrisischer Repräsentation**: Winkel in Bezug auf das rotierte KS

**Extrisischer Repräsentation**: Winkel in Bezug auf ein festes Welt-KS 

Die Wahl der Rotationsachsen ist weniger relevant, da sämtliche der insgesamt 24 möglichen Repräsentationen äquivalent sind.

- Echte Eulerwinkel: x-y-x, x-z-x,y-x-y,y-z-y,z-x-z,z-y-z
- Tait-Bryan Winkel (auch Cardanwinkel genannt): x-y-z, x-z-y, y-x-z, y-z-x, z-x-y, z-y-x

Im Folgenden verwenden wir die extrinsische z-y-z Repräsentation

**Gesucht:** Koordinaten eines Punktes $P$ nach einer Rotation um die Achse $G$ mit dem Winkel $\psi$

Extrinsischer z-y-z Ansatz:

1. Transformiere den Punkt $P$ so dass die Rotationsachse mit der $z$-Achse übereinstimmt
2. Wende eine Rotationsmatrix $R_z(\psi)$ für die Rotation um $\psi$ an
3. Invertiere die ursprüngliche Hilfstransformation (Schritt 1.)

(Falls $G$ bereits die $z$-Achse ist, entfallen die Schritte 1. und 3.)

**Schritt 1:**
![[Pasted image 20240510175524.png]]

Rotiere den Vektor $b$ in die $(z,x)$-Ebene: $b\rightarrow b'$

$P$ wird auf $P'$ abgebildet mittels $P' = R_z(-\theta) \cdot P$


$$\begin{align}R_z(\theta) &= \begin{pmatrix}\cos(\theta)&\sin(\theta)&0&0\\-\sin(\theta)&\cos(\theta)&0&0\\0&0&1&0\\0&0&0&1\end{pmatrix}\\&=\frac{1}{d}\begin{pmatrix}b_x&b_y&0&0\\-b_y&b_x&0&0\\
0&0&d&0\\0&0&0&d\end{pmatrix}\end{align}$$

Die zweite der obigen Matrizen ergibt sich aus den trigonometrischen Zusammenhängen aus der Abbildung:

$\cos(\theta) = \frac{\textrm{Ankathete}}{\textrm{Hypothenuse}} = \frac{b_x}{d}$ 

Und selbiges für $\sin(\theta)$

**Schritt 2:**
![[Pasted image 20240510175745.png]]

Rotiere den Vektor $b'$ auf die $z$-Achse: $b'\rightarrow b''$

$P'$ wird auf $P''$ abgebildet mittels $P'' = R_y(-\phi)\cdot P'$ mit

$$\begin{align}R_y(-\phi)&=\begin{pmatrix}\cos(\phi)&0&-\sin(\phi)&0\\
0&1&0&0\\\sin(\phi)&0&\cos(\phi)&0\\0&0&0&1\end{pmatrix}\\&=\begin{pmatrix}b_z&0&-d&0\\0&1&0&0\\d&0&b_z&0\\0&0&0&1poö\end{pmatrix}\end{align}$$

**Schritt 3:**

![[Pasted image 20240510191000.png]]

Rotiere um den Winkel $\psi$ um die $z$-Achse

$P''$ wird auf $P'''$ abgebildet mit $P''' = R_z(\psi) \cdot P''$ mit

$$R_z(\psi) = \begin{pmatrix}\cos(\psi)&-\sin(\psi)&0&0\\\sin(\psi)&\cos(\psi)&0&0\\0&0&1&0\\0&0&0&1\end{pmatrix}$$
**Schritt 4 und 5:**

Invertiere die Rotationsschritte 1. und 2. in umgekehrter Reihenfolge

$P'''$ wird auf den gesuchten rotierten Punkt $Q$ abgebildet mit $Q = R_z(\theta)R_y(\phi)\cdot P'''$

$$R_y(\phi) = \begin{pmatrix}b_z & 0&d&0\\0&1&0&0\\-d&0&b_z&0\\0&0&0&1\end{pmatrix} $$
$$R_z(\theta) = \frac{1}{d}\begin{pmatrix}b_x&-b_y&0&0\\b_y&b_x&0&0\\0&0&d&0\\0&0&0&d\end{pmatrix}$$


###### Resultat

Die gesamte Transformation kann als Konkatenation der einzelnen Transformationen realisiert werden:

$$M_b(\psi) = R_z(\theta)R_y(\phi)R_z(\psi)R_y(-\phi)R_z(-\theta)$$

###### Allgemeiner Fall:

Falls die Rotationsachse eine zufällige Linie

$$G=\{a+\lambda \cdot b:\lambda \in \mathbb{R}, a=(a_x,a_y,a_z)^t,||b||=1\}$$

Vor dem ersten Schritt und nach dem letzten Schritt muss eine Translation angewendet werden, d.h.

$$M_b(\psi)=T(a)R_z(\theta)R_y(\phi)R_z(\psi)R_y(-\phi)R_z(-\theta)T(-a)$$
## Affine Abbildungen:

Wir unterscheiden zwischen drei Arten von affinen Abbildungen:

#### Affine Abbildung (Affine Transformation)
$$P' = A\cdot P + T$$

Wobei $T$ eine Translation ist und $A$ eine lineare Abbildung.


Lineare Abbildungen sind bspw. Translation, Rotation, Scheerung, Reflektion

Im allg. wird ein rechteck auf ein rotiertes und verschobenes Parallelogramm abgebildet.

Eigenschaften der Affinen Abbildung sind:

1. Verhältnisse bleiben unverändert
   $$F(\lambda P + (1 - \lambda) Q) = \lambda F(P) + (1-\lambda) F(Q) \quad \textrm{mit} \quad 0\leq\lambda \leq 1$$Für allgemeine Punkte $P_i$ gilt dann
   $$F\left(\sum_{i=0}^n\alpha_i P_i\right) = \sum_{i=0}^n\alpha_i F(P_i),\quad \sum_{i=0}^n\alpha_i = 1$$

2. Parallele Linien bleiben parallel
3. Winkel, Längen, Richtungen und Orientierung können sich ändern

##### 2D
$$\textrm{mit}\quad A=\begin{pmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{pmatrix}\quad \&\quad T= \begin{pmatrix}a_{10}\\a_{20}\end{pmatrix}$$

4. Um die 6 Parameter $a_{ij}$ zu bestimmen werden 3 linear unabhängige Punkte in beiden Koordinatensystemen benötigt.

##### 3D

$$\textrm{mit}\quad A=\begin{pmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{pmatrix}\quad \&\quad T= \begin{pmatrix}a_{10}\\a_{20}\\ a_{30}\end{pmatrix}$$


4. Um die 12 Parameter $a_{ij}$ zu bestimmen werden 3 linear unabhängige Punkte in beiden Koordinatensystemen benötigt.

#### Ähnlichkeitstransformation (Similarity Transformation)

$$P' = s\cdot R\cdot P + T$$

Wobei $s$ ein Skalierungsfaktor, $R$ eine Rotation und $T$ eine Translation sind.

Eigenschaften der Ähnlichkeitstransformation:

1. Verhältnisse, Winkel und parallele Linien bleiben erhalten
2. Längen, Richtungen und Orientierungen können sich ändern
##### 2D

$$\textrm{mit}\quad R=\begin{pmatrix}r_{11}&r_{12}\\r_{21}&r_{22}\end{pmatrix}\quad \&\quad T=\begin{pmatrix}r_{10}\\r_{20}\end{pmatrix}$$

3. Um die 4 Parameter $r_{10}, r_{20}, s, \alpha$ zu bestimmen werden mindestens zwei korrespondierende Punkte in beiden KS benötigt

Im allg. wird ein rechteck auf ein skaliertes, rotiertes und verschobenes Rechteck abgebildet.

##### 3D
$$\textrm{mit}\quad R=\begin{pmatrix}r_{11}&r_{12}&r_{13}\\r_{21}&r_{22}&r_{23}\\r_{31}&r_{32}&r_{33}\end{pmatrix}\quad \&\quad T=\begin{pmatrix}r_{10}\\r_{20}\\r_{30}\end{pmatrix}$$

Um die 7 Parameter $r_{10}, r_{20},r_{30}, s, \alpha, \beta$, $\gamma$  zu bestimmen werden mindestens drei korrespondierende Punkte in beiden KS benötigt

#### Starrkörperbewegung (Rigid Body Motion)

$$P' = A \cdot P + T$$

Wobei $A$ eine orthogonal Transformation, d.h. $A^T = A^{-1}$ und $T$ eine Translation ist
##### 2D
 $$\quad \textrm{mit}\quad A=\begin{pmatrix}a_{11}&a_{12}\\a_{21}&a_{22}\end{pmatrix}\quad \&\quad T=\begin{pmatrix}a_{10}\\a_{20}\end{pmatrix}$$

##### 3D
$$\quad \textrm{mit}\quad A=\begin{pmatrix}a_{11}&a_{12}&a_{13}\\a_{21}&a_{22}&a_{23}\\a_{31}&a_{32}&a_{33}\end{pmatrix}\quad \&\quad T=\begin{pmatrix}a_{10}\\a_{20}\\a_{30}\end{pmatrix}$$

##### Eigenschaften:

1. Es handelt sich um eine Kombination aus Rotation, Translation und Reflektion (falls $det(A) = 1$, siehe unten)
2. Verhältnisse, Winkel, Längen und parallele Linien bleiben erhalten.
3. Orientierungen können sich ändern, falls $det(A) = -1$ siehe ***improper rigid body motion***

Im allg. wird ein Rechteck auf ein rotiertes und verschobenes Rechteck abgebildet.
##### Improper Rigid Body Motion (Spezialfall)

$$P' = A\cdot P + T\quad \textrm{mit}\quad det(A) = -1$$

## Projektive Geometrie

### Parallel Projektion

Beispiele für unterschiedliche Strahlenführungen in Projektionen:

**Collimator**
![[Pasted image 20240510201350.png]]

Alle Strahlen passieren ein System paralleler Kanäle
- (Fast) parallele Strahlen in der Bildebene
- Auch für divergente Lichtquellen fast parallele Strahlen


**Pinhole-Kameras**
![[Pasted image 20240510201419.png]]

Alle Strahlen passieren ein Center of Projection
- Das Loch ist im Idealfall ein einzelner Punkt (COP) $N$
- Fast radiale Strahlen von $N$ in der Bildebene
- Das Bild wird kopfüber Dargestellt

### Einstieg in die projektive Geometrie

**Definition:** Eine Projektion ist eine Abbildung die einen Raum der Dimension $n$ auf einen der Dimension $<n$ abbildet.

Da Monitore und Kameras $2d$ Geräte sind, werden $3d$ Objekte in $2d$ geplottet und aufgezeichnet.
- Ein Punkt im Raum $A$ wird entlang eines Projektionsstrahls (direction of projection) auf eine gegebene Projektionsebene (image plane) abgebildet.

![[Pasted image 20240510201813.png]]

Die Richtung einer Projektion wird durch das Center of Projection und den Punkt im Raum $A$ bestimmt.

Der Schnittpunkt des Projektionsstrahls mit der Projektionsebene bestimmt den projezierten Bildpunkt $A'$ 


#### Klassifikation von unterschiedlichen Projektionen

![[Pasted image 20240510202127.png]]


#### Parallele Projektionen

![[Pasted image 20240510203735.png]]

**Eigenschaften von Parallelprojektionen:**

- Alle Projektionsstrahlen sind Parallel in eine Richtung
- Das Center of Projection (in diesem Fall Fernpunkt) ist ein Punkt in der Unendlichkeit.

**Nachteil:**
- Weniger realistische Darstellung

**Vorteil:**
- Erlaubt exakte Messungen auf Basis des Bildes

##### Beispiele:

![[Pasted image 20240510203801.png]]

#### Perspektivische Projektion

![[Pasted image 20240510210957.png]]

Die Perspektivische Projektion auch Zentralprojektion genannt funktioniert wie folgt:

**Kamerasystem** $(O; x,y,z)$ im Welt-KS.
**Bildraum** $(O'; x', y')$ und ***image principal Point H***
- letzteres ist der Punkt der Bildebene der dem Center of Projection am nähesten liegt.
**Vereinfachung:** $H=O'$ und das Kamerasystem entspricht dem Welt-KS mit Blickrichtung entlang der negativen $z-Achse$

**Abbildung**

$\mathcal{P}: \begin{pmatrix}x\\y\\z\end{pmatrix}\in \mathbb{R}^3\mapsto\begin{pmatrix}x'\\y'\end{pmatrix}\in\mathbb{R}^2$    

in affinen Koordinaten:

$\mathcal{P}:\begin{pmatrix}x\\y\\z\end{pmatrix} \in \mathbb{R}^3\mapsto \begin{pmatrix}x'\\y'\end{pmatrix}\in\mathbb{R}^2$$

mit:
$$\begin{pmatrix}x'\\y'\end{pmatrix}=-\frac{f}{z}\begin{pmatrix}x\\y\end{pmatrix}$$

Und in homogenen Koordinaten:

$$\begin{pmatrix}x'\\y'\\1\end{pmatrix}\sim\begin{pmatrix}f&0&0&0\\0&f&0&0\\0&0&-1&0\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix}$$

### Perspektivische Projektion von Punkten

Ein 3D Punkt $P$ wird auf einen 2D Punkt $P'$ in der Bildebene abgebildet.

> Wenn die $z$-Koordinate 0 ist kann der Punkt nicht projeziert werden.


Falls der Punkt $P$ in der $xy$-Ebene des Kamerasystems liegt, kann er nicht projeziert werden, da der Projektionsstrahl parallel zur Bildebene verläuft.

![[Pasted image 20240511182026.png]]

### Perspektivische Projektion von Linien

Eine 3D Linie $G$ wird auf eine 2D Linie $G'$ in der Bildebene abgebildet.

Eine affine 3D Linie in Kamerakoordinaten ist eine Menge von Punkten mit $\lambda \in \mathbb{R}$,

$$G(\lambda) = \begin{pmatrix}a_1\\a_2\\a_3\end{pmatrix}+\lambda \begin{pmatrix}g_1\\g_2\\g_3\end{pmatrix}=\vec{a}+\lambda\vec{g}$$
Diese wird abgebildet auf:
$$G'(\lambda) = -\frac{f}{a_3+\lambda g_3}\left(\begin{pmatrix}a_1\\a_2\end{pmatrix}+\lambda \begin{pmatrix}g_1\\g_2\end{pmatrix}\right)$$

![[Pasted image 20240511182918.png]]


Falls $g_3 = 0, a_3 = 0$ ist die Linie parallel zur Bildebene und liegt in der $xy$-Ebene der Kamera $\Rightarrow$ Linie kann nicht projeziert werden.

![[Pasted image 20240511183106.png]]

Falls $g_3 = 0, a_3 \neq 0$ die Linie ist parallel zur Bildebene und passiert das Center of Projection ($N$) nicht. Die Linie wird gemäß der untenstehenden Vorschrift $G'(\lambda)$ auf die Bildebene abgebildet.

$$G'(\lambda) = -\frac{f}{a_3}\left(\begin{pmatrix}a_1\\a_2\end{pmatrix}+\lambda \begin{pmatrix}g_1\\g_2\end{pmatrix}\right)$$

![[Pasted image 20240511183500.png]]

Falls $g_3 \neq 0, \vec{a} = 0$ passiert die Linie das Center of Projection ($N$) und wird auf 

$$G'(\lambda)=-\frac{f}{\lambda g_3}\left(\lambda\begin{pmatrix}g_1\\g_2\end{pmatrix}\right) = -\frac{f}{g_3}\begin{pmatrix}g_1\\g_2\end{pmatrix}$$
Dabei handelt es sich lediglich um einen einzelnen Punkt auf der Bildebene.

![[Pasted image 20240511184630.png]]

Falls $g_3 \neq 0, \vec{a} = \lambda_0 \vec{g}$  passiert die Linie ebenfalls das Center of Projection und wird auf einen einzelnen Punkt in der Bildebene abgebildet.

$$\begin{align}G'(\lambda) &= -\frac{f}{(\lambda+\lambda_0)g_3}\left((\lambda + \lambda_0)\begin{pmatrix}g_1\\g_2\end{pmatrix}\right)\\&=-\frac{f}{g_3}\begin{pmatrix}g_1\\g_2\end{pmatrix}\end{align}$$

![[Pasted image 20240511185206.png]]

Es handelt sich hier um eine Verallgemeinerung des Falls $g_3 \neq 0, \vec{a} = 0$


Eine Linie in allgemeiner Position, d.h. $g_3 \neq 0, \vec{a} \neq 0$ mit $\vec{g} \neq k \cdot \vec{a}\quad \forall k \in \mathbb{R}$  
wird auf einen Strahl mit Fluchtpunkt $F$ in der Bildebene projeziert.

$$\lim_{\lambda\rightarrow\infty} G'(\lambda) = -\frac{f}{g_3}\begin{pmatrix}g_1\\g_2\end{pmatrix} =: F.$$
Parallele Linien mit identischem $\vec{g}$ haben den selben Fluchtpunkt $F$, sie schneiden sich im gemeinsamen Fluchtpunkt $F$ in der Bildebene.

![[Pasted image 20240511190601.png]]
![[Pasted image 20240511190642.png]]


Im Allgemeinen gilt: Bilder von parallelen Linien schneiden sich in einem Fluchtpunkt.

Jeder Punkt in der Bildebene ist ein Fluchtpunkt für eine Menge paralleler Linien.

Falls die Koordinatenachsen des Weltsystems in allgemeiner Position vorliegen, korrespondieren die Koordinatenachsen mit den Fluchtpunkten, falls sie nicht parallel zur Bildebene liegen.

Die verschiedenen perspektivischen Projektionen werden auch als 

- Ein-Punkt Perspektive
  ![[Pasted image 20240511191853.png]]
- Zwei-Punkt Perspektive
  ![[Pasted image 20240511191913.png]]
- Drei-Punkt Perpektive
  ![[Pasted image 20240511191933.png]]
bezeichnet

Eine Linie die das Center Of Projection nicht passiert, wird auf eine "Halblinie" in der Bildebene abgebildet

Längen, parallele Linien, Winkel und Verhältnise können sich ändern.

Doppelverhältnisse (Cross-ratios) sind invariant:

$$\begin{align}\frac{\overline{AC}\cdot\overline{BD}}{\overline{AD}\cdot\overline{BC}} &= \frac{\overline{A'C'}\cdot\overline{B'D'}}{\overline{A'D'}\cdot\overline{B'C'}}\\&=\frac{\overline{A''C''}\cdot\overline{B''D''}}{\overline{A''D''}\cdot\overline{B''C''}}\end{align}$$
![[Pasted image 20240511192726.png]]

### Allgemeines perspektivisches Kameramodell

Bisher haben wir den Spezialfall betrachtet bei dem das Kamerasystem zugleich auch das Welt-KS ist.

**Extrinsische Kameraparameter**
- Kamerakoordinatensystem $M_b(\alpha)$ oder Eulerwinkel (3 DOF)
- Center of Projection $N$ (3 DOF)

**Intrinsische Kameraparameter**
- Kameraparameter $f$ (Brennweite) (1 DOF)
- Principal Point $H$ (2 DOF)

**Kalibrierung**
- Bestimme die 9 Kameraparameter aus Bildern von Referenzobjekten.

![[Pasted image 20240511193259.png]]

### Allgemeine Perspektivische Projektion

- Translation des Center of Projectoon $N$, d.h. $N \neq O$
- Rotation des Kamerakoordinatensystems um $M_b(\alpha) \in \mathbb{R}^{3\times 3}$ 
- Translation des Image Principal Points $H$, d.h. $H \neq O$

Ähnlichkeitstransformation mit ($s = 1$, auch isometrie, Starrkörperbewegung) des Kamerasystems.

Perspektivische Projektion mit Translation des 

- Center of Projection $N = \begin{pmatrix}x_0\\y_0\\z_0\end{pmatrix}$ 
- Image Principal Point $H = \begin{pmatrix}x'_0\\y'_0\end{pmatrix}$

Abbildung:

$$\begin{pmatrix}x'-x'_0\\y'-y'_0\end{pmatrix} = -\frac{f}{z-z_0}\begin{pmatrix}x-x_0\\y-y_0\end{pmatrix}$$
für $z -z_0 \neq 0$

![[Pasted image 20240511195806.png]]

**In homogenen Koordinaten**

$$\begin{pmatrix}x'\\y'\\1\end{pmatrix}\sim\begin{pmatrix}f&0&x'_0\\0&f&y'_0\\0&0&-1\end{pmatrix}\begin{pmatrix}1&0&0&-x_0\\0&1&0&-y_0\\0&0&1&-z_0\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix}$$

Perspektivische Projektion mit Translation des Projektionszentrums (Center of Projection) ($N$) und des Image Principal Points $H$ und
- affiner Rotation des Kamerasystems mit $R = (r_{ij}) = M_b(\alpha)\in\mathbb{R}^{3\times 3}$,
- d.h. $R^t \cdot N = (\tilde{x}_0, \tilde{y}_0, \tilde{z}_0)^t$

Abbildung wie gehabt:

$$\begin{pmatrix}x'\\y'\end{pmatrix} = \begin{pmatrix}x'_0\\y'_0\end{pmatrix} -\frac{f}{z_c}\begin{pmatrix}x_c\\y_c\end{pmatrix}$$
mit $z_c \neq 0$

$$\begin{pmatrix}x_c\\y_c\\z_c\end{pmatrix} = R^t\left(\begin{pmatrix}x\\y\\z\end{pmatrix}-N\right)$$

**In homogenen Koordinaten**

$$\begin{pmatrix}x'\\y'\\1\end{pmatrix}\sim\ \begin{pmatrix}f&0&x'_0\\0&f&y'_0\\0&0&-1\end{pmatrix}\begin{pmatrix}r_{11}&r_{21}&r_{31}&-\tilde{x}_0\\r_{12}&r_{22}&r_{32}&-\tilde{y}_0\\r_{13}&r_{23}&r_{33}&-\tilde{z}_0\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \begin{pmatrix}f\cdot I&H\\0&-1\end{pmatrix}(R^t,-R^tN)\begin{pmatrix}P\\1\end{pmatrix}$$

Abbildung:

$$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}x'_0\\y'_0\end{pmatrix}-\frac{f}{z_c}\begin{pmatrix}x_c\\y_c\end{pmatrix}$$
mit $z_c \neq 0$ und

$$\begin{pmatrix}x_c\\y_c\\z_c\end{pmatrix}=R^t\left(\begin{pmatrix}x\\y\\z\end{pmatrix}-N\right)$$
In homogenen Koordinaten:

$$\begin{pmatrix}x'\\y'\\1\end{pmatrix}\sim\ \underbrace{\underbrace{\begin{pmatrix}f&0&x'_0\\0&f&y'_0\\0&0&-1\end{pmatrix}}_{= K\in\mathbb{R}^{3\times3}}\underbrace{\begin{pmatrix}r_{11}&r_{21}&r_{31}&-\tilde{x}_0\\r_{12}&r_{22}&r_{32}&-\tilde{y}_0\\r_{13}&r_{23}&r_{33}&-\tilde{z}_0\end{pmatrix}}_{=(R^t|-R^tN)\in\mathbb{R}^{3\times 4}}}_{\textrm{Alle Kameraparameter (Kameramatrix)}}\begin{pmatrix}x\\y\\z\\1\end{pmatrix}$$

$K$ entspricht den Intrinsischen Kameraparametern (Kamerakalibrierungs Matrix).

$(R^t|-R^tN)$ entspricht den extrinsischen Kameraparametern. 

Jeder Punkt des 3D Objekts $(x,y,z)^t$ liefert genau einen Bildpunkt $(x', y')^t$

$$x' = x'_0-f\frac{r_{11}(x-x_0)+r_{21}(y-y_0)+r_{31}(z-z_0)}{r_{13}(x-x_0)+r_{23}(y-y_0)+r_{33}(z-z_0)},$$
$$y' = y'_0-f\frac{r_{12}(x-x_0)+r_{22}(y-y_0)+r_{32}(z-z_0)}{r_{13}(x-x_0)+r_{23}(y-y_0)+r_{33}(z-z_0)}.$$

Für die allgemeine perspektivische Projektion mit 

- Translation des Center of Projection $N = (x_0, y_0, z_0)^t$
- Translation des Image Principal Points $H = (x'_0, y'_0)^t$
- und der Rotation des Kamerasystems mit $R = (r_{ij}) = M_b(\alpha)\in\mathbb{R}^{3\times 3}$
  d.h. $R^t \cdot N = (\tilde{x}_0, \tilde{y}_0, \tilde{z}_0)^t$

Existieren drei äquivalente Versionen
- Affine Version
- Homogene Version
- Explizite Version

### Räumliche Rekonstruktion aus perspektivischer Projektion

Jeder Objektpunkt $(x,y,z)^t$ liefert genau einen Bildpunkt $(x',y')^t$ gemäß:

$$\begin{pmatrix}x'\\y'\end{pmatrix}=\begin{pmatrix}x'_0\\y'_0\end{pmatrix}-\frac{f}{z_c}\begin{pmatrix}x_c\\y_c\end{pmatrix}\quad\textrm{mit}\quad \begin{pmatrix}x_c\\y_c\\z_c\end{pmatrix} = R^t \left(\begin{pmatrix}x\\y\\z\end{pmatrix}-N\right)\quad \textrm{falls}\quad z_c \neq 0$$

Auflösen der Folgenden Gleichungen nach $x, y, z$

$$x' = x'_0-(z-z_0)\frac{r_{11}(x-x_0)+r_{21}(y-y_0)+r_{31}(z-z_0)}{r_{13}(x-x_0)+r_{23}(y-y_0)+r_{33}(z-z_0)},$$
$$y' = y'_0+(z-z_0)\frac{r_{12}(x-x_0)+r_{22}(y-y_0)+r_{32}(z-z_0)}{r_{13}(x-x_0)+r_{23}(y-y_0)+r_{33}(z-z_0)}.$$

Jeder Bildpunkt $(x', y')^t$ korrespondiert mit unendlich vielen Objektpunkten

Ein einzelnes Bild reicht nicht aus um ein räumliches Objekt zu rekonstruieren.

Für die räumliche Rekonstruktion werden mehrere korrespondierende Punkte benötigt (vorrausgesetzt die Kameraparameter sind bekannt), d.h. 3D Objektpunkte die in mehreren 2D Bildern aus unterschiedlichen perspektiven zu sehen sind.

![[Pasted image 20240512081116.png]]

Ein Objektpunkt $P=(x,y,z)^t$ welcher in zwei verschiedenen Bildpunkten $P_1' = (x_1', y_1')^t$ und $P'_2 = (x_2', y_2')^t$ abgebildet wird, liefert:

- 4 Gleichungen (siehe oben), die 3 Unbekannte $(x,y,z)$ beinhalten

Vorraussetzung ist eine gute Kalibrierung, um alle Kameraparameter zu bestimmen.

#### Kalibrierung

Alle Methoden, die dazu dienen die unbekannten Kameraparameter zu bestimmen, werden *Kalibrierung* genannt.

Typischerweise werden Referenzpunkte (*ground truth points*) auf einem Kalibirierungsobjekt verwendet.
- Es handelt sich dabei um Punkte deren Bild- und Objektkoordinaten bekannt sind.

Kalibrierungsgleichungen:

$$x = x_0 + (z - z_0) \frac{r_{11}(x'-x'_0)+r_{12}(y'-y'_0)-r_{13}f}{r_{31}(x'-x'_0)+r_{32}(y'-y'_0)-r_{33}f}$$
$$y = y_0 + (z-z_0)\frac{r_{21}(x'-x_0')+r_{22}(y'-y'_0)-r_{23}f}{r_{31}(x'-x'_0)+r_{32}(y'-y_0')-r_{33}f}$$

Jeder Referenzpunkt resultiert in zwei Gleichungen

Um alle 9 Kameraparameter zu bestimmen, werden mindestens 5 Referenzpunkte benötigt.
- Falls nur die Orientierung von Interesse ist, reichen auch zwei Referenzpunkte

Einige Probleme:
- Verrauschte Messungen
- Falsche Korrespondenzen (Übereinstimmungen)
- Physik realer Kameras
	- Schwache Lichtintensität von Pinhole Kameras
		- Verwenden Linsen um Licht einzufangen
		- Linsenverzerrungen
	- Refraktionen an Materialübergängen mit unterschiedlichen Refraktionsindizes
		- Abhängig von der Wellenlänge
	- Rasterisierung der Bildebene in Pixeln, damit begrenzte Genauigkeit
- Auswahl von möglichst simplen Referenzpunkten (Kalibrierungsobjekten)

### Zentralprojektion planarer Objekte

Wähle das Objektkoordinatensystem so, dass planare Objekte in der $xy$-Ebene liegen, d.h. $z = 0$

Die Kalibrierungsgleichungen 

$$x = x_0 + (z - z_0) \frac{r_{11}(x'-x'_0)+r_{12}(y'-y'_0)-r_{13}f}{r_{31}(x'-x'_0)+r_{32}(y'-y'_0)-r_{33}f}$$
$$y = y_0 + (z-z_0)\frac{r_{21}(x'-x_0')+r_{22}(y'-y'_0)-r_{23}f}{r_{31}(x'-x'_0)+r_{32}(y'-y_0')-r_{33}f}$$

Vereinfachen sich dann zu:

$$x = \frac{a_1x'+a_2y'+a_3}{c_1x'+c_2y'+1}$$
$$y = \frac{b_1x'+b_2y'+b_3}{c_1x'+c_2y'+1}$$

mit bspw. 

$$a_1 = \frac{z_0r{11}-x_0r{31}}{r_{33}f}$$
$a_2, a_3$ analog

**Rekonstruktion**
Ein Bild ist ausreichend für die Rekonstruktion eines solchen planaren Kalibrierungsobjekts

**Kalibrierung**
Die Zentralprojektion eines planaren Objekts wird durch 8 Parameter bestimmt:

- Dafür werden $n\geq 4$ Referenzpunkte benötigt
- Jeder Referenzpunkt $(x_i, y_i,0)^t,(x_i',y_i')^t, i = 1,\dots,n$ resultiert in zwei linearen Gleichungen (Multiplikation mit Nenner)
  
  $x_i = x_i'a_1+y_i'a_2+a_3-x_ix_i'c_1 - x_iy'_ic_2$
  $y_i = x_i'b_1+y_i'b_2+b_3-y_ix_i'c1-y_iy_i'c_2.$
  
  oder in Matrixdarstellung:

$$\begin{pmatrix}x'1&y_1'&1&0&0&0&-x_1x_1'&-x_1y_1'\\
0&0&0&x_1'&y_1'&1&-y_1x_1'&-y_1y_1'\\
x'_2&y_2'&1&0&0&0&-x_2x_2'&-x_2y_2'\\\vdots&\vdots&\vdots&\vdots&\vdots&\vdots&\vdots&\vdots\\x'n&y'_n&1&0&0&0&-x_nx_n'&-x_ny_n'\\0&0&0&x_n'&y_n'&1&-y_ny_n'&-y_ny_n'\end{pmatrix} \cdot \begin{pmatrix}a_1\\a_2\\a_3\\b_1\\b_2\\b_3\\c_1\\c_2\end{pmatrix}=\begin{pmatrix}x_1\\y_1\\x_2\\y_2\\\vdots\\x_n\\y_n\end{pmatrix}$$

kurz: $M\cdot \vec{a} = \vec{x}$

Die unbekannten Parameter werden durch $\vec{a}=M^{-1}\vec{x}$ bestimmt

Da $M$ überbestimmt ist, existiert im allgemeinen keine inverse Matrix dafür
- Die Lösung erfolgt über least square Methode
- singular value decomposition (SVD)

### Physik von Kameraprojektionen

Optik ist ein Teilbereich der Physik, welcher sich mit den Eigenschaften von Licht und dessen Interaktionen mit anderen physikalischen Materialien befasst.

- Es existieren verschiedene Modelle um unterschiedliche Phänomene des Lichts zu beschreiben, bspw.
	- Lichtstrahlen (geometrische Optik)
	- Elektromagnetische Wellen/Strahlung (Wellen bzw. physikalische Optik)
	- Elektromangnetischer Energietransport (Photogrammetrie bzw. Radiometrie)
	- Photonen (Quantendynamik)
In der geometrischen Optik, wird Licht als Lichtstrahlen angenommen um die Ausbreitung des Lichts zu approximieren

In der Computervision beschränkt man sich häufig auf die Paraxial Optik, wo die Winkel der Lichtstrahlen in Bezug auf die Optische Achse relativ klein sind.

**Reflektion und Refraktion**

**Reflektion** tritt an Grenzflächen, nichtdurchsichtiger Materialien auf, bei denen der auftreffende Lichtstrahl am Schnittpunkt $p$ reflektiert wird und mit einem Winkel $\alpha_1 = \alpha_1'$ in Bezug auf die Oberflächennormale $N$ fortgesetzt wird.

**Refraktion** tritt an Grenzflächen mit durchsichtigen oder halbdurchlässigen Materialien auf, bei denen der auftreffende Lichtstrahl das Objekt passiert und mit einem Winkel $\alpha_2$ im Bezug auf die Oberflächennormale $N$ mit
$n_1\cdot \sin(\alpha_1) = n_2\cdot\sin(\alpha_2)$ 
wobei $n_1<n_2$ die Refraktionsindizes sind, fortgesetzt wird.

(In der Paraxialen-Optik gilt: $n_1\alpha_1=n_2\alpha_2)$

Wichtiger Hinweis:
Beide Phänomene sind planar, d.h. sie treten in einer durch den eintreffenden lLchtstrahl und der Oberflächennormale aufgespannten Ebene auf.

![[Pasted image 20240512112324.png]]


**Lichtintensität**

Pinhole Kameras erzeugen geringe Lichtintensitäten, da das Licht an einem einzelnen Punkt auf der Bildebene aus einem sehr kleinen Raumkegel stammt.

In der Praxis werden Linsen verwendet, welche parallele Strahlen bzw. mehrere Strahlen von individuellen Objekten auf einen einzelnen Bildpunkt abbilden.

> Die Lichtintensität im Bildpunkt wird dadurch erhöht

**Linsen Eigenschaften**

![[Pasted image 20240512120122.png]]

- Optische Achse: Symmetrieachse der Linse
- Brennpunkt: Alle zur optischen Achse parallel verlaufenden Strahlen schneiden sich im Brennpunkt $F'$ in der Bildseite der Linse
- Hauptebenen: Eingehende und ausgehende Strahlen schneiden sich in den Hauptebenen der Linse (einmal auf der Objektseite $p$ und der Bildseite $p'$)
- Hauptpunkte: Schnittpunkte $P,P'$ der Hauptebenen mit der optischen Achse
- Brennweite: Die Distanz zwischen dem Hauptpunkt der Bildseite und dem Brennpunkt der Bildseite wird Brennweite genannt $f'$


**Konstruktion eines optischen Pfads**: Ein Strahl vom Objekt, parallel zur optischen Achse, wird an der Hauptebene der Bildseite refraktiert, so dass der Strahl den Brennpunkt $F'$ passiert.

Anmerkung: Es handelt sich lediglich um eine Approximation der tatsächlichen physikalischen Vorgänge (da einfach zu berechnen)

**Chromatische Aberration (Farbfehler)**: Der Refraktionsindex ist abhängig von der Wellenlänge.
Die Brennweite ist ebenfalls von der Wellenlänge Abhängig.

![[Pasted image 20240512124232.png]]

**Dünne Linsen**: Bei dünnen Linsen fallen die Haupebenen annähernd zusammen.

In diesem Fall, vereinfachen sich die Linsengleichungen zu:

$$\frac{1}{d}+\frac{1}{d'} = \frac{1}{f'}$$
wobei $d$ der Abstand zum Objekt und $d'$ der Abstand zum Bild ist.

![[Pasted image 20240512124735.png]]

**Knotenpunkt**: Strahlen welche durch den Hauptpunkt verlaufen, passieren die Linse ohne Refraktion

Der Linsenhauptpunkt entspricht dem Knotenpunkt

**Nachteile im Vergleich zur Pinhole Kamera**:
Für unterschiedlich weit entfernte Objekte muss der Bildabstand, bzw. der Refraktionsindex der Linse angepasst werden.

Die Tiefe des Bildbereichs ist limitiert.


### Fragen

**Was ist ein kartesisches Koordinatensystem?**
- Ein orthonormales + rechtshändisch orientiertes Koordinatensystem

**Wie werden Translationen, Rotationen und Skalierungen in 2D und 3D dargestellt?**
- Über (homogene) Transformationsmatrizen, im Falle der Rotation in 3D, kann es sich auch um eine konkatenation von einzelnen Rotationsmatrizen um die Koordinatenachsen handeln.

**Was ist eine Ähnlichkeitstransformation?**
- Es handelt sich um eine Transformation vom Typ:
  $P' = s\cdot R\cdot P + T$
  Wobei $s$ ein uniformer Skalierungsfaktor, $R$ eine Rotation und $T$ eine Translation ist.
  
  Längen, Winkel, Orientierung und parallele Linien bleiben bei dieser Transformation erhalten. (Rechteck -> skaliertes, rotiertes & verschobenes Rechteck)

**Was ist eine Starrkörperbewegung**?
- Es handelt sich um eine Transformation vom Typ:
  $P' = A\cdot P + T$
  Wobei $A$ eine orthogonal Transformation ist.
  Winkel, Längen und parallele Linien bleiben erhalten. Falls die Orientierung sich ändert, falls $det(A) < 0$, sprechen wir von *improper rigid body motion*

**Was sind homogene Koordinaten?**
- Homogene Koordinaten erlauben es uns Translationen und Rotationen in einer Transformationsmatrix zusammenzufassen. Hierzu wird die Dimension um 1 erhöht, und die involvierten Vektoren und Matrizen um eine Komponente $w$ ergänzt, $w = 1$ nach Konvention (kein Zwang)

**Was ist eine Perspektivische Projektion?**
- Es handelt sich um einen Projektionstyp bei dem die Projektion durch ein Center of Projection verläuft (reales Beispiel Pinhole Kamera). Wir unterscheiden 1-Punkt, 2-Punkt und 3-Punkt Projektionen.

**Was ist eine Parallele Projektion?**
- Es handelt sich um einen Projektionstyp bei dem die Projektionsstrahlen (annähernd) parallel (d.h. Fluchtpunkt $\infty$) auf die Bildebene treffen (reales Beispiel Collimatoren). Weniger realistische Darstellung dafür präzise abmessungen möglich.

**Was sind die paramter einer Perspektivischen Projektion?**
- 




# Kapitel 3: Datenerfassung

### Übersicht

Es gibt verschiedene Methoden der Datenerfassung bzw. Aufnahme, welche sich anhand ihrer Eigenschaften in verschiedene Kategorien einteilen lassen. Und abhängig vom Einsatzgebiet ausgewählt werden.

Oft werden die unten dargestellten Verfahren in Kombination verwendet.

Hier eine Übersicht über gängige Verfahren der Datenerfassung:

![[Pasted image 20240525092745.png]]

### 3D Datenerfassung

Die 3D Datenerfassung folgt oft einem 2 Stufenansatz:

- Lokalisierung des Sensors
- Lokalisierung der 3D Daten relativ zum Sensor

### Beispiele für 3D Datenerfassung

#### FARO Laserscanner

![[Pasted image 20240525094027.png]]

##### Verfahren
Kombination aus:
- CMM
- Lasertriangulation

![[Pasted image 20240525094122.png]]

#### Arrac Sys 3D Scanner

![[Pasted image 20240525094212.png]]


##### Verfahren
Kombination aus:
- Infrarot Tracker
- Laser Triangulation

![[Pasted image 20240525100236.png]]

#### Microsoft Hololens

![[Pasted image 20240525100036.png]]

##### Extras:
- 2 RGB Video
- 4 Mikrophone
- Ambient Light Sensoren

##### Verfahren:
Kombination aus:
- Accelerometer, Gyroskop, Magnetometer
- 2 ToF Kameras

![[Pasted image 20240525100219.png]]

#### Ultraschall

![[Pasted image 20240525100619.png]]

##### Verfahren
Kombination aus:
- Mehreren Ultraschall-Messungen

Analog für CT, MRI, etc.

![[Pasted image 20240525101757.png]]

#### MRI (Magnetic Resonance Imaging / Magnetresonanztomografie)

![[Pasted image 20240525102010.png]]

![[Pasted image 20240525102027.png]]

![[Pasted image 20240525102050.png]]

![[Pasted image 20240525102118.png]]

#### Kamerasensorik Katamaran

![[Pasted image 20240525102728.png]]

##### Verfahren

Kombination aus:
- Zwei Stereo Kameras
- LIDAR
- IMU + GPS
- Radar (derzeit erforscht)

![[Pasted image 20240525103354.png]]

### Stereo Vision

#### Grundlagen

Stereosicht und Tiefenwahrnehmung basieren auf
- den Unterschieden zwischen zwei Bildern aus unterschiedlichen Perspektiven (bspw. linkes/rechtes Auge)
- der daraus resultierenden Parallaxe

**Parallaxe**: Ist die Positionsveränderung eines Objekts, betrachtet aus unterschiedlichen Perspektiven (bsp. Finger auf Nasenspitze, linkes Auge - rechtes Auge)
- Unterschiedliche Bildkoordinaten aus identischen Weltkoordinaten eines Objektes
- Unterschiedliche Kamerakoordinaten aus identischen Weltkoordinaten eines Objektes

Beide Bilder zusammen bilden ein *Stereogramm* und die individuellen Einzelbilder werden dann Halbbilder genannt.

##### Abweichungen

Als Abweichungen bezeichnen wir die Unterschiede in zwei oder mehr Bildern ein und desselben Objekts.

1. **Punktabweichung** - Horizontale und Vertikale Abweichung
	- Horizontale Abweichung bspw. im Normalfall 
	- Vertikale Abweichung, bspw. wenn die Viewdirections nicht perfekt Co-Planar ausgerichtet sind.
	![[Pasted image 20240526180029.png]]
	
2. **Abweichung der Orientierung**, allgemeine Form und Größenabweichungen zwischen den (beiden) Bildern
	- Führt immer auch zu Punktabweichungen 
	![[Pasted image 20240526180115.png]]

3. **Grauwert und Shading Abweichung** wird durch unterschiedliche Normalen der Objektpunkte in diffusen Reflektionen in den Bildern hervorgerufen.
   ![[Pasted image 20240526180250.png]]

4. **Photometrische Abweichung** wird durch Oberflächenreflektionen (Specular Reflection) hervorgerufen.
	- Highlights treten an unterschiedlichen Positionen in den jeweiligen Bildern auf
	![[Pasted image 20240526180433.png]]

5. **Monokulare Okklusionen an Objektkanten**
   - Schwer für Stereo Algorithmen.
    ![[Pasted image 20240526180649.png]]


Wichtig für die Rekonstruktion ist die Information über die relative Position und Orientierung beider Kameras:
- Die extrinsichen Kameraparameter unterscheiden sich in Kamerarichtung/Kameraorientierung und dem Center of Projection
- Die intrinsischen Kameraparameter sind typischerweise identisch und beinhalten die *focal length* (Brennweite) und *image principal point* 

**Anmerkung**: Die Kamerakalibrierung muss sehr genau sein, da bereits kleine Kalibrierungsfehler zu großen Fehlern in der Rekonstruktion führen.

##### Stereoskopische Geometrie

Die Skereoskopische Geometrie unterscheidet sich abhängig von der Ausrichtung der Kameraachsen zueinander.

- Parallele Kameraachsen, sogenannter Normalfall
- Konvergierende bzw. divergierende Kameraachsen

Im folgenden wird aus Gründen der Einfachheit nur der stereoskopische Normalfall betrachtet


#### Normalfall

**Eingabe**: Zwei korrespondierende Bildpunkte $P_1'$ und $P_2'$ desselben Objektpunktes $P$, von zwei *Halbbildern* welche eine Überlappung von ca. 60% aufweisen

**Ausgabe:** Eine Rekonstruktion des Objekts von korrespondierenden Bildpunkten $P_1'$, $P_2'$ 

**Annahmen:**
- intrinsische Kameraparameter $f, H$ 
- extrinsische Kameraparameter $R,N$
- Die relativen Kamerapositionen sind bekannt.

![[Pasted image 20240526182311.png]]

**Notation:** Index 1 bezeichnet Größen im ersten bzw. linken *Halbbild*, Index 2 bezeichnet Größen im zweiten bzw. rechten *Halbbild*

**Normalfall:** Die Rekonstruktion eines 3D Objekts wird besonders einfach, falls folgende Beziehungen gegeben sind.
- $N_i = O_i, H_i = O_i', i=1,2$ und
- Beide View direction Vektoren rechtwinklig zur *Baseline* in x-Richtung verlaufen. (Die Baseline ist die Linie die die jeweiligen Center of Projections der einzelnen Kameras miteinander verbindet)
- einen Abstand $b$ (auch base length genannt) haben und
- parallel zueinander verlaufen

![[Pasted image 20240526183321.png]]

- $N_1 = (0,0,0)^t$,
- $N_2=(b,0,0)^t,$
- $H_1 = H_2 = (0,0)^t$
- $R_1 = R_2 = I$,
- $f_1 = f_2 = f$

##### Räumlicher Vorwärtsschritt (Spatial forward step):
Die allgemeine räumliche Konstruktion , ausgedrückt durch

$$x = x_0 + (z-z_0) \frac{r_{11}(x'-x_0')+r_{12}(y'-y_0')-r_{13}f}{r_{31}(x'-x_0')+r_{32}(y'-y_0')-r_{33}f}$$
$$y=y_0+(z-z_0) \frac{r_{21}(x'-x'_0) + r_{22} (y'-y'_0)-r_{23}f}{r_{31}(x'-x'_0)+r_{32}(y'-y'0)-r_{33}f}$$
Vereinfacht sich im Normalfall mit:
- $N_1 = (0,0,0)^t$
- $N_2 = (b,0,0)^t$
- $H_1 = H_2 = (0,0)^t$
- $R_1 = R_2 = I$
- $f_1 = f_2 = f$

Zu:

*linkes Bild:*

$$x = -z\frac{x_1'}{f},\quad y = -z\frac{y_1'}{f}$$
*rechtes Bild*:
$$x = b-z\frac{x'_2}{f},\quad y= -z\frac{y_2'}{f}$$

Der Punkt $P = (x,y,z)^t$ im Raum korrespondiert mit den zwei Bildpunkten $P_i' =(x_i', y_i'), i = 1,2$ mit der selben $y'$-Koordinate
- Es existiert keine $y'$ Parallaxe
- Es existiert nur eine $x'$ Parallaxe $p_{x'} = x_1' - x_2'$


Die Korrespondenz eines Bildes eines Punktes im linken Halbbild ist in der selben Zeile im rechten Halbbild

Dies vereinfacht die Suche der korrespondierenden Punkte

Gleichsetzen der $x$-Koordinaten der beiden Bildpunkte liefert:
$$-z\frac{x_1'}{f} = b-z\frac{x_2'}{f}$$
und damit:
- $z=-f\cdot \frac{b}{x'_1-x_2'} = -f\frac{b}{p_x}$, mit $p_{x'} = x_1'-x_2'$ ($x'$ Parallaxe)
- $y = -z\frac{y_1'}{f} = -z\frac{y_2'}{f}$ (zur Kontrolle)
- x = $-z\frac{x'_1}{f}$

Je größer die Parallaxe, desto näher ist der Punkt an der Kamera

#### Fehleranalyse des Normalfalls

In der Stereorekonstruktion werden die räumlichen Positionen indirekt aus den 2D-Bildpositionen $x_1', y_1'$ und der parallaxe $p_{x'}$ ermittelt.

Fehler in den 2D Bildpositionen verursachen Fehler in der berechneten räumlichen Rekonstruktion

Mit der Gausschen Fehlerfortpflanzung können wir die Fehlerfortpflanzung eines Fehlers in den Bildpositionen auf die räumliche Rekonstruktion ermitteln.

Die Varianz $\sigma_v$ einer Größe $v = F(u_1, \dots, u_n)$, berechnet aus den Fehlerhaften Parametern $u_1,\dots , u_n$ ist gegeben durch:

$$\begin{align}\sigma_v^2 &= \sum_{i=1}^n\left(\frac{\partial F}{\partial u_i}\bigg|_{u_i,\dots , u_n}\cdot \sigma_{u_i}\right)^2\\ &=\left(\frac{\partial}{\partial u_1}\bigg|_{u_1,\dots,u_n}\cdot \sigma_{u_1}\right)^2+\left(\frac{\partial}{\partial u_2}\bigg|_{u_1,\dots,u_n}\cdot \sigma_{u_2}\right)^2+\cdots+\left(\frac{\partial}{\partial u_n}\bigg|_{u_1,\dots,u_n}\cdot \sigma_{u_n}\right)^2\end{align}$$

**Anmerkung:** Diese Approximation eignet sich nur für hinrechend kleine Fehler.

**Annahme:** Base length $b$ und principal distance $f$ sind genau

Anwendung der Fehlerfortpflanzung auf $z = \frac{-f\cdot b}{p_{x'}}$, $y = -z\frac{y_1'}{f}$, $x=-z\frac{x_1'}{f}$

$$\sigma_z^2 = \left(\frac{\partial z}{\partial p_{x'}}\bigg|_{p_{x'}}\cdot \sigma_{p_{x'}}\right)^2 = \left(\frac{f\cdot b}{p_{x_{x'}}^2}\right)^2\sigma_{p_{x'}}^2$$
$$\sigma_y^2 = \left(\frac{\partial y}{\partial z}\bigg|_{z,y_1'}\cdot\sigma_z\right)^2+\left(\frac{\partial y}{\partial y_1'}\bigg|_{z,y_1'}\cdot\sigma_{y_1'}\right)^2=\left(\frac{y_1'}{f}\right)\sigma_z^2+\left(\frac{z}{f}\right)^2\sigma_{y_1'}^2$$
$$\sigma_x^2 = \left(\frac{\partial y}{\partial z}\bigg|_{z,x_1'}\cdot\sigma_z\right)^2+\left(\frac{\partial y}{\partial x_1'}\bigg|_{z,x_1'}\cdot\sigma_{x_1'}\right)^2=\left(\frac{x_1'}{f}\right)\sigma_z^2+\left(\frac{z}{f}\right)^2\sigma_{x_1'}^2$$

**Allgemein**:
Der Fehler in der $z$-Koordinate wächst quadratisch mit der Distanz

**Bildskalierung**:
Die Fehler in allen drei Koordinaten wachsen proportional zur Größe des Bildes $m_B = z/f$ 

**Base Ratio**:
- Der Fehler in der $z$-Koordinate wächst umgekehrt proportional zur base ratio $m_V = b/z.$
- Die Fehler in den $x$- und $y$- Koordinaten zerfallen kaum in $m_V = b/z.$
- Für $m_V = b/z = 1$ sind alle drei Fehler ungefähr gleich.
#### Räumlicher Vorwärtsschritt

Die räumliche Rekonstruktion aus allgemeinen Spektrogrammen wird als *räumlicher Vorwärtsschritt* (spatial forward step) bezeichnet.

- Die Halbbilder müssen sich im Zielpunkt $p = (x,y,z)^t$ überlappen
  $x = x_0 + (z-z_0) \frac{r_{11}(x'-x'_0)+r_{12}(y'-y_0')-r_{13}f}{r_{31}(x'-x_0')+r_{32}(y'-y_0')-r_{33}f} = y_0+(z-z_0)\cdot k_x(x',y')$
  $y = y_0 + (z-z_0)\frac{r_{21}(x'-x_0')+r_{22}(y'-y_0')-r_{23}f}{r_{31}(x'-x'_0)+r_{32}(y'-y_0')-r_{33}f} = y_0 + (z-z_0) \cdot k_y(x',y')$    

Daraus erhalten wir vier Gleichungen (in zwei Bildern) für drei Unbekannte

Mögliche Lösungen:
- Ignoriere die dritte und vierte Gleichung, löse jedes Gleichungssystem nach $z$ auf und bilde den Durchschnitt aus beiden Lösungen.
	- Relativ ungenau, je größer die Abweichung vom Normalfall desto größer die Ungenauigkeit.
- Nichtlineare Regression:
	- Zeitaufwendige Berechnung der Korrespondenzen: epi-polar geometrie

### Laser Scanning

Es gibt zwei technische Prinzipien des Laserscannings:
- **Time of Flight (ToF)**: Ermittle die Zeit zwischen einem Laserpuls zum Zeitpunkt $t_0$ und der Sensorrückmeldung zum Zeitpunkt $t_1$: $d = \frac{t_1-t_0}{2}c$ mit $c$ als Lichtgeschwindigkeitskonstante
  ![[Pasted image 20240526211643.png]]
- **Optische Triangulation**: Ermittle die Verzerrung eines projezierten Musters
  ![[Pasted image 20240526211656.png]]

Unterschied zwischen Stereovision (links) und triangulations basierten Laserscanning-Verfahren (rechts)

![[Pasted image 20240526211853.png]]

##### Optische Triangulation

Mindestens eine Kamera + Projektor, bspw. Laserpointer, Strukturiertes licht, Lichtpunktmuster, etc.

Kamera im Ursprung $O_1$ und Projektor im Ursprung $O_2$ haben feste relative Positionen, bspw. Abstand $b$

Kamerabild des Laserpunkts bzw. Musters basiert auf der Geometrie des 3D Zielobjekts, und ändert sich gleichermaßen mit der Geometrie des 3D Zielobjekts.

![[Pasted image 20240526212557.png]]

Die Distanz zum Objektpunkt $P$ wird mittels trigonometrischen Verfahren ermittelt (Triangulation)

$$z = ||P-O_1||\cdot \sin(\varphi_1) = b\cdot \frac{\sin(\varphi_1)\sin(\varphi_2)}{\sin(\pi-\varphi_1-\varphi_2)}$$
mit $\pi = \varphi_1 + \varphi_2 + \varphi_3$

**Achtung:** Auch hier hängt die Korrektheit des Resultats wieder von der exakten Kalibrierung ab.

![[Pasted image 20240526212920.png]]

#### Fragen:

1. Nenne einige 3D Datenerfassungsbeispiele und klassifiziere sie gemäß der in diesem Kapitel vorgestellten Taxonomie
2. Was sind *Abweichung* und *Parallaxe*?
3. Was ist der Normalfall der Stereo Vision?
4. Wie lauten die Rekonstruktionsgleichungen im Normalfall der Stereo Vision?
5. Wie erfolgt die Fehlerfortpflanzung im Normalfall der Stereo Vision?
6. Was ist das Grundprinzip von ToF?
7. Was ist das Grundprinzip von optischer Triangulation (Strukturiertes Licht bzw. Lasertriangulation)?



# Kapitel 4: Datenrepräsentation

### Übersicht

#### Einführung: Die 3D Rekonstruktionspipeline

Im Falle der Datenräpresentation befinden wir uns im grün markierten Teil der 3D Rekonstruktionspipeline

![[Pasted image 20240527155402.png]]

#### Topologie vs Geometrie

**Topologie**:
Bei der Topologie handelt es sich um eine Menge von Eigenschaften eines Objekts, die sich unter Festkörpertransformationen nicht verändern.

=> Die Struktur des Models

![[Pasted image 20240527155748.png]]

Im Beispiel: Das Polygon hat drei Ecken, welche durch Kanten verbunden sind.

**Geometrie:** 
Bei der Geometrie handelt es sich um die *Instanz* der topologie durch Spezifikation der Position im Raum (Koordinaten)

=> Die Form des Modells

Im Beispiel: Die Koordinaten der Ecken

**Attribute**:
Bspw. Farbe, Normalen, Textur, Transparenz, Materialeigenschaften, etc.


Sowohl Topologie als auch Geometrie eines Objekts können sowohl explizit als auch implizit gespeichert bzw. dargestellt werden.

**explizite Darstellung der Topologie**:
- Punktmeshes, etc.
  ![[Pasted image 20240527160636.png]]

**implizite Darstellung der Topologie**:
- Grid, Spacepartitioning Techniken, etc.
  ![[Pasted image 20240527160825.png]]

**explizite Darstellung der Geometrie**:
- Punktwolken, CAD-Modelle, etc.
  ![[Pasted image 20240527160922.png]]
  
**implizite Darstellung der Geometrie**:
- Skalarfelder, Nullstellenmenge einer Funktion, etc.
  ![[Pasted image 20240527161705.png]]

**Anmerkung**: Implizite Geomterie kommt oft zusammen mit impliziter Topologie (Grid) aufgrund einer Methode namens *Marching Cubes* welche
- Simpel und einfach zu implementieren ist
- relativ robust ist

**Anmerkung:** Manchmal sind Geometrie und Topologie implizit über Attribute definiert.

- Beispiel: Iso-Linien in einem Druckfeld, auch Isobaren genannt
- Beispiel: Iso-Linien in einem Temperaturfeld, auch Isothermallinien genannt.
- Beispiel: Iso-Linien in einem Höhenfeld, auch Konturlinien genannt.
- Beispiel: Linie des größten Gradientenwerts in einem RGB-Bild, auch Kontur oder Silhouette genannt.
- Beispiel: Iso-Fläche in einem Stapel MRI-Grauwertbildern

**Dimensionalität der Geometrie:**
1.  $1.5$-dimensional (Funktion): $1d$-Funktionen
	   $f: \mathbb{R}\rightarrow \mathbb{R}, \mapsto f(x) = y$
	   
	   ![[Pasted image 20240528082330.png]]
   
2. 
   - (a) $2$-dimensional (Kurve): 1-parametrische Kurve, auch 1-Mannigfaltigkeiten genannt, eingebettet in $\mathbb{R}^2$
     $c:\mathbb{R} \rightarrow \mathbb{R}^2,t\mapsto c(t) = \begin{pmatrix}x(t)\\y(t)\end{pmatrix}$
     
     ![[Pasted image 20240528082359.png]]
     
   - (b) 2-dimensional: 2-parametrische Oberfläche eingebettet in $\mathbb{R}^2$
     
     $s:\mathbb{R}^2\rightarrow \mathbb{R}^2,(u,v)\mapsto s(u,v)=\begin{pmatrix}x(u,v)\\y(u,v)\end{pmatrix}$
     
     ![[Pasted image 20240528082925.png]]
     
   - (c) $2.5$-dimensional: (Höhenfeld): $2d$-Funktionen, Höhenfelder, 2d-Skalarfelder
     
	  $h:\mathbb{R}^2\rightarrow \mathbb{R},(x,y)\mapsto h(x,y) = z$
	  
	  ![[Pasted image 20240528085340.png]] 
3. 
   - (a) $3$-dimensional, (3D-Kurve): Raumkurve, 1-Mannigfaltigkeiten eingebettet in $\mathbb{R}^3$
     
     $c: \mathbb{R}\rightarrow\mathbb{R}^3,t\mapsto c(t) =\begin{pmatrix}x(t)\\y(t)\\z(t)\end{pmatrix}$
     
     ![[Pasted image 20240528090032.png]]
     
 - (b) $3$-dimensional: (Oberfläche): 2-parametrische Oberflächen, 2-Mannigfaltigkeiten eingebettet in $\mathbb{R}^3$
   
	$s:\mathbb{R}^2 \rightarrow \mathbb{R}^3, t\mapsto c(t) = \begin{pmatrix}x(t)\\y(t)\\z(t)\end{pmatrix}$
	
	![[Pasted image 20240528091400.png]]

 - (c)  $3$-dimensional (3D-Skalarfelder): Skalarwerte eingebettet in $\mathbb{R}^3$
  
   $S: \mathbb{R}^3\rightarrow\mathbb{R},(u,v,w)\mapsto S(u,v,w) = s$
  
   Beispiel: CT-, MRI, Ultraschall-Daten und daraus extrahierte Iso-Oberflächen.
   
 -  (d)  $3$-dimensional: $kd$-Vektorfeld eingebettet in $\mathbb{R}^3$
    $V:\mathbb{R}^3\rightarrow \mathbb{R}^k, (u,v,w)\mapsto V(u,v,w)=\begin{pmatrix}x_1(u,v,w)\\ \vdots \\ x_k(u,v,w)\end{pmatrix}$
  
    Beispiel: FEM-Simulationen, Windtunnel, etc.
  
 -  (e) $3$-dimensional: Tensorfeld eingebettet in $\mathbb{R}^3\dots$ 
  
    Beispiel: FEM-Simulationen


**Konversion**:
Die Datenerfassung liefert häufig Punktwolken, d.h. eine Diskrete Repräsentation

Allerdings ist eine kontinuierliche Datenrepräsentation oft besser für die aufbauenden Pipelineschritte (Post-Processing)

Konversion einer Punktwolkenrepräsentation in eine kontinuierliche Repräsentation:
- **(Scattered data) Interpolation/Approximation**: $1.5d$-Punktwolken in eine Funktion oder Polygon 
- **Kurven-interpolation/-approximation**: $2d$-Punktsequenz zu einer parametrischen Kurve oder einem Polygon
- **Scattered data - Interpolation/-Approximation**: $2.5d$-Punktwolken zu $2d$-Funktionen
- **Oberflächenrekonstruktion**: $3d$-Punktwolke zu Parametrischen Oberflächen
- **Punktwolken Triangulation**: $3d$-Punktwolke zu Mesh
  
### Punktwolken: Datenstrukturen

#### Grids

#### Quad- und Oct-Trees

#### kd-Trees

#### BSP-Trees

### Meshdatenstrukturen

#### Mesh: Grundlagen

#### Halbkanten Datenstrukturen
