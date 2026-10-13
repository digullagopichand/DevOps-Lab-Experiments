# Week 12: Node.js Registration Form, Docker Containerization, and Selenium Testing

## Aim

To create a registration form using Node.js, containerize the application using Docker, and test the application using Selenium WebDriver.

## Software Requirements

- Node.js and npm
- Visual Studio Code
- Docker Desktop
- Google Chrome
- Selenium WebDriver

## Step 1: Create the Node.js Application

Create a project folder named `nodejs-registration`.

Open the folder in Visual Studio Code and create the following files and folders:

```text
nodejs-registration/
├── app.js
├── package.json
├── Dockerfile
├── public/
│   └── index.html
└── selenium-tests/
    └── test_registration.js
```

### Create `package.json`

```json
{
  "name": "nodejs-registration",
  "version": "1.0.0",
  "description": "Simple Node.js registration form",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "body-parser": "^1.20.2"
  }
}
```

Install the required packages:

```bash
npm install
```

### Create `app.js`

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const path = require('path');

const app = express();

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static('public'));

app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

app.post('/register', (req, res) => {
  const { username, email, password } = req.body;

  console.log(`Username: ${username}, Email: ${email}`);

  res.send('Registration successful!');
});

const PORT = 3000;

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

**Explanation:** Express creates the web server. The application displays the registration form and processes submitted registration details at the `/register` route.

## Step 2: Create the Registration Form

Inside the `public` folder, create `index.html`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registration Form</title>
</head>
<body>
  <h2>Registration Form</h2>

  <form action="/register" method="POST">
    <label for="username">Username:</label>
    <input type="text" id="username" name="username" required>
    <br><br>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    <br><br>

    <label for="password">Password:</label>
    <input type="password" id="password" name="password" required>
    <br><br>

    <button type="submit">Register</button>
  </form>
</body>
</html>
```

**Explanation:** The form accepts a username, email, and password. When the Register button is clicked, the form sends the information to the Node.js server.

## Step 3: Run the Node.js Application

Run the following command from the project directory:

```bash
npm start
```

Open the browser and visit:

```text
http://localhost:3000
```

Enter the registration details and click **Register**.

The application should display:

```text
Registration successful!
```

Stop the application with `Ctrl + C` before proceeding if needed.

## Step 4: Containerize the Application Using Docker

Create a file named `Dockerfile` in the project root directory.

```dockerfile
FROM node:14

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

**Explanation:**

- `FROM node:14` selects the Node.js base image used in the lab manual.
- `WORKDIR` sets the working directory inside the container.
- `COPY` copies the application files.
- `RUN npm install` installs the dependencies.
- `EXPOSE 3000` documents the application port.
- `CMD` starts the Node.js application.

### Build the Docker Image

Run this command from the directory containing the Dockerfile:

```bash
docker build -t nodejs-registration-app .
```

### Run the Docker Container

```bash
docker run -d -p 3000:3000 --name nodejs-registration nodejs-registration-app
```

### Verify the Container

```bash
docker ps
```

Open the application in the browser:

```text
http://localhost:3000
```

The registration form should now run inside the Docker container.

### View Container Logs

```bash
docker logs nodejs-registration
```

## Step 5: Set Up Selenium Testing

Open a new terminal and move into the Selenium test directory:

```bash
cd selenium-tests
npm init -y
npm install selenium-webdriver
```

Ensure Google Chrome is installed. Selenium WebDriver may manage the compatible browser driver automatically; otherwise, configure a compatible ChromeDriver.

Create `test_registration.js` inside the `selenium-tests` folder.

```javascript
const { Builder, By, until } = require('selenium-webdriver');

async function runTest() {
  const driver = await new Builder().forBrowser('chrome').build();

  try {
    await driver.get('http://localhost:3000');

    await driver.findElement(By.id('username')).sendKeys('testuser');
    await driver.findElement(By.id('email')).sendKeys('testuser@example.com');
    await driver.findElement(By.id('password')).sendKeys('password123');

    await driver.findElement(By.tagName('button')).click();

    await driver.wait(
      until.elementLocated(By.tagName('body')),
      5000
    );

    const bodyText = await driver.findElement(By.tagName('body')).getText();

    if (bodyText.includes('Registration successful!')) {
      console.log('Test Passed: Registration was successful.');
    } else {
      console.log('Test Failed: Registration was not successful.');
    }
  } catch (error) {
    console.error('Error:', error);
  } finally {
    await driver.quit();
  }
}

runTest();
```

**Explanation:** Selenium opens the registration page, fills in the fields, clicks Register, and checks whether the success message appears.

## Step 6: Execute the Selenium Test

Make sure the Docker container is running:

```bash
docker ps
```

If it is not running, start it:

```bash
docker start nodejs-registration
```

From the `selenium-tests` directory, execute:

```bash
node test_registration.js
```

### Expected Output

```text
Test Passed: Registration was successful.
```

The browser should open, submit the registration form, and verify the server response.

## Result

The Node.js registration application was created and executed, containerized using Docker, and tested using Selenium WebDriver.

## Screenshots and Outputs

*Add the actual screenshots directly in this README after completing all weekly README files.*

1. **Node.js Registration Form** — `![Registration Form](images/week12-registration-form.png)`
2. **Docker Image Build** — `![Docker Build](images/week12-docker-build.png)`
3. **Running Docker Container** — `![Docker Container](images/week12-docker-container.png)`
4. **Application in Browser** — `![Application in Browser](images/week12-application.png)`
5. **Selenium Test Output** — `![Selenium Test Output](images/week12-selenium-test.png)`