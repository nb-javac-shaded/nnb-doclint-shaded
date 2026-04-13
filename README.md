# NNB DocLint

A standalone extraction of the DocLint utility from OpenJDK's javadoc tool.

**Group ID**: `net.oxbeef`  
**Artifact ID**: `nnb-doclint`

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

This library depends on the Java Compiler API:
- `javax.lang.model.*` - Language model API
- `javax.tools.*` - Java tools API
- `com.sun.source.*` - Compiler tree API
- `com.sun.tools.javac.*` - Internal javac APIs

These are available in:
- Java 8: Via `tools.jar`
- Java 9+: Via `jdk.compiler` module

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

## License

This code is extracted from OpenJDK and retains the original GPL v2 + Classpath Exception license.
See the header in each source file for full license details.

## Notes

- This is a direct extraction with minimal modifications
- The code depends on internal javac APIs which may change between Java versions
- For production use, test with your target Java version
