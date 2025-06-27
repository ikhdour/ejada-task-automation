# Java Test Automation Framework

## Overview

This project is a modular test automation framework built in Java using:

- **Selenium WebDriver** for browser UI automation
- **Cucumber + Gherkin** for BDD-style test cases
- **TestNG** for test execution and parallel test support
- **RestAssured** for API testing
- **ExtentReports** for HTML test execution reports
- **Maven** for build and dependency management

---

## Key Features

- 🔄 Cross-browser testing: Chrome & Firefox (via `config.properties`)
- ⚡ Parallel execution using TestNG
- 📦 Page Object Model (POM) for UI layers
- 🔐 Centralized configuration
- 📈 ExtentReports integration for HTML test reporting
- 🌐 API validation with REST Assured

---

## Project Structure

```
qa-automation-framework-java/
├── pom.xml
├── testng.xml
├── README.md
├── src/
│   ├── main/java/framework/
│   │   ├── base/
│   │   ├── config/
│   │   ├── drivers/
│   │   ├── pages/
│   │   ├── utils/
│   └── test/java/
│       ├── api/
│       ├── runners/
│       └── stepdefinitions/
│   └── test/resources/
│       ├── features/
│       └── config.properties
```

---

## Installation & Setup

1. **Clone this repository:**

```bash
git clone https://github.com/yourusername/qa-automation-framework-java.git
cd qa-automation-framework-java
```

2. **Install dependencies:**

```bash
mvn clean install
```

3. **Configure settings:** Edit `src/test/resources/config.properties`

```properties
browser=chrome
url=https://www.saucedemo.com
```

---

## Running Tests

### 🧪 UI Tests

To run the Cucumber + Selenium tests with TestNG:

```bash
mvn test
```

To run with a specific browser:

```properties
browser=firefox
```

### 📑 View Reports

After running tests, open:

```
target/extent-report/ExtentReport.html
```

---

## API Testing (REST Assured)

Run API tests directly or group under TestNG:

```java
@Test
public void testGetBooks() {
    given().baseUri("https://simple-books-api.glitch.me")
    .when().get("/books")
    .then().statusCode(200);
}
```

Operations covered:

- GET all books
- POST order with token
- PATCH update order
- DELETE order

---

## Parallel Test Execution

The `testng.xml` file allows parallel execution by browser:

```xml
<suite name="Suite" parallel="tests" thread-count="2">
  <test name="ChromeTests">
    <parameter name="browser" value="chrome"/>
    <classes>
      <class name="runners.TestRunner"/>
    </classes>
  </test>
  <test name="FirefoxTests">
    <parameter name="browser" value="firefox"/>
    <classes>
      <class name="runners.TestRunner"/>
    </classes>
  </test>
</suite>
```

---

## Reporting with ExtentReports

### Add to pom.xml:

```xml
<dependency>
  <groupId>com.aventstack</groupId>
  <artifactId>extentreports</artifactId>
  <version>5.1.1</version>
</dependency>
```

### Create ReportManager:

```java
ExtentReports extent = new ExtentReports();
ExtentSparkReporter spark = new ExtentSparkReporter("target/extent-report/ExtentReport.html");
extent.attachReporter(spark);
extent.flush();
```

---

# ejada-task
