# Robot-Java-Plugin
A plugin executor for Robot tool, executes any Robot test/suite/commands and generates report. Can be integrated with any automation framework for E2E solution validation.

# Robot-Java-Plugin
A java based plugin executor for Robot tool, executes any Robot test/suite/commands and generates report. Can be integrated with any automation framework for E2E solution validation.

# Goal:
**Analysis and demonstration on how to:**
* Reuse an existing Robot-suite (developed by [Robot Framework](http://robotframework.org/) from any java based test automation framework (java with cucumber)
* Execute a Robot-suite from java
![image](https://user-images.githubusercontent.com/17194046/155359682-1490efeb-f25c-48db-9f19-cfe99efd1aa6.png)

# About Robot
* Robot Framework is an open source test automation framework that was initially developed at Nokia Networks and it is nowadays sponsored by Robot Framework Foundation.
* Hosted on GitHub for further documentation, source code, and issue tracker and Downloads are hosted at PyPI. 
**Features:**
A generic Keyword-Driven test automation framework for acceptance testing and acceptance test-driven development (ATDD). Core framework is implemented using Python and runs also on Jython (JVM) and IronPython (.NET). Testing approach with tabular test data syntax and testing capabilities can be extended by test libraries implemented either with Python or Java.Test-Suite File format : '.robot'
![image](https://user-images.githubusercontent.com/17194046/155359969-11dca740-b438-477f-a4d7-43d0126e11e6.png)

# How to Execute Robot-Test/Suite From Java?
Robot-Executors-Plugin:
* A java based plugin executor: Executes any robot-test/suite/robot-commands and generates report
* Can be integrated with any java based test automation framework.
![image](https://user-images.githubusercontent.com/17194046/155360159-cb6b2e12-5b68-4778-a26b-024b650abe40.png)

# Concept:
![image](https://user-images.githubusercontent.com/17194046/155474014-370ac392-3ea0-4f9c-a333-d988e74e00e8.png)

# A. Robot-Python-Runner:
* An Executor(RobotPyRunner) that triggers Robot-Suite and other robot-commands by core robot-python module(robot.run).
* Faster to initiate and execute robot-suite same as the robot-core-framework.

**Pre-requisite:** 
* Python3 Must be installed in the system 
* Robot-framework must be installed in the system (pip install robotframework)
* Robot-Suite Must be available in the system

**Reference:** 
* https://robot-framework.readthedocs.io/en/v3.1.1/_modules/robot/run.html

**API-Details:**
![image](https://user-images.githubusercontent.com/17194046/155474413-8db09e75-aaac-4ce6-afcc-fc6ce933de41.png)

**Example:**
![image](https://user-images.githubusercontent.com/17194046/155474507-e42bed39-844d-4cc5-9626-890261ea41f9.png)

**Sample Robot-Argument File:**
![image](https://user-images.githubusercontent.com/17194046/155474630-432e1f80-a9ed-4802-b9da-dafb5a1c1406.png)

# B.Robot-Jar-Runner:
An Executor(RobotJarRunner) that triggers Robot-Suite and other robot-commands via core robot-framework-jar(robotframework.jar).
A bit slower to initiate and execute robot-suite w.r.t the robot-framework as Jython converts java code into python.

**Pre-requisite:** 
* No need to install Python, Robot-framework
* Include robot-famrework.jar(3.1.1 version) in your project
* Robot-Suite Must be available in the system

**API-Details:**
![image](https://user-images.githubusercontent.com/17194046/155474805-61faeebe-e33b-4e63-a1c1-c1037d91b496.png)
![image](https://user-images.githubusercontent.com/17194046/155474850-d37c5dcb-11dc-4b1c-b0a6-a56e6b50f409.png)

# C.Maven-Plugin:
* An inbuilt maven plugin of developed core Robot-Framework-JAR (robotframework.jar) for that triggering any Robot-Suite via various maven goals :
* robotframework:run - behaves like invoking the jybot Robot Framework command for executing test cases
* robotframework:acceptance-test - Runs the tests, like the run-goal, but does not verify the test results.
* robotframework:verify - Verifies the results from acceptance-test goal.
* robotframework:libdoc - invokes the libdoc Robot Framework command for generating keyword documentation for test libraries and resource files
* robotframework:testdoc - invokes the testdoc Robot Framework command for generating high level overview of test suites
* robotframework:rebot - invokes the rebot Robot Framework command that separately allows creating custom reports and logs as well as combining and merging results. It can also be used to separate test execution and report generation to different maven profiles.
* A bit slower to initiate and execute robot-suite w.r.t the robot-framework as Jython converts java code into python.

**Pre-requisite:** 
* No need to install Python, Robot-framework, 
* No need to include robot-famrework.jar
* Robot-Suite Must be available in the system
* The project must be integrated with maven along with 'robotframework-maven-plugin' in project pom.xml as below:
 ![image](https://user-images.githubusercontent.com/17194046/155475119-f2761a25-ba80-4d12-a168-f05632eb38f7.png)
 
**Sample Maven-POM File:**
* Executed from project dir by below maven command: mvn robotframework:run 
* Reference : 
** http://robotframework.org/MavenPlugin/
** https://robotframework.org/MavenPlugin/acceptance-test-mojo.html

```xml
<!-- Run : mvn robotframework:run -->
<!-- Ref : https://robotframework.org/MavenPlugin/acceptance-test-mojo.html 
	https://robot-framework.readthedocs.io/en/v3.1.1/_modules/robot/run.html 
	https://twiki.cern.ch/twiki/bin/view/EMI/RobotFrameworkAdvancedGuide -->
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>Robot-Plugin</groupId>
	<artifactId>Robot-Plugin</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>Robot-Plugin</name>
	<description>A Java Plugin For Robot Framework</description>
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<!-- <jython.version>2.7.0</jython.version> -->
		<robot.version>3.1.1</robot.version>

		<Robot-maven-plugin-version>1.5.1</Robot-maven-plugin-version>
		<Robot-TestSuiteDir>${project.basedir}/RobotTestsuites</Robot-TestSuiteDir>
		<Robot-OutputDir>${project.basedir}/target/MyReports/MyOutput.xml</Robot-OutputDir>
	</properties>

	<dependencies>
		<!-- <dependency> <groupId>org.python</groupId> <artifactId>jython</artifactId> 
			<version>${jython.version}</version> </dependency> -->
		<!-- Used For Plugin-Runner, Not For robotframework-maven-plugin -->
		<dependency>
			<groupId>org.robotframework</groupId>
			<artifactId>robotframework</artifactId>
			<version>${robot.version}</version>
		</dependency>
		<dependency>
			<groupId>log4j</groupId>
			<artifactId>apache-log4j-extras</artifactId>
			<version>1.0</version>
		</dependency>
	</dependencies>
	<build>
		<plugins>
			<!-- robotframework-maven-plugin -->
			<!-- Not Required to include 'robotframework' and 'jython' dependencies -->
			<plugin>
				<groupId>org.robotframework</groupId>
				<artifactId>robotframework-maven-plugin</artifactId>
				<version>1.5.1</version>
				<executions>
					<execution>
						<goals>
							<goal>run</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<testCasesDirectory>${Robot-TestSuiteDir}</testCasesDirectory>
					<output>${Robot-OutputDir}</output>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>
```

# Challenges:
* Robot-Test can be executed with a runtime argument-file (--argumentfile) i.e. needs to be updated for any dynamic data input. 
* Java unable to control over any robot-steps while executing Robot-Test/Suite
* Java unable to access any value returned from robot-steps while executing Robot-Test/Suite.
* Java can assign values to only global-variables(--variable) defined in Robot-Suite/Test level. 
* Java unable to fetch any dynamic value of variable while executing a Robot-Test.
* Java fails to decompile the Robot-Keywords and it's Grammer based syntax defined in Robot-Test.As Robot report format is based on the execution of keyword-steps, 
* Report Merging is required with other automation-frameworks.
* Huge Keywords(built-in, user-defined)  and several standard/eternal libraries that are bundled in with the framework, 
* We have to understand those keywords and it's grammer/syntax before writing any Test use case.
* ![image](https://user-images.githubusercontent.com/17194046/155475732-7ac0b197-0ba7-498a-b7ad-fedcd2f2e976.png)







