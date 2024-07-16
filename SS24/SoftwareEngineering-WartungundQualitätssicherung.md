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

&rarr; **Quiz:** Das Wasserfallmodell in seiner "Reinform" hat folgende Nachteile und sollte deshalb (so) nicht verwendet werden: “纯粹形式”的瀑布模型具有以下缺点：因此不应该使用（像这样）

==A) Die Anforderungen an ein Softwareprodukt werden sehr früh "eingefroren".== 软件产品的需求很早就被“冻结”了

B) Es wird zu viel Aufwand in die Erstellung von Anforderungsdokumenten investiert. 在创建需求文档上投入了太多的精力

C) Es entsteht in der Regel wenig vertrauenswürdige Software. 通常，会创建不可信的软件

==D) Für die Wartung der Software gibt es kein strukturiertes Vorgehensmodell.==  没有用于维护软件的结构化过程模型

E) In die Kommunikation mit Nutzern der Software wird zu viel Zeit investiert. 在与软件用户的沟通上投入了太多的时间

**Einfaches Software-Lebenszyklus-Prozessmodell für die Wartung**

![Screenshot_2024-06-07 19.31.27_APyxiH](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 19.31.27_APyxiH.jpg)

**Das V-Modell (Standard der Bundeswehr bzw. aller Bundesbehörden)**

![Screenshot_2024-06-07 19.38.44_yrqtDQ](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 19.38.44_yrqtDQ.jpg)

* **Systemanforderungsanalyse 系统需求分析:** Gesamtsystem einschließlich aller Nicht-DV-Komponenten wird beschrieben (fachliche Anforderungen und Risikoanalyse) 描述了包括所有非 DP 组件的整个系统（技术要求和风险分析）
* **Systementwurf 系统设计:** System wird in technische Komponenten (Subsysteme) zerlegt, also die Grobarchitektur 粗略架构 des Systems definiert
* **Softwareanforderungsanalyse 软件需求分析:** technische Anforderungen an die bereits identifizierten Komponenten werden definiert 系统被分解为技术组件（子系统），即定义了系统的粗略架构
* **Softwaregrobentwurf 软件粗略设计:** Softwarearchitektur wird bis auf Modulebene festgelegt 软件架构被定义到模块级别
* **Softwarefeinentwurf 详细软件设计:** Details einzelner Module werden festgelegt 各个模块的详细信息已确定
* **Softwareimplementierung 软件实现:** wie beim Wasserfallmodell (inklusive Modultest) 与瀑布模型一样（包括模块测试）
* **Software-/Systemintegration 软件/系统集成:** schrittweise Integration und Test der verschiedenen Systemanteile 各种系统组件的逐步集成和测试
* **Überleitung in die Nutzung 转用:** entspricht Auslieferung bei Wasserfallmodell 对应瀑布模型交付



### 1.4 Forward-, Reverse- und Reengineering

### 1.5 Zusammenfassung



## 2. Konfigurationsmanagement

### 2.1 Einleitung

**Definition von Software-KM nach IEEE-Standard 828-1988**

—— **SCM (Software Configuration Management) 软件配置管理** constitutes good engineering practice for all software projects, whether phased development, rapid prototyping, or ongoing maintenance. It enhances the reliability and quality of software by: 构成所有软件项目的良好工程实践，无论是分阶段开发、快速原型设计还是持续维护。它通过以下方式提高软件的可靠性和质量

* Providing structure for ==identifying and controlling== documentation, code, interfaces, and databases to support all life cycle phases 提供识别和控制文档、代码、接口和数据库的结构，以支持所有生命周期阶段
* Supporting a chosen ==development/maintenance methodology== that fits the requirements, standards, policies, organization, and management philosophy 支持所选的开发/维护方法，符合要求、标准、政策、组织和管理理念
* Producing ==management and product information== concerning the status of baselines, change control, tests, releases, audits etc. 生成管理和产品信息有关基线、变更控制、测试、发布、审核等状态
* Anmerkung
  + wenig konkrete Definition 很少有具体的定义
  + Unabhängig von "Software" 独立于“软件”

