
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

5. Run the `Main` class by using following methods:
   1. right-clicking on the file and selecting `Run` from the context menu. You should see the following output in the terminal:
   2. Go to debug pane on the left side of the window, click on the **Run and debug** button to run the `Main` class.
   3. In the editor window, hover the `main` method and click on the `Run` (or `Debug`) to run the `Main` class.




## Exercise 2: Add dependecy in Maven

Add `<dependencies>` section in `pom.xml` file, like below:

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

## สร้าง Class Calculator

เราจะคลิกขวาที่ Class Calculator และเลือก 

```java
package th.in.nextflow;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

## ใช้ Testing Tools

คลิกเลือก Testing เราควรเห็นชื่อโปรเจค ชื่อ package และชื่อ class ที่เราจะรันทดสอบ

กดปุ่ม run test ที่ class `CalculatorTest` และดูผลลัพธ์ที่ได้


## เปลี่ยนแปลงการทำงานของ Class

จำลองการแก้ไข class `Calculator` ที่ทำให้ผลการทำงานเปลี่ยนไปจากเดิม