
# Lab 03: Use workflow as pull request validator

## Exercise 0: Prepare github project

1. Ensure you completed the previous lab.

## Exercise 1: Edit the existing workflow to use as a pull request validator

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
```


5. Select **Commit Changes** button on the top right corner of the page to save the changes.
6. On the commit page, select **Create a new branch for this commit and start a pull request**.
7. select **Commit change**
8. fill in the pull request details and select **Create pull request**.
9. Please notice that we have a workflow run to test the pull request. before merging the pull request.
10. wait for the workflow to complete. then merge the pull request.



## Summary 

In this lab, we used the workflow as a pull request validator. We modified the existing workflow to run on pull requests and the workflow_dispatch event. We also learned how to create a pull request and merge it after the tests pass.