# Generisches Delivery Pipeline GUI

Wir möchten ein Build-Tool unabhängiges UI für Build / Delivery Pipelines anbieten können.
Ev. können wir gerade einen [Open Standard](https://fsfe.org/freesoftware/standards/def.de.html) dazu definieren.

**Weiterführende Informationen:** 

Generische Ansichten

* Build
* Reports (Tests, Security, Scanning, ...)
* Pipeline Abhängigkeiten


Plugins / Importer für Build Tools

* Jenkins
* GitLab CI/CD
* Tekton
* GitHub Workflows
* CircleCI
* Travis
* TeamCity
* ...


## Ziel

1. Definition erstellen
2. In Open Standard Format bringen https://codimd.puzzle.ch/GenerischesDeliveryPipelineKonzept
3. Blogpost
4. ~~Referenzimplementierung~~

## Infos

* https://github.com/puzzle/delivery-pipeline-concept
* Mobitor: https://bitbucket.org/mobiliar/
  * Infos zu Build und Umgebungen
  * Plugin Based
  * div. Plugins zur Infobeschaffung

## Umsetzung

Mo - Mi

* Bestandesaufnahme
  * Must have
  * Vergleich versch. Tools mit Pro's und Con's
  * 



### Must have

Stages:

1. Build and Unit Tests
    * Code Compilation and Build
      * Resultat
      * Logs
    * Unit Tests
      * siehe Allgemein
    * Static Analysis
      * siehe Allgemein
    * Dependency Checks
      * inkl. Licenses
    * Artifact Generation
2. Packaging
3. Automated Tests
4. ~~Manual Tests~~
5. Release

Allgemein:

* Naming
  * Jobs/Stages/Workflows ...
  * Runs/Executions ...
* Test
  * Resultat
    * Anzahl gefailter Tests
    * Anzahl neu gefailter Tests
    * Flaky Tests?
    * Historie / Veränderung (Grafisch?)
    * Test-Detail-Seite à la Gradle da strukturiert/gruppiert nach Package 
      (bei Jenkins nicht ganz so toll, da ALLE Unittests angezeigt werden, bei GitLab eher zu spartanisch)
  * Logs
  * Stacktrace

* Static Analysis
  * Resultat
    * Success/Failure (optional inkl. Coverage)
    * Historie / Veränderung (Grafisch?)

Rest:

* PR/MR
* Triggering
* manuelle Steuerung

Qualitätsanforderungen:

* GUI nicht überladen
  * was wann anzeigen? (weniger ist mehr/wieviel ist zu viel?)

### Resultate
* Aktualisierung/Konsolidierung des Pipeline Konzepts

### TODO / Fragen

* [ ] andere Konzepte
  * [ ] https://concourse-ci.org/
    * [ ] **https://github.com/concourse/rfcs**
  * [ ] https://harness.io/
    * [ ] https://harness.io/learn/ebooks/ebook-pipeline-patterns

* [ ] Vulnerabilities so wie Tests behandeln?

* [ ] Anforderungen an Aktualität der Daten
  * [ ] Logausgaben in "Echtzeit"?
  * [x] Option zum manuellen Aktualisieren? 

* BaseImage Update?
  * nur Image Bauen
  * Stages skippen

* Struktur
  * Projekt mit mehreren Pipelines? (etwa verschiedene Umgebungen)
    * Pipeline triggert weitere Pipeline? (verlinkbare Pipelines) -> Jenkins
    * Eine Pipline mit mehreren Stages? (mit manuell ausführbaren Triggern) -> GitLab

* Steuerung
  * Pipeline
    * starten
    * stoppen
    * restart
  * Stages
    * starten
    * stoppen
    * restart

* Details / Zusatzinfos
  * Run
      * Zeitpunkt/Dauer der Ausführung
      * Benutzer/Hook, welcher den Run gestartet hat
      * SCM(Git)-Infos
      * Übersicht mit den einzelnen Stages
      * GitLab als macht diesen Teil sehr gut
      * Test-Summary (Anzahl erfolgreicher/gefailter Tests)
        * Link auf Test-Detail Seite
      * Buildstabilität à la Jenkins sinnvoll?
      * Alle Runs als Liste
      * anhand von Branches gruppierte Runs
        * inkl. Verlauf/History

* [x] Pipeline Konzept
  * [x] **@cra**: Reto **Schreibzugriff** für das Repo gewähren
  * [x] Performance Tests hinzufügen https://github.com/puzzle/delivery-pipeline-concept/blob/master/stages/03-automated-tests/README.md
  * [x] **@cra**: Docker -> Container (Naming)
  * [x] Security Checks (Dynamic Application Security Testing (DAST)) nicht statisch -> autom. Test Stage
  * [x] Readme Link updaten: draw.io -> https://app.diagrams.net/


### Babylon
* Jenkins:  Job:   Pipeline > Stages > Steps
* GitLab:   Run:   Pipeline > Stages > Jobs
* GitHub:   Run:   Workflow > Jobs > Steps
* CircleCI: ???:   Workflow > Jobs > Steps
* Tekton:   Run:   Pipeline > ??? > Tasks
* TeamCity: Build: 

* **Puzzle:  Run: Pipeline > Stages > Steps**