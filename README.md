# java-scriptengine Jigsaw example

Example project to use the `java-scriptengine` in .

## Unnamed module

When you run your java application in a runtime environment >= Java 9
and you do not care about Jigsaw modules then your classes
will run in the unnamed-module. 

The following command shows how classes in the unnamed module can
use the `java-scriptengine`
```console
./gradlew :unnamed-module:run
```

## Named module

When you run your java application in a runtime environment >= Java 9
and you have added the `module-info.java` in the root of your project
then your classes will run inside a Jigsaw module.

This has some impact when using the `java-scriptengine`
because the compiled script class will be running in the unnamed module. 
Classes from a named module will *not* be visible to the compiled script class.

The following command will show the problem:
```console
./gradlew :named-module:run
```

The simpler scripts that do not import classes from the calling application are actually working fine
but the more complex scripts that
import `ch.obermuhlner.scriptengine.example.Person` are failing. 
