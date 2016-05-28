# jmeter-lightning-maven-plugin-example
This repo contains [JMeter Lightning Maven Plugin](https://github.com/automatictester/jmeter-lightning-maven-plugin) usage example.

Prerequisites:
- Java 7 or above
- Git
- Maven 3

Steps:
- Clone this repo: `git clone https://github.com/automatictester/jmeter-lightning-maven-plugin-example.git`
- Go to cloned directory: `cd jmeter-lightning-maven-plugin-example`
- Run JMeter tests with jmeter-maven-plugin and results analysis with jmeter-lightning-maven-plugin: `mvn clean verify`.
This will execute jmeter-maven-plugin at `integration-test` and jmeter-lightning-maven-plugin at `post-integration-test` phase.
JMeter test results will be saved to `target/jmeter/results/example.csv`
- Your output should contain output similar to this:

```
[INFO] --- jmeter-lightning-maven-plugin:0.1.1:lightning (default) @ jmeter-lightning-maven-plugin-example ---
[INFO] Test name:            JMeter home page - average response time
[INFO] Test type:            avgRespTimeTest
[INFO] Transaction name:     JMeter home page
[INFO] Expected result:      Average response time <= 1000
[INFO] Actual result:        Average response time = 67.0
[INFO] Transaction count:    10
[INFO] Longest transactions: [171, 58, 57, 56, 56]
[INFO] Test result:          Pass
[INFO] 
[INFO] Test name:            JMeter home page - failed tests
[INFO] Test type:            passedTransactionsTest
[INFO] Transaction name:     JMeter home page
[INFO] Expected result:      Number of failed transactions <= 0
[INFO] Actual result:        Number of failed transactions = 0
[INFO] Transaction count:    10
[INFO] Test result:          Pass
[INFO] 
[INFO] ============= EXECUTION SUMMARY =============
[INFO] Tests executed:    2
[INFO] Tests passed:      2
[INFO] Tests failed:      0
[INFO] Tests errors:      0
[INFO] Test set status:   Pass
[INFO] Execution time:    80ms
[INFO] ##teamcity[buildStatisticValue key='JMeter home page - average response time' value='67.0']
[INFO] ##teamcity[buildStatisticValue key='JMeter home page - failed tests' value='0']
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 3.680 s
[INFO] Finished at: 2016-05-28T18:35:19+01:00
[INFO] Final Memory: 13M/226M
[INFO] ------------------------------------------------------------------------
```

JUnit XML report will be saved to `target/jmeter/bin/junit.xml`:

```
<?xml version="1.0" encoding="UTF-8"?>
<testsuite errors="0" failures="0" name="Lightning" tests="2" time="0">
    <testcase name="JMeter home page - average response time" time="0"/>
    <testcase name="JMeter home page - failed tests" time="0"/>
</testsuite>
```

Properties file for Jenkins Build Name Setter plugin will be saved to `lightning-jenkins.properties`:

```
#In Jenkins Build Name Setter Plugin, define build name as: ${PROPFILE,file="lightning-jenkins.properties",property="result.string"}
#Mon May 02 19:08:52 BST 2016
result.string=Tests executed\: 2, failed\: 0
```

- Feel free to play with plugin configuration in `pom.xml`, JMeter test plan `src/test/jmeter/example.jmx` and Lightning config file `src/test/resources/lightning.xml`. Once you familiarised yourself with the tool, create your own JMeter tests, plugin configuration and plug it into your CI/CD server. Check Lightning [home page](http://automatictester.github.io/lightning/index.html) for more info.
