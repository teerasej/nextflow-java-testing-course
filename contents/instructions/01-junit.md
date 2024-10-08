
# Understanding Unit Testing with JUnit

Clone the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/start)

## Exercise 1: Explore the calculator

1. Open the project in Visual Studio Code
2. Open the `Calculator` class in `src/main/java/th/in/nextflow/Calculator.java`
3. You should see the following implemented code in this class:

    ```java
    package th.in.nextflow;

    public class Calculator {
        public int add(int a, int b) {
            return a + b;
        }
    }
    ```

4. Open the `Main` class in `src/main/java/th/in/nextflow/Main.java`, you should see the following implemented code in this class:

    ```java
    package th.in.nextflow;

    public class Main {
        public static void main(String[] args) {
            System.out.println("Hello world!");

            // Using the Calculator class
            Calculator calculator = new Calculator();
            System.out.println("2 + 3 = " + calculator.add(2, 3));
        }
    }
    ```

1. Run the `Main` class by using following methods:
   1. right-clicking on the file and selecting `Run Java` from the context menu:
      <img width="638" alt="2024-10-08_12-41-30" src="https://github.com/user-attachments/assets/ad7caa87-54af-41cd-bf9e-8bd2dde4d11f">

   2. Go to debug pane on the left side of the window, click on the **Run and debug** button to run the `Main` class.
      <img width="407" alt="2024-10-08_12-42-33" src="https://github.com/user-attachments/assets/0e2a467a-f680-425c-a5df-8c40f6e6f863">

   3. In the editor window, hover the `main` method and click on the `Run` (or `Debug`) to run the `Main` class.
      <img width="813" alt="2024-10-08_12-43-16" src="https://github.com/user-attachments/assets/a02f627e-209f-4b56-8cda-68451cf2385e">

2. You should see the following output in the terminal:

    ```
    Hello world!
    2 + 3 = 5
    ```

## Exercise 2: Add dependecy in Maven

1. Add `<dependencies>` section in `pom.xml` file, like below:

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

2. When asked about synchronize the Java configuration, select `Yes` to confirm:
    <img width="491" alt="Screenshot 2567-10-08 at 12 55 44" src="https://github.com/user-attachments/assets/59270a08-0d68-44c5-9501-57e8cdbd647c">


## Exercise 3: Create a test class

1. Create a new package `th.in.nextflow` in `src/test/java` directory. For example, `src/test/java/th/in/nextflow`. 

    > **Note:** You can right-click on the `src/test/java` directory and select `New Folder` to create a new package by type in: `th/in/nextflow`.

2. From Explorer pane, Right-click on `th.in.nextflow` package and select `New Java File > Class`, then name the file as: `CalculatorTest`.
3. You will see the `src/test/java/th/in/nextflow/CalculatorTest.java` file is created with the following code:

    ```java
    package th.in.nextflow;

    public class CalculatorTest {

    }
    ```

## Exercise 4: Using the Test Explorer

1. From Visual Studio Code, open the **Testing** pane to reach the **Test Explorer**, at the moment you should see the `project` in the list.
2. Try to run the test by clicking on **Run** button on the `Project`.
3. You will see the **Test Results** in the bottom of the window with timestamp in run the test.

<img width="1188" alt="2024-10-08_13-10-53" src="https://github.com/user-attachments/assets/9ccbde1e-058d-4f43-9da6-d598d5534783">



## Exercise 5: Adding the unit test

### 1. Add the positive number test

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Add the following code to the `CalculatorTest` class like below:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;

    import org.junit.jupiter.api.Test;

    public class CalculatorTest {
        @Test
        public void testAddPositiveNumbers() {
            Calculator calculator = new Calculator();
            assertEquals(5, calculator.add(2, 3));
        }

    }
    ```
3. Save file.
4. Switch to the **Test Explorer**, you will see the test `testAddPositiveNumbers` is added to the list with some test buttons.
5. Click on the **Run** button to run the test.
    <img width="395" alt="2024-10-08_13-17-35" src="https://github.com/user-attachments/assets/07aea66f-5d5c-499e-8963-eac1b057ea36">


    > **Note:** You can use `Run` button in front of line number in the code to run the test instead.
    > <img width="640" alt="2024-10-08_13-17-51" src="https://github.com/user-attachments/assets/f696fd91-6509-4faf-8caf-fea934dd1331">


6. You will see the **Test Results** in the bottom of the window with timestamp in run the test. You can select the test case to 

### 2. Add more test cases

1. Open `CalculatorTest` class in `src/test/java/th/in/nextflow/CalculatorTest.java`
2. Update the `CalculatorTest` class with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertEquals;

    import org.junit.jupiter.api.Test;

    public class CalculatorTest {
        @Test
        public void testAddPositiveNumbers() {
            Calculator calculator = new Calculator();
            assertEquals(5, calculator.add(2, 3));
        }

        @Test
        public void testAddNegativeNumbers() {
            Calculator calculator = new Calculator();
            assertEquals(-5, calculator.add(-2, -3));
        }

        @Test
        public void testAddWithZero() {
            Calculator calculator = new Calculator();
            assertEquals(2, calculator.add(2, 0));
        }
    }
    ```

3. Save file.
4. Switch to the **Test Explorer**, you will see the test `testAddNegativeNumbers` and `testAddWithZero` are added to the list with some test buttons.
5. Click on the **Run** button to run the test.
6. You will see the **Test Results** in the bottom of the window with timestamp in run the test.

## Summary

In this exercise, you have learned how to create a simple unit test using JUnit 5 in Java. You have also learned how to run the test using the Test Explorer in Visual Studio Code.