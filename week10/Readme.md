# Week 10: Install and Explore Selenium for Automated Testing

## What is Selenium?

Selenium is an open-source tool used for automating web browsers. It provides a suite of tools for testing web applications across different browsers and platforms. The Selenium WebDriver API allows you to interact with web pages programmatically by simulating user actions like clicking, typing, and navigating.

## Installation of Selenium WebDriver

### Step 1: Install Node.js and npm

If you don't have Node.js installed, download it from the official website: https://nodejs.org/

Follow the instructions for your operating system.

Verify the installation by running the following commands in the terminal:

```bash
node -v
npm -v
```

### Step 2: Create a Project Folder

1. Open Visual Studio Code.
2. Create a new folder named `SeleniumLab`.
3. Open the terminal in VS Code and initialize a Node.js project:

```bash
npm init -y
```

### Step 3: Install Selenium WebDriver

Install the `selenium-webdriver` package:

```bash
npm install selenium-webdriver
```

Download the ChromeDriver that matches your Chrome browser version from the official Chrome for Testing page:

https://googlechromelabs.github.io/chrome-for-testing/

Extract the downloaded ChromeDriver and place it in the project folder if your setup requires a separate driver executable.

## Part 3: Writing a Simple Selenium Test Script

### Step 1: Create a JavaScript Test File

1. Inside the `SeleniumLab` folder, create a new file named `test.js`.
2. Copy and paste the following code into `test.js`.

**test.js**

```javascript
const { Builder, By, Key, until } = require('selenium-webdriver');

async function testGoogleSearch() {

    // Step 1: Launch the Chrome browser
    let driver = await new Builder().forBrowser('chrome').build();

    try {

        // Step 2: Open the Google homepage
        await driver.get('https://www.google.com');

        // Step 3: Locate the search box and enter a search query
        await driver.findElement(By.name('q'))
            .sendKeys('Selenium WebDriver', Key.RETURN);

        // Step 4: Wait for the search results to load
        await driver.wait(
            until.titleContains('Selenium WebDriver'),
            5000
        );

        // Step 5: Print the page title in the console
        let title = await driver.getTitle();
        console.log('Page Title:', title);

        // Step 6: Check if the search results are displayed
        if (title.includes('Selenium WebDriver')) {
            console.log(
                'Test Passed: Search results loaded successfully.'
            );
        } else {
            console.log(
                'Test Failed: Search results not loaded.'
            );
        }

    } catch (error) {
        console.error('Error:', error);
    } finally {

        // Step 7: Close the browser
        await driver.quit();
    }
}

testGoogleSearch();
```

### Explanation of the Code

1. **Import Selenium WebDriver**
   - `Builder`: Used to create a new browser instance.
   - `By`: Used to locate elements on a web page.
   - `Key`: Simulates keyboard actions.
   - `until`: Used for waiting until a condition is met.

2. **`testGoogleSearch` function**
   - Step 1: Launches the Chrome browser.
   - Step 2: Opens `https://www.google.com`.
   - Step 3: Finds the search box using its name attribute and types the query `Selenium WebDriver`.
   - Step 4: Waits until the page title includes `Selenium WebDriver`.
   - Step 5: Prints the page title.
   - Step 6: Verifies whether the search results loaded correctly.
   - Step 7: Closes the browser.

## Part 4: Running the Selenium Test Script

### Step 1: Run the Script

1. Make sure ChromeDriver is configured for your setup.
2. Open the terminal in Visual Studio Code.
3. Run the test script:

```bash
node test.js
```

### Expected Output

The Chrome browser should open, navigate to Google, perform a search for `Selenium WebDriver`, and display the search results.

The terminal should display output similar to:

```text
Page Title: Selenium WebDriver - Google Search

Test Passed: Search results loaded successfully.
```

The exact page title may vary.

## Part 5: Exploring Selenium Commands

### Commonly Used Selenium Commands

**1. Navigating to a URL**

```javascript
await driver.get('https://example.com');
```

**2. Locating Elements**

By ID:

```javascript
await driver.findElement(By.id('elementId'));
```

By Class Name:

```javascript
await driver.findElement(By.className('className'));
```

By Name:

```javascript
await driver.findElement(By.name('elementName'));
```

**3. Performing Actions**

Click an Element:

```javascript
await driver.findElement(By.id('buttonId')).click();
```

Enter Text:

```javascript
await driver.findElement(By.name('inputName'))
    .sendKeys('Hello World');
```

**4. Waiting for Elements**

```javascript
await driver.wait(
    until.elementLocated(By.id('elementId')),
    5000
);
```

**5. Closing the Browser**

```javascript
await driver.quit();
```

## Result

Selenium WebDriver was installed and explored using Node.js and JavaScript. A simple automated test was executed to search Google for Selenium WebDriver, retrieve the page title, and verify the result.

## Screenshots

Screenshots of Node.js installation, npm version, project setup, Selenium installation, source code, browser execution, and terminal output will be added to this README after all experiments are completed.