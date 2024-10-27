
### Lernziele

Wissen welche Rolle Software Qualitätssicherung, insbesondere das Testen, im Softwareentwicklungsprozess spielt und kennen der wichtigsten Praktiken und Prozesse.

Kenntnis über  Methoden, Techniken und Werkzeuge für jeden Zeitpunkt in der Softwareentwicklung um die Korrektheit der Software zu überprüfen und die praktische Anwendung ebendieser.

## Abschnitt 1
### Intro

#### Software Qualität

##### Was ist Software Qualität?

*Unter Softwarequalität versteht man die Geamtheit der Merkmalswerte eines Softwareprodukts, die sich auf dessen Eignung beziehen, festgelegte oder vorausgesetzte Erfordernisse zu erfüllen*

**Soll = Ist**

#### Software Engineering

##### Was ist Softwareengineering?

Softwareengineering ist eine Ingenieursdispziplin, welche sich mit allen Aspekten der Softwareentwicklung angefangen von den frühen Stadien der Systemspezifikation bis hin zur Wartung eines in der Anwendung befindlichen System befasst.

#### Softwareprozess

##### Was ist der Softwareprozess?

Eine strukturierte Menge an Aktivitäten um ein Softwaresystem zu entwickeln

Es gibt viele verschiedene Formen von Softwareprozesse aber sie alle beinhalten

- Spezifikation
- Design und Implementierung
- Validierung
- Evolution

#### Qualitätssicherung

##### Konstruktive Qualitätssicherung

Vermeiden, dass Fehler entstehen.

##### Analytische Qualitätssicherung

Überprüfen der Software nach ihrer Fertigstellung auf Fehler.


#### Validierung und Verifikation

##### Validierung: (Bauen wir das richtige Produkt?)

Bestätigung durch Bereitstellung eines objektiven Nachweises, dass die Anforderungen für einen spezifischen beabsichtigten Gebrauch oder eine spezifische beabsichtigte Anwendung erfüllt worden sind. [ISO 9000]

##### Verifikation: (Bauen wir das Produkt richtig?)

Bestätigung durch Bereitstellung eines objektiven Nachweises, dass festgelegte Anforderungen erfüllt worden sind. [ISO 9001]


#### Vorgehensmodelle

Definieren:

- eine festgelegte Reihenfolge von Aktivitäten, um Projekte abzuarbeiten.
- definieren oft auch Rollen, Artefakte, Vor- und Nachbedingungen.

Wir unterscheiden zwischen folgenden Typen von Vorgehensmodellen:

##### Plan-Driven (z.B. V-Modell):
Alle Aktivitäten werden im vornherein geplant, und Fortschritt wird gegen diesen Plan gemessen.

![[Pasted image 20240423080803.png]]

##### Agile (z.b. SCRUM):
Die Planung wird inkrementell vollzogen, und es ist einfacher sich ändernden Anforderungen anzupassen.

![[Pasted image 20240423080924.png]]

#### Fehler

Als Fehler definieren wir:

1. Nichterfüllung einer Anforderung (EN ISO 9000:2005)
2. Abweichung zwischen Ist- und Sollverhalten

**Soll $\neq$ Ist**

#### Definitionen (1)

##### Fehlerwirkung (failure)
Beim Testen oder Benutzen der Software wird ein Fehler nach außen sichtbar.

##### Fehlerzustand (fault)
Ursache einer Fehlerwirkung (syn.: defect, bug)

##### Fehlhandlung
Die menschliche Handlung, die zu einem Fehlerzustand führt ([nach IEEE 610])

#### Testbegriff

Der Prozess der Ausführung oder Evaluation eines Systems oder einer Systemkomponente ,entweder manuell oder automatisiert, um die Erfüllung einer spezifizierten Anforderung zu verifizieren oder zur Identifikation der Abweichung von erwarteten und tatsächlichen Resultaten.

**Soll = Ist**

#### Fehler

![[Pasted image 20240423084408.png]]

**Testen ist nicht Debugging!**

##### Beispiel: Gebührenberechnung eines Campingplatz im Winter 2019/2020

**Soll:**
Der Campingplatz ist geöffnet von 01. Januar bis 29. Februar. Hochsaison (Saison B) ist vom 1. Januar bis einschließlich 5. Januar und vom 20. bis 29. Februar (jeweils einschließlich). An den anderen Daten ist Nebensaison (Saison A). Für die Standplatzpreise gilt:

![[Pasted image 20240423084923.png]]

**Ist:**
Die Methode **tagGültig** soll bestimmen, ob die Eingabedaten für die Gebürenberechnung korrekt sind, d.h. ob ein Preis für ein Datum existiert. Leider hat sich in der Implementierung ein Fehler eingeschlichen, in Zeile 1 fehlt ein Klammernpaar.

```java
public class Kalender implements IKalender {
	public boolean tagGültig(int tag, int monat) {
		if (tag == 30 || tag == 31 && monat == 2) {
			return false;
		}
		if (tag <= 0 || tag > 31) {
			return false;
		}
		if (monat < 1 || monat > 3) {
			return false;
		}
		return true;
	}
}

public interface IKalender {
	public boolean tagGültig(int tag, int monat);
}
```

**a) Für welchen Parameter liefert die  Methode fehlerhafte Werte?

-> tag = 32, monat = 2

