# finaldev
Itzik Eliyahu
Final DevOps Project Containerized GitOps Application
Welcome to my final DevOps project. This project demonstrates a complete CI/CD pipeline using a GitOps approach. The application is containerized, managed by Helm, and deployed automatically to a Kubernetes cluster using ArgoCD.
Project Overview
CI/CD Jenkins automates the build and push process.
GitOps ArgoCD ensures the cluster state matches the Git repository.
Deployment Argo Rollouts for advanced deployment strategies like Canary or Blue-Green.
Scaling Horizontal Pod Autoscaler HPA manages load dynamically.
Architecture
Instructions for the Instructor
Prerequisites
To review this project, ensure you have access to a Kubernetes cluster, kubectl configured, and ArgoCD and Argo Rollouts installed on the cluster.
Getting the Files
The source code and infrastructure configuration are stored in this repository:
git clone https://github.com/eliyahui1971-il/finaldev.git
cd finaldev
Deployment Steps
The project uses GitOps, so the deployment is handled automatically by ArgoCD.
1 Configure ArgoCD Apply the application manifest to sync the repository with your cluster:
kubectl apply -f application.yaml
2 Verify Deployment Check that the ArgoCD application status is Synced and Healthy:
kubectl get rollouts -n default
kubectl get hpa -n default
3 Check Service Access the application via the Service node port:
kubectl get svc -n default
Project Structure
/helm Contains the Helm Chart templates for Rollout, Service, and HPA.
/helm/values.yaml Configuration file for replicas, images, and autoscaling.
application.yaml The ArgoCD Application manifest.
Jenkinsfile The automation pipeline logic.
Key Features Implemented
Automated Scaling HPA is configured to scale based on CPU utilization.
Advanced Rollouts Using Argo Rollouts for safer deployments.
Self-Healing ArgoCD automatically reverts manual changes in the cluster to match the Git state.
Also adding Docker hub: https://hub.docker.com/r/ieliyahu1971/final-app
This project taught me how important it is to maintain correct parameters and precise naming, including case sensitivity. The frustration of failing due to such small mistakes is immense.





