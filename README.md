# Building a Java Project with Jenkins and Maven

## Overview

This guide demonstrates how to set up a Jenkins Freestyle project to build a simple Java application using Maven. This is a fundamental step in establishing a Continuous Integration/Continuous Deployment (CI/CD) pipeline.

## Prerequisites

* **Jenkins:** Installed locally or via Docker.
* **Java Development Kit (JDK):** Version 8 or 11.
* **Maven:** A build automation tool.
* **Git:** (Optional) Required if your project source code is hosted in a Git repository.

## Project Structure

The sample Java project has the following directory structure:

hello-java-maven/

├── src/

│   └── main/

│       └── java/

│           └── HelloWorld.java

└── pom.xml

### Code Files

* **`HelloWorld.java`**
* **`pom.xml`**

## Setup Instructions

### 1.  Set up the Java Application

    * Create the directory structure as shown in the "Project Structure" section.
    * Create the `HelloWorld.java` file with the provided code.
    * Create the `pom.xml` file with the provided configuration.

### 2.  Start Jenkins

    * **Using Docker:**

        ```bash
        docker run -p 8080:8080 jenkins/jenkins:lts
        ```

        Open your browser and access Jenkins at `http://localhost:8080`.  Follow the on-screen instructions to retrieve the initial admin password or the below command and complete the setup.
         ```bash
        docker logs <container ID>
        ```
    * **Local Installation:**
        If you have Jenkins installed locally, start the Jenkins service.  The method for starting the service varies depending on your operating system.  Consult the Jenkins documentation for details.  Once started, access Jenkins through your browser (usually at `http://localhost:8080`).

### 3.  Configure Maven in Jenkins

    * Go to "Manage Jenkins" -> "Global Tool Configuration".
    * Scroll down to the "Maven" section.
    * Click "Add Maven".
    * Configure the Maven installation:
        * **Name:** Provide a name (e.g., "Maven 3.8.6").
        * **Installation:**
            * If Maven is installed on your system, uncheck "Install automatically" and enter the `MAVEN_HOME` path.
            * To have Jenkins download and manage Maven, leave "Install automatically" checked and select the desired version.
    * Click "Save".

### 4.  Create a New Freestyle Project

    * On the Jenkins dashboard, click "New Item".
    * Enter a project name (e.g., "JavaMavenBuild").
    * Select "Freestyle project" and click "OK".

### 5.  Configure the Freestyle Project

    * **Source Code Management:**
        * **Git:** If your project is in a Git repository, configure the repository URL and any necessary credentials.
        * **None:** If your project is in a local directory on the Jenkins machine, you can select "None" and copy the files to the Jenkins workspace, or configure Jenkins to access the directory.

    * **Build Triggers:**
        * Configure how Jenkins should detect changes to your project and initiate a build (e.g., polling a Git repository, using webhooks).  For manual builds, you can skip this section.

    * **Build Environment:**
        * Configure any environment settings required for your build (e.g., setting environment variables).

    * **Build:**
        * Click "Add build step" and select "Invoke top-level Maven targets".
        * **Maven Version:** Select the Maven configuration from "Global Tool Configuration" (e.g., "Maven 3.8.6").
        * **Goals:** Enter `clean package`.
            * `clean`:  Removes previously built artifacts.
            * `package`:  Compiles the Java code and creates a distributable archive (e.g., a JAR file).
        * Click "Save".

### 6.  Run the Build

    * On the project page, click "Build Now".
    * Jenkins will start the build process.  The build status will appear in the "Build History" section.
    * Click on the build number to view the "Console Output".
    * A successful build will display a "BUILD SUCCESS" message in the console.