**b) Was ist die Fehlerwirkung und und der Fehlerzustand in diesem Fall?

-> Fehlerwirkung: Falsches Datum wird ausgewertet

-> Fehlerzustand: Fehlende Klammer in Zeile 1

```java
if ((tag == 30 || tag == 31) && monat == 2)
```

#### Definitionen (2)

##### Fehlermaskierung
Die Wirkung eines Fehlers (Fehlerzustand) ist nach außen hin nicht sichtbar (keine Fehlerwirkung), weil er durch einen weiteren Fehler verborgen (überlagert / maskiert) wird.

##### Beispiel: Gebührenrechnung eines Campingplatzes im Winter 2019/2020

**Soll**:
Der Campingplatz ist geöffnet von 01. Januar bis 29. Februar. Hochsaison (Saison B) ist vom 1. Januar bis einschließlich 5. Januar und und vom 20. bis 29. Februar (jeweils einschließlich). An den anderen Daten ist Nebensaison (Saison A). Für die Standplatzpreise gilt:

![[Pasted image 20240423215913.png]]

**Ist**:
Bei einer fehlerhaften Implementierung der Methode saisonKalender.isHochSaison(), die immer `true` zurückliefert können Fehler in der Methode `berechneGebuehr()`
maskiert werden.

```java
public class Tagespreise {
	private IKalender kalender;
	private ISaisonKalender saisonKalender;

	public Tagespreise(IKalender kalender, ISaisonKalender saisonKalender) {
		this.kalender = kalender;
		this.saisonKalender = saisonKalender;
	}

	public int berechneGebuehr(int tag, int monat, Standplatz s) {
		if (!kalender.tagGültig(tag, monat)) return -1;
		if (s == null) return -1;
		boolean hochSaison = saisonKalender.istHochSaison();
		if (s.equals(Standplatz.K)) {
			return hochSaison ? 25 : 14;
		} else {
			return hochSaison ? 28 : 18;
		}
	}
}
```

(Die Methode gibt einen zu geringen Wert für einen Stellplatz in der Hochsaison zurück)

#### Zusammenfassung: Fehler

![[Pasted image 20240423222321.png]]

### Einschub: Junit 

#### xUnit

**xUnit** ist die Bezeichnung für verschiedene Frameworks für automatisierte Unit-Tests (Komponenten Test).

Das erste xUnit-Framework SUnit wurde von **Kent Beck** für die Programmiersprache Smalltalk entwickelt.

xUnit Frameworks für Java JVM sind **JUnit** und **TestNG** (oder Spock)

**NUnit** für das **.NET**-Framework, **PHPUnit** für PHP, **CppUnit** für **C++**

#### JUnit Basics

Methoden, die Unit Tests implementieren werden mit der Annotation `@Test` versehen.

Test Methoden haben `void` als Rückgabewert

Die Überprüfung der Testergebnisse wird durch die statischen Methoden der Klasse **Assert** durchgeführt, z.B.:

- assertTrue(...)
- assertEquals(...)
- assertNotEquals(...)

Die `equals/notEquals` Methoden stehen für viele Typen bereit

Wenn die Tests in einer Standardumgebung ausgeführt werden wie einer IDE (Eclipse, IntelliJ) oder einem build tool (Ant, Maven, ...) muss nicht mehr beachtet werden, alles andere erledigt die Umgebung

#### Kontext von Testen

![[Pasted image 20240424194846.png]]

Fehlerfreiheit muss aus dem beobachtbaren Verhalten geschlossen werden!

#### Best Practices: Four-Phase Test

![[Pasted image 20240424195349.png]]

#### Best Practices: Organisation des Testcodes

Trennen von Produktionscode und Testcode
- Organisisere Testklassen in eine parallele Struktur zu den Produktionsklassen aber in einem separaten Verzeichnis (Standard in Maven).
- Eine Testklasse pro Produktionsklasse
	- Manchmal nicht ausreichend, Alternative: Eine Klasse pro Anwendungsfall
- Separate Verzeichnisse
- Spiegeln der Package Struktur

#### Build und Dependency Management mit Maven

**Most Common Maven Lifecycle Phases**
- **validate**: validate the project is correct and all necessary information is available
- **compile**: compile the source code of the project
- **test:** test the compiled source code using a suitable unit testing framework. These tests should not require the code to be packaged or deployed
- **package**: take the compiled code and package it in its distributable format, such as a JAR
- **integration-test**: process and deploy the package if necessary into an environment where integration tests can be run
- **verify**: run any checks to verify the package is valid and meets quality criteria
- **install**: install the package into the local repository, for use as a dependency in other projects locally
- **deploy**: done in an integration or release environment, copies the final package to the remote repository for sharing with other developers and projects.

**Other Maven Lifecycle Phases:**
- **clean:** cleans up artifacts created by prior builds
- **site**: generates site documentation for this project

#### FIRST Principle

- Fast
- Independent
- Repeatable
- Self-validating
- Timely

### Einschub: Basiswissen Softwaretester

## Abschnitt 2

### Requirements

### Einschub: Systemkontext und Use-Cases

## Abschnitt 3

### Grundlagen Testen

### Einschub: Reviews

### Einschub: Automatisierte UI Tests

## Abschnitt 4
### Einführung in Agiles Software Development & Testing

## Abschnitt 5

## Abschnitt 6


