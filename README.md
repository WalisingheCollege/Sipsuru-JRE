# Sipsuru-JRE
Minimal JRE and JVM for Sipsuru Apps (Utils and Addons)

JLink JDK -> Sipsuru JRE

   ## Required Modules (for now) 
   - ```java.base```
   - ```java.desktop```
   > Note that in future we'll need to add more modules to JRE (Like crypto when we create authentication system)

   ## How to
   - You need to have a **jdk installed and configured** (Adding *bin* folder to *path* environment variable will make your job easier) to create Sipsuru JRE
     - **Java 22+** is a requirement and we highly reccomend you to use either **Oracle JDK** or **Oracle GraalVM**
     - Other JDK's should work but we're currently encountering to errors with IBM JDK.
     - Amazan Corretto and Microsoft JDK can be used.
     - Jetbrains JRE is not reccomended as they do UI improvements, which may affect our UI negative. And currently they are at Java 21, which can't be used.
   - Know what modules are needed.
     - The modules given in previous section are thre requirements for now.
     - But we highly reccoment you to check the required modules after building each fat/uber jar. You can do it by
         - ```jdeps --module-path out -s --module jlinkModule``` or
         - ```jdeps -s jarFile.jar``` or etc.
     - Then you'll have a list of required modules by that program. Do the same to all Sipsuru applications that need a JRE and combine them.
     - Then you can create the JRE, the *Sipsuru JRE* with
         - ```jlink --compress zip-9 --module-path <path> --add-modules <modules pointed by jdep> --output "Sipsuru JRE"```
           - ```<path>``` is jdk's jmod folder path &
           - ```<modules pointed by jdep>``` is required modules combine for all Sipsuru Applications.
           - Note that if ```<path>``` for ```--module-path``` isn't provided **current jdk's mods** will be used.
          
     - Note that, Sipsuru Collection use "Sipsuru JRE" env since after 1.0.0 release. Corrected it.
     - ***After all you need to add env: `SIPSURU_JRE`, pointing `JRE's home directory` (Not the bin)***
       > Note that, we've changed `SIPSURU_JVM` (Old env) to `SIPSURU_JRE`. We have to change Launch4J configs as well.
       > ## `SIPSURU_JRE` is a requrement for running, `Sipsuru Dynamic Poster Customizer`, `Sipsuru Media Downloader` & `Sipsuru Share & Receive.`
