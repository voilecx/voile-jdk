# VoileJDK

Builds of VoileJDK, a Java runtime based on OpenJDK 27. This repository holds releases only:
there is no source here, and nothing is built here.

## Downloads

Every build is a [release](https://github.com/voilecx/voile-jdk/releases) with two files:

| File | What it is |
| --- | --- |
| `voilejdk-<version>-windows-x86_64.zip` | The runtime for 64-bit Windows |
| `voilejdk-<version>-windows-x86_64.zip.sha256` | The SHA-256 of that archive |

Windows x86-64 is the only platform published here.

## What is in the archive

```
voilejdk-<version>-windows-x86_64/
  bin/java.exe       the launcher, with the VM and the native libraries linked into it
  bin/modules        the runtime's classes
  bin/classes.jsa    the class data sharing archive
  lib/               time zone and font configuration data
  LICENSE, ASSEMBLY_EXCEPTION, ADDITIONAL_LICENSE_INFO
```

The image is static: `java.exe` needs no `jvm.dll` and no other DLL of the JDK beside it, and
imports only DLLs that Windows ships. Keep the files together in the layout above; the launcher
finds `modules` and `classes.jsa` beside itself.

It is a runtime, not a development kit. There is no `javac`, and only these modules are in it:

`java.base`, `java.compiler`, `java.datatransfer`, `java.desktop`, `java.logging`,
`java.management`, `java.naming`, `java.net.http`, `java.prefs`, `java.security.sasl`, `java.sql`,
`java.transaction.xa`, `java.xml`, `jdk.httpserver`, `jdk.localedata`, `jdk.management`, `jdk.net`,
`jdk.unsupported`, `jdk.zipfs`.

## Using it

Unpack the archive anywhere and run the launcher:

```powershell
.\voilejdk-<version>-windows-x86_64\bin\java.exe -version
```

```powershell
.\voilejdk-<version>-windows-x86_64\bin\java.exe -cp app.jar com.example.Main
```

`java --list-modules` prints the modules of the build you have.

## Checking a download

```powershell
(Get-FileHash .\voilejdk-<version>-windows-x86_64.zip -Algorithm SHA256).Hash
```

The value must equal the one in the `.sha256` file of the same release.

## Requirements

64-bit Windows on an x86-64 processor.

## License

VoileJDK is based on OpenJDK and is distributed under the GNU General Public License,
version 2, with the Classpath Exception. The license texts are in every archive: `LICENSE`,
`ASSEMBLY_EXCEPTION` and `ADDITIONAL_LICENSE_INFO`.

Java and OpenJDK are trademarks or registered trademarks of Oracle and/or its affiliates.
