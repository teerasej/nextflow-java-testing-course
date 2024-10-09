
# Lab 04: Code Coverage as Artifact

## Exercise 0: Prepare github project

1. Ensure you completed the previous lab.

## Exercise 1: Add Jacoco to the project

1. open the `pom.xml` file.
2. Add the following plugin to the `build` section of the `pom.xml` file.

    ```xml
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
    ```
3. Save the file.
4. Commit the changes to the repository and push the changes to **main** branch.

## Exercise 2: Edit the existing workflow to use as a pull request validator

1. From the github repository, click on the **Actions** tab.
2. From the left side menu, click on the **Build and test** workflow.
3. Click on edit button to edit the workflow.
4. Modify the code like below:

```yml
name: Build and run

on:
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up JDK 17
      uses: actions/setup-java@v2
      with:
        java-version: '17'
        distribution: 'temurin'

    - name: Build with Maven
      run: ./mvnw clean install

    - name: Run tests
      run: ./mvnw test

    - name: Generate code coverage report
      run: mvn jacoco:report

    - name: Upload code coverage report
      uses: actions/upload-artifact@v4.4.3
      with:
        name: code-coverage-report
        path: target/site/jacoco
```
   
5. Select **Commit Changes** button on the top right corner of the page to save the changes.
6. On the commit page, select **Commit to main**.
7. select **Commit change**
8. Go back to the **Actions** tab.
9. Click on the **Build and Test** workflow.
10. Click on the **Run workflow** button. then click on the **Run workflow** button on the pop-up dialog.
11. wait for the workflow to complete
12. On summary section, click on the **artifact** link to download the code coverage report.


## Summary 

In this lab, we added Jacoco to the project to generate code coverage report. We modified the existing workflow to generate the code coverage report and upload it as an artifact. We also learned how to download the artifact from the workflow run.

## Challenge 1: Make the fault pull request 

- Use the Java code in the repository to create a pull request that will fail the tests.
- The pull request should not be merged until the tests pass.
- Change the code in the repository to make the tests pass.