**Definition nach DIN EN ISO 10007:**

——**"KM (Konfigurationsmanagement)" 配置管理** ist eine Managementdisziplin, die über die gesamte Entwicklungszeit eines Erzeugnisses angewandt wird, um Transparenz und Überwachung seiner funktionellen und physischen Merkmale sicherzustellen. Der KM-Prozess umfasst die folgenden integrierten Tätigkeiten: 配置管理是一种应用于产品整个开发阶段的管理准则，以确保其功能和物理特性的透明度和监控。知识管理流程包括以下综合活动

+ **Konfigurationsidentifizierung 配置识别:** Definition und Dokumentation der Bestandteile eines Erzeugnisses, Einrichten von Bezugskonfigurationen, ... 产品组件的定义和文档、设置参考配置、...
+ **Konfigurationsüberwachung 配置监控:** Dokumentation und Begründung von Änderungen, Genehmigung oder Ablehnung von Änderungen, Plannung von Freigaben, ... 变更的记录和理由、变更的批准或拒绝、发布的规划…… 
+ **Konfigurationsbuchführung 配置统计:** Rückverfolgung aller Änderungen bis zur letzten Bezugskonfiguration, ... 跟踪直到最后一个参考配置的所有更改，...
+ **Konfigurationsauditierung 配置审计:** Qualitätssicherungsmaßnahmen für Freigabe einer Konfiguration eines Erzeugnisses 发布产品配置的质量保证措施
+ **KM-Planung 配置管理规划:** Festlegung der Grundsätze und Verfahren zum KM in Form eines KM-Plans 以知识管理计划的形式确定知识管理的原则和程序

**Werkzeugorientierte Sicht auf KM-Aktivitäten 配置管理活动的工具导向视图:**

+ **KM-Planung:** Beschreibung der Standards, Verfahren und Werkzeuge, die für KM ventzt werden; wer darf/muss wann was machen 知识管理所使用的标准、程序和工具的描述；谁可以/必须做什么以及何时
+ **Versionmanagement:** Verwaltung der Entwicklungsgeschichte eines Produkts; also wer hat wann, wo, was und warum geändert 管理产品的开发历史；即谁改变了时间、地点、内容和原因
+ **Variantenmanagement:** Verwaltung parallel existierender Ausprägungen eines Produkts für verschiedene Anforderungen, Länder, Plattformen 针对不同要求、国家、平台管理产品的并行版本
+ **Releasemanagement 发布管理:** Verwaltung und Planung von Auslieferungsständen; wann wird eine neue Produktversion mit welchen Features auf den Markt geworfen 交付状态的管理和计划；新产品版本什么时候上市，有哪些功能
+ **Änderungsmanagement:** Verwaltung von Änderungsanforderungen; also Bearbeitung von Fehlermeldungen und Änderungswünschen sowie Zuordnung zu Auslieferungsständen 管理变更请求；即处理错误消息和更改请求以及将它们分配给交付状态

**Integration des Konfigurationsmanagements im V-Modell: 配置管理在V模型中的集成**

![Screenshot_2024-06-07 20.55.18_kaVgKM](/Users/summer/Pictures/截屏/Screenshot_2024-06-07 20.55.18_kaVgKM.jpg)

**Grafische Übersicht über Aufgaben- und Rollenverteilung:**

![Screenshot_2024-06-08 00.50.18_KnVTHX](/Users/summer/Pictures/截屏/Screenshot_2024-06-08 00.50.18_KnVTHX.jpg)

**Workspaces für das Konfigurationsmanagement:**

![Screenshot_2024-06-08 00.52.13_fgNkCE](/Users/summer/Pictures/截屏/Screenshot_2024-06-08 00.52.13_fgNkCE.jpg)

