# Setup a local workspace

This guide explains how to set up your environment for development of JabRef. It includes information about prerequisites, configuring your IDE, and running JabRef locally to verify your setup.

For a complete step-by-step guide (using IntellJ as the IDE), have a look at the following video instructions:

<p align="center">
  <a href="http://www.youtube.com/watch?v=FeQpygT0314"><img src="http://img.youtube.com/vi/FeQpygT0314/0.jpg" /></a>
</p>

## Prerequisites

### Java Development Kit 13

A working Java 13 installation is required. In the command line (terminal in Linux, cmd in Windows) run `javac -version` and make sure that the reported version is Java 13 (e.g `javac 13.0.1`). If `javac` is not found or a wrong version is reported, check your PATH environment variable, your JAVA_HOME environment variable or install the most recent JDK.

### git

It is strongly recommend that you have git installed: [official installation instructions](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

* In Debian-based distros: `sudo apt-get install git`
* In Windows: [Download the installer](http://git-scm.com/download/win) and install it. For more advanced tooling, you may use [Git Extensions](http://gitextensions.github.io/) or [SourceTree](https://www.sourcetreeapp.com/). - See also our [tool recommendations](tools.md) for installation hints including [chocolatey](https://chocolatey.org/).

If you do not yet have a GitHub account, please [create one](https://github.com/join).

### IDE

We suggest [IntelliJ IDEA](https://www.jetbrains.com/idea/) or [Eclipse](https://eclipse.org/) (`2019-12` or newer).

Under Ubuntu Linux, you can follow the [documentation from the Ubuntu Community](https://help.ubuntu.com/community/EclipseIDE#Download_Eclipse) or the [step-by-step guideline from Krizna](www.krizna.com/ubuntu/install-eclipse-in-ubuntu-12-04/) to install Eclipse. Under Windows, download it from [www.eclipse.org](http://www.eclipse.org/downloads/) and run the installer.

## Get the code

### Fork JabRef into your GitHub account

1. Log into your GitHub account
2. Go to <https://github.com/JabRef/jabref>
3. Create a fork by clicking at fork button on the right top corner
4. A fork repository will be created under your account (https://github.com/YOUR_USERNAME/jabref)

### Clone your forked repository on your local machine

* In a command line, navigate to the folder where you want to place the source code (parent folder of `jabref/`). To prevent issues along the way, it is strongly recommend to choose a path that does not contain any special (non-ASCII or whitespace) characters.
* Run `git clone --depth=10 https://github.com/YOUR_USERNAME/jabref.git`. The `--depth--10` is used to limit the download to ~20 MB instead of downloading the complete history (~800 MB). If you want to dig in our commit history, feel free to download everything.
* Go to the newly created jabref folder: `cd jabref`
* Generate additional source code: `./gradlew assemble`
* Start JabRef: `./gradlew run`
  * The JabRef's GUI should now start up.

## Configure your IDE

### Setup for IntelliJ IDEA

IntelliJ IDEA fully supports Gradle as a build tool, but also has an internal
build system which is usually faster. For JabRef, Gradle is required to make a
full build but once set up, IntelliJ IDEA's internal system can be used for sub-sequent
builds.

To configure IntelliJ IDEA for developing JabRef, you should first ensure that
you have enabled both bundled plugins *Gradle* and *Gradle Extension*

* Navigate to **File | Settings | Plugins | Installed** and check that you have
the *Gradle* and *Gradle Extension* enabled.

After that, you can open `jabref/build.gradle` as a project.
It is crucial that Java 13 is used consistently for the JabRef project which
includes ensuring the right settings for your project structure, Gradle build,
and run configurations.

* Ensure you have a Java 13 SDK configured by navigating to
**File | Project Structure | Platform Settings | SDKs**. If you don't have one, add a new Java JDK and point it to the
location of a JDK 13.
* Navigate to **File | Project Structure | Project** and ensure that the projects' SDK is Java 13
* Navigate to **File | Settings | Build, Execution, Deployment | Build Tools | Gradle** and select the Java 13 SDK as
the Gradle JVM at the bottom.

To prepare IntelliJ's build system two additional steps are required

* Navigate to **File | Settings | Build, Execution, Deployment | Compiler | Java Compiler**, and under
"Override compiler parameters per-module" add ([+]) the following compiler arguments for the `JabRef.main` module:
   ```
   --add-exports=javafx.controls/com.sun.javafx.scene.control=org.jabref
   --add-exports=org.controlsfx.controls/impl.org.controlsfx.skin=org.jabref
   ```
* Enable annotation processors by navigating to
**File | Settings | Build, Execution, Deployment | Compiler | Annotation processors** and check "Enable annotation processing"

#### Using Gradle from within IntelliJ IDEA

Ensuring JabRef builds with Gradle should always the first step because, e.g. it generates additional sources that are
required for compiling the code.
After adjusting all settings mentioned earlier, your first step should be to

* Open the Gradle Tool Window with the small button that can usually be found on the right side of IDEA or navigate to
**View | Tool Windows | Gradle**.
* In the Gradle Tool Window, press the "Reimport All Gradle Projects" button to ensure that all settings are up-to-date
with the setting changes.

After that, you can use the Gradle Tool Window to build all parts JabRef and run it. To do so, expand the JabRef
project in the Gradle Tool Window and navigate to Tasks. From there, you can

* Build and run JabRef by double-clicking **JabRef | Tasks | application | run**.
After that a new entry called "jabref [run]" will appear in the run configurations.
* Now you can also select "jabref [run]" and either run or debug the application from within IntelliJ.

You can run any other development task in a similar way.
Equivalently, this can also be executed from the terminal by running `./gradlew run`.

#### Using IntelliJ's internal build system

You can use IntelliJ IDEA's internal build system for compiling and running JabRef during development which is
usually more responsive. However, **it's important** that you understand that JabRef relies on generated sources
which are only build through Gradle. Therefore, to build or update these dependencies you need to run the `assemble`
Gradle task at least once.

To use IntelliJ IDEA's internal build system when you build JabRef through **Build | Build Project** or use the provided
"JabRef Main" run configuration, ensure that

* in **File | Settings | Build, Execution, Deployment | Build Tools | Gradle** the setting "Build and run using" and
"Test using" is set to "IntelliJ IDEA".

To use the "JabRef Main" run configuration, open **Run | Edit Configurations... | Application | JabRef Main** and

* Verify, that your JDK 13 is used
* Set "VM Options" to the following:

    ```
    --patch-module org.jabref=build/resources/main
    --add-exports javafx.controls/com.sun.javafx.scene.control=org.jabref
    --add-exports org.controlsfx.controls/impl.org.controlsfx.skin=org.jabref
    --add-exports javafx.graphics/com.sun.javafx.scene=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.scene.traversal=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.css=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.behavior=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.inputmap=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.event=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.collections=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.runtime=org.controlsfx.controls
    --add-exports javafx.web/com.sun.webkit=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.css=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix
    --add-exports com.oracle.truffle.regex/com.oracle.truffle.regex=org.graalvm.truffle
    --add-opens javafx.controls/javafx.scene.control=org.jabref
    --add-opens org.controlsfx.controls/org.controlsfx.control.textfield=org.jabref
    --add-opens javafx.controls/javafx.scene.control.skin=org.controlsfx.controls
    --add-opens javafx.graphics/javafx.scene=org.controlsfx.controls
    --add-opens javafx.controls/com.sun.javafx.scene.control=org.jabref
    --add-opens javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix
    --add-opens javafx.base/com.sun.javafx.binding=com.jfoenix
    --add-opens javafx.graphics/com.sun.javafx.stage=com.jfoenix
    --add-opens javafx.base/com.sun.javafx.event=com.jfoenix
    ```

     Optionally the following entries can also be added (but they currently only produce warnings and they are not needed):

   ```
    --patch-module test=fastparse_2.12-1.0.0.jar
    --patch-module test2=fastparse-utils_2.12-1.0.0.jar
    --patch-module test3=sourcecode_2.12-0.1.4.jar
   ```

Essentially, you now have the best of both worlds: You can run Gradle tasks using the Gradle Tool Window and unless you
haven't made changes to input files that generate sources, you can compile and run with IntelliJ's faster internal
build system.

#### Using JabRef's code-style

Contributions to JabRef's source code need to have a code formatting that is consistent with existing source code.
For that purpose, JabRef provides code-style and check-style definitions.

* Install the [CheckStyle-IDEA plugin](http://plugins.jetbrains.com/plugin/1065?pr=idea), it can be found via the plug-in repository:
    1. Navigate to **File | Settings | Plugins | Marketplace** and search for "Checkstyle" and choose "CheckStyle-IDEA"
    2. Close the settings afterwards and restart IntelliJ
* Go to **File | Settings | Editor | Code Style**
* Click on the settings wheel (next to the scheme chooser), then click "Import Scheme"
* Select the IntelliJ configuration file `config/IntelliJ Code Style.xml`.
* Go to **File | Settings | Other Settings | Checkstyle | Configuration File**
    1. Import the CheckStyle configuration file by clicking the [+] button
    2. For the description provide e.g. "CheckStyle"
    3. Click "Browse" and choose `config/checkstyle/checkstyle.xml`
    4. Click "Next" and "Finish"
    5. Activate the CheckStyle configuration file by ticking it in the list
    6. Save settings by clicking "OK"

#### Troubleshooting when using both IDEA and Eclipse

If you have configured Eclipse for the same project (the required steps are described below),
then the additionally added file `Log4jPlugins.java` must be excluded from the compilation process,
otherwise an error will occur during the compilation of the project:

* **File | Settings | Build, Execution, Deployment | Compiler | Excludes** and add the following file to the
list ([+]), in order to exclude it:
    * `src/main/java/org/jabref/gui/logging/plugins/Log4jPlugins.java`

### Setup for Eclipse

Make sure your Eclipse installation us up to date, Eclipse 2019-12 or newer is required.

1. Run `./gradlew run` to generate all resources and to check if JabRef runs.
   * The JabRef GUI should finally appear.
   * This step is only required once.
2. Run `./gradlew eclipse`
   * **This must always be executed, when there are new upstream changes.**
3. Copy the file `Log4jPlugins.java` from `build/generated/sources/annotationProcessor/java/main/org/jabref/gui/logging/plugins` to `src/main/java/org/jabref/gui/logging/plugins/`
   * Usually, the folder `plugins` must be created for that.
4. Open or import the existing project in Eclipse as Java project.
   * Remark: Importing it as gradle project will not work correctly.
   * Refresh the project in Eclipse
5. Create a run/debug configuration for the main class `org.jabref.JabRefLauncher` and/or for `org.jabref.JabRefMain` (both can be used equivalently)
   * In the tab "Arguments" of the run/debug configuration, enter the following runtime VM arguments:
     * Set "VM Arguments" to:

    ```
    --patch-module test=fastparse_2.12-1.0.0.jar
    --patch-module test2=fastparse-utils_2.12-1.0.0.jar
    --patch-module test3=sourcecode_2.12-0.1.4.jar
    --add-exports javafx.controls/com.sun.javafx.scene.control=org.jabref
    --add-exports org.controlsfx.controls/impl.org.controlsfx.skin=org.jabref
    --add-exports javafx.graphics/com.sun.javafx.scene=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.scene.traversal=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.css=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.behavior=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.inputmap=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.event=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.collections=org.controlsfx.controls
    --add-exports javafx.base/com.sun.javafx.runtime=org.controlsfx.controls
    --add-exports javafx.web/com.sun.webkit=org.controlsfx.controls
    --add-exports javafx.graphics/com.sun.javafx.css=org.controlsfx.controls
    --add-exports javafx.controls/com.sun.javafx.scene.control.behavior=com.jfoenix
    --add-exports com.oracle.truffle.regex/com.oracle.truffle.regex=org.graalvm.truffle
    --patch-module org.jabref=build\resources\main
    ```

6. Optional: Install the [e(fx)clipse plugin](http://www.eclipse.org/efxclipse/index.html) from the Eclipse marketplace:
   1. Help -> Eclipse Marketplace... -> Search tab
   2. Enter "e(fx)clipse" in the search dialogue
   3. Click "Go"
   4. Click "Install" button next to the plugin
   5. Click "Finish"
7. Now you can build and run/debug the application by either using "JabRefLauncher" or "JabRefMain". This is the recommended way, since the application starts quite fast.

## Final comments

Got it running? GREAT! You are ready to lurk the code and contribute to JabRef. Please make sure to also read our [contribution guide](https://github.com/JabRef/jabref/blob/master/CONTRIBUTING.md).

## Common issues

### Java installation

An indication that `JAVA_HOME` is not correctly set or no JDK 13 is installed is following error message:

```text
compileJava FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':compileJava'.
> java.lang.ExceptionInInitializerError (no error message)
```

Another indication is following output

```text
java.lang.UnsupportedClassVersionError: org/javamodularity/moduleplugin/ModuleSystemPlugin has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0
```

### Problems with generated source files

In rare cases you might encounter problems due to out-dated automatically generated source files. Running `./gradlew clean` deletes these old copies. Do not forget to run at least `./gradlew eclipse` or `./gradlew build` afterwards to regenerate the source files.
