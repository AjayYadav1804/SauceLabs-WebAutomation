# Sauce Labs Test Automation Framework

## Project Overview
This project provides an automated testing framework for the Sauce Demo web application using Selenium WebDriver with Java. The framework follows the Page Object Model (POM) design pattern to create a maintainable and scalable automation solution.

## What We Test
This framework automates the end-to-end testing of the Sauce Demo e-commerce application at https://www.saucedemo.com/v1/, including:

- User authentication (login/logout)
- Shopping cart functionality
- Checkout process
- Product selection and quantity adjustment
- Payment information handling
- Order placement
- Complete end-to-end workflows


### End-to-End Shopping Flow
1. Browser Launch & Navigation
   - Launch mobile browser (Chrome/Firefox/Edge)
   - Navigate to Sauce Labs demo site
2. Authentication
   - Login with valid credentials
3. Product Selection
   - Choose product
   - Update quantity
   - Add to cart
4. Checkout Process
   - Cart verification
   - Shipping information
   - Payment details
   - Order placement
5. Post-Order Validation
   - Order confirmation
   - Return to home screen
   
## End-to-End Test Case
The primary automated test case follows this workflow:
1. Launch browser in mobile view (Chrome, Firefox, or Edge)
2. Navigate to https://www.saucedemo.com/v1/
3. Click on Menu
4. Click on Login
5. Login using valid credentials
6. Choose a product
7. Click on counter plus button to increase quantity
8. Click on Add to Cart button
9. Click on Cart badge
10. Click on Proceed to Checkout button
11. Fill checkout information
12. Fill payment information
13. Click on Place Order button
14. Click on Continue Shopping button
15. Validate that user returns to Home screen

## Tech Stack
- **Programming Language**: Java
- **Build Tool**: Maven
- **Testing Framework**: TestNG (based on project configuration)
- **UI Automation**: Selenium WebDriver
- **Reporting**: ExtentReports
- **Browsers Supported**: Chrome, Firefox, Edge
- **Logging**: Log4j2
- **Data Management**: Excel (TestData.xlsx)
- **Email Notification**: Automated email reports after test execution

## Project Structure

```
saucedemo-tests/
├── src/
│   ├── main/java/
│   │   ├── com.saucedemo.pageobjects/
│   │   │   ├── Actions.java                # Common actions for page interactions
│   │   │   ├── CartPage.java               # Cart page object
│   │   │   ├── CheckoutPage.java           # Checkout page object
│   │   │   ├── InventoryPage.java          # Inventory/products page object
│   │   │   ├── LoginPage.java              # Login page object
│   │   │   └── LogoutPage.java             # Logout page object
│   │   ├── com.saucedemo.utils/
│   │   │   ├── EmailSender.java            # Utility for sending email reports
│   │   │   ├── ExcelUtils.java             # Excel data handling utilities
│   │   │   ├── ExtentReportManager.java    # Test report generation management
│   │   │   ├── LoggingUtils.java           # Logging utilities
│   │   │   └── ScreenshotUtils.java        # Screenshot capture utilities
│   │   └── resources/
│   │       ├── config.properties           # Configuration properties
│   │       └── log4j2.xml                  # Log4j2 configuration
│   └── test/java/
│       ├── com.saucedemo.listeners/
│       │   └── TestListener.java           # Test execution listeners
│       ├── com.saucedemo.tests/
│       │   ├── BaseTest.java               # Base test class with common setup/teardown
│       │   └── EndToEndWorkflowTest.java   # End-to-end test scenarios
│       └── resources/
│           └── TestData.xlsx               # Test data in Excel format
├── libs/                                   # WebDriver executables
│   ├── chromedriver.exe
│   ├── geckodriver.exe
│   └── msedgedriver.exe
├── reports/                                # Test execution reports
│   ├── screenshots/                        # Test screenshots
│   └── testReport.html                     # HTML test reports
├── test-output/                            # Test execution outputs
│   ├── EndToEndTest.xml                    # Test results in XML format
│   └── pom.xml                             # Maven configuration
```

## Key Components Explanation

### Page Objects
The framework uses the Page Object Model pattern to represent each page of the application:
- **LoginPage**: Handles authentication functionality
- **InventoryPage**: Manages product browsing and selection
- **CartPage**: Handles shopping cart operations
- **CheckoutPage**: Manages the checkout process
- **LogoutPage**: Handles logout functionality
- **Actions**: Contains common actions that can be performed across multiple pages

### Utilities
The framework includes several utility classes:
- **ExcelUtils**: Handles test data operations with Excel files
- **ExtentReportManager**: Manages test reporting with ExtentReports
- **LoggingUtils**: Provides logging capabilities using Log4j2
- **ScreenshotUtils**: Captures screenshots for test documentation
- **EmailSender**: Sends email notifications with test results and attached HTML reports after test execution

### Tests
- **BaseTest**: Contains common setup and teardown operations for all tests
- **EndToEndWorkflowTest**: End-to-end test scenarios that validate complete workflows

### Resources
- **config.properties**: Contains configuration parameters like URLs, timeouts, email settings, etc.
- **log4j2.xml**: Configuration for logging
- **TestData.xlsx**: Test data in Excel format for data-driven testing

## How to Run the Tests

### Prerequisites
- Java JDK 8 or higher installed
- Maven installed
- Web browsers (Chrome, Firefox, Edge) installed
- Configure email settings in config.properties for report delivery

### Setup Steps
1. Clone the repository
2. Navigate to the project directory
3. Update the `config.properties` file with your environment-specific settings:
   ```properties
   # Browser Configuration
   browser=chrome
   
   # Application URL
   baseUrl=https://www.saucedemo.com/v1/
   
   # Test Data
   username=standard_user
   password=secret_sauce
   
   # Email Configuration
   mail.smtp.host=smtp.gmail.com
   mail.smtp.port=587
   mail.username=your-email@gmail.com
   mail.password=your-app-password
   mail.recipient=recipient-email@example.com
   mail.subject=Sauce Demo Test Execution Report
   ```

### Running Tests via Maven
Run all tests:
```bash
mvn clean test
```

Run a specific test class:
```bash
mvn clean test -Dtest=EndToEndWorkflowTest
```

### Running Tests in a Specific Browser
By default, tests run in Chrome. To run in a different browser, update the browser parameter in the config.properties file or pass it as a Maven parameter:

```bash
mvn clean test -Dbrowser=firefox
```

### Email Reporting
After test execution, an email with the HTML test report will be automatically sent to the configured recipients. The email will include:
- Test execution summary
- Attached HTML report
- Timestamp of execution
- Browser information

To configure the email settings:
1. Update the SMTP settings in the config.properties file
2. For Gmail, you may need to generate an App Password
3. Specify recipient email addresses

### Viewing Reports Locally
After test execution, reports can be found in:
- HTML Report: `reports/testReport.html`
- Screenshots: `reports/screenshots/`
- XML Results: `test-output/EndToEndTest.xml`


## Troubleshooting
- **WebDriver Issues**: Ensure that the WebDriver executables in the libs folder match your browser versions
- **Email Sending Failures**: Check your SMTP settings and ensure less secure apps are allowed (for Gmail)
- **Test Data Issues**: Verify the format and content of TestData.xlsx

