# Week 5 – Integrate Java Project with Jenkins

## Aim
To create a Java program and automate its build using Jenkins.

## Requirements
- Java JDK
- Git
- GitHub account
- Jenkins
- Visual Studio Code or another text editor

## 1. Create a Java Program

Create a file named `Demo.java`.

```java
public class Demo {
    public static void main(String[] args) {
        System.out.println("hello world");
    }
}
```

## 2. Execute the Java Program

Open the terminal in the folder containing `Demo.java`.

```bash
javac Demo.java
java Demo
```

### Expected output

```text
hello world
```

## 3. Push the Java Project to GitHub

Create an empty GitHub repository named `Java-Jenkins`.

Run the following commands from the folder containing `Demo.java`. Replace the example URL with your repository URL.

```bash
git init
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git add .
git commit -m "Adding Java program"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/Java-Jenkins.git
git push -u origin main
```

## 4. Configure Jenkins

1. Open the Jenkins web interface.
2. Click **New Item**.
3. Enter a job name, such as `Java-Build`.
4. Select **Freestyle project** and click OK.
5. Under Source Code Management, select **Git**.
6. Enter your GitHub repository URL.
7. Select the correct branch, such as `*/main`.
8. Under Build Triggers, select **Poll SCM** and enter:

```text
H/5 * * * *
```

9. Under Build Steps, select **Execute Windows batch command**.

Enter the following build commands:

```bat
javac Demo.java
java Demo
```

10. Click **Save**.

## 5. Run the Jenkins Job

1. Open the `Java-Build` job.
2. Click **Build Now**.
3. Open the build number under Build History.
4. Click **Console Output** to view the result.

## Outputs

### Output 1: Java program execution

![Java program output](images/java-output.png)

### Output 2: GitHub repository

![GitHub repository containing Demo.java](images/github-repository.png)

### Output 3: Jenkins job configuration

![Jenkins Freestyle project configuration](images/jenkins-job-configuration.png)

### Output 4: Jenkins build console

![Jenkins console output showing hello world](images/jenkins-console-output.png)

> Replace these image paths with your actual screenshots saved in the `images/` folder. The images must exist in the repository for them to display on GitHub.

## Files Included
- `experiment-record.pdf` – Lab record
- `Demo.java` – Java source code
- `README.md` – Experiment documentation
- `images/` – Execution screenshots

## Result
A Java program is integrated with Jenkins, and the Jenkins job is configured to compile and execute the program.