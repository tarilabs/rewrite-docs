---
description: Sets a matching dependency to a fixed version.
---

# ChangeDependencyVersion

`ChangeDependencyVersion` changes a matching dependency to a fixed version that you specify.

`ChangeDependencyVersion` is configured with these parameters:

* `groupId` - Update parent versions when they match this Maven group ID.
* `artifactId`- Update dependency versions when they match this Maven artifact ID. This is optional. If it is not specified, update every dependency matching the group. This is useful to update a family of dependencies all at once, such as those in the `com.fasterxml.jackson` group.
* `toVersion` - The version to set.

## Java Definition

```java
MavenParser parser = MavenParser.builder().build();
Iterable<Maven.Pom> poms = parser.parse(...);

ChangeDependencyVersion cdv = new ChangeDependencyVersion();
cdv.setGroupId("com.fasterxml.jackson.core");
// omitting artifactId for the sake of this example
cdv.setToVersion("1.5.22.RELEASE");

Collection<Change> changes = new Refactor().visit(cdv).fix(poms);
```

## YAML Definition

Adding the following to your rewrite.yml and setting the `com.yourorg.ChangeJacksonVersionRecipe` recipe as active in your build plugin will apply the visitor as shown in the example.

```yaml
---
type: specs.openrewrite.org/v1beta/visitor
name: com.yourorg.ChangeJacksonVersion
visitors:
  - org.openrewrite.maven.ChangeDependencyVersion:
    groupId: com.fasterxml.jackson.core
    # artifactId: ... (optional)
    toVersion: 2.11.2
---
type: specs.openrewrite.org/v1beta/recipe
name: com.yourorg.ChangeJacksonVersionRecipe
include:
  - 'com.yourorg.ChangeJacksonVersion'
```

## Example

Before:

```markup
<project>
   <dependencies>
     <dependency>
       <groupId>com.fasterxml.jackson.core</groupId>
       <artifactId>jackson-databind</artifactId>
       <version>2.9.0</version>
     </dependency>
     <dependency>
       <groupId>com.fasterxml.jackson.core</groupId>
       <artifactId>jackson-annotations</artifactId>
       <version>2.9.0</version>
     </depenency>
   </dependencies>
</project>
```

After:

```markup
<project>
   <dependencies>
     <dependency>
       <groupId>com.fasterxml.jackson.core</groupId>
       <artifactId>jackson-databind</artifactId>
       <version>2.11.2</version>
     </dependency>
     <dependency>
       <groupId>com.fasterxml.jackson.core</groupId>
       <artifactId>jackson-annotations</artifactId>
       <version>2.11.2</version>
     </depenency>
   </dependencies>
</project>
```
