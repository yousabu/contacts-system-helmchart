# Agenda:
- Application Overview
- Docker compose and Dev ENV
- Helm Overview.
- Frontend Helm Deployment
- Backend Helm Deployment
- Infrastructure Configurations
- Pipeline and Repository URLs
- Monitoring and Observability

## 1) Application Overview
Contacts application for managing contacts, where contacts are stored in a MongoDB database. You can delete, update, and add new contacts.

- App URL: https://intouch.cloud-stacks.com/

- home page:
![Screenshot from 2024-08-11 17-35-42](https://github.com/user-attachments/assets/2ba30062-b5a2-4e52-a7ad-deaa31f5b8ae)

- contacts page:
![Screenshot from 2024-08-11 17-36-15](https://github.com/user-attachments/assets/87affc94-5684-46b8-8014-3dc2d1298dab)

- api endpoint
![Screenshot from 2024-08-11 17-36-32](https://github.com/user-attachments/assets/40df9df2-57c5-4508-8189-42b7487368ad)


## 2) Docker compose and Dev ENV
* For Backend check ReadMe File in this repo:  https://github.com/yousabu/contacts-system-backend.git
* For Frontend check ReadMe File in this repo: https://github.com/yousabu/contacts-system-frontend.git

## 3) Helm Overview.
* I have created a Helm template that can be used for both frontend and backend deployments. By using the values.yaml file located in each repository (frontend/backend), the deployment logic will be determined.
 
 Backend values.yaml : https://github.com/yousabu/contacts-system-backend/blob/main/values.yaml
 
 Frontend values.yaml: https://github.com/yousabu/contacts-system-frontend/blob/main/values.yaml

 ``` File Tree
 Helm Values Configuration
├── replicaCount
│
├── backend/frontend
│
├── namespace
│
├── image
│   ├── repository
│   ├── tag
│   └── pullPolicy
│
├── service
│   ├── type
│   ├── port
│   └── nodeport
│
├── autoscaling
│   ├── enabled
│   ├── minReplicas
│   ├── maxReplicas
│   └── targetCPUUtilizationPercentage
│
├── env vars
```
## 4) Frontend Helm Deployment
* As per image bellow: 

* Runnig Resources:

## 5) Backend Helm Deployment
* As per image bellow: 
![Screenshot from 2024-08-11 16-41-22](https://github.com/user-attachments/assets/e756e25e-65de-4955-b0c7-9f92f95f5f0f)

* Runnig Resources:

![Screenshot from 2024-08-11 18-09-29](https://github.com/user-attachments/assets/917d34bc-df0b-44df-9b0c-2e413fa877f8)

## 6) Infrastructure Configurations

*  Cluster: I used MicroK8s installed on an EC2 instance on AWS to create a lightweight cluster and enabled public access to it. I then generated a configuration file (config) for future use.

* Service Connection: I set up the connection between Azure DevOps and the cluster using the configuration file.

* Connections: The cluster contains an internal ingress to route traffic between the frontend and backend.

* Ingress: I set up an Ingress for the domain (https://intouch.cloud-stacks.com/) and requested a certificate for it using Cert Manager, issued by Let's Encrypt.
* Horizontal Pod Autoscaler (HPA): Configured to automatically scale the number of pod replicas up or down based on observed CPU utilization or other selected metrics. This ensures that the application can handle varying loads efficiently

## 7) Pipeline and Repository URLs

We have two pipelines, each in its own repository, to build, push, and deploy the application using Helm:

* HelmChart Repository: https://github.com/yousabu/contacts-system-helmchart.git
-----------
* Pipeline For Backend & Frontend on azure:  https://dev.azure.com/abuhamda/retail-media-org/_build
-----------
* Backend GitHub Repository: https://github.com/yousabu/contacts-system-backend.git
* Frontend GitHub Repository: https://github.com/yousabu/contacts-system-frontend.git



## 8) Monitoring and Observability
* Due to a lack of resources, I didn't use Prometheus and Grafana, even though they are the most popular monitoring tools. Instead, I used a New Relic free trial as a lightweight monitoring tool.

Dashboard:

![Screenshot from 2024-08-11 18-14-54](https://github.com/user-attachments/assets/b4ee7dec-9652-446b-b7a2-0b8255c9ea02)

![Screenshot from 2024-08-11 18-17-26](https://github.com/user-attachments/assets/f57123dd-dbe7-43f6-b858-72c02f9cb777)

Runnig Service:

![Screenshot from 2024-08-11 18-18-20](https://github.com/user-attachments/assets/045e741b-a721-4926-bee3-a7c3fd25801c)
![Screenshot from 2024-08-11 18-18-31](https://github.com/user-attachments/assets/f70f3cf9-aa27-495a-ac8b-5408c93f3553)

