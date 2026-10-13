# Week 6: Basic Docker Commands for Content Management

## Aim
To learn how to install Docker and use basic Docker commands to manage images and containers.

## Requirements
- Windows 10/11 compatible with Docker Desktop requirements
- Internet connection
- Administrator access if required
- PowerShell or Command Prompt
- GitHub account for submitting the lab work

## 1. Download Docker Desktop

Download Docker Desktop for Windows from the official website:

https://docs.docker.com/desktop/setup/install/windows-install/

### Procedure
1. Open the official download page.
2. Download the Docker Desktop installer for Windows.
3. Check that hardware virtualization is enabled and your system meets Docker's requirements.
4. Run the downloaded installer.
5. Follow the installation wizard and use the WSL 2 backend if supported.
6. Restart your computer if prompted.
7. Open Docker Desktop from the Windows Start menu.
8. Wait until the Docker Engine is running.

If WSL installation or updating is required, open PowerShell as Administrator and execute:

```powershell
wsl --install
wsl --update
```

Restart if prompted and reopen Docker Desktop.

### Output screenshot

Save a screenshot of Docker Desktop showing that it has started:

`images/01-docker-desktop.png`

![Docker Desktop running](images/01-docker-desktop.png)

## 2. Verify Docker Installation

Open PowerShell or Command Prompt and execute:

```bash
docker --version
```

### Expected output

The terminal displays the installed Docker version.

Check the Docker Engine:

```bash
docker info
```

### Expected output

Docker displays information about the client, server, containers, images, and system configuration.

### Output screenshot

`images/02-docker-version.png`

![Docker version output](images/02-docker-version.png)

## 3. Download a Docker Image

Execute:

```bash
docker pull hello-world
```

### Expected output

Docker downloads the `hello-world` image from Docker Hub or reports that it is already available locally.

### Output screenshot

`images/03-docker-pull.png`

![Docker pull output](images/03-docker-pull.png)

## 4. Run a Docker Container

Execute:

```bash
docker run hello-world
```

### Expected output

The terminal displays a message beginning with:

```text
Hello from Docker!
```

This confirms that Docker successfully ran the test container.

### Output screenshot

`images/04-docker-run.png`

![Docker run output](images/04-docker-run.png)

## 5. List Containers

List currently running containers:

```bash
docker ps
```

List all containers, including stopped containers:

```bash
docker ps -a
```

### Expected output

The second command should show the Hello World container, usually with an exited status.

### Output screenshot

`images/05-docker-containers.png`

![Docker container list](images/05-docker-containers.png)

## 6. Search for Docker Images

Execute:

```bash
docker search hello-world
```

### Expected output

Docker displays matching images from Docker Hub.

### Output screenshot

`images/06-docker-search.png`

![Docker search output](images/06-docker-search.png)

## 7. List Local Images

Execute:

```bash
docker images
```

### Expected output

The downloaded `hello-world` image appears in the list.

### Output screenshot

`images/07-docker-images.png`

![Docker images output](images/07-docker-images.png)

## 8. Create a Named Container

Execute:

```bash
docker run --name week6-test hello-world
```

Check the container:

```bash
docker ps -a
```

### Expected output

The container named `week6-test` appears in the container list. It will usually be stopped after printing the Hello World message.

### Output screenshot

`images/08-named-container.png`

![Named Docker container](images/08-named-container.png)

## 9. Run a Container in the Background

Execute:

```bash
docker run -d --name week6-nginx -p 8080:80 nginx
```

Check the running container:

```bash
docker ps
```

Open the following address in your browser:

http://localhost:8080

### Expected output

The Nginx welcome page appears in the browser.

### Output screenshot

`images/09-nginx-browser.png`

![Nginx welcome page](images/09-nginx-browser.png)

## 10. Stop and Start a Container

Stop the container:

```bash
docker stop week6-nginx
```

Start it again:

```bash
docker start week6-nginx
```

Verify:

```bash
docker ps
```

