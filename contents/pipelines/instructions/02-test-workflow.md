
# Lab 02: Test Workflow

## Exercise 0: Prepare github project

1. Ensure you completed the previous lab.

## Exercise 1: Create a new workflow for testing

1. From the github repository, click on the **Actions** tab, which now has our first workflow.
2. From the left side menu, click on the **New workflow** button.
   
3. Select **Set up a workflow yourself**.
   
4. Rename the file to `build-and-test.yml`.
5. Provide the following code in 

```yml
name: Build and run

on:
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

6. Notice that we have another job called `test` that runs the tests.
7. Click on **Commit changes**
8. Merge the pull request to the main branch.
9. After completing the merge, go to the **Actions** tab.
10. Click on the **Build and Test** workflow.
11. Click on the **Run workflow** button. then click on the **Run workflow** button on the pop-up dialog.
12. Examine the logs and the steps of the workflow.

## Summary 

In this lab, we created a new workflow that builds and tests the project. We used the `workflow_dispatch` event to trigger the workflow manually. We also learned how to run multiple jobs in a workflow.