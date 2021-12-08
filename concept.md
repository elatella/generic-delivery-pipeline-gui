# Generisches Delivery Pipeline GUI Konzept

## Abstract
Dieses Dokument Beschreibt die Anforderungen an ein generisches GUI für Delivery Pipelines.

## Einführung

### Motivation
Es existiert eine Vielzahl von Delivery Pipeline Lösungen. Jede dieser Lösungen verfügt über ein proprietäres GUI mit eigener Navigationslogik und unterschiedlichem Naming. Mit einem einheitlichen, generischen GUI könnte der Betrieb von und der Wechsel zwischen unterschiedlichen Delivery Pipelines vereinfacht werden.

### Zweck
Ziel dieses Dokuments ist es, die Anforderungen an ein generisches GUI für Delivery Pipelines zu definieren, welches:
* unabhängig von der verwendeten Delivery Pipeline ist
* modular aufgebaut ist
* beliebig erweitert werden kann
* quelloffen ist

Dieses Dokument versucht nicht:
* eine konkrete technische Umsetzung zu spezifizieren
 
## Spezifikation
 
### Begriffsdefinitionen

#### Pipeline
Eine Pipeline besteht aus einer oder mehreren Stages.

Beispielsweise:

![Delivery Pipeline Overview](https://raw.githubusercontent.com/chrira/delivery-pipeline-concept/images/images/delivery-pipeline-overview.svg)


#### Stage
Eine Stage ist in einen oder mehrere Steps unterteilt.

Beispielsweise:

![Build Stage Overview](https://raw.githubusercontent.com/chrira/delivery-pipeline-concept/images/images/build-stage.svg)

#### Step
Ein Step bildet die kleinste Einheit einer Pipeline.

#### Run
Als Run wird die Ausführung einer Pipeline bezeichnet. Eine Pipeline kann beliebig oft ausgeführt werden. 
Ein Run bezieht sich stets auf eine individuelle Ausführung einer spezifischen Pipeline.


## Detailanforderungen

### GUI

#### Bestandteile

#### Übersichtseite
* Auflistung (aller) Runs
* Gruppierungen
  * [ ] (TODO: wie? welche? verschachtelt?)
  * Tabs -> Pipeline (Jenkins) oder per Gruppe -> Repo/Pipeline (GitLab)
* Möglichkeit, Runs anhand von Branches zu gruppieren
  * [ ] seperates Tab, View oder Seite?
  * inkl. Verlauf/History
* Zeitpunkt der letzten Aktualisierung
* Möglichkeit die Aktualisierung der Daten manuell auszulösen (optional)

**Pipeline Groups**
![Pipeline Groups](https://raw.githubusercontent.com/chrira/delivery-pipeline-concept/images/images/pipeline-groups.svg)

**Pipeline Group**
![Pipeline Group](https://raw.githubusercontent.com/chrira/delivery-pipeline-concept/images/images/pipeline-group.svg)

##### Informationen zu einem Run
* ID
* Status
* Zeitpunkt und Dauer der Ausführung
* Benutzer oder Hook, welcher den Run ausgelöst hat
* VCS (Git) Infos
* Übersicht mit den einzelnen Stages
  * Status der Stages
* Klick/Link auf Run öffnet Run-Detail Seite

**Pipeline Overview**
![Pipeline Overview](https://raw.githubusercontent.com/chrira/delivery-pipeline-concept/images/images/pipeline-overview.svg)

#### Run-Detail Seite
* Infos wie oben, aber detaillierter
  * z.B. Git Commit Message
* Übersicht mit den einzelnen Stages
  * Status der Stages
  * Steps
    * Status
    * Klick/Link auf Step öffnet Step-Detail Seite
* Test-Summary (Total erfolgreiche/gefailte Tests)
  * Link auf Test-Detail Seite

#### Step-Detail Seite
* Name
* Dauer
* Invoker
* Status
* Links
  * Test-Detail Seite (Resultat von diesem Step)
  * Logs
  * Stacktrace (bei gefailten Steps)

#### Test-Detail Seite
* Resultat Übersicht
  * Total erfolgreiche/gefailte Tests
  * Total bei diesem Run neu gefailte Tests
  * Historie/Veränderung/Tendenz (ev. grafisch)
  * Steps mit Tests als Übersicht
* Resultat pro Step
  * Anzahl erfolgreiche/gefailte Tests
  * Anzahl bei diesem Run neu gefailte Tests
  * Flaky Tests (optional)
* Auflistung der ausgeführten Tests, strukturiert/gruppiert nach Steps, danach nach Package
  * bei gefailten Tests
    * Logs
    * Stacktrace

### Allgemeines

* Keine Pipeline Konfigurationen, stateless!

#### Aktionen / Steuerelemente
* start
* stop
* retry

Diese sollen verfügbar sein für:

* Pipelines
* Stages

### Berechtigungskonzept

* [ ] Zugriff auf Build Server/Data Source
* [ ] Einschränkung auf Gruppen/Pipelines?
  * ev. mit Zugriff als eingeloggter User
  * ev. Konfigurationsdatei in VCS


### Viewmodel


### APIS

#### Jenkins
* API-Doku: https://www.jenkins.io/doc/book/using/remote-access-api/
* JAVA-Lib: https://github.com/cdancy/jenkins-rest
* Authentifizierung: Token oder Basic-HTTP

#### GitLab
* API-Doku: https://docs.gitlab.com/ee/api/api_resources.html
* Authentifizierung: OAuth2-, Persönliches- oder Projekt-Token

#### Github:
* API-Doku: https://docs.github.com/en/rest
* Authentifizierung: Token oder Basic-HTTP

#### CircleCI
* API-Doku: https://circleci.com/docs/api/v2/
* Authentifizierung: Token oder Basic-HTTP

#### Tekton
* API-Doku: K8S mit Tekton CRD
* Tektion CLI (tkn): https://github.com/tektoncd/cli/tree/main/docs
* Authentifizierung: mit OC Tool (OpenShift) oder kubectl (K8S)

#### TeamCity
* API-Doku: https://www.jetbrains.com/help/teamcity/rest/teamcity-rest-api-documentation.html
* Authentifizierung: Token oder Basic-HTTP

