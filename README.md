# whatsapp-sftp-reports

## Overview
This project is designed to automate the process of generating reports from WhatsApp data and sending them to an SFTP server. It utilizes Spring Boot for backend operations, including scheduled tasks for automatic report generation and handling data with JPA.

## Project Structure
- `src/main/java/`: Contains all Java source files organized by package:
  - `com.aldeamo.whatsapp.whatsappsftpreports.model`: Data models representing the structure of the data in the application.
  - `com.aldeamo.whatsapp.whatsappsftpreports.repository`: Interfaces for database access operations.
  - `com.aldeamo.whatsapp.whatsappsftpreports.service`: Services that encapsulate business logic.
  - `com.aldeamo.whatsapp.whatsappsftpreports.util`: Utility classes, including scheduled tasks and SFTP file upload handling.
- `src/main/resources/`: Configuration files and resources.
- `pom.xml`: Maven configuration file that includes project dependencies and build configuration.
- `.git/`: Contains Git version control configurations and history.
- `mvnw`, `mvnw.cmd`: Maven wrapper scripts that allow building and running the project without a pre-installed Maven.
- `README.md`: Provides an overview of the project, setup instructions, and general information.
- `HELP.md`: Additional guidance and help related to project setup and troubleshooting.
- `.project`, `.classpath`, `.settings/`: Eclipse IDE specific configuration files that help in setting up the project in the Eclipse environment.


# PGPEncryptionService

## Overview
`PGPEncryptionService` is a Java utility class designed for encrypting files using the PGP (Pretty Good Privacy) encryption standard. It utilizes the Bouncy Castle Crypto API to provide functionality for encrypting data with options for compression and integrity checks, ensuring secure file transfers or storage.

## Requirements
- Java 8 or higher.
- Bouncy Castle Crypto API libraries (`bcprov-jdk15on` and `bcpg-jdk15on`).

## Installation
Include the Bouncy Castle libraries in your project by adding the following dependencies to your `pom.xml` file if you are using Maven:

```xml
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcprov-jdk15on</artifactId>
    <version>[Latest version]</version>
</dependency>
<dependency>
    <groupId>org.bouncycastle</groupId>
    <artifactId>bcpg-jdk15on</artifactId>
    <version>[Latest version]</version>
</dependency>
