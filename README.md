# whatsapp-sftp-reports

## Overview
This project is designed to automate the process of generating reports from WhatsApp data and sending them to an SFTP server. It utilizes Spring Boot for backend operations, including scheduled tasks for automatic report generation and handling data with JPA.

## Project Structure
- `src/main/java/`: Contains all Java source files organized by package:
  - `com.aldeamo.whatsapp.whatsappsftpreports`: Root package for the project.
    - `WhatsappSftpReportsApplication.java`: Main class for running the Spring Boot application.
    - `config`: Contains configuration classes.
      - `BouncyCastleProviderConfig.java`: Configuration for Bouncy Castle provider.
      - `DatabaseConfig.java`: Configuration for database connections.
    - `model`: Contains data models.
      - `SftpConnectionModel.java`: Model representing the SFTP connection details.
    - `repository`: Contains interfaces for database access operations.
      - `MessageRepository.java`: Repository interface for message entity operations.
    - `service`: Contains service interfaces and implementations.
      - `ReportServiceI.java`: Interface for report services.
      - `ReportTCServiceImpl.java`: Implementation of report service for TC reports.
    - `util`: Contains utility classes.
      - `PGPEncryptionService.java`: Utility class for PGP encryption.
      - `DayUtility.java`: Utility class for handling day-related operations.
      - `schedule`: Contains classes related to scheduled tasks.
        - `ScheduledTasks.java`: Class for defining scheduled tasks.
      - `sftp`: Contains classes related to SFTP operations.
        - `SFTPUploader.java`: Utility class for uploading files via SFTP.
    - `entity`: Contains entity classes.
      - `WhatsappScotiabankTCEntity.java`: Entity class representing WhatsApp Scotiabank TC data.
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
	<version>1.68</version>
</dependency>
<dependency>
	<groupId>org.bouncycastle</groupId>
	<artifactId>bcpg-jdk15on</artifactId>
	<version>1.68</version>
</dependency>
```

## Usage

### Encrypting a File
To encrypt a file, use the `encryptFile` method as shown below:

```java
String publicKeyPath = "path/to/public/key.asc";
String inputFile = "path/to/input/file.txt";
String outputFile = "path/to/output/file.pgp";

try {
    PGPPublicKey publicKey = PGPEncryptionService.readPublicKey(publicKeyPath);
    PGPEncryptionService.encryptFile(outputFile, inputFile, publicKey, true, true);
} catch (IOException | PGPException | NoSuchProviderException e) {
    e.printStackTrace();
}
```

This method encrypts a file using a specified PGP public key with options for ASCII armor and integrity check, compressing the file data before encryption.

Reading a Public Key
To read a public key from a file, utilize the readPublicKey method:

```java
try {
    PGPPublicKey publicKey = PGPEncryptionService.readPublicKey("path/to/public/key.asc");
} catch (IOException | PGPException e) {
    e.printStackTrace();
}
```
This retrieves an encryption-capable public key from a specified file containing a PGP key ring.

## How It Works

### encryptFile Method
**Inputs:**
- `outputFileName`: The name of the output file where the encrypted data will be written.
- `inputFileName`: The name of the input file to be encrypted.
- `encKey`: The public key used for encryption.
- `armor`: If true, the output will be ASCII armored.
- `withIntegrityCheck`: If true, the encryption will include an integrity check.

**Process:**
- Initializes an output stream for the encrypted file.
- If `armor` is true, wraps the output stream in an `ArmoredOutputStream` for ASCII armor.
- Compresses the input file and writes it to a literal data packet.
- Creates a PGP encrypted data generator with the specified encryption key and options.
- Encrypts the compressed literal data and writes the encrypted data to the output stream.

**Output:** The method produces an encrypted file that can only be decrypted by the corresponding private key.

### readPublicKey Method
**Input:**
- `publicKeyFilePath`: The path to the file containing the public key.

**Process:**
- Reads and parses the public key file into a `PGPPublicKeyRingCollection`.
- Iterates through the key rings and keys to find an encryption-capable key.

**Output:** Returns a `PGPPublicKey` if a valid key is found, throws an exception otherwise.
This retrieves an encryption-capable public key from a specified file containing a PGP key ring.

## How It Works

### encryptFile Method
**Inputs:**
- `outputFileName`: The name of the output file where the encrypted data will be written.
- `inputFileName`: The name of the input file to be encrypted.
- `encKey`: The public key used for encryption.
- `armor`: If true, the output will be ASCII armored.
- `withIntegrityCheck`: If true, the encryption will include an integrity check.

**Process:**
- Initializes an output stream for the encrypted file.
- If `armor` is true, wraps the output stream in an `ArmoredOutputStream` for ASCII armor.
- Compresses the input file and writes it to a literal data packet.
- Creates a PGP encrypted data generator with the specified encryption key and options.
- Encrypts the compressed literal data and writes the encrypted data to the output stream.

**Output:** The method produces an encrypted file that can only be decrypted by the corresponding private key.

### readPublicKey Method
**Input:**
- `publicKeyFilePath`: The path to the file containing the public key.

**Process:**
- Reads and parses the public key file into a `PGPPublicKeyRingCollection`.
- Iterates through the key rings and keys to find an encryption-capable key.

**Output:** Returns a `PGPPublicKey` if a valid key is found, throws an exception otherwise.


