
# Lab 01: Try GitHub Actions

## Exercise 0: Prepare github project

1. Go to the repository `https://github.com/teerasej/nextflow-spring-boot-test/`
2. Fork the repository to your own account.

## Exercise 1: Create a new workflow

1. From the github repository, click on the **Actions** tab.
2. Explore the available workflows and select **Set up this workflow** for the **Java with Maven** workflow.

   <img width="1052" alt="2024-10-10_00-15-53" src="https://github.com/user-attachments/assets/dbd0f83d-e1ba-4e9a-b123-672b6cc0689a">

4. it will create a new file `.github/workflows/maven.yml` in the repository. Like example below:

    ```yml
    # This workflow will build a Java project with Maven, and cache/restore any dependencies to improve the workflow execution time
    # For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven

    # This workflow uses actions that are not certified by GitHub.
    # They are provided by a third-party and are governed by
    # separate terms of service, privacy policy, and support
    # documentation.

    name: Java CI with Maven

    on:
    push:
        branches: [ "main" ]
    pull_request:
        branches: [ "main" ]

    jobs:
    build:

        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v4
        - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
            java-version: '17'
            distribution: 'temurin'
            cache: maven
        - name: Build with Maven
        run: mvn -B package --file pom.xml

        # Optional: Uploads the full dependency graph to GitHub to improve the quality of Dependabot alerts this repository can receive
        - name: Update dependency graph
        uses: advanced-security/maven-dependency-submission-action@571e99aab1055c2e71a1e2309b9691de18d6b7d6
    ```

5. On the top, rename the file to `build.yml`.
6. Modify the code like below:

```yml
# This workflow will build a Java project with Maven, and cache/restore any dependencies to improve the workflow execution time
# For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven

# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

name: Build my project

on:
  workflow_dispatch:

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: maven
    - name: Build with Maven
      run: mvn -B package --file pom.xml
```

7. Select **Commit Changes** button on the top right corner of the page to save the changes.
8. Make a pull request and merge to the main branch. 

    > **Note**: The workflow will be showed in the **Actions** tab. only when the workflow file (.yml) is in the main branch. (or default branch)

## Exercise 2: Trigger the workflow

1. Go to the **Actions** tab.
2. Click on the **Build my project** workflow.
3. Select **Run Workflow** button on the right side of the page.
4. Select **Run Workflow** button on the pop-up dialog.

    <img width="1655" alt="2024-10-10_00-42-22" src="https://github.com/user-attachments/assets/cc2e4159-b096-4de1-930e-d440d5bff896">

5. Wait for the workflow's status show
6. click on the **Build my project** workflow to see the details of the workflow.
7. Explore the logs and the steps of the workflow.
8. If the workflow is successful, you will see the **blue** checkmark on the top of the page.

## Summary

In this lab, we created a new workflow that builds and tests the project. We used the `workflow_dispatch` event to trigger the workflow manually. We also learned how to run multiple jobs in a workflow.
