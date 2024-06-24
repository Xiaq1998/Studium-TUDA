# Software-Engineering - Wartung und Qualitätssicherung

## 1. Software-Entwicklung, -Wartung und (Re-)Engineering

### 1.1 Einleitung

**Hauptgründe für Scheitern von Projekten:** Unklare Anforderungen und Abhängigkeiten sowie Probleme beim Änderungsmanagement. 不明确的需求和依赖关系以及变更管理问题。



### 1.2 Software-Qualität

**Qualitätsmerkmale gemäß 质量特征符合:** Funktionalität (Functionality) 

**Nichtfunktionale Merkmale:** 非功能性特征

+ Zuverlässigkeit (Reliability) 可靠性
+ Benutzbarkeit (Usability) 可用性
+ Effizienz (Efficiency) 效率
+ Änderbarkeit (Maintainability) 可变性
+ Übertragbarkeit (Portability) 便携性

**Prinzipien 原则 der Qualitätssicherung:**

+ **Qualitätszielbestimmung 确定质量目标:** Auftraggeber und Auftragnehmer legen vor Beginn der Software-Entwicklung gemeinsames Qualitätsziel für Software-System mit nachprüfbarem Kriterienkatalog 标准目录 fest (als Bestandteil des abgeschlossenen Vertrags zur Software-Entwicklung)
+ **quantitative 定量 Qualitätssicherung:** Einsatz automatisch ermittelbarer Metriken zur Qualitätsbestimmung 使用自动确定的指标来确定质量 (objektivierbare, ingenieurmäßige Vorgehenqweise)
+ **konstruktive Qualitätssicherung 建设性的质量保证:** Verwendung geeigneter Methoden, Sprachen und Werkzeuge (Vermeidung von Qualitätsprobleme)
+ **integrierte 集成的, frühzeitige analytische Qualitätssicherung:** systematische Prüfung aller erzeugten Dokumente (Aufdeckung von Qualitätsproblemen)
+ **unabhängige Qualitätssicherung:** Entwicklungsprodukte werden durch eigenständigen Qualitätssicherungsabteilung überprüft und abgenommen (verhindert u.a. Verzicht auf Testen zugunsten Einhaltung des Entwicklungszeitplans)

**Konstruktives Qualitätsmanagement zur Fehlervermeidung:**

+ technische Maßnahmen: 
  + Sprachen
  + Werkzeuge
+ organisatorische Maßnahmen:
  + Richtlinien
  + Standards
  + Checklisten

**Analytisches Qualitätsmanagement zur Fehleridentifikation:**

+ **analysierende Verfahren:** der "Prüfling" (Programm, Modell, Dokumentation) wird von Menschen oder Werkzeugen auf Vorhandensein/Abwesenheit von Eigenschaften untersucht.
  + Review
  + statische Analyse
  + (formale) Verifikation
+ **testende Verfahren:** der "Prüfling" wird mit konkreten 具体的 oder abstrakten 抽象的 Eingabewerten 输入值 auf einem Rechner ausgeführt.
  + dynamischer Test
  + symbolischer Test



### 1.3 Iterative Softwareentwicklung

**Die Phasen des Wasserfallmodells 瀑布模型 im Überblick (nach Royce):**

![Screenshot_2024-06-06 21.10.19_p4vnn2](/Users/summer/Pictures/截屏/Screenshot_2024-06-06 21.10.19_p4vnn2.jpg)

+ **Machbarkeitsstudie (feasibility study) 可行性研究**
  + Die Machbarkeitsstudie schätz ==Kosten und Ertrag der geplanten Software-Entwicklung== ab. Dazu grobe Analyse des Problems mit Lösungsvorschlägen.
  + Aufgaben:
    + Problem informell und abstrahiert beschreiben
    + verschiedene Lösungsansätze erarbeiten
    + Kostenschätzung durchführen
    + Angebotserstellung
  + Ergebnisse:
    + Lastenheft需求规范
    + Projektalkulation 项目成本核算
    + Projektplan 
    + Angebot an Auftraggeber
+ **Anforderungsanalyse (requirements engineering) 需求分析**
  + In der Anforderungsanalyse wird exakt 确切的 festgelegt, ==was die Software leisten soll==, aber nicht wie diese Leistungsmerkmale 性能特征 erreicht werden.
  + Aufgaben:
    + genaue Festlegung der Systemeigenschaften wie Funktionalität, Leistung, Benutzungsschnittstelle, ... im Pflichtenheft
    + Bestimmen von Testfällen
    + Festlegung erforderlicher Dokumentationsdokumente
  + Ergebnisse:
    + Pflichtenheft = Anforderungsanalysedokument
    + Akzeptanztestplan
    + Benutzungshandbuch
