---
slug: 01-create-project
id: ia8vpw1gqjex
type: challenge
title: Topic 1 - Getting started with a Quarkus QuickStart
teaser: Topic 1 - Getting started with a Quarkus QuickStart
notes:
- type: text
  contents: |-
    In this track, you will get an introduction to [Quarkus](https://quarkus.io).

    |What you need to know before you start:|
    |----|
    |In order to get full benefit from taking this track you should...<br>• Have experience programming applications in Java using the [Maven](https://maven.apache.org/) framework.<br>• Understand how Maven uses the Project Object Model (POM) to manage artifacts and plugins.<br>• Know how Maven applications are described and built using a Maven [`pom.xml`](https://maven.apache.org/guides/introduction/introduction-to-the-pom.html) file.|

    <br>

    # What is Quarkus?

    Quarkus is a Kubernetes Native Java stack tailored for [GraalVM](https://www.graalvm.org/) and [OpenJDK HotSpot](https://openjdk.java.net/groups/hotspot/). Quarkus is also crafted from the best of breed Java libraries and standards. Amazingly fast boot time, incredibly low RSS memory (not just heap size!) offering near instant scale up and high density memory utilization in container orchestration platforms like Kubernetes. Quarkus uses a technique called compile time boot. [Learn more](https://quarkus.io/vision/container-first).

    Quarkus maximizes the Developer Productivity with the following features:
    * [Zero-config Live coding](https://quarkus.io/guides/maven-tooling#dev-mode/)
    * [Dev Services](https://quarkus.io/guides/dev-services)
    * [Continuous testing](https://quarkus.io/guides/continuous-testing)
    * [Dev UI](https://quarkus.io/guides/dev-ui)
    * [Command Line Interface (CLI)](https://quarkus.io/guides/cli-tooling)
    * [Remote Development](https://quarkus.io/guides/maven-tooling#remote-development-mode)

    Application requirements have changed over the last few years. For any application to succeed in the era of big data, IoT or cloud computing, adhering to the principles and practices of the [reactive architecture style](https://developers.redhat.com/coderland/reactive/reactive-intro) is essential.
tabs:
- title: Terminal 1
  type: terminal
  hostname: crc
- title: Visual Editor
  type: code
  hostname: crc
  path: /root/projects/quarkus
- title: Terminal 2
  type: terminal
  hostname: crc
- title: Dev UI
  type: service
  hostname: crc
  path: /q/dev
  port: 8080
difficulty: basic
timelimit: 300
---
In this topic you will use Quarkus to create an API application that publishes a `/hello` endpoint. Also, you will use dependency injection to build on the `/hello` endpoint to publish an additional endpoint `/hello/greeting` by creating a **Greeting** bean.

The Maven project you're going to create has the following structure:
* An `org.acme.quickstart.GreetingResource` resource exposed on `/hello`
* An associated unit test
* A landing page that is accessible on `http://localhost:8080` after starting the application
* An example `Dockerfile`s for a variety of build targets (native, jvm, etc)
* The application configuration file


# Creating a basic project using Quarkus

`Step 1:` Run the following command in the **Terminal 1** window to the left to go to the working directory for the Quarkus application you're going to create. (The directory was created as part of the tracks setup process.)

```
cd /root/projects/quarkus/ && pwd
```

You'll get the following output.

```
/root/projects/quarkus/
```

----

`Step 2:` Run the following command in the **Terminal 1** window to create the basic Maven project.

```
mvn io.quarkus:quarkus-maven-plugin:2.16.2.Final:create \
    -DprojectGroupId=org.acme \
    -DprojectArtifactId=getting-started \
    -DclassName="org.acme.quickstart.GreetingResource" \
    -Dpath="/hello"
```

The `mvn` command shown above invokes the installation process that creates all the files and artifacts needed to get the application up and running.

The snippet of code below shows you the output you'll get at the end of the installation process. The date information will be different in your output.

```
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```

# Running the Application

You are ready to run the Quarkus application

`Step 3` Run the following command in Terminal 1 to the left to compile and run the demonstration project.

```
mvn quarkus:dev -Dquarkus.http.host=0.0.0.0 -f /root/projects/quarkus/getting-started
```

There will be a lot of output to the screen. When the process is finished running, you will see the following:

```
__  ____  __  _____   ___  __ ____  ______
 --/ __ \/ / / / _ | / _ \/ //_/ / / / __/
 -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \
--\___\_\____/_/ |_/_/|_/_/|_|\____/___/
INFO  [io.quarkus] (Quarkus Main Thread) getting-started 1.0.0-SNAPSHOT on JVM (powered by Quarkus x.x.x.Final) started in 1.194s. Listening on: http://0.0.0.0:8080
INFO  [io.quarkus] (Quarkus Main Thread) Profile dev activated. Live Coding activated.
INFO  [io.quarkus] (Quarkus Main Thread) Installed features: [cdi, resteasy]
--
Tests paused, press [r] to resume, [h] for more options>
```

----

Let's verify that the demonstration application is actually up and running.

`Step 4:` Click the **Terminal 2** tab on the horizontal menu bar over the pane to the left.

----

`Step 5:` Run the following command in the **Terminal 2** window that appears:

```
curl -w "\n" localhost:8080/hello/
```

You'll get the following output:

```
Hello from RESTEasy Reactive
```

As you can see, the service endpoint is up and running.

# Exercising the Quarkus Live Reload Feature

A useful feature of Quarkus is that it will update and redeploy an application automatically when you make a code change.

Let's take a look.

----

You are going to change the output of the **Hello App** API application from `Hello RESTeasy Reactive` to `Hola RESTeasy Reactive` by doing nothing more than changing one line of code. Quarkus will take care of everything else.

----

`Step 6:`  Click the **Visual Editor** tab in the horizontal menu bar over the terminal window to the left. You'll see the code editor that is part of the interactive learning environment.

----

`Step 7a:`  Scroll through the file tree on the left side of the editor until you get to the file `/root/projects/quarkus/getting-started/src/main/java/org/acme/quickstart/GreetingResource.java`. Then click on the filename in the tree.


`Step 7b:`  Change the word `Hello` to `Hola` at Line 14 in the file `GreetingResource.java` as shown in the figure below at Callout 2.

![Change to Hola](../assets/change-to-hola-01.png)

`Step 7c:`  Click the save icon to save your changes, as shown in the figure above at Callout 3.

----

`Step 8:` Return to **Terminal 2** and tun the following command in the terminal window:

```
curl -w "\n" localhost:8080/hello/
```

You'll get the following output with the new phrase:

```
Hola from RESTEasy Reactive
```

As you can see, all you did was change a string in a line of code. Quarkus did the rest!

# Working with the Dev UI

When running in Developer mode, a Quarkus application exposes a useful UI for inspecting and making on-the-fly changes to the application (much like live coding mode). The Quarkus UI allows you to quickly visualize a number of things.

You can see all the extensions currently loaded. You can see and edit their configuration values.

Also, you can see an extension's status and go directly to its documentation.

----

`Step 9:` Click the tab `Dev UI` on the horizontal menu bar over the interactive learning window on the left.

You'll see the Dev UI for your running application as shown in the figure below.

![Dev UI](../assets/config-editor-00.png)

----

`Step 10:`  Click on the `Config Editor` link within the `Configuration` file to see and make updates to the configuration as shown in the figure below.

![Config Editor](../assets/config-editor-01.png)

As you can see in the figure below, the `Config Editor` allows developers to make configuration changes or experiment with various application settings in a very detailed manner.

![Config Editor Detail](../assets/config-editor-02.png)

|NOTE:|
|----|
|The Dev UI is only enabled when in `developer` mode. It is not deployed when in `production` mode because, as the name implies, it's designed for developers to use during development. For more detail on what you can do in developer mode, check out the [Dev UI Guide](https://quarkus.io/guides/dev-ui).|

# Implementing continuous testing

Quarkus enables you to automatically and continuously run your application's unit tests when you are in developer mode. (You put this instance of the application into developer mode when you started it using the command `mvn quarkus:dev`).

As you might recall, when you ran `mvn quarkus:dev` you were presented with the prompt  `Tests paused, press [r] to resume, [h] for more options>` as the end of installation process.

Entering the character `r` at the testing prompt will run the application's unit test.

----

`Step 11:` Click the **Terminal 1** tab and then press the `r` key in the terminal window. (The installation process will still be running in the terminal.)

As you will see from all the red error text in Terminal 1 on the left, the unit tests are failing. The reason for the failure is that previously you changed the word `Hello` to `Hola`. The unit test expects the output `Hello RESTEasy Reactive`. The output failed to meet the expectation.

Let's fix the code and get the tests to pass.

----

`Step 12:` Click the **Visual Editor** tab in horizontal menu bar over the interactive learning window.

----

`Step 13:` Navigate to the file `/root/projects/quarkus/getting-started/src/main/java/org/acme/quickstart/GreetingResource.java`.

----

`Step 14:` Change `Hola RESTEasy Reactive` back to `Hello RESTEasy Reactive` in the editor.

----

`Step 15:` Click the **Save File** icon on the top of the **Visual Editor** as shown above at `Step 7c`.


As soon as your reset the code, Quarkus automatically re-runs the test.

----

`Step 16:` Click the **Terminal 1** tab to go back a review the output from the continuous testing output.

----

`Step 17:` Look at the output at the bottom of the **Terminal 1** window. You'll see output similar to the following.

```
All 1 test is passing (0 skipped), 1 test was run in 618ms. Tests completed at 03:33:55 due to changes to GreetingResource.class.
```

Quarkus was smart enough to detect that you made a change to the code and ran the relevant test automatically.

The way Quarkus works is that it analyzes your unit tests and only re-runs the tests that are affected by code changes.

# Congratulations!

You've learned how to create a new Quarkus application. Then, you could keep developing the application without recompiling, rebuilding, redeploying, and restarting the application runtime based on Quarkus Live Coding. You also saw how Quarkus runs tests continuously to turbocharge your development tasks and facilitate test-driven development.

----

# What's Next?

Congratulations on completing this lab. Keep learning about OpenShift:

* Visit the [Red Hat Developer learning page](https://developers.redhat.com/learn) for more labs and resources
* [Want to try a free, instant 30-day OpenShift cluster? Get started with the Developer Sandbox for Red Hat OpenShift](https://developers.redhat.com/developer-sandbox)

Don't forget to finish the lab and rate your experience on the next page. Thanks for playing!
