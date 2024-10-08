
# Lab 02: Test Fixture in JUnit

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment

### 1. Prepare the project

1. Open Visual Studio Code
2. Download the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/test-fixture-start) as **test-fixture-start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-java-unit-test/
    ```
    Ensure you check out the `test-fixture-start` branch

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

        <!-- Here is the the junit api and junit engine -->
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

    </project>
    ```


## Exercise 1: Add the test fixture

1. Open the project in Visual Studio Code
2. In the Explorer pane, expand the **Java Projects** section at the bottom of the pane, you should see the `nextflow-java-unittest` project.
3. Right-click on the project's name, then select **Rebuild project** from the menu.

### 1. Isolate `Calculator` class' instance

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Modify the following code to the `CalculatorTest` class like below:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;

    import org.junit.jupiter.api.Test;

    public class CalculatorTest {

        // declare the calculator instance to use in each test unit
        private Calculator calculator;

        @Test
        public void testAddPositiveNumbers() {

            // use calculator instance in the test unit
            calculator = new Calculator();
            assertEquals(5, calculator.add(2, 3));
        }

        @Test
        public void testAddNegativeNumbers() {

            // use calculator instance in the test unit
            calculator = new Calculator();
            assertEquals(-5, calculator.add(-2, -3));
        }

        @Test
        public void testAddWithZero() {

            // use calculator instance in the test unit
            calculator = new Calculator();
            assertEquals(2, calculator.add(2, 0));
        }
    }
    ```
3. Save file.
4. Switch to the **Test Explorer**, you will see the test units still available in the list.
5. Click on the **Run** button to run the test.
6. You will see the **Test Results** in the bottom of the window with timestamp in run the test.

### 2. Add `@BeforeEach` and `@AfterEach` methods

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Update the `CalculatorTest` class with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;

    import org.junit.jupiter.api.Test;

    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.AfterEach;

    public class CalculatorTest {

        private Calculator calculator;
        
        // setup the calculator instance before each test unit
        @BeforeEach
        public void setUp() {
            calculator = new Calculator();
        }

        // clean up the calculator instance after each test unit
        @AfterEach
        public void tearDown() {
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
    }
    ```

3. Save file.
4. Put break points in the `setUp` and `tearDown` methods.
5. Put break points in the `testAddPositiveNumbers`, `testAddNegativeNumbers`, and `testAddWithZero` methods.
6. Switch to the **Test Explorer**.
7. Click on the **Debug** button to run the test.
8. Examine the flow of the test units.
9. You will see the **Test Results** in the bottom of the window with timestamp in run the test.

### 3. Remove the break points

1. Remove the break points in the `setUp` and `tearDown` methods.
2. Remove the break points in the `testAddPositiveNumbers`, `testAddNegativeNumbers`, and `testAddWithZero` methods.

## Summary

In this lab, you have learned how to add the test fixture to the test units in JUnit 5. You have also learned how to use the `@BeforeEach` and `@AfterEach` methods to setup and clean up the test fixture before and after each test unit.