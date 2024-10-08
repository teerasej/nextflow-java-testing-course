
# Lab 06: Time out Test

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment

### 1. Prepare the project

1. Open Visual Studio Code
2. Download the project from [nextflow-java-unit-test](https://github.com/teerasej/nextflow-java-unit-test/tree/timeout-test-start) as **timeout-test-start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-java-unit-test/
    ```
    Ensure you check out the `timeout-test-start` branch

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


## Exercise 1: Add new `WebApiClient` class

1. Create a new Java class `WebApiClient` in `src/main/java/th/in/nextflow` directory with the following code:

    ```java
    package th.in.nextflow;

    public class WebApiClient {
        public void callWebApi() throws InterruptedException {
            // Simulate a long-running web API call
            Thread.sleep(5000); // Sleep for 5 seconds
        }
    }
    ```

2. Create its test class `WebApiClientTest` in `src/test/java/th/in/nextflow` directory with the following code:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertTimeout;
    import static java.time.Duration.ofSeconds;

    import org.junit.jupiter.api.Test;

    public class WebApiClientTest {

        @Test
        public void testCallWebApiTimeout() {
            WebApiClient client = new WebApiClient();

            // Assert that the callWebApi method will complete within 3 seconds
            // If it takes longer than 3 seconds, the test will fail
            assertTimeout(ofSeconds(3), () -> {
                client.callWebApi();
            });
        }

        // Test that the callWebApi method will complete within 6 seconds
        // If it takes longer than 6 seconds, the test will fail
        // But in this case, the test will pass because the callWebApi method will complete within 5 seconds
        @Test
        public void testCallWebApiNoTimeout() {
            WebApiClient client = new WebApiClient();
            assertTimeout(ofSeconds(6), () -> {
                client.callWebApi();
            });
        }
    }
    ```

3. Switch to the **Test Explorer**.
4. Click on the **Run** button to run the test.
5. You will see the failed test results with the `AssertionFailedError` error.

    ```bash
    org.opentest4j.AssertionFailedError: execution exceeded timeout of 3000 ms by 2005 ms
    ```

    > **Note:** The test failed because the `callWebApi` method took longer than 3 seconds to complete. this is expected behavior.

6. Back to the `WebApiClientTest` class.
7. Modify the Test to use the `assertThrows` method to handle the exception, so this test will pass.:

    ```java
    package th.in.nextflow;

    import static org.junit.jupiter.api.Assertions.assertThrows;
    import static org.junit.jupiter.api.Assertions.assertTimeout;
    import static java.time.Duration.ofSeconds;

    import org.junit.jupiter.api.Test;

    public class WebApiClientTest {
        @Test
        public void testCallWebApiTimeout() {
            WebApiClient client = new WebApiClient();
            assertThrows(AssertionError.class, () -> {
                assertTimeout(ofSeconds(3), () -> {
                    client.callWebApi();
                });
            });
        }

        @Test
        public void testCallWebApiNoTimeout() {
            WebApiClient client = new WebApiClient();
            assertTimeout(ofSeconds(6), () -> {
                client.callWebApi();
            });
        }
    }
    ```

8. Save file.
9. Switch to the **Test Explorer**.
10. Click on the **Run** button to run the test.
11. You will see the passed test results.

## Summary

In this lab, you have learned how to write a test that asserts that a method completes within a specified time limit using the `assertTimeout` method. You have also learned how to handle the exception using the `assertThrows` method.