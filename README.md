# Trivy

Trivy is an open-source vulnerability scanner tool specifically designed for container images and Docker. It helps identify security vulnerabilities in the dependencies and packages included in container images. Trivy scans container images and provides detailed reports on any known vulnerabilities, including CVE (Common Vulnerabilities and Exposures) identifiers.

What Trivy can scan:
```
- Container Image
- File System
- Git Repo (Remote)
- Virtual Machine Image
- Kubernetes
- AWS
```
What Trivy can find:
```
- OS Packages and software dependencies in user
- Known vulnerabilities 
- IaC issues and misconfigurations
- Sensitive Information and secrets
- Software licenses
```

---
# Working with Trivy

1. Update Repo and Install Docker:
```
sudo apt-get update -y

sudo apt-get install docker.io

sudo usermod -aG docker $USER
```
```
sudo reboot
```
`Reboot is required to make Ubuntu user execute the Docker commands`

2. Install Trivy:
```
sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy
```

3. Check Trivy Version:
```
trivy -v
```

4. Pull any docker image
```
docker pull nginx
```

5. Now run Trivy scan on Nginx image
```
trivy image nginx
```

6. To filter a severity
```
trivy image --severity HIGH,CRITICAL nginx
```

7. Clone a repo:
```
git clone https://github.com/jacob-bd/kubeturbo-sample-yamls.git
```

8. Now run Trivyscan on a folder(cloned)
```
trivy fs --security-checks vuln,config kubeturbo-sample-yamls
```

9. Download a local copy of the report in JSON format for Nginx image

trivy image -f json -o results.json nginx


10. To scan a K8s cluster

trivy k8s --report summary cluster
