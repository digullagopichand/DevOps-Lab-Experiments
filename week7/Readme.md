# Week 7: Create a Simple Java Containerized Application Using Docker

## 1. Aim

To create a simple Java application and containerize it using Docker.

## 2. Requirements

- Docker Desktop
- Visual Studio Code
- Java JDK (for local execution, optional)
- Internet connection
- Docker Hub account (for publishing the image)

## 3. Create the Application Folder

1. Create a folder named `Java-Docker`.
2. Open Visual Studio Code.
3. Select **File → Open Folder**.
4. Select the `Java-Docker` folder.
5. Create a new file named `Test.java`.

## 4. Write the Java Program

Enter the following code in `Test.java`:

```java
public class Test {
    public static void main(String[] args) {
        int a = 20, b = 30, c;

        c = a * b;

        System.out.println("Hello world");
        System.out.println("value of c is " + c);
    }
}
```

Save the file.

### Expected output

```text
Hello world
value of c is 600
```

## 5. Create the Dockerfile

Create a file named `Dockerfile` in the same folder. Do not add a file extension.

Enter:

```dockerfile
FROM openjdk
WORKDIR /sam
COPY . /sam
RUN javac Test.java
CMD ["java", "Test"]
```

Save the file.

### Dockerfile explanation

- `FROM openjdk` — specifies the Java base image.
- `WORKDIR /sam` — sets the working directory inside the container.
- `COPY . /sam` — copies the application files into the container.
- `RUN javac Test.java` — compiles the Java program during image creation.
- `CMD ["java", "Test"]` — runs the Java program when the container starts.

## 6. Open the Terminal

1. Start Docker Desktop and wait until the Docker Engine is running.
2. Open the `Java-Docker` folder in Visual Studio Code.
3. Select **Terminal → New Terminal**.
4. Verify that the terminal is in the application folder.

Check the Docker installation:

```bash
docker --version
```

List existing images:

```bash
docker images
```

### Output screenshot

![Docker version and images](images/01-docker-version-images.png)

## 7. Build the Docker Image

Execute:

```bash
docker build -t helloworld .
```

The dot (`.`) specifies the current directory as the build context.

Docker reads the Dockerfile, downloads the base image if needed, copies the application, compiles the Java source, and creates the image.

Verify the image:

```bash
docker images
```

### Expected result

The image list includes `helloworld`.

### Output screenshot

![Docker image build output](images/02-docker-build.png)

## 8. Run the Docker Container

Execute:

```bash
docker run --name mycontainer helloworld
```

Docker creates a container and runs the Java application.

### Expected output

```text
Hello world
value of c is 600
```

### Output screenshot

![Java application running in Docker](images/03-docker-run.png)

## 9. Verify the Container Output

Execute:

```bash
docker logs mycontainer
```

### Expected output

```text
Hello world
value of c is 600
```

Check all containers:

```bash
docker ps -a
```

The container will usually show an exited status because the Java program finishes after printing the output.

### Output screenshot

![Docker container logs](images/04-docker-logs.png)

## 10. Create a Docker Hub Repository

1. Open [Docker Hub](https://hub.docker.com/).
2. Sign in to your account.
3. Click **Create repository**.
4. Enter the repository name `java-docker-demo`.
5. Choose Public or Private.
6. Create the repository.

### Output screenshot

![Docker Hub repository](images/05-dockerhub-repository.png)

## 11. Log In to Docker Hub

Execute:

```bash
docker login
```

Follow the authentication prompts.

Do not put passwords or access tokens in screenshots or README files.

### Output screenshot

![Docker login output](images/06-docker-login.png)

## 12. Tag the Docker Image

Replace `YOUR-DOCKERHUB-USERNAME` with your Docker Hub username.

```bash
docker tag helloworld YOUR-DOCKERHUB-USERNAME/java-docker-demo:latest
```

Verify the image tag:

```bash
docker images
```

### Expected result

The image appears with your Docker Hub username, repository name, and `latest` tag.

### Output screenshot

![Docker image tagging output](images/07-docker-tag.png)

## 13. Push the Image to Docker Hub

Execute:

```bash
docker push YOUR-DOCKERHUB-USERNAME/java-docker-demo:latest
```

Wait for the upload to complete.

Open Docker Hub and verify that the image is listed in the repository.

### Output screenshot

![Docker image push output](images/08-docker-push.png)

## 14. Troubleshooting

### Dockerfile not found

Ensure the file is named `Dockerfile` without an extension and the terminal is in the correct folder.

### Docker build fails

Check the Dockerfile syntax and confirm that `Test.java` exists in the same folder.

### Container name already exists

Remove the old container or use another name:

```bash
docker rm mycontainer
```

### Docker Hub push fails

Check your internet connection, verify your Docker Hub login, and confirm the image tag uses the correct username and repository name.

## 15. Project Structure

```text
Week-07/
├── README.md
├── experiment-record.pdf
└── Java-Docker/
    ├── Test.java
    └── Dockerfile
```

## 16. Result

A Java application was containerized using Docker, executed inside a container, and the image was prepared for publishing to Docker Hub.