+ **Systementwurf (system design/programming-in-the-large) 系统设计:**
  + Im Systementwurf wird exakt festgelegt, wie die Funktionen der Software zu realisieren sind. Es wird der ==Bauplan der Software==, die Software-Architektur, entwickelt.
  + Aufgaben:
    + Programmieren-im-Großen = Entwicklung eines Bauplans
    + Grobentwurf, der System in Teilsysteme-Module zerlegt
    + Auswahl bereits existierender Software-Bibliotheken, Rahmenwerke, ...
    + Feinentwurf, der Modulschnittstellen und Algorithmen vorgibt
  + Ergebnisse:
    + Entwurfsdokument mit Software-Bauplan
    + detailierte(re) Testpläne
+ **Codieren und Modultest (programming-in-the-small) 编码和单元测试:**
  + Die eigentliche ==Implementierungs- und Testphase==, in der einzelne Module (in einer bestimmten Reihenfolge) realisiert und validiert werden.
  + Aufgaben:
    + Programmieren-im-Kleinen = Implementierung einzelner Module
    + Einhaltung von Programmierrichtlinien
    + Code-Inspektionen kritischer Modulteile (Walkthroughs)
    + Test der erstellten Module
  + Ergebnisse:
    + Menge realisierter Module
    + Implementierungsberichte
    + technische Dokumentation einzelner Module
    + Testprotokolle
+ **Integration und Systemtest 集成和系统测试:**
  + Die einzelnen Module werden schrittweise zum ==Gesamtsystem zusammengebaut==. Diese Phase kann mit vorigen Phase verschmolzen werden, falls der Test isoliertenr Module nicht praktikabel ist.
  + Aufgaben:
    + Systemintegration = Zusammenbau der Module
    + Gesamtsystemtest in Entwicklungsorganisation durch Kunden
    + Fertigstellung der Dokumentation
  + Ergebnisse:
    + fertiges System
    + Benutzerhandbuch
    + technische Dokumentation
    + Testprotokolle
+ **Auslieferung und Installation 送货及安装:**
  + Die Auslieferung (Installation) und Inbetriebnahme der Software beim Kunden findet häufig in zwei Phasen statt.
  + Aufgaben:
    + Auslieferung an ausgewählte (Pilot-)Benutzer
    + Auslieferung an alle Benutzer
    + Schulung der Benutzer
  + Ergebnisse:
    + fertiges System 
    + Akzeptanztestdokument
+ **Wartung (Maintenance)维护:**
  + Nach der ersten Auslieferung der Software an die Kunden beginnt das Elend der Software-Wartung, das ca. 60% der gesamten Software-Kosten ausmacht.
  + Aufgaben:
    + ca. 20% Fehler beheben
    + ca. 20% Anpassungen durchühren
    + ca. 50% Verbesserungen vornehmen
  + Ergebnisse:
    + Software-Problemberichte
    + Software-Änderungsvorschläge
    + neue Software-Versionen

**Einfaches Software-Lebenszyklus-Prozessmodell für die Wartung**

![Screenshot_2024-06-07 19.31.27_APyxiH](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 19.31.27_APyxiH.jpg)

**Das V-Modell (Standard der Bundeswehr bzw. aller Bundesbehörden)**

![Screenshot_2024-06-07 19.38.44_yrqtDQ](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 19.38.44_yrqtDQ.jpg)

* **Systemanforderungsanalyse 系统需求分析:** Gesamtsystem einschließlich aller Nicht-DV-Komponenten wird beschrieben (fachliche Anforderungen und Risikoanalyse)
* **Systementwurf 系统设计:** System wird in technische Komponenten (Subsysteme) zerlegt, also die Grobarchitektur 粗略架构 des Systems definiert
* **Softwareanforderungsanalyse 软件需求分析:** technische Anforderungen an die bereits identifizierten Komponenten werden definiert
* **Softwaregrobentwurf 软件粗略设计:** Softwarearchitektur wird bis auf Modulebene festgelegt
* **Softwarefeinentwurf 详细软件设计:** Details einzelner Module werden festgelegt
* **Softwareimplementierung 软件实现:** wie beim Wasserfallmodell (inklusive Modultest)
* **Software-/Systemintegration 软件/系统集成:** schrittweise Integration und Test der verschiedenen Systemanteile
* **Überleitung in die Nutzung 转用:** entspricht Auslieferung bei Wasserfallmodell



### 1.4 Forward-, Reverse- und Reengineering

### 1.5 Zusammenfassung



## 2. Konfigurationsmanagement

### 2.1 Einleitung

**Definition von Software-KM nach IEEE-Standard 828-1988**

—— **SCM (Software Configuration Management) 软件配置管理** constitutes good engineering practice for all software projects, whether phased development, rapid prototyping, or ongoing maintenance. It enhances the reliability and quality of software by:

