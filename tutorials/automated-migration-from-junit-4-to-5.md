---
description: Migrate your tests in minutes
---

# Migrating from JUnit 4 to 5

This tutorial will show you how to get your JUnit 4 tests migrated to being JUnit 5 tests, ready to be run by the JUnit Jupiter engine, in only a few minutes.

In broad terms, the steps are:

1. Apply the rewrite plugin to your build tool
2. Take a compile-time-only dependency on rewrite-testing-frameworks
3. Configure the rewrite plugin to apply the JUnit Migration Recipe
4. Run the migration
5. Inspect the results
6. Commit to source control

For most builds this whole process should take only a few minutes.

## Example Before and After

Here's a JUnit 4 test:

```java
package org.openrewrite.java.testing.junit5;

import org.junit.AfterClass;
import org.junit.Assert;
import org.junit.Before;
import org.junit.Rule;
import org.junit.Test;
import org.junit.rules.ExpectedException;
import org.junit.rules.TemporaryFolder;

import java.io.File;
import java.io.IOException;

public class ExampleJunitTestClass {

    @Rule
    public TemporaryFolder folder = new TemporaryFolder();

    @Before
    public void beforeClass() {
        // Some setup
    }

    @AfterClass
    public static void afterClass() {
        // Some teardown
    }

    @Test(expected = RuntimeException.class)
    public void foo() throws IOException {
        File tempFile = folder.newFile();
        File tempFile2 = folder.newFile("filename");
        File tempDir = folder.getRoot();
        File tempDir2 = folder.newFolder("parent", "child");
        File tempDir3 = folder.newFolder("subdir");
        File tempDir4 = folder.newFolder();
        String foo = "foo";
        throw new RuntimeException(foo);
    }

    @Test(expected = IndexOutOfBoundsException.class)
    public void foo2() {
        int arr = new int[]{}[0];
    }

    @Rule
    public ExpectedException throwz = ExpectedException.none();

    @Test
    public void foo3() {
        throwz.expect(RuntimeException.class);
        throw new RuntimeException();
    }

    @Test
    public void assertsStuff() {
        Assert.assertEquals("One is one", 1, 1);
        Assert.assertArrayEquals("Empty is empty", new int[]{}, new int[]{});
        Assert.assertNotEquals("one is not two", 1, 2);
        Assert.assertFalse("false is false", false);
        Assert.assertTrue("true is true", true);
        Assert.assertEquals("foo is foo", "foo", "foo");
        Assert.assertNull("null is null", null);
        Assert.fail("fail");
    }

    @Test(timeout = 500)
    public void bar() { }
}
```

Here's the same test class, automatically migrated to JUnit 5 after following this guide:

```java
package org.openrewrite.java.testing.junit5;

import org.junit.jupiter.api.*;
import org.junit.jupiter.api.io.TempDir;
import org.mockito.Mock;

import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertThrows;

public class ExampleJunitTestClass {

    @TempDir
    public File folder;

    @BeforeEach
    public void beforeClass() {
        // Some setup
    }

    @AfterAll
    public static void afterClass() { 
        // Some teardown
    }

    @Mock
    List<String> mockedList;

    @Test
    public void foo() throws IOException {
        assertThrows(RuntimeException.class, () -> {
            File tempFile = File.createTempFile("junit", null, folder);
            File tempFile2 = newFile(folder, "filename");
            File tempDir = folder;
            File tempDir2 = newFolder(folder, "parent", "child");
            File tempDir3 = newFolder(folder, "subdir");
            File tempDir4 = Files.createTempDirectory(folder.toPath(), "junit").toFile();
            String foo = "foo";
            throw new RuntimeException(foo);
        });
    }

    @Test
    public void foo2() {
        assertThrows(IndexOutOfBoundsException.class, () -> {
            int arr = new int[]{}[0];
        });
    }

    @Test
    public void foo3() {
        assertThrows(RuntimeException.class, () -> {
            throw new RuntimeException();
        });
    }

    @Test
    public void assertsStuff() {
        Assertions.assertEquals(1, 1, "One is one");
        Assertions.assertArrayEquals(new int[]{}, new int[]{}, "Empty is empty");
        Assertions.assertNotEquals(1, 2, "one is not two");
        Assertions.assertFalse(false, "false is false");
        Assertions.assertTrue(true, "true is true");
        Assertions.assertEquals("foo", "foo", "foo is foo");
        Assertions.assertNull(null, "null is null");
        Assertions.fail("fail");
    }

    @Test
    @Timeout(500)
    public void bar() { }

    private static File newFile(File root, String fileName) throws IOException {
        File file = new File(root, fileName);
        file.createNewFile();
        return file;
    }

    private static File newFolder(File root, String ... folders) throws IOException {
        File result = new File(root, String.join("/", folders));
        if(!result.mkdirs()) {
            throw new IOException("Couldn't create folders " + root);
        }
        return result;
    }
}
```

## Build Tool Setup

### Maven

