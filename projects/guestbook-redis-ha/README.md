# PHP Guestbook with Redis HA Backend
This is a simple PHP guestbook application with a redis backend. All parts of the application are deployed using Helm charts.

<br>

## Getting Started
### 0. Replace Docker Image
Skip this step if you are using Minikube or Docker Desktop Kubernetes.

If you are **not** using Minikube or Docker Desktop Kubernetes, you need to replace:
```
your-docker-username
```
with with your actual Docker Hub username in the following two files:
- `devspace.yaml` (line 4)
- `src/manifests/frontend/deployment.yaml` (line 22)

### 1. Install DevSpace
<details>
<summary>via NPM (recommended for Windows)</summary>

```
npm install -g devspace
```

</details>

<details>
<summary>via Mac Terminal</summary>

```
curl -s -L "https://github.com/devspace-cloud/devspace/releases/latest" | sed -nE 's!.*"([^"]*devspace-darwin-amd64)".*!https://github.com\1!p' | xargs -n 1 curl -L -o devspace && chmod +x devspace;
sudo mv devspace /usr/local/bin;
```

</details>

<details>
<summary>via Linux Bash</summary>

```
curl -s -L "https://github.com/devspace-cloud/devspace/releases/latest" | sed -nE 's!.*"([^"]*devspace-linux-amd64)".*!https://github.com\1!p' | xargs -n 1 curl -L -o devspace && chmod +x devspace;
sudo mv devspace /usr/local/bin;
```

</details>

<details>
<summary>via Windows Powershell</summary>

```
md -Force "$Env:APPDATA\devspace"; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]'Tls,Tls11,Tls12';
wget -UseBasicParsing ((Invoke-WebRequest -URI "https://github.com/devspace-cloud/devspace/releases/latest" -UseBasicParsing).Content -replace "(?ms).*`"([^`"]*devspace-windows-amd64.exe)`".*","https://github.com/`$1") -o $Env:APPDATA\devspace\devspace.exe; & "$Env:APPDATA\devspace\devspace.exe" "install"; $env:Path = (Get-ItemProperty -Path HKCU:\Environment -Name Path).Path
```

</details>

### 2. Choose a Kubernetes Cluster
If you already have a cluster and your kube-context is setup correctly, just run:
```bash
devspace use namespace [NAMESPACE] # will be created automatically if not existing
```
Alternative Option: To get a free Kubernetes namespace in DevSpace Cloud, run:
```bash
devspace create space [SOME_NAME]
```

### 3. Deploy
```bash
devspace deploy
```
See how your pods are starting and wait until everything has `STATUS = Running`:
```bash
kubectl get pod -w
```

### 4. Open via Browser
```bash
devspace open
```

Choose the first option `via localhost` when DevSpace asks:
```bash
? How do you want to open your application?
  [Use arrows to move, space to select, type to filter]
> via localhost (provides private access only on your computer via port-forwarding) # <<<<<<<< THIS ONE
  via domain (makes your application publicly available via ingress) ! an ingress controller must be installed in your cluster
```

Choose `guestbook-frontend:80` when DevSpace asks:
```bash
? Please specify the service you want to make available on 'localhost:'
  [Use arrows to move, space to select, type to filter]
> guestbook-frontend:80 # <<<<<<<< THIS ONE
  guestbook-redis-master:0
  guestbook-redis-slave:0
```

### 5. Develop
```bash
devspace dev
```
Wait until the browser open and then change a file, e.g. `src/index.html`, and reload your application in the browser.

<br>

## Reset Variable DOCKER_USERNAME
```bash
devspace reset vars
```

<br>

## Cleanup
### Remove Charts & Keep Namespace and Tiller
```bash
devspace purge
```

### Delete Everything (including namespace)
```bash
kubectl delete namespace [NAMESPACE]
```

<br>

## FAQ
### Why don't I see my image in Docker Hub when using Minikube or Docker Desktop?
Because DevSpace skips the image push step because the Kubernetes Docker daemon is the same as the Docker daemon used to build and tag the image, so pushing is not required and speeds things up.

### Can I use a different Docker registry other than Docker Hub?
**Yes**. Just replace `your-docker-username` with the full registry URL. See [0. Replace Docker Image](#0-replace-docker-image).