+ alle Dokumente (Objekte, Komponenten) zu einem bestimmten Projekt werden in einem gemeinsamen Repository (public workspace) aufgehoben 特定项目的所有文档（对象、组件）都存储在公共存储库（公共工作区）中
+ im Repository 存储库 werden nicht nur aktuelle Versionen, sondern auch alle früheren Versionen aller Dokumenten gehalten 不仅当前版本，所有文档的所有以前版本都保存在存储库中
+ beteiligte Entwickler bearbeiten ihre eigenen Versionen dieser Dokumente in ihrem privaten Arbeitsbereich (private workspace, developer workspace) 参与的开发人员在其私有工作区（私有工作区、开发人员工作区）中编辑这些文档的自己版本
+ es gibt genau einen Integrationsarbeitsbereich (integrations workspace) für die Systemintegration 系统集成只有一个集成工作区



### 2.2 Versionsmanagement

&rarr; **Versionsmanagement 版本管理** befasst sich (in erster Linie) mit der Verwaltung der zeitlich aufeinander folgenden Revisionen eines Dokuments 版本管理（主要）涉及管理文件的连续修订

#### SCSS (Source Code Control System) von AT&T (Bell Labs)

**SCSS 源代码控制系统** 

&rarr; SCCS是一种用于管理源代码版本的系统，由AT&T Bell Labs开发

&rarr; Je Dokument (Quelltextdatei) gibt es eine eigene **History-Datei**, die alle Revisionen als eine Liste jeweils geänderter (Text-)Blöcke speichert 每个文档（源代码文件）都有自己的历史文件，其中包含所有修订作为已更改（文本）块的列表

+ Delta: 增量
  + jeder Block ist ein Delta, das Änderungen zwischen Vorgängerrevision und aktueller Revision beschreibt 每个块都是一个增量，描述了先前版本和当前版本之间的更改
+ SCCS-Identifikationsnummer: SCCS标识号
  + jedes Delta hat SCCS-Identifikationsnummer der zugehörigen Revision 每个增量都有一个 SCCS 标识号，用于标识相关的修订版本
  + 标识号的格式为：<ReleaseNo>, <LevelNo>, <BranchNo>, <SequenceNo>

**Eigenschaften von SCCS:**

+ für beliebige (Text-)Dateien verwendbar (und nur für solche) 可用于任何（文本）文件（且仅适用于文本文件）
+ **Schreibsperren** auf “ausgecheckten” Revisionen 对“签出”修订进行写锁
+ Revisionsbäume mit manuellem Konsistenthalten von Entwicklungszweigen 修订树与开发分支的手动一致性
+ Rekonstruktionszeit von Revisionen steigt linear mit der Anzahl der Revisionen (Durchlauf durch Blockliste) 修订的重建时间随修订次数线性增加（遍历块列表）
+ Revisionsidentifikation nur durch Nummer und Datum 仅通过编号和日期识别修订版本

**Offene Problem:**

+ kein Konfigurationsbegriff und kein Variantenbegriff 没有配置概念和变体概念
+ keine Unterstützung zur Verwaltung von Konsistenzbeziehungen zwischen verschiedenen Objekten 不支持管理不同对象之间的一致性关系

**Probleme mit Schreibsperren:**

&rarr; SCCS realisiert ein sogenanntes „pessimistisches“ Sperrkonzept. Gleichzeitige Bearbeitung einer Datei durch mehrere Personen wird verhindert: 实现了一种所谓的“悲观”锁定概念，防止多个用户同时编辑同一文件

+ ein Checkout zum Schreiben (single write access) 写入时签出（单一写访问）
+ mehrere Checkouts zum Lesen (multiple read access) 读取时签出（多重读访问）

**Exkurs zu "diff" und "patch" - Beispiel**

&rarr; 使用'diff'和'patch'工具有效的管理代码的更改和版本控制

+ diff
  + 补丁文件，用于显示两个文件之间的差异
+ patch
  + 应用这些差异以更新文件

![Screenshot_2024-07-16 15.12.49_LBzjmR](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 15.12.49_LBzjmR.jpg)

**Rückwärtsdeltas 逆向增量 - Beispiel**

&rarr; 表示从当前版本退回到前一个版本所需的变化

![Screenshot_2024-07-16 15.19.48_fLIWCG](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 15.19.48_fLIWCG.jpg)

