# Week 9: Automate the Running of a Containerized Application

## 1. Aim

To automate the deployment and running of a containerized Java application using Docker and Kubernetes.

## 2. Theory

Kubernetes is an open-source platform used to manage containerized applications. It automates application deployment, scaling, and management.

Docker packages an application and its dependencies into a container image. Kubernetes uses that image to run and manage application containers.

## 3. Prerequisites

- Docker installed and running.
- A running Kubernetes cluster.
- `kubectl` command-line tool installed.
- Docker Hub account.
- Java application source code.

## 4. Kubernetes Architecture

Kubernetes follows a client-server architecture consisting of a control plane and worker nodes.

### Control Plane Components

1. **Kube-API Server:** Receives and processes Kubernetes requests.
2. **Kube-Scheduler:** Selects suitable nodes for Pods.
3. **Kube-Controller-Manager:** Maintains the desired state of the cluster.
4. **etcd:** Stores Kubernetes cluster data.

### Node Components

1. **Container Runtime:** Runs containers.
2. **kubelet:** Ensures containers are running as specified.
3. **kube-proxy:** Supports network communication for Services.

A Pod is the smallest deployable unit in Kubernetes and contains one or more containers.

## 5. Procedure

### Step 1: Create the Java Application

Create a file named `Test.java`.

```java
import java.io.IOException;
import java.net.InetSocketAddress;
import com.sun.net.httpserver.HttpServer;

public class Test {
    public static void main(String[] args) throws IOException {
        int port = 8080;

        System.out.println("Starting server on port " + port);

        HttpServer server = HttpServer.create(
            new InetSocketAddress(port), 0
        );

        server.createContext("/", exchange -> {
            String response = "Hello, Kubernetes!";
            exchange.sendResponseHeaders(
                200, response.getBytes().length
            );
            exchange.getResponseBody().write(response.getBytes());
            exchange.close();
        });

        server.setExecutor(null);
        server.start();

        System.out.println(
            "Server is running at http://localhost:" + port
        );
    }
}
```

**Explanation:** The Java program creates an HTTP server on port `8080`. When a request arrives, it responds with `Hello, Kubernetes!`.

### Step 2: Create the Dockerfile

Create a file named `Dockerfile` in the same directory.

```dockerfile
FROM openjdk:17-alpine

WORKDIR /app

COPY . /app

RUN javac Test.java

EXPOSE 8080

CMD ["java", "Test"]
```

**Explanation:**

- `FROM` selects the Java base image.
- `WORKDIR` sets the working directory.
- `COPY` copies the application files.
- `RUN` compiles the Java program.
- `EXPOSE` documents the application's port.
- `CMD` starts the Java application.

### Step 3: Build the Docker Image

Open a terminal in the project directory and run:

```bash
docker build -t my-java-app .
```

**Explanation:** This command builds a Docker image named `my-java-app` using the Dockerfile.

### Step 4: Log In to Docker Hub

```bash
docker login
```

**Explanation:** This authenticates your Docker client with Docker Hub so you can upload the image.

### Step 5: Tag and Push the Image

Replace `YOUR-DOCKERHUB-USERNAME` with your Docker Hub username.

```bash
docker tag my-java-app:latest YOUR-DOCKERHUB-USERNAME/my-java-app:latest
```

**Explanation:** The tag identifies the image under your Docker Hub account.

Push the image:

```bash
docker push YOUR-DOCKERHUB-USERNAME/my-java-app:latest
```

**Explanation:** This uploads the image to Docker Hub so Kubernetes can pull it.

### Step 6: Create the Kubernetes Deployment

Create a file named `deployment.yaml`.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-java-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-java-app
  template:
    metadata:
      labels:
        app: my-java-app
    spec:
      containers:
        - name: my-java-app
          image: YOUR-DOCKERHUB-USERNAME/my-java-app:latest
          ports:
            - containerPort: 8080
          env:
            - name: PORT
              value: "8080"
```

**Explanation:** The Deployment instructs Kubernetes to run three replicas of the application. Replace the image username with your own Docker Hub username.

Apply the Deployment:

```bash
kubectl apply -f deployment.yaml
```

**Explanation:** This creates or updates the Deployment in the Kubernetes cluster.

### Step 7: Create the Kubernetes Service

Create a file named `service.yaml`.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-java-app-service
spec:
  selector:
    app: my-java-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
      nodePort: 30007
  type: NodePort
```

**Explanation:** The Service routes network traffic to the application Pods. The NodePort exposes the application on port `30007`.

Apply the Service:

```bash
kubectl apply -f service.yaml
```

### Step 8: Verify the Deployment

Check the Deployment:

```bash
kubectl get deployments
```

Check the Pods:

```bash
kubectl get pods
```

Check the Service:

```bash
kubectl get svc
```

**Explanation:** These commands display the Deployment status, running Pods, and Service configuration. Wait for the Pods to become ready before testing the application.

### Step 9: Access the Application

Open the following URL in your browser:

```text
http://localhost:30007
```

**Expected output:**

```text
Hello, Kubernetes!
```

**Explanation:** The request reaches the Kubernetes Service, which forwards it to the Java application running inside a Pod.

If the application does not open, verify that Kubernetes is running, all Pods are ready, and the Service has been created correctly.

## 6. Result

The Java application was containerized using Docker, uploaded to Docker Hub, deployed with three replicas using Kubernetes, and exposed through a NodePort Service.