### Expected output

The container appears as running after it has been started.

### Output screenshot

`images/10-start-stop.png`

![Docker start and stop commands](images/10-start-stop.png)

## 11. Restart a Container

Execute:

```bash
docker restart week6-nginx
```

Verify the container:

```bash
docker ps
```

### Expected output

Docker restarts the container successfully.

### Output screenshot

`images/11-restart-container.png`

![Docker restart output](images/11-restart-container.png)

## 12. Kill a Running Container

Execute:

```bash
docker kill week6-nginx
```

Verify:

```bash
docker ps -a
```

### Expected output

The container appears stopped or exited.

### Output screenshot

`images/12-kill-container.png`

![Docker kill output](images/12-kill-container.png)

## 13. Build an Image from a Dockerfile

Create a folder named `docker-demo`.

Inside the folder, create a file named `Dockerfile` with this content:

```dockerfile
FROM alpine:latest
CMD ["echo", "Hello from my Docker image"]
```

Open a terminal in the `docker-demo` folder and execute:

```bash
docker build -t week6-demo .
```

Run the image:

```bash
docker run --name week6-demo-container week6-demo
```

### Expected output

```text
Hello from my Docker image
```

### Output screenshot

`images/13-docker-build.png`

![Docker image build and run output](images/13-docker-build.png)

## 14. Log In to Docker Hub

Execute:

```bash
docker login
```

Follow the authentication instructions.

### Expected output

Docker confirms successful login.

**Security:** Never include your password, access token, or other credentials in screenshots.

### Output screenshot

`images/14-docker-login.png`

![Docker login output](images/14-docker-login.png)

## 15. Tag and Push an Image to Docker Hub

Replace `YOUR-DOCKERHUB-USERNAME` with your actual Docker Hub username.

Tag the image:

```bash
docker tag week6-demo YOUR-DOCKERHUB-USERNAME/week6-demo:latest
```

Push it:

```bash
docker push YOUR-DOCKERHUB-USERNAME/week6-demo:latest
```

### Expected output

Docker uploads the image to your Docker Hub repository.

### Output screenshot

`images/15-docker-push.png`

![Docker push output](images/15-docker-push.png)

## 16. Remove a Container

Remove the stopped test container:

```bash
docker rm week6-test
```

Remove the stopped demo container:

```bash
docker rm week6-demo-container
```

### Expected output

Docker returns the names or IDs of the removed containers.

### Output screenshot

`images/16-remove-container.png`

![Docker remove container output](images/16-remove-container.png)

## 17. Remove a Docker Image

Remove the local Hello World image:

```bash
docker rmi hello-world
```

If the image is still referenced by a container, remove that container first.

### Expected output

Docker confirms that the image was removed.

### Output screenshot

`images/17-remove-image.png`

![Docker image removal output](images/17-remove-image.png)

## 18. Final Folder Structure

Organize your Week 6 folder as follows:

```text
Week-06/
├── README.md
├── experiment-record.pdf
├── docker-demo/
│   └── Dockerfile
└── images/
    ├── 01-docker-desktop.png
    ├── 02-docker-version.png
    ├── 03-docker-pull.png
    ├── 04-docker-run.png
    ├── 05-docker-containers.png
    ├── 06-docker-search.png
    ├── 07-docker-images.png
    ├── 08-named-container.png
    ├── 09-nginx-browser.png
    ├── 10-start-stop.png
    ├── 11-restart-container.png
    ├── 12-kill-container.png
    ├── 13-docker-build.png
    ├── 14-docker-login.png
    ├── 15-docker-push.png
    ├── 16-remove-container.png
    └── 17-remove-image.png
```

## Result

Docker Desktop was installed and verified. Docker images were downloaded, containers were created and managed, a custom image was built, and image publishing to Docker Hub was demonstrated.

**Note:** Capture each screenshot while performing the corresponding step and save it using the specified filename. The image links will display your screenshots on GitHub once the image files have been added.