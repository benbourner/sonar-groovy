# SonarQube plugin for Groovy

[![Build Status](https://travis-ci.com/Inform-Software/sonar-groovy.svg?branch=master)](https://travis-ci.com/Inform-Software/sonar-groovy)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=org.sonarsource.groovy%3Agroovy&metric=alert_status)](https://sonarcloud.io/dashboard?id=org.sonarsource.groovy%3Agroovy)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=org.sonarsource.groovy%3Agroovy&metric=coverage)](https://sonarcloud.io/dashboard?id=org.sonarsource.groovy%3Agroovy)

## Description

The plugin enables analysis of Groovy within SonarQube.

It leverages [CodeNarc](http://codenarc.sourceforge.net/) to raise issues against coding rules, [GMetrics](http://gmetrics.sourceforge.net/) for cyclomatic complexity and [Cobertura](http://cobertura.sourceforge.net/) or [JaCoCo](http://www.eclemma.org/jacoco/) for code coverage.

Plugin    | 1.4/1.5 | 1.6
----------|---------|---------
CodeNarc  | 0.25.2  | 0.25.2
GMetrics  | 0.7     | 0.7
SonarQube | 5.6-6.7 | 6.7-7.5

## Steps to Analyze a Groovy Project
1. Install SonarQube Server
1. Install SonarQube Scanner and be sure you can call `sonar-scanner` from the directory where you have your source code
1. Install the Groovy Plugin.
1. Create a _sonar-project.properties_ file at the root of your project
1. Run `sonar-scanner` command from the project root dir
1. Follow the link provided at the end of the analysis to browse your project's quality in SonarQube UI

## Notes
*CodeNarc*
It is possible to reuse a previously generated report from CodeNarc by setting the `sonar.groovy.codenarc.reportPaths` property.

*Groovy File Suffixes*
It is possible to define multiple groovy file suffixes to be recognized by setting the `sonar.groovy.file.suffixes` property. Note that by default, only files having `.groovy` as extension will be analyzed.

*Unit Tests Execution Reports*
Import unit tests execution reports (JUnit XML format) by setting the sonar.junit.reportsPath property. Default location is _target/surefire-reports_.

*JaCoCo and Binaries*
The groovy plugin requires access to source binaries when analyzing JaCoCo reports. Consequently, property `sonar.groovy.binaries` has to be configured for the analysis (comma-separated paths to binary folders). For Maven and gradle projects, the property is automatically set.

## Coverage Results Import
The Groovy Plugin does not generate its own test coverage report, but re-uses the ones generated by Cobertura or JaCoCo. 

### Code Coverage with Cobertura
To display code coverage data:

1. Prior to the SonarQube analysis, execute your unit tests and generate the Cobertura XML report.
1. Import this report while running the SonarQube analysis by setting the `sonar.groovy.cobertura.reportPath` property to the path to the Cobertura XML report. The path may be absolute or relative to the project base directory.

### Code Coverage with JaCoCo
To display code coverage data:

1. Prior to the SonarQube analysis, execute your tests and generate the JaCoCo exec file(s).
1. In order to be able to read the exec report file, and as JaCoCo bases its analysis on binaries, set the `sonar.groovy.binaries` property.
1. Set the `sonar.groovy.jacoco.reportPath` property to the path to the JaCoCo exec file related to your unit tests.
1. (Optional) If you are running integration tests on top of your unit tests, you may want to set the `sonar.groovy.jacoco.itReportPath` to the path to JaCoCo exec file related to the integration tests.
1. Run the SonarQube analysis.

## Contributions

Contributions via GitHub [issues] and pull requests are very welcome. This
project tries to adhere to the [Google Java Style], but we don't want a global
reformat to keep the Git history readable. To help with this, you can use the
[fmt-maven-plugin] to format your changes:

    mvn fmt:format -DfilesNamePattern=TestUtils\.java

You can use the `fileNamePattern` option to restrict the formatter to the files
you changed.

[issues]: https://github.com/Inform-Software/sonar-groovy/issues/new
[Google Java Style]: https://google.github.io/styleguide/javaguide.html
[fmt-maven-plugin]: https://github.com/coveo/fmt-maven-plugin