**Genauere Instruktionen zur Erzeugung von Deltas:**

&rarr; Jedes „diff“-Werkzeug hat seine eigenen Heuristiken, wie es möglichst kleine und/oder lesbare Deltas/Patches erzeugt, die die Unterschiede zweier Dateien darstellen. Ein möglicher Satz von Regeln zur Erzeugung von Deltas sieht wie folgt aus 每个 `diff` 工具都有自己的启发式方法来生成尽可能小且易读的增量/补丁文件，表示两文件之间的差异。以下是一组用于生成增量的规则

+ 最小化更改行数
  + Die Anzahl der geänderten, gelöschten und neu erzeugten Zeilen aller Hunks eines Deltas zweier Dateien wird möglichst **klein gehalten**. 所有区块（Hunks）中更改、删除和新建行的数量应尽可能小
+ 区块的开始
  +  Jeder Hunk beginnt mit genau einer unveränderten Kontextzeile und enthält sonst nur geänderte, gelöschte oder neu eingefügte Zeilen (Ausnahme: Dateianfang). 每个区块以恰好一行未更改的上下文行（Kontextzeile）开始，之后仅包含更改、删除或新建的行（文件开头除外）
+ 区块之间的分隔
  + Aufeinander folgende Hunks sind also durch jeweils mindestens eine unveränderte Zeile getrennt. 连续的区块至少应由一行未更改的行分隔
+ 替代删除和新建
  + Optional: Anstelle von Löschen und Neuerzeugen einer Zeile i verwendet man die Änderungsmarkierung „!“ 删除和新建某一行 i 时使用更改标记 **“！”**

**Unifield Diff Format 统一差异格式 - Beispiel:**

&rarr; Es handelt sich „nur“ um eine etwas andere Art der Darstellung von Unterschieden zwischen verschiedenen Dateien (Dateirevisionen) 只是一种表示文件之间差异的方式。它通过显示删除的行和新增的行来直观地展示不同文件版本之间的变化

![Screenshot_2024-07-16 15.34.37_SGcsMR](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 15.34.37_SGcsMR.jpg)

**Create- und Apply-Patch in Eclipse**

&rarr; Die „Create Patch“- und „Apply Patch“-Funktionen in Eclipse benutzen genau das gerade eingeführte „Unified Diff“-Format. 

+ Create Patch —— Bei der **Erzeugung von Hunks 生成区块** wohl folgende Heuristiken/Regeln verwendet:
  + 区块开始：ein Hunk scheint in der Regel mit drei unveränderten Kontextzeilen zu beginnen (inklusive Leerzeilen). 每个区块通常以三行未更改的上下文行（包括空行）开始
  + 区块间分隔：zwei Blöcke geänderter Zeilen müssen durch mindestens sieben unveränderte Zeilen getrennt sein, damit dafür getrennte Hunks erzeugt werden 两个更改行的区块必须至少有七行未更改的行分隔，以便生成单独的区块
+ Apply Patch —— Bei der Anwendung von Patches werden folgende Heuristiken/Regeln verwendet:
  + 上下文或删除行的匹配：werden der Kontext oder die zu löschenden Zeilen eines Patches so nicht gefunden, dann endet die Patch-Anwendung mit einer Fehlermeldung 如果无法找到补丁中的上下文或删除行，则补丁应用将以错误消息结
  + 位置不变性：befindet sich die zu patchende Stelle eines Textes nicht mehr an der angegebenen Stelle (Zeile), so wird trotzdem der Patch angewendet 如果要补丁的位置不再位于指定行，补丁将仍然应用于文本中的该位置
  + 多个相同的位置：gibt es mehrere (identische) Stellen in einem Text, auf die ein Patch angewendet werden kann, so wird die Stelle verändert, die am nächsten zur alten Position ist 如果文本中有多个相同的位置，补丁将应用于最接近原始位置的地方



#### RCS (Revision Control System) von Rerkley/Purduce University

**RCS 修订控制系统**