* Providing structure for ==identifying and controlling== documentation, code, interfaces, and databases to support all life cycle phases
* Supporting a chosen ==development/maintenance methodology== that fits the requirements, standards, policies, organization, and management philosophy
* Producing ==management and product information== concerning the status of baselines, change control, tests, releases, audits etc.
* Anmerkung
  + wenig konkrete Definition
  + Unabhängig von "Software"

**Definition nach DIN EN ISO 10007:**

——**"KM (Konfigurationsmanagement)" 配置管理** ist eine Managementdisziplin, die über die gesamte Entwicklungszeit eines Erzeugnisses angewandt wird, um Transparenz und Überwachung seiner funktionellen und physischen Merkmale sicherzustellen. Der KM-Prozess umfasst die folgenden integrierten Tätigkeiten:

+ **Konfigurationsidentifizierung 配置识别:** Definition und Dokumentation der Bestandteile eines Erzeugnisses, Einrichten von Bezugskonfigurationen, ...
+ **Konfigurationsüberwachung 配置监控:** Dokumentation und Begründung von Änderungen, Genehmigung oder Ablehnung von Änderungen, Plannung von Freigaben, ...
+ **Konfigurationsbuchführung 配置统计:** Rückverfolgung aller Änderungen bis zur letzten Bezugskonfiguration, ...
+ **Konfigurationsauditierung 配置审计:** Qualitätssicherungsmaßnahmen für Freigabe einer Konfiguration eines Erzeugnisses
+ **KM-Planung 配置管理规划:** Festlegung der Grundsätze und Verfahren zum KM in Form eines KM-Plans

**Werkzeugorientierte Sicht auf KM-Aktivitäten 配置管理活动的工具导向视图:**

+ **KM-Planung:** Beschreibung der Standards, Verfahren und Werkzeuge, die für KM ventzt werden; wer darf/muss wann was machen
+ **Versionmanagement:** Verwaltung der Entwicklungsgeschichte eines Produkts; also wer hat wann, wo, was und warum geändert
+ **Variantenmanagement:** Verwaltung parallel existierender Ausprägungen eines Produkts für verschiedene Anforderungen, Länder, Plattformen
+ **Releasemanagement 发布管理:** Verwaltung und Planung von Auslieferungsständen; wann wird eine neue Produktversion mit welchen Features auf den Markt geworfen
+ **Änderungsmanagement:** Verwaltung von Änderungsanforderungen; also Bearbeitung von Fehlermeldungen und Änderungswünschen sowie Zuordnung zu Auslieferungsständen

**Integration 集成 des Konfigurationsmanagements im V-Modell:**

![Screenshot_2024-06-07 20.55.18_kaVgKM](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 20.55.18_kaVgKM.jpg)

**Grafische Übersicht über Aufgaben- und Rollenverteilung:**

![Screenshot_2024-06-08 00.50.18_KnVTHX](/Users/summer/Pictures/截屏/Screenshot_2024-06-08 00.50.18_KnVTHX.jpg)

**Workspaces für das Konfigurationsmanagement:**

![Screenshot_2024-06-08 00.52.13_fgNkCE](/Users/summer/Pictures/截屏/Screenshot_2024-06-08 00.52.13_fgNkCE.jpg)

+ alle Dokumente (Objekte, Komponenten) zu einem bestimmten Projekt werden in einem gemeinsamen Repository (public workspace) aufgehoben
+ im Repository 存储库 werden nicht nur aktuelle Versionen, sondern auch alle früheren Versionen aller Dokumenten gehalten
+ beteiligte Entwickler bearbeiten ihre eigenen Versionen dieser Dokumente in ihrem privaten Arbeitsbereich (private workspace, developer workspace)
+ es gibt genau einen Integrationsarbeitsbereich (integrations workspace) für die Systemintegration



### 2.2 Versionsmanagement



### 2.3 Variantenmanagement

### 2.4 Releasemanagement

### 2.6 Änderungsmanagement

### 2.7 Zusammenfassung



## 3. Statische Programmanalysen und Metriken

### 3.1 Einleitung

### 3.3 Strukturierte Gruppenprüfungen

### 3.4 Kontroll- und datenflussorientierte Analysen

### 3.5 Softwaremetriken

### 3.6 Zusammenfassung



## 4. Dynamische Programmanalysen und Testen

### 4.1 Einleitung

### 4.3 Funktionsprientierte Testverfahren

### 4.4 Kontrollflussbasierte Testverfahren

### 4.5 Datenflussbasierte Testverfahren

### 4.6 Testen objektorientierter Programme

### 4.7 Mutationsbasierte Testverfahren

### 4.8 Testmanagement und Testwerkzeuge



