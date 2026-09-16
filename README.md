Django Todo App – DevOps CI/CD Project

A containerized Django Todo application deployed using Jenkins CI/CD, Docker, Kubernetes, Prometheus, Grafana, Node Exporter, and Coroot.

The project uses a GitHub repository as the source code repository and demonstrates a complete DevOps workflow from source code management to application deployment and monitoring.


🚀 Project Overview

This project demonstrates the following DevOps activities:

Maintain application source code in GitHub
Build Docker images using Jenkins CI/CD
Push Docker images to Docker Hub
Run the application using Docker
Deploy the application on Kubernetes
Monitor the server/node using Prometheus and Node Exporter
Visualize monitoring data using Grafana
Monitor the application and infrastructure using Coroot

Solution: 
Job-01: 
Step-01: Prepare the GitHub Repository. Forked from MdRasel0/django-todo-appt GitHub link and Repository name is “django-todo-appt” Ensure the repo contains:

-   Application code

-   requirements.txt

-   Dockerfile

-   Jenkinsfile

Step-02: Prepare Jenkins Server Add Jenkins user to Docker group $ sudo usermod -aG docker jenkins $ sudo systemctl restart jenkins

Step-03: You need to generate your Python dependencies file so Docker can install them.

$ git clone https://github.com/nawshad298/django-todo-appt.git $ cd django-todo-appt

Create a Python virtual environment-- $ python3 -m venv venv $ source venv/bin/activate $ pip install django $ pip freeze > requirements.txt

$ git add requirements.txt $ git commit -m "Add requirements.txt" $ git push

Step-03: Create Jenkins Pipeline Job

Notes: 1. Update Dockerfile. 2. Add requirements.txt for Docker build. The repo does NOT contain a requirements.txt file at the root.

Job-02: $ docker build -t django-todo-app .

Job-03:

$ sudo nano django-todo-appt.yml

$ kubectl create -f django-todo-appt.yml 
$ kubectl get deployments.app todo-deployment
 $ kubectl get svc


Job-04: Grafana:

$ sudo mkdir monitoring $ cd monitoring $ sudo mkdir Prometheus $ cd Prometheus $ sudo nano prometheus.yml

$ cd .. $ sudo nano docker-compose.yml

$ sudo docker compose up –d $ sudo docker ps –a

Checking --- 172.16.208.30:3000

Node-exporter: Node-exporter Data server হতে collect করে prometheus পর্যন্ত দিবে। আর, Prometheus grafana তে vizualization দিবে।

Installation Node-exporter:

$ sudo docker run -d \

--name node-exporter \

--restart always \

-p 9100:9100 \

--net="host" \

quay.io/prometheus/node-exporter:latest

Prometheus:

Create the monitoring directory:

sudo mkdir monitoring
cd monitoring

Create the Prometheus directory:

sudo mkdir Prometheus
cd Prometheus

Create the Prometheus configuration:

sudo nano prometheus.yml

Prometheus collects metrics from monitored targets.

Prometheus URL:

http://172.16.208.30:9090

The documented environment uses port 9090 for Prometheus.

Prometheus collects the metrics, and Grafana provides visualization of those metrics.

Checking --- 172.16.208.30:9090

Add Another Server to Monitoring

To monitor another server:

Install Node Exporter on the server.
Configure the server as a Prometheus target.
Reload/restart Prometheus.
Verify the target in Prometheus.
Create or update the Grafana dashboard.

Install Node Exporter using:

sudo docker run -d \
  --name node-exporter \
  --restart always \
  -p 9100:9100 \
  --net="host" \
  quay.io/prometheus/node-exporter:latest

The project instructions state that Node Exporter should be installed on an additional server using the previous command.


Coroot:

Coroot is included in the monitoring architecture for application and infrastructure observability.

The project documentation specifies Coroot as part of the monitoring solution.