&rarr; RCS 是由 Berkeley 和 Purdue University 开发的修订控制系统

&rarr; Je Dokument (immer Textdatei) gibt es eine eigene History-Datei, die eine neueste Revision vollständig und andere Revisionen als Deltas speichert 每个文档（始终是文本文件）都有自己的历史文件，该文件将最新版本完整存储，并将其他版本存储为增量

+ optionale Schreibsperren (verhindern ggf. paralleles Ändern) 可选的写保护机制，以防止并行修改文档
+ **Revisionsbäume 修订树** mit besserem Zugriff auf Revisionen: 修订树提供更好的修订访问机制
  + schneller Zugriff auf neueste Revision auf Hauptzweig 快速访问主分支上的最新修订版本
  + langsamer Zugriff auf ältere Revisionen auf Hauptzweig (mit Rückwärtsdeltas) 较慢地访问主分支上的旧修订版本（使用反向增量）
  + langsamer Zugriff auf Revisionen auf Nebenzweigen (mit Vorwärtsdeltas)  较慢地访问分支上的修订版本（使用正向增量）
+ Versionsidentifikation auch durch frei wählbare Bezeichner 通过自由选择的标识符来标识修订版本
+ Offene Probleme:
  + kein Konfigurationsbegriff und kein Variantenbegriff 没有配置管理和变体管理的概念

**Beispielszenario der Softwareentwicklung:**

![Screenshot_2024-07-16 16.12.37_R7HlFs](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 16.12.37_R7HlFs.jpg)

**Deltaspeicherung von Revisionen als gerichtete Graphen:**

![Screenshot_2024-07-16 16.23.48_IhkXim](/Users/summer/Pictures/截屏/Screenshot_2024-07-16 16.23.48_IhkXim.jpg)

+ logische Struktur 逻辑结构
  + 最基本的版本关系图，显示了每个版本之间的直接继承关系
+ SCSS: Vorwärtsdeltas 前向增量
  + SCSS使用前向增量存储方法
  + 每个版本都存储了从前一个版本到当前版本的差异（增量）
+ Rückwärtsdeltas 后向增量
  + 存储从当前版本到前一个版本的差异

+ RCS: Vorwärts- und Rückwärtsdeltas 前向和后向增量
  + RCS使用了前向和后向增量的结合
  + 主分支上的最新版本存储为完整版本，其他分支版本存储为增量

#### CVS (Concurrent Version (Control) System) 

**CVS 协作版本系统**

 &rarr; CVS是基于RCS的一种协作版本系统

&rarr; Zunächst Aufsatz auf RCS (später Reimplementierung), das Revisionsverwaltung für ganze Directorybäume durchführt und zusätzlich anbietet 关于 RCS 的第一篇文章（后来重新实现），修订管理执行整个目录树并提供它们

+ 乐观锁概念与自动合并

  + optimistisches Sperrkonzept mit (fast) automatischem Verschmelzen (merge) von parallel durchgeführten Änderungen in verschiedenen privaten Arbeitsbereichen 乐观锁定概念，（几乎）自动合并不同私有工作空间中并行进行的更改

    &rarr; Dreiwegeverschmelzen mit manueller Konfliktbehebung 使用三路合并技术，手动解决冲突

+ 修订版识别与版本管理

  + Revisionsidentifikation und damit rudimentäres Releasemanagement auch durch frei wählbare Bezeichner 修订标识以及基本的发布管理也通过可自由选择的标识符

    &rarr; Auszeichnen zusammengehöriger Revisionen durch symbolische Namen (mit Hilfe sogenannter Tags) 通过符号名称（Tags）标记相关的修订版，使管理更方便

+ diverse Hilfsprogramme 多种辅助工具

  + wie z.B. „cvsann“, das jeder Zeile einer Textdatei die Information voranstellt, wann sie von wem zum letzten Mal geändert wurde 提供各种辅助工具，如 `cvsann`，能够显示文本文件中每一行的最后修改信息以及修改时间和修改者

#### Subversion SVN - CVS-Nachfolger von CollabNet initiiert



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



