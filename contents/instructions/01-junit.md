
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
