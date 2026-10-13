# Week 8: Integrate Kubernetes with Docker

## 1. Aim

To enable Kubernetes on Docker Desktop and prepare the system to run Kubernetes commands.

## 2. Requirements

- Windows computer
- Docker Desktop
- Internet connection
- Command Prompt or PowerShell
- `kubectl` command-line tool

## 3. Introduction

Kubernetes, also known as K8s, is an open-source system for automating the deployment, scaling, and management of containerized applications.

### Benefits of Kubernetes

- **Container orchestration:** Manages the placement and scheduling of containers.
- **Scalability:** Supports scaling applications based on requirements.
- **Self-healing:** Can restart or replace failed containers to maintain the desired state.
- **Rolling updates and rollbacks:** Supports application updates and reverting changes.
- **Storage orchestration:** Manages persistent storage for applications.

### Difference Between Docker and Kubernetes

Docker is used to build, ship, and run containers. Kubernetes is used to orchestrate and manage containerized applications, particularly across clusters.

## 4. Start Docker Desktop

1. Open Docker Desktop from the Windows Start menu.
2. Wait until Docker Desktop has started.
3. Confirm that the Docker Engine is running.

### Output

Docker Desktop should open successfully and show that the engine is running.

![Docker Desktop running](images/01-docker-desktop.png)

## 5. Enable Kubernetes in Docker Desktop

1. Open the Docker Desktop dashboard.
2. Click **Settings**.
3. Select **Kubernetes** in the left sidebar.
4. Enable **Kubernetes**.
5. Click **Apply & restart**.
6. If prompted, click **Install** to confirm the required Kubernetes components.
7. Wait for Kubernetes to finish starting.

The first startup may take several minutes.

### Output

Docker Desktop should indicate that Kubernetes is enabled and running.

![Kubernetes enabled in Docker Desktop](images/02-enable-kubernetes.png)

## 6. Install kubectl

`kubectl` is the command-line tool used to communicate with a Kubernetes cluster.

Follow the official Windows installation instructions:

https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

Download the appropriate Windows executable using the official instructions. The executable is normally named `kubectl.exe`.

Place it in a folder included in your Windows `PATH`, or add the folder containing the executable to the `PATH` environment variable.

**Note:** The lab PDF mentions `kubectlconvert.exe`; the standard Kubernetes command-line executable is `kubectl.exe`. Use the official installation instructions to install the correct tool.

### Output

After installation, the executable should be accessible from Command Prompt or PowerShell.

![kubectl installation](images/03-kubectl-installation.png)

## 7. Verify kubectl Installation

Open a new Command Prompt or PowerShell window and execute:

```bash
kubectl version --client
```

### Expected output

The terminal displays the installed `kubectl` client version.

![kubectl client version](images/04-kubectl-version.png)

## 8. Verify the Kubernetes Cluster

Execute:

```bash
kubectl get nodes
```

### Expected output

If Kubernetes is enabled and running correctly, the command lists the local cluster node and its status. The status should normally be `Ready`.

Example format:

```text
NAME             STATUS   ROLES           AGE   VERSION
docker-desktop   Ready    control-plane   ...   ...
```

The exact node name, age, and version may differ.

![Kubernetes nodes output](images/05-kubectl-nodes.png)

## 9. List Kubernetes Pods

Execute:

```bash
kubectl get pods
```

This command lists pods in the current namespace. If no pods exist in that namespace, the output may show that no resources were found.

To list pods across all namespaces, execute:

```bash
kubectl get pods --all-namespaces
```

### Expected output

The command displays available pods and their statuses. Some system pods may take time to start.

![Kubernetes pods output](images/06-kubectl-pods.png)

## 10. Troubleshooting

### Docker Desktop is not running

Open Docker Desktop and wait until the Docker Engine has started.

### Kubernetes is still starting

Wait a few minutes and check the Kubernetes status again.

### `kubectl` is not recognized

Check that `kubectl.exe` is installed and its folder is included in the Windows `PATH`. Open a new terminal after changing environment variables.

### Connection to the cluster fails

Make sure Kubernetes is enabled in Docker Desktop and has finished starting. Then retry:

```bash
kubectl get nodes
```

## 11. Project Structure

```text
Week-08/
├── README.md
├── experiment-record.pdf
└── images/
    ├── 01-docker-desktop.png
    ├── 02-enable-kubernetes.png
    ├── 03-kubectl-installation.png
    ├── 04-kubectl-version.png
    ├── 05-kubectl-nodes.png
    └── 06-kubectl-pods.png
```

## 12. Result

Kubernetes was enabled in Docker Desktop, `kubectl` was installed and verified, and Kubernetes commands were used to inspect the cluster and its pods.