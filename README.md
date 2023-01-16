= Shade Minimize Jar Example

This project present minimum example how Minimizing a Fat Jar works in Maven and Gradle.

```shell
mvn install
```

produce a Fat Jar that contains only part of Guava package:

```shell
jar -tf target/shade-minimize-jar-example-0.0.1.jar
```

Shows only 2 classes included in Jar (I don't count package-info.class)

```text
com/google/common/annotations/Beta.class
com/google/common/annotations/GwtCompatible.class

```

It's because `@Beta` is used in my code and `@Beta` uses `@GwtCompatible`.

When executing a Gradle build:

```shell
./gradlew clean build --console=plain 
```

Then `com.github.johnrengelman.shadow` plugin include the whole Guava dependency:

```shell
jar -tf build/libs/shade-minimize-jar-example-all.jar
```

```text
com/google/common/annotations/Beta.class
com/google/common/annotations/GwtCompatible.class
com/google/common/annotations/GwtIncompatible.class
com/google/common/annotations/VisibleForTesting.class
com/google/common/base/
com/google/common/base/Absent.class
...
```

