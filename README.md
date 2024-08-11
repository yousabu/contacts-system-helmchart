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

- api endpoint:
  
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

  ![ang](https://github.com/user-attachments/assets/9db261ea-2e51-4893-83d5-303ab12ded61)


* Runnig Resources:
![front](https://github.com/user-attachments/assets/c2da7540-105b-4b3e-972e-5321e45ad7aa)

  

## 5) Backend Helm Deployment
* As per image bellow:
  
![express](https://github.com/user-attachments/assets/c3b84e3f-704f-4221-8aef-8e7b1085557b)

* Runnig Resources:

![Screenshot from 2024-08-11 18-33-33](https://github.com/user-attachments/assets/133a499f-1936-46da-87da-f455001411a5)


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

## Security Note
 * The best practice for managing secrets is to use a mechanism like Sealed Secrets, which encrypts secret files so that only the cluster can decrypt them. However, I did not implement this here because it requires Sealed Secrets Manager, and I had limited resources to set it up.

