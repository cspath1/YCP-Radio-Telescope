---
title: "Gradle Build System"
weight: 1
---

The back-end of the Radio Telescope uses the Spring Framework, and builds are being managed using the Gradle build
system. The build script has several Gradle tasks set up to streamline the develop -> test -> publish workflow.

## Gradle Tasks
The syntax for running a Gradle task from command line is as follows:
```bash
gradle taskName # run a single task
gradle task1 task2 task3 # run multiple tasks one after the other, stopping after first failure
```

### Gradle Verify
The build script has a "gradle verify" task that will run all of the tests and uses [Jacoco](https://github.com/jacoco/jacoco)
to verify that the code coverage is at a certain threshold. This task is important to run before pushing any code,
as the [Travis CI](https://travis-ci.com/) server we use for continuous integration will run this task in order to pass or fail builds.

### Gradle Dokka
The build script has a "gradle dokka" task that uses [dokka](https://github.com/Kotlin/dokka) to generate an html page containing
all of the javadocs documentation for the back-end application. This html is hosted [here](https://cspath1.github.io/RT-Contracts/).
Running the task will only generate the html files in a "docs" folder in the root of the project. These files must then be placed on the
gh-pages branch. There is a bash script that will automate this process "./publish-api-docs.sh". This script first requires you to run
"gradle dokka" to generate the html, then it will handle the rest. **NOTE:** This will only work if the project was cloned via ssh **NOT**
https