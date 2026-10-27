# Week 11: JavaScript Registration Form Testing Using Selenium

## 1. Objective

To create a simple registration form using HTML and JavaScript and perform automated functional testing using Selenium.

## 2. Requirements

- Node.js and npm
- Visual Studio Code
- Google Chrome
- Selenium WebDriver

## 3. Install Node.js and npm

Download Node.js from https://nodejs.org/.

Verify the installation:

```bash
node -v
npm -v
```

**Explanation:** These commands check whether Node.js and npm are installed.

## 4. Create the Registration Form

Create a folder named `RegistrationForm` in Visual Studio Code.

Inside the folder, create a file named `index.html`. Use the HTML registration form from Week 1, ensuring it contains these elements:

- Username: `id="username"`
- Email: `id="email"`
- Password: `id="password"`
- Form: `id="registrationForm"`
- Message: `id="message"`
- Register button

Add the following JavaScript inside the HTML file's `<script>` tag.

```javascript
<!DOCTYPE html>
<html>
<head>
    <title>Registration Form</title>
</head>
<body>
    <h2>Registration Form</h2>

    <form id="registrationForm">
        <input id="username" placeholder="Username"><br><br>
        <input id="email" placeholder="Email"><br><br>
        <input id="password" type="password" placeholder="Password"><br><br>
        <button type="submit">Register</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("registrationForm")
        .addEventListener("submit", function(event) {
            event.preventDefault();

            let username = document.getElementById("username").value;
            let email = document.getElementById("email").value;
            let password = document.getElementById("password").value;
            let message = document.getElementById("message");

            let pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

            if (!username || !email || !password)
                message.textContent = "All fields are required!";
            else if (!pattern.test(email))
                message.textContent = "Invalid email format!";
            else {
                message.textContent = "Registration Successful!";
                message.style.color = "green";
                this.reset();
            }
        });
    </script>
</body>
</html>
```

**Explanation:** The JavaScript validates the input fields and email format. If all details are valid, it displays `Registration Successful!` and clears the form.

## 5. Run the Web Application

Open the terminal inside the `RegistrationForm` folder.

Run:

```bash
npx http-server
```

Open the browser and visit:

`http://localhost:8080`

**Expected output:** The registration form appears with Username, Email, Password, and Register fields.

## 6. Install Selenium WebDriver

Open a second terminal inside the same project folder.

Run:

```bash
npm init -y
npm install selenium-webdriver
```

Configure ChromeDriver if your setup requires a separate driver executable.

**Explanation:** Selenium WebDriver automates browser actions, including filling out the registration form and clicking Register.

## 7. Create the Selenium Test Script

Create a file named `test.js` in the `RegistrationForm` folder.

Add the following code:

```javascript
<!DOCTYPE html>
<html>
<head>
    <title>Registration Form</title>
</head>
<body>
    <h2>Registration Form</h2>

    <form id="registrationForm">
        <input id="username" placeholder="Username"><br><br>
        <input id="email" placeholder="Email"><br><br>
        <input id="password" type="password" placeholder="Password"><br><br>
        <button type="submit">Register</button>
    </form>

    <p id="message"></p>

    <script>
        document.getElementById("registrationForm")
        .addEventListener("submit", function(event) {
            event.preventDefault();

            let username = document.getElementById("username").value;
            let email = document.getElementById("email").value;
            let password = document.getElementById("password").value;
            let message = document.getElementById("message");

            let pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

            if (!username || !email || !password)
                message.textContent = "All fields are required!";
            else if (!pattern.test(email))
                message.textContent = "Invalid email format!";
            else {
                message.textContent = "Registration Successful!";
                message.style.color = "green";
                this.reset();
            }
        });
    </script>
</body>
</html>
```

**Explanation:**

- `driver.get()` opens the registration form.
- `sendKeys()` enters the test details.
- `click()` submits the form.
- `getText()` retrieves the success message.
- The condition checks whether registration was successful.
- `driver.quit()` closes Chrome.

## 8. Execute the Selenium Test

Keep the HTTP server running in the first terminal.

In the second terminal, execute:

```bash
node test.js
```

**Expected output:**

```text
Test Result: Registration Successful!
Test Passed
```

Chrome should open automatically, fill in the registration details, submit the form, and close after the test.

## 9. Result

The registration form was created using HTML and JavaScript. Selenium WebDriver automated form submission and verified the successful registration message.

## 10. Screenshots to Add Later

- `images/01-node-npm-installation.png`
- `images/02-registration-form.png`
- `images/03-javascript-code.png`
- `images/04-selenium-installation.png`
- `images/05-test-js-code.png`
- `images/06-automated-browser-test.png`
- `images/07-test-output.png`
