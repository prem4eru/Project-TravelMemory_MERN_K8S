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

1. *Start Minikube*:

    bash
    minikube start
    

2. *Switch Context to Minikube*:

    bash
    kubectl config use-context minikube
    

3. *Apply Namespace Configuration*:

    bash
    kubectl apply -f db-namespace.yml
    

4. *Set Up Persistent Volumes*:

    bash
    kubectl apply -f pv.yml
    kubectl apply -f pvc.yml
    

5. *Deploy MongoDB*:

    bash
    kubectl apply -f db-deployment.yml
    kubectl apply -f db-service.yml
    

6. *Verify the Setup*:

    Check that the pods are running correctly:

    bash
    kubectl get pods -n database
    

    Check the services:

    bash
    kubectl get svc -n database
    

7. *Test DNS Resolution*:

    bash
    kubectl run -i --tty --rm debug --image=busybox --restart=Never -- sh
    nslookup mongodb-service.database.svc.cluster.local
    exit
    

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
