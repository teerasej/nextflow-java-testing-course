
# Understanding Integration Testing in Spring Boot Project

> **Noted**: Please ensure you have setup the environment as mentioned in [setup](../setup.md) before proceeding with this lab.

## Exercise 0: Prepare the environment

1. Open Visual Studio Code
2. Download the project from [Nextflow Spring boot test](https://github.com/teerasej/nextflow-spring-boot-test/tree/start) as **start** branch

    > **Note:** You can clone the project by using the following command in the terminal:

    ```bash
    git clone https://github.com/teerasej/nextflow-spring-boot-test/
    ```
    Ensure you check out the `start` branch

## Exercise 1: Explore dependecy in `pom.xml`

1. Check that we have `spring-boot-starter-test` dependency in the `pom.xml` file:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
        <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
            <modelVersion>4.0.0</modelVersion>
            <parent>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-parent</artifactId>
                <version>3.3.4</version>
                <relativePath/> <!-- lookup parent from repository -->
            </parent>
            <groupId>th.in.nextflow</groupId>
            <artifactId>NextflowBoot</artifactId>
            <version>0.0.1-SNAPSHOT</version>
            <name>NextflowBoot</name>
            <description>Example project for spring boot test environment</description>
            <url/>
            <licenses>
                <license/>
            </licenses>
            <developers>
                <developer/>
            </developers>
            <scm>
                <connection/>
                <developerConnection/>
                <tag/>
                <url/>
            </scm>
            <properties>
                <java.version>17</java.version>
            </properties>
            <dependencies>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-actuator</artifactId>
                </dependency>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-web</artifactId>
                </dependency>

                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-devtools</artifactId>
                    <scope>runtime</scope>
                    <optional>true</optional>
                </dependency>
                <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-test</artifactId>
                    <scope>test</scope>
                </dependency>
            </dependencies>

            <build>
                <plugins>
                    <plugin>
                        <groupId>org.springframework.boot</groupId>
                        <artifactId>spring-boot-maven-plugin</artifactId>
                    </plugin>
                </plugins>
            </build>

        </project>

    ```

## Exercise 2: Create a controller

1. Open the project in Visual Studio Code
2. In the Explorer pane, expand the **Java Projects** section at the bottom of the pane, you should see the `nextflow-java-unittest` project.
3. Right-click on the project's name, then select **Rebuild project** from the menu.
4. Create the new controller `HelloController` class in the `src/main/java/th/in/nextflow/NextflowBoot/controller` package. 

    ```java
    package th.in.nextflow.NextflowBoot.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class HelloController {
        @GetMapping("/hello")
        public Message sayHello() {
            return new Message("Hello, World!");
        }

        public static class Message {
            private String message;

            public Message(String message) {
                this.message = message;
            }

            public String getMessage() {
                return message;
            }

            public void setMessage(String message) {
                this.message = message;
            }
        }
    }
    ```

5. Open terminal in visual studio code and run the following command to start the application:

    ```bash
    ./mvnw spring-boot:run     
    ```

6. Open the browser and navigate to `http://localhost:8080/hello`, you should see the following output:

    ```json
    {"message":"Hello, World!"}
    ```


## Exercise 3: Create an integration test class

1. Create a new package `src/test/java/th/in/nextflow/NextflowBoot/`. 
2. Create a new class `HelloControllerTest` in the `src/test/java/th/in/nextflow/NextflowBoot/` package.

    ```java
    package th.in.nextflow.NextflowBoot;

    import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
    import org.junit.jupiter.api.Test;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
    import org.springframework.boot.test.context.SpringBootTest;
    import org.springframework.test.web.servlet.MockMvc;

    // This annotation is used to tell JUnit to run the test using the Spring Boot test environment.
    @SpringBootTest

    // This annotation is used to tell Spring Boot to automatically configure the MockMvc instance. It does following actions:
    // - Load the application context
    // - Load the web server
    // - Load the MockMvc instance
    @AutoConfigureMockMvc
    public class HelloControllerIntegrationTest {

        // This annotation is used to tell Spring Boot to inject the MockMvc instance into the test class. 
        // This instance is used to send HTTP requests to the web server.
        @Autowired
        private MockMvc mockMvc;

        @Test
        public void shouldReturnDefaultMessage() throws Exception {

            // This method is used to send an HTTP GET request to the web server.
            this.mockMvc.perform(get("/hello"))
                    // This method is used to check that the HTTP status code is 200 (OK).
                    .andExpect(status().isOk())
                    // This method is used to check that the response body is equal to the expected JSON string.
                    .andExpect(content().json("{\"message\":\"Hello, World!\"}"));
        }
    }
    ```

1. From Visual Studio Code, open the **Testing** pane to reach the **Test Explorer**, at the moment you should see the `project` in the list.
2. Try to run the test by clicking on **Run** button on the `Project`.
3. You will see the **Test Results** in the bottom of the window with timestamp in run the test.

## Exercise 4: Use mock technique with the service

### 1. Add a new controller class **ProfileController**

1. Create a new controller `ProfileController` class in the `src/main/java/th/in/nextflow/NextflowBoot/controller` package. 

    ```java
    package th.in.nextflow.NextflowBoot.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;


    @RestController
    public class ProfileController {

        @GetMapping("/profiles")
        public String getProfiles() {
            return "[{\"id\":\"1\",\"name\":\"John Doe\"}]";
        }
    }

    ```
2. Create a new class `ProfileControllerTest` in the `src/test/java/th/in/nextflow/NextflowBoot/` package.

    ```java
    package th.in.nextflow.NextflowBoot;

    import static org.assertj.core.api.Assertions.assertThat;
    import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
    import org.junit.jupiter.api.Test;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
    import org.springframework.boot.test.context.SpringBootTest;
    import org.springframework.test.web.servlet.MockMvc;

    @SpringBootTest
    @AutoConfigureMockMvc
    public class ProfileControllerIntegrationTest {

        @Autowired
        private MockMvc mockMvc;

        @Test
        public void shouldReturnProfiles() throws Exception {
            this.mockMvc.perform(get("/profiles"))
                    .andExpect(status().isOk())
                    .andExpect(content().string("[{\"id\":\"1\",\"name\":\"John Doe\"}]"));
        }
    }
    ```
2. Save file.
3. Switch to the **Test Explorer**, you will see the test `testAddPositiveNumbers` is added to the list with some test buttons.
4. Click on the **Run** button to run the test.
5. You will see the **Test Results** in the bottom of the window with timestamp in run the test.


## Exercise 5: Add a new service class

1. Create a `ProfileService` class at `src/main/java/th/in/nextflow/NextflowBoot/ProfileService.java`
   
    ```java
    package th.in.nextflow.NextflowBoot;

    import org.springframework.stereotype.Service;
    import org.springframework.web.client.RestTemplate;

    // This annotation is used to tell Spring Boot that this class is a service class.
    // it is used to create a singleton instance of the class.
    @Service
    public class ProfileService {

        // the restTemplate instance is used to send HTTP requests to the web server.
        private final RestTemplate restTemplate;
        
        // This constructor is used to inject the RestTemplate instance into the class.
        public ProfileService(RestTemplate restTemplate) {
            this.restTemplate = restTemplate;
        }

        // This method is used to send an HTTP GET request to the web server.
        // It returns the response body as a string.
        public String getProfiles() {
            String url = "https://651d740c44e393af2d59d2b4.mockapi.io/api/profiles";
            return restTemplate.getForObject(url, String.class);
        }
    }
    ```
2. Save file.
3. Open `src/main/java/th/in/nextflow/NextflowBoot/controller/ProfileController.java` to use **ProvideService** as an instance.
    
    ```java
    package th.in.nextflow.NextflowBoot.controller;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RestController;
    import org.springframework.beans.factory.annotation.Autowired;
    import th.in.nextflow.NextflowBoot.ProfileService;


    @RestController
    public class ProfileController {

        // This annotation is used to tell Spring Boot to inject the ProfileService instance into the class.
        // This instance is used to call the getProfiles method.
        @Autowired
        private ProfileService profileService;

        @GetMapping("/profiles")
        public String getProfiles() {
            // This method is used to call the getProfiles method of the ProfileService instance.
            return profileService.getProfiles();
        }
    }

    ```
4. Go to **Test Explorer**, then try to run the test. Explore the result. 

## Exercise 6: Create the integration test class 

1. Create a new class `src/test/java/th/in/nextflow/NextflowBoot/ProfileControllerIntegrationTest.java`.

    ```java
    package th.in.nextflow.NextflowBoot;

    import static org.assertj.core.api.Assertions.assertThat;
    import static org.mockito.Mockito.when;
    import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
    import org.junit.jupiter.api.Test;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
    import org.springframework.boot.test.context.SpringBootTest;
    import org.springframework.boot.test.mock.mockito.MockBean;
    import org.springframework.test.web.servlet.MockMvc;

    @SpringBootTest
    @AutoConfigureMockMvc
    public class ProfileControllerIntegrationTest {

        @Autowired
        private MockMvc mockMvc;

        // This annotation is used to tell Spring Boot to inject the ProfileService instance into the test class.
        // it will be used to mock the ProfileService instance.
        @MockBean
        private ProfileService profileService;

        @Test
        public void shouldReturnProfiles() throws Exception {
            
            // This method is used to mock the getProfiles method of the ProfileService instance.
            // it makes the getProfiles method return the expected JSON string.
            // reduce the dependency on the external service.
            when(profileService.getProfiles()).thenReturn("[{\"id\":\"1\",\"name\":\"John Doe\"}]");

            this.mockMvc.perform(get("/profiles"))
                    .andExpect(status().isOk())
                    .andExpect(content().string("[{\"id\":\"1\",\"name\":\"John Doe\"}]"));
        }
    }
    ```
2. Save file.
3. Run the test in the **Test Explorer**.
4. Examine the result.

> Note: it will be failed because we have not mocked the service class yet. especially the `RestTemplate` instance.

## Exercise 6: Provide necessary bean for application context

1. Create `AppConfig` class at `src/main/java/th/in/nextflow/NextflowBoot/AppConfig.java`

    ```java
    package th.in.nextflow.NextflowBoot;

    import org.springframework.context.annotation.Bean;
    import org.springframework.context.annotation.Configuration;
    import org.springframework.web.client.RestTemplate;

    // This annotation is used to tell Spring Boot that this class is a configuration class.
    @Configuration
    public class AppConfig {

        // This method is used to create a RestTemplate instance.
        // The RestTemplate instance is used to send HTTP requests to the web server.
        @Bean
        public RestTemplate restTemplate() {
            return new RestTemplate();
        }
    }
    ```
2. Save file.
3. Try to run the test in the **Test Explorer**.
4. Examine the result.

   
## Summary

In this lab, we created an integration test for the Spring Boot application. We used the `@SpringBootTest` annotation to run the test using the Spring Boot test environment. We also used the `@AutoConfigureMockMvc` annotation to automatically configure the MockMvc instance. We used the `@MockBean` annotation to mock the ProfileService instance. We also used the `@Bean` annotation to provide the RestTemplate instance to the application context.