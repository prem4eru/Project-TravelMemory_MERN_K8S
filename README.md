# TravelMemory MERN Kubernetes Deployment

## Problem Statements

TravelMemory is a full-stack MERN application designed to help users document and share their travel experiences. The primary challenges addressed by this project include:

1. *Scalability*: The need to deploy a scalable application that can handle increasing user traffic.
2. *Deployment*: Implementing a Kubernetes-based deployment for managing microservices and ensuring the reliability of the application.
3. *Data Management*: Managing a robust MongoDB database in a distributed environment.
4. *Continuous Integration/Continuous Deployment (CI/CD)*: Facilitating automated deployment and updates to the application.

## Objectives

The objectives of this project include:

1. *Containerization*: Dockerizing the frontend and backend services for consistent and reliable deployments.
2. *Kubernetes Deployment*: Setting up a Kubernetes cluster to manage and scale the microservices.
3. *Database Integration*: Deploying MongoDB within the Kubernetes cluster and integrating it with the application.
4. *High Availability*: Ensuring that the application is resilient and can handle failures effectively.
5. *Documentation*: Providing comprehensive documentation for deploying and managing the application.

## Configuration

### Prerequisites

Before you begin, make sure you have the following installed:

- *Docker*: For creating and managing container images.
- *Kubernetes (kubectl)*: For managing Kubernetes clusters.
- *Minikube*: For running a local Kubernetes cluster (optional if deploying on a cloud provider).
- *Helm*: For managing Kubernetes packages.
- *Node.js and npm*: Required for running and building the Node.js application.
- *MongoDB*: For local database testing (optional).

### Steps

1. *Clone the Repository*:

    bash
    git clone https://github.com/prem4eru/TravelMemory_MERN_K8S.git
    cd TravelMemory_MERN_K8S
    

2. *Build Docker Images*:

    Navigate to each microservice directory and build Docker images.

    bash
    cd frontend
    docker build -t <your-dockerhub-username>/travelmemory-frontend .
    docker push <your-dockerhub-username>/travelmemory-frontend
    

    Repeat for the backend and other services.

3. *Set Up Kubernetes Cluster*:

    - *Minikube*: Start a local cluster with minikube start.
    - *Cloud Provider*: Set up a Kubernetes cluster using a cloud provider.

4. *Deploy MongoDB*:

    Create a Kubernetes secret for MongoDB credentials and deploy MongoDB using Helm.

    bash
    kubectl create secret generic mongodb-secret --from-literal=mongo-root-username=<username> --from-literal=mongo-root-password=<password>
    helm install mongodb bitnami/mongodb --set auth.rootPassword=<password>,auth.username=<username>,auth.password=<password>,auth.database=travelmemory
    

5. *Deploy the Application*:

    Apply the Kubernetes YAML files located in the k8s directory.

    bash
    kubectl apply -f k8s/mongodb-deployment.yaml
    kubectl apply -f k8s/backend-deployment.yaml
    kubectl apply -f k8s/frontend-deployment.yaml
    

6. *Access the Application*:

    - *Minikube*: Use minikube service travelmemory-frontend-service.
    - *Cloud Provider*: Get the external IP using kubectl get svc travelmemory-frontend-service.

7. *Monitoring and Logging*:

    Use kubectl logs <pod-name> to check logs and minikube dashboard for the Kubernetes Dashboard.

8. *Cleanup*:

    Remove Kubernetes resources with:

    bash
    kubectl delete -f k8s/
    

    Stop Minikube:

    bash
    minikube stop
    

## Reference

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Helm Charts](https://helm.sh/docs/)
- [MongoDB Kubernetes Operator](https://www.mongodb.com/docs/kubernetes-operator/)

## Contribution

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch (git checkout -b feature-branch).
3. Make your changes and commit them (git commit -m 'Add some feature').
4. Push to the branch (git push origin feature-branch).
5. Open a Pull Request.

For major changes, please open an issue first to discuss what you would like to change.

---

This README provides all necessary information for deploying and contributing to the TravelMemory MERN Kubernetes project. Happy coding!
