# Convert deprecated IOUtils method invocations with their charset specific equivalent

** org.openrewrite.java.migrate.apache.commons.io.ApacheIOUtilsUseExplicitCharset**
_This convert deprecated `IOUtils` method invocations with their charset specific equivalent, e.g. converts `IOUtils.readLines(inputStream);` to `IOUtils.readLines(inputStream, StandardCharsets.UTF_8);`_

## Source

[Github](https://github.com/openrewrite/rewrite-migrate-java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite.recipe/rewrite-migrate-java/1.7.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 1.7.0

## Options

| Type | Name | Description |
| -- | -- | -- |
| `String` | encoding | *Optional*. The default encoding to use, must be a standard charset. |


## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite.recipe:rewrite-migrate-java:1.7.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.22.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.apache.commons.io.ApacheIOUtilsUseExplicitCharset")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:1.7.0")
}
```
{% endcode %}
{% endtab %}

{% tab title="Maven" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>4.25.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.java.migrate.apache.commons.io.ApacheIOUtilsUseExplicitCharset</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
            <version>1.7.0</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipesorg.openrewrite.java.migrate.apache.commons.io.ApacheIOUtilsUseExplicitCharset`