
# Lab 04: Parameterzied Test in JUnit

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment

### 1. Prepare the project

1. Open Visual Studio Code
2. Download the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/parameterized-test-start) as **parameterized-test-start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-java-unit-test/
    ```
    Ensure you check out the `parameterized-test-start` branch

### 2. Explore dependecy in Maven

1. Open the `pom.xml` file in the project directory. Explore that we have the following dependencies for JUnit 5 and Jacoco plugin.
2. We will add more dependencies for the parameterized test.
    
    ```xml
    <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>5.8.1</version>
            <scope>test</scope>
    </dependency>
    ```

3. the complete `pom.xml` file should look like below:

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

        <!-- Add more artifact for parameterized test -->
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


## Exercise 1: Update the concrete class

1. Open the project in Visual Studio Code
2. In the Explorer pane, expand the **Java Projects** section at the bottom of the pane, you should see the `nextflow-java-unittest` project.
3. Right-click on the project's name, then select **Rebuild project** from the menu.

### 1. Add more method to `Calculator` class

1. Open `Calculator` class in `src/main/java/th/in/nextflow/Calculator.java`
2. Modify the following code to the `Calculator` class like below:

    ```java
    package th.in.nextflow;

    public class Calculator {
        public int add(int a, int b) {
            return a + b;
        }

        public int multiply(int a, int b) {
            return a * b;
        }

        public boolean isEven(int number) {
            return number % 2 == 0;
        }
    }

    ```
3. Save file.
4. Switch to the **Test Explorer**, you will see the test units still available in the list.
5. Click on the **Run with Test Coverage** button to run the test.
6. You will see the **Test Results** and **Test Code Coverage** in the bottom of the window with timestamp in run the test.
7. Code Coverage will show the percentage of the code that is covered by the test units **which is not good at this point**.

## Exercise 2: Add Test with parameterized value

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Update the `CalculatorTest` class with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;
    import static org.junit.jupiter.api.Assertions.assertFalse;
    import static org.junit.jupiter.api.Assertions.assertTrue;

    import org.junit.jupiter.api.Test;

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.AfterEach;
    import org.junit.jupiter.params.ParameterizedTest;
    import org.junit.jupiter.params.provider.ValueSource;

    public class CalculatorTest {

        private Calculator calculator;

        @BeforeEach
        public void setUp() {
            calculator = new Calculator();
        }

        @AfterEach
        public void tearDown() {
            // Clean up resources if needed
            calculator = null;
        }

        @Test
        public void testAddPositiveNumbers() {
            calculator = new Calculator();
            assertEquals(5, calculator.add(2, 3));
        }

        @Test
        public void testAddNegativeNumbers() {
            calculator = new Calculator();
            assertEquals(-5, calculator.add(-2, -3));
        }

        @Test
        public void testAddWithZero() {
            calculator = new Calculator();
            assertEquals(2, calculator.add(2, 0));
        }

        // Use annotation to define the parameterized test
        @ParameterizedTest
        // Use the ValueSource to provide the parameterized value
        // The test will run with each value in the ValueSource
        @ValueSource(ints = {2, 4, 6, 8, 10})
        public void testIsEven(int number) {
            assertTrue(calculator.isEven(number));
        }

        // Use annotation to define the parameterized test, this test will run with each value in the ValueSource, and the test will pass if the value is not even
        @ParameterizedTest
        @ValueSource(ints = {1, 3, 5, 7, 9})
        public void testIsNotEven(int number) {
            assertFalse(calculator.isEven(number));
        }
    }

    ```

3. Save file.
4. Switch to the **Test Explorer**.
5. Click on the **Run with Code Coverage** button to run the test.
6. Examine the flow of the test units and the code coverage.

> **Note:** You will see the result in the **Test Explorer** that show each test unit with parameterized value.

## Exercise 3: Add more parameterized test with CSV data

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Update the `CalculatorTest` class with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;
    import static org.junit.jupiter.api.Assertions.assertFalse;
    import static org.junit.jupiter.api.Assertions.assertTrue;

    import org.junit.jupiter.api.Test;

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.AfterEach;
    import org.junit.jupiter.params.ParameterizedTest;
    import org.junit.jupiter.params.provider.CsvSource;
    import org.junit.jupiter.params.provider.ValueSource;

    public class CalculatorTest {

        private Calculator calculator;

        @BeforeEach
        public void setUp() {
            calculator = new Calculator();
        }

        @AfterEach
        public void tearDown() {
            // Clean up resources if needed
            calculator = null;
        }

        @Test
        public void testAddPositiveNumbers() {
            calculator = new Calculator();
            assertEquals(5, calculator.add(2, 3));
        }

        @Test
        public void testAddNegativeNumbers() {
            calculator = new Calculator();
            assertEquals(-5, calculator.add(-2, -3));
        }

        @Test
        public void testAddWithZero() {
            calculator = new Calculator();
            assertEquals(2, calculator.add(2, 0));
        }

        @ParameterizedTest
        @ValueSource(ints = {2, 4, 6, 8, 10})
        public void testIsEven(int number) {
            assertTrue(calculator.isEven(number));
        }

        @ParameterizedTest
        @ValueSource(ints = {1, 3, 5, 7, 9})
        public void testIsNotEven(int number) {
            assertFalse(calculator.isEven(number));
        }
        
        // Use annotation to define the parameterized test, this test will run with each value in the CSVSource
        // The test name will also be generated from the parameters
        @ParameterizedTest(name = "Add {0} to {1} equals {2}")
        @CsvSource({
            "1, 1, 2",
            "2, 3, 5",
            "-1, -1, -2",
            "0, 5, 5"
        })
        public void testAdd(int a, int b, int expected) {
            assertEquals(expected, calculator.add(a, b));
        }

        // Use annotation to define the parameterized test, this test will run with each value in the CSVSource
        // The test name will also be generated from the parameters
        @ParameterizedTest(name = "Multiply {0} by {1} equals {2}")
        @CsvSource({
            "1, 1, 1",
            "2, 3, 6",
            "-1, -1, 1",
            "0, 5, 0"
        })
        public void testMultiply(int a, int b, int expected) {
            assertEquals(expected, calculator.multiply(a, b));
        }
    }


    ```

3. Save file.
4. Switch to the **Test Explorer**.
5. Click on the **Run with Code Coverage** button to run the test.
6. Examine the flow of the test units and the code coverage.


> **Note:** You can add more parameterized test with different data types and sources. You can refer to the [official documentation](https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests) for more information.

## Summary

In this lab, you have learned how to add the `junit-jupiter-params` dependency to the `pom.xml` file to enable the parameterized test in JUnit 5. You have also learned how to write the parameterized test with different sources and data types.