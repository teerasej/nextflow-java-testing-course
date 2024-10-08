
# Lab 05: Exception Test

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment

### 1. Prepare the project

1. Open Visual Studio Code
2. Download the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/exception-test-start) as **exception-test-start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-java-unit-test/
    ```
    Ensure you check out the `exception-test-start` branch

### 2. Explore dependecy in Maven

1. Open the `pom.xml` file in the project directory. Explore that we have the following dependencies for JUnit 5:

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
                
                <dependency>
                    <groupId>org.junit.jupiter</groupId>
                    <artifactId>junit-jupiter-params</artifactId>
                    <version>5.8.1</version>
                    <scope>test</scope>
                </dependency>
            </dependencies>

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


## Exercise 1: Add new `Divider` class

1. Create a new Java class `Divider` in `src/main/java/th/in/nextflow` directory with the following code:

    ```java
    package th.in.nextflow;

    public class Divider {
        public int divide(int a, int b) {
            return a / b;
        }
    }
    ```

2. Create its test class `DividerTest` in `src/test/java/th/in/nextflow` directory with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;
    import static org.junit.jupiter.api.Assertions.assertThrows;

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.Test;

    public class DividerTest {
        private Divider divider;

        @BeforeEach
        public void setUp() {
            divider = new Divider();
        }

        @Test
        public void testDivideByNonZero() {
            assertEquals(2, divider.divide(4, 2));
        }

        @Test
        public void testDivideByZero() {
            assertEquals(2, divider.divide(4, 0));
        }
    }
    ```

3. Switch to the **Test Explorer**.
4. Click on the **Run** button to run the test.
5. You will see the failed test results with the `ArithmeticException` error.

    ```bash
    java.lang.ArithmeticException: / by zero
        at th.in.nextflow.Divider.divide(Divider.java:5)
        at th.in.nextflow.DividerTest.testDivideByZero(DividerTest.java:24)
        at java.base/java.util.ArrayList.forEach(ArrayList.java:1511)
        at java.base/java.util.ArrayList.forEach(ArrayList.java:1511)
    ```

    > **Note:** The test failed because the `Divider` class throws an `ArithmeticException` when dividing by zero. This is an expected behavior, and we need to handle this exception in the test unit.

6. Back to the `DividerTest` class.
7. Modify the Test to use the test fixture with `@BeforeEach` and `@AfterEach` methods.:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;
    import static org.junit.jupiter.api.Assertions.assertThrows;

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.Test;

    public class DividerTest {
        private Divider divider;

        @BeforeEach
        public void setUp() {
            divider = new Divider();
        }

        @Test
        public void testDivideByNonZero() {
            assertEquals(2, divider.divide(4, 2));
        }

        @Test
        public void testDivideByZero() {
            assertThrows(ArithmeticException.class, () -> {
                divider.divide(4, 0);
            });
        }
    }
    ```

8. Save file.
9. Switch to the **Test Explorer**.
10. Click on the **Run** button to run the test.
11. You will see the passed test results with the test fixture.

## Summary

In this lab, you have learned how to handle the exception in the test unit by using the `assertThrows` method from JUnit 5.