1. Take a `provided` scope dependency on `rewrite-testing-frameworks`.

   ```markup
    <dependency>
        <groupId>org.openrewrite.recipe</groupId>
        <artifactId>rewrite-testing-frameworks</artifactId>
        <version>0.8.1</version>
        <scope>provided</scope>
    </dependency>
   ```

2. Add the rewrite-maven-plugin to your build and configure it to set the `org.openrewrite.java.testing.JUnit5Migration` recipe as active.

   ```markup
    <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>2.4.3</version>
        <configuration>
            <activeRecipes>
                <recipe>org.openrewrite.java.testing.JUnit5Migration</recipe>
            </activeRecipes>
        </configuration>
        <executions>
            <execution>
                <goals>
                    <goal>publish</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
   ```

With these steps taken, your pom.xml will look similar to this:

```markup
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <artifactId>your-project</artifactId>
    <groupId>your-org</groupId>
    <version>1.0.0-SNAPSHOT</version>
    <name>Your Project</name>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-testing-frameworks</artifactId>
            <version>0.8.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.openrewrite.maven</groupId>
                <artifactId>rewrite-maven-plugin</artifactId>
                <version>2.4.3</version>
                <configuration>
                    <activeRecipes>
                        <recipe>org.openrewrite.java.testing.JUnit5Migration</recipe>
                    </activeRecipes>
                </configuration>
                <executions>
                    <execution>
                        <goals>
                            <goal>publish</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

You are now ready to run the migration.

### Gradle

1. Add the Rewrite Gradle Plugin to your build by following [these instructions](../getting-started/rewrite-gradle-plugin.md)
2. Take a `testCompileOnly` dependency on `rewrite-testing-frameworks`.
3. Set the `org.openrewrite.java.testing.JUnit5Migration` recipe as active via the `rewrite` extension.

#### Single-Module Gradle projects

With these steps taken, a single-project build.gradle should look similar to this one:

```groovy
 plugins {
     id("java")
     id("org.openrewrite.rewrite").version("2.3.1")
 }

 repositories {
     jcenter()
 }

 dependencies {
     testImplementation("junit:junit:4.12")
     testCompileOnly("org.openrewrite.recipe:rewrite-testing-frameworks:0.8.1")
 }

 rewrite {
     activeRecipe("org.openrewrite.java.testing.JUnit5Migration")
 }
```

You are now ready to run the migration.

### Multi-Module Gradle Projects

With these steps taken, the root project's build.gradle should look similar to this:

```groovy
 plugins {
     id("org.openrewrite.rewrite").version("2.3.1").apply(false)
 }

 subprojects {
     apply plugin: "java"
     apply plugin: "org.openrewrite.rewrite"

     repositories {
         jcenter()
     }

     dependencies {
         testImplementation("junit:junit:4.12")
         testCompileOnly("org.openrewrite.recipe:rewrite-testing-frameworks:0.8.1")
     }

     rewrite {
         activeRecipe("org.openrewrite.java.testing.JUnit5Migration")
     }
 }
```

You are now ready to run the migration.

## Running the Migration

If you're using Maven run `maven rewrite:fix`.

If you're using Gradle run `gradle rewriteFix`.

![Example rewriteFix output for applying this recipe to Netflix Conductor](../.gitbook/assets/rewrite-fix-gradle-output.png)

Expect the process to take a roughly similar amount of time as regular Java compilation. Upon completion the migration will print a list of sources that were refactored. You can then inspect those sources for accuracy & correctness, manually fix any problems, and then commit the results.

## Inspecting the Results

Using `git diff`, or your VCS's equivalent, you can see exactly what alterations have been made to your sources.

![Example git diff output for changes made to Netflix Conductor by this recipe](../.gitbook/assets/rewrite-fix-git-diff-output.png)

If you're using Maven, your pom.xml should have been updated to remove the JUnit 4 dependency entry and add entries for junit-jupiter-engine and junit-jupiter-api.

```markup
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

With JUnit 5 configured to execute tests, you should now be able to run your newly updated JUnit 5 test suite. Congratulations!

## Known Limitations

{% hint style="info" %}
If your Maven build configures its test dependencies in a separate module you will have to manually update your test dependencies.
{% endhint %}

{% hint style="info" %}
Rewrite does not yet support parsing & refactoring of build.gradle or build.gradle.kts files. Gradle users will have to manually update their dependencies to use JUnit 5 instead of JUnit 4. See JUnit's [user guide](https://junit.org/junit5/docs/current/user-guide/#running-tests-build-gradle) for more information on how to configure JUnit 5 with Gradle.
{% endhint %}

There are parts of JUnit 4 which we have not yet added support for automatic migration. See the rewrite-testing-frameworks [issue tracker](https://github.com/openrewrite/rewrite-testing-frameworks/issues) for the most up to date information about bugs and known issues. Reach out to us there if you run into a bug. Also reach out if your build uses JUnit 4 features not yet automatically migrated by the recipe. We accept pull requests, questions, as well as any details of your JUnit 4 usage which would help us to prioritize any aspect of this migration.
