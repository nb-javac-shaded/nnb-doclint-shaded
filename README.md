# NNB DocLint Shaded

[![](https://jitpack.io/v/nb-javac-shaded/nnb-doclint-shaded.svg)](https://jitpack.io/#nb-javac-shaded/nnb-doclint-shaded)

A shaded extraction of the DocLint utility from OpenJDK's javadoc tool, with all compiler APIs relocated to `shaded.*` packages for compatibility with shaded nb-javac.

**Group ID**: `shaded.nbjavac`  
**Artifact ID**: `nnb-doclint-shaded`

## What is DocLint?

DocLint is a utility that checks documentation comments in Java source code for:
- HTML syntax errors
- Missing or invalid JavaDoc tags
- Accessibility issues
- Reference errors
- And other documentation quality issues

## Extracted Files

This library includes the following components from OpenJDK JDK 26:

### Source Files
- `com.sun.tools.doclint.DocLint` - Base DocLint class (from jdk.compiler)
- `jdk.javadoc.internal.doclint.DocLint` - Main DocLint implementation (from jdk.javadoc)
- `jdk.javadoc.internal.doclint.Checker` - Core checking logic
- `jdk.javadoc.internal.doclint.Env` - Environment/context for checks
- `jdk.javadoc.internal.doclint.Messages` - Message formatting
- `jdk.javadoc.internal.tool.AccessLevel` - Access level enumeration

### Resources
- `doclint.properties` - English messages
- `doclint_de.properties` - German messages  
- `doclint_ja.properties` - Japanese messages
- `doclint_zh_CN.properties` - Chinese messages

## Dependencies

This library depends on the Java Compiler API, **relocated to shaded packages**:
- `shaded.javax.lang.model.*` - Language model API (relocated)
- `shaded.javax.tools.*` - Java tools API (relocated)
- `shaded.com.sun.source.*` - Compiler tree API (relocated)
- `shaded.com.sun.tools.javac.*` - Internal javac APIs (relocated)

**Important**: This artifact is shaded to work with shaded nb-javac. All compiler API packages are relocated from their original locations (e.g., `com.sun.source.*`) to shaded locations (e.g., `shaded.com.sun.source.*`). This prevents ClassCastException when used with a shaded version of nb-javac.

The specific shaded nb-javac implementation this library targets can be found at: https://github.com/nb-javac-shaded/nb-javac-shaded

Original APIs are available in:
- Java 8: Via `tools.jar`
- Java 9+: Via `jdk.compiler` module

## Usage

This library is designed to be used with shaded nb-javac via ServiceLoader. The DocLint implementation is automatically discovered when javac loads plugins.

### Maven Dependency

Add the JitPack repository and dependency to your `pom.xml`:

```xml
<repositories>
  <repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
  </repository>
</repositories>

<dependencies>
  <dependency>
    <groupId>com.github.nb-javac-shaded</groupId>
    <artifactId>nnb-doclint-shaded</artifactId>
    <version>jdk-26-35</version>
  </dependency>
</dependencies>
```

### ServiceLoader Integration

The JAR includes a service provider configuration at:
```
META-INF/services/shaded.com.sun.tools.doclint.DocLint
```

When shaded nb-javac is configured with `-Xdoclint` options, it automatically discovers and loads this DocLint implementation via ServiceLoader.

## Building

### Prerequisites
- Java 17 or later
- Maven 3.6+

### Build Commands

```bash
# Compile
mvn clean compile

# Package as JAR
mvn clean package

# Install to local Maven repository
mvn clean install
```

## Target Compatibility

- **Source Level**: Java 17
- **Target Level**: Java 17

The code has been extracted from JDK 26 and targets Java 17. Modern syntax features (switch expressions, pattern matching) are preserved.

## Publishing to JitPack

This project is published via JitPack:

1. Create and push a tag matching the version: `git tag jdk-26-35 && git push --tags`
2. JitPack automatically builds when someone requests the version
3. View build status at: https://jitpack.io/#nb-javac-shaded/nnb-doclint-shaded

## Updating to newer JDK versions

To update to a newer JDK version:

1. Extract DocLint classes from the new JDK version
2. Update the `<version>` in `pom.xml` to match (e.g., `jdk-27-1`)
3. Update package relocations if needed
4. Test with the corresponding nb-javac-shaded version
5. Tag and push to trigger a new JitPack build

## License

This code is extracted from OpenJDK and retains the original GPL v2 + Classpath Exception license.
See the header in each source file for full license details.

## Notes

- This is a direct extraction with minimal modifications
- The code depends on internal javac APIs which may change between Java versions
- For production use, test with your target Java version
