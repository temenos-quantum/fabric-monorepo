# Fabric Monorepo

**Fabric** allows integrations to leverage custom [pre-processors, post-processors](https://docs.kony.com/konylibrary/konyfabric/kony_fabric_user_guide/Default.htm#Java_Pre-Post_Samples.htm) and [services](https://docs.kony.com/konylibrary/konyfabric/kony_fabric_user_guide/Default.htm#Java_Adapter.htm), which can be written in **Java** —among other options.

For projects creating these custom assets usign Java, versioning the source code of such assets becomes a necessity. One proposed and *recommended* practice is to use a [Monorepo](https://en.wikipedia.org/wiki/Monorepo) approach, whereby the Fabric application or service (as it results from exporting it from Fabric and decompressing it) and the source code for its Java assets, are *versioned together*.

**App Factory**'s v9 release will support the import of these **Fabric** applications while building their Java dependencies from Git repositories following this monorepo approach.

The following tree depicts an example of what such a monorepo could look like.

```
Monorepo
│
├── .gitignore
├── FabricAppOrService1
│   └── Apps
│       ├── FooApp
│       │   ├── Meta.json
│       │   └── icon.png
│       ├── Version.json
│       ├── _Identity
│       ├── _Integration
│       ├── _JARs
│       ├── _ObjectServices
│       └── _Orchestration
│
├── FabricAppOrService2
├── ...
├── FabricAppOrServiceN
│
└── path
    └── to
        └── java
            ├── .gitignore
            ├── pom.xml
            └── src
               └── com
                   └── acme
                       ├── CustomService1.java
                       ├── ...
                       ├── CustomServiceN.java
                       │
                       ├── PostProcessor1.java
                       ├── ...
                       ├── PostProcessorN.java
                       │
                       ├── PreProcessor1.java
                       ├── ...
                       └── PreProcessorN.java

```
**Notice**

* The same monorepo can potentially hold several Fabric applications or services, and that `path/to/java` just represents any custom path of your choosing.
* The `_JARs` directory in line 21 above is only represented for the sake of completeness, as the contents of that directory when you export a Fabric application are just Java JAR files, which should ideally not be pushed to source control.
* The tree depicts a [Maven POM file](https://howtodoinjava.com/maven/maven-pom-files/), as Maven is the only dependency manager currently supported by **App Factory**.

Another more elaborate structure is to develop the different Java assets in different projects. In such scenarios, and because all of these projects will likely have the same dependencies, the use of a [parent POM file](https://howtodoinjava.com/maven/maven-parent-child-pom-example/) is supported.

```
Monorepo
│
├── .gitignore
├── FabricAppOrService1
│   └── Apps
│       ├── FooApp
│       │   ├── Meta.json
│       │   └── icon.png
│       ├── Version.json
│       ├── _Identity
│       ├── _Integration
│       ├── _JARs
│       ├── _ObjectServices
│       └── _Orchestration
├── FabricAppOrService2
├── ...
├── FabricAppOrServiceN
│
└── path
    └── to
        └── java
            ├── parent-pom.xml
            │
            ├── CustomService1
            │   ├── .gitignore
            │   ├── pom.xml
            │   └── src
            ├── ...
            ├── CustomServiceN
            │
            ├── PostProcessor1
            │   ├── .gitignore
            │   ├── pom.xml
            │   └── src
            ├── ...
            ├── PostProcessorN
            │
            ├── PreProcessor1
            │   ├── .gitignore
            │   ├── pom.xml
            │   └── src
            ├── ...
            └── PreProcessorN
```
