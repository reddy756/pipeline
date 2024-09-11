# Jenkins Maven Tool - Unit Tests and Integration 
---
## Unit Tests vs Integration Tests:
- **The unit test** run configuration is a part of the Maven default project configuration. Maven runs these tests automatically if following criteria are met:
  - The tests are in the directory **src/test/java** 
  - The test class name either **starts** with **Test** or **ends** with **Test** or **TestCase**.

  Maven runs these tests during the [Mavens' build lifecycle](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) phase test. Surefire plugin is responsible for unit tests.

- **The integration test** run configuration has to be done manually. It exists Maven plugins that can help. We want that the following criteria are met:

   - Integration tests are stored in the directory **src/it/java** 
   - The integration test class name either **starts** with **IT** or **ends** with **IT** or **ITCase**
  
   Maven runs these tests during the Mavens' build lifecylce phase integration-test. Failsafe plugin is responsible for integration tests.

   We should configure Maven in a such way Surefire doesn't execute Integration tests and Failsafe doesn't execute unit tests. surefire doesn't execute Integration tests and Failsafe doesn't execute unit tests.

## Running Unit Tests and Integration Tests Seperatel 

Maven has a build lifecycle made up out of several phases. When you call a particular one, all phases before that one will be executed first. See https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

There are two ways how you could solve what you want:

- use `-Dsurefire.skip=true/false` and `-DskipITs=true/false`(https://www.mkyong.com/maven/how-to-skip-maven-unit-test/)
- call the plugin goal directly `mvn clean test-compile failsafe:integration-test`
