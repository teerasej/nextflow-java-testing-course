
# Lab 03: Code Coverage

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment


1. Open Visual Studio Code
2. Download the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/code-coverage-start) as **code-coverage-start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-java-unit-test/
    ```
    Ensure you check out the `code-coverage-start` branch

## Exercise 1: Add plugin in Maven

1. Open the `pom.xml` file in the project directory. You will add the `jacoco-maven-plugin` plugin to the `build` section of the `pom.xml` file.

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <groupId>th.in.nextflow</groupId>
        <artifactId>nextflow-java-unittest</artifactId>
        <version>1.0-SNAPSHOT</version>

        <properties>
            <maven.compiler.source>17</maven.compiler.source>
            <maven.compiler.target>17</maven.compiler.target>
        </properties>

        <dependencies>
            <dependency>
                <groupId>org.junit.jupiter</groupId>
                <artifactId>junit-jupiter-api</artifactId>
                <version>5.8.1</version>
                <scope>test</scope>
            </dependency>
            <dependency>
                <groupId>org.junit.jupiter</groupId>
                <artifactId>junit-jupiter-engine</artifactId>
                <version>5.8.1</version>
                <scope>test</scope>
            </dependency>
        </dependencies>

        <!-- Here is the the jacoco plugin -->
        <build>
            <plugins>
                <plugin>
                    <groupId>org.jacoco</groupId>
                    <artifactId>jacoco-maven-plugin</artifactId>
                    <version>0.8.7</version>
                    <executions>
                        <execution>
                            <goals>
                                <goal>prepare-agent</goal>
                            </goals>
                        </execution>
                        <execution>
                            <id>report</id>
                            <phase>test</phase>
                            <goals>
                                <goal>report</goal>
                            </goals>
                        </execution>
                    </executions>
                </plugin>
            </plugins>
        </build>

    </project>
    ```
2. Rebuild project with Java Projects Explorer in Visual Studio Code, by right-click on the project's name, then select **Rebuild project** from the menu.

## Exercise 2: Run the test with coverage 

1. Switch to the **Test Explorer**.
2. Click on the **Run with Code Coverage** button on the project's scope to run the test.
   <img width="542" alt="2024-10-08_16-41-52" src="https://github.com/user-attachments/assets/3eb6941c-d091-43de-8001-c798df6240ae">

4. After the test is completed, you will see the **Coverage** section below the **Test Explorer**. like the following image:
    <img width="395" alt="2024-10-08_16-24-33" src="https://github.com/user-attachments/assets/58acfb46-7c5e-4b88-8699-42613ec3863a">

5. Click on the **Calculator.java** which has 100% coverage, you will see the highlighted code in the editor.
    <img width="585" alt="2024-10-08_16-27-17" src="https://github.com/user-attachments/assets/06c389d6-bc58-4ca9-a228-e441d6ab76ef">


6. Click on the **Main.java** which has 0% coverage, you will see the **red** highlighted code in the editor.
    <img width="827" alt="2024-10-08_16-24-39" src="https://github.com/user-attachments/assets/d80e67a7-2c79-462c-ad7a-563b92b8f1d6">


## Summary

In this lab, you have learned how to add the `jacoco-maven-plugin` plugin to the `pom.xml` file to generate the test coverage report. You have also learned how to run the test with coverage and view the coverage report in Visual Studio Code.
