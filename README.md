# Shade Minimize Jar Example

This project present minimum example how Minimizing a Fat Jar works in Maven and Gradle.

The following command:

```shell
mvn clean install
```

produces a Fat Jar that contains only part of Guava package:

```shell
jar -tf target/shade-minimize-jar-example-0.0.1.jar | grep .class
```

Shows only 2 classes from `Guava` and one from `commons-lang3` included in Jar (I don't count package-info.class): 

```text
org/apache/commons/lang3/BitField.class
com/google/common/annotations/Beta.class
com/google/common/annotations/GwtCompatible.class
...
```

It's because `@Beta` is used in my code and `@Beta` uses `@GwtCompatible`.
The same for `BitField`.

When executing a Gradle build:

```shell
./gradlew clean build --console=plain 
```

Then `com.github.johnrengelman.shadow` plugin include the whole Guava dependency:

```shell
jar -tf build/libs/shade-minimize-jar-example-all.jar | grep .class
```

```text
com/google/common/annotations/Beta.class
com/google/common/annotations/GwtCompatible.class
com/google/common/annotations/GwtIncompatible.class
com/google/common/annotations/VisibleForTesting.class
com/google/common/base/Absent.class
...
com/google/thirdparty/publicsuffix/TrieParser.class
org/apache/commons/lang3/BitField.class
com/google/common/util/concurrent/internal/InternalFutureFailureAccess.class
...
```

Why it's such difference?

Why `com.github.johnrengelman.shadow` plugin is not able to remove unused classes from Guava in shadow Jar?
