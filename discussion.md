# Discussion

**Additional information:**

Generic views

* Build
* Reports (tests, security, scanning, ...)
* Pipeline dependencies

Plugins / importers for build tools like

* Jenkins
* GitLab CI/CD
* Tekton
* GitHub workflows
* CircleCI
* Travis
* TeamCity
* ConcourseCI
* ...

## Info

* <https://github.com/puzzle/delivery-pipeline-concept>
* Mobitor: <https://bitbucket.org/mobiliar/>
  * Information on build and environments
  * Plugin Based
  * various plugins for obtaining information

## Implementation

* Inventory
  * Must have
  * Comparison of different tools with Pro's and Con's

### Must have

Stages:

1. Build and Unit Tests
   * Code Compilation and Build
      * Results
      * Logs
   * Unit tests
      * see general
   * Static Analysis
      * see general
   * Dependency checks
      * including licenses
   * Artifact Generation
2. Packaging
3. Automated tests
4. ~~Manual Tests~~
5. Release

Generally:

* Naming
  * Jobs / Stages / Workflows ...
  * Runs / Executions ...
* Test
  * Result
    * Number of failed tests
    * Number of newly failed tests
    * Flaky tests?
    * History / change (graphically?)
    * Test detail page à la Gradle because it is structured / grouped according to package
      * (not so great with Jenkins, as ALL unit tests are displayed, with GitLab rather too spartan)
  * Logs
  * Stacktrace

* Static Analysis
  * Result
    * Success / Failure (optional including coverage)
    * History / change (graphically?)

Div:

* PR / MR
* Triggering
* manual control

Quality requirements:

* GUI not overloaded
  * show what and when? (less is more / how much is too much?)

### TODO / questions

* [ ] other concepts
  * [ ] <https://concourse-ci.org/>
    * [ ] **https: //github.com/concourse/rfcs**
  * [ ] <https://harness.io/>
    * [x] <https://harness.io/learn/ebooks/ebook-pipeline-patterns> ---> Added to [concept](https://github.com/puzzle/delivery-pipeline-concept)

* [ ] Treat vulnerabilities like tests?

* [ ] Requirements for the actuality of the data
  * [ ] Log outputs in "real time"?
  * [x] option to update manually?

* BaseImage Update?
  * Build image only
  * Skipping stages

* Structure
  * Project with multiple pipelines? (e.g. different environments)
    * Pipeline triggers another pipeline? (linkable pipelines) -> Jenkins
    * A pipeline with multiple stages? (with manually executable triggers) -> GitLab

* Steering
  * Pipeline
    * start
    * to stop
    * restart
  * Stages
    * start
    * to stop
    * restart

* Details / additional information
  * Run
    * Time / duration of execution
    * User / hook who started the run
    * SCM (Git) info
    * Overview with the individual stages
    * GitLab as does this part very well
    * Test summary (number of successful / failed tests)
      * Link to test details page
    * Build stability like Jenkins makes sense?
    * All runs as a list
      * Runs grouped by branches
      * including history

### Babylon

* Jenkins:  Job:   Pipeline > Stages > Steps
* GitLab:   Run:   Pipeline > Stages > Jobs
* GitHub:   Run:   Workflow > Jobs > Steps
* CircleCI: ???:   Workflow > Jobs > Steps
* Tekton:   Run:   Pipeline > ??? > Tasks
* TeamCity: Build:

* **Puzzle:  Run: Pipeline > Stages > Steps**
