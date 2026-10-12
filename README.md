# End-to-End DevSecOps CI/CD Pipeline on AWS

A YouTube Clone application deployed using an automated DevSecOps workflow with Jenkins, SonarQube, Trivy, Docker, Docker Hub, Kubernetes, Amazon EKS, Terraform, Prometheus, and Grafana.

> **Project status:** Hands-on implementation completed. The AWS lab infrastructure was terminated after testing to avoid ongoing cloud costs. Screenshots and deployment evidence should be added to document the completed implementation.

## Project Overview

This project demonstrates how DevOps and DevSecOps tools can be integrated to build, scan, package, and deploy a containerized web application.

The original application is a React-based YouTube Clone. I used it as the application layer for building a CI/CD pipeline and practicing cloud-native deployment and monitoring.

## Technology Stack

| Category                     | Tools                                              |
| ---------------------------- | -------------------------------------------------- |
| Source code management       | Git, GitHub                                        |
| Infrastructure as Code       | Terraform                                          |
| CI/CD automation             | Jenkins                                            |
| Code quality analysis        | SonarQube                                          |
| Security scanning            | Trivy                                              |
| Containerization             | Docker                                             |
| Container registry           | Docker Hub                                         |
| Cloud platform               | AWS                                                |
| Container orchestration      | Amazon EKS, Kubernetes                             |
| Application exposure         | Kubernetes LoadBalancer Service, AWS Load Balancer |
| Monitoring and visualization | Prometheus, Grafana                                |
| Supporting monitoring tools  | Alertmanager, Node Exporter, kube-state-metrics    |

## Architecture

The intended workflow is:

1. Developer updates the application source code and pushes changes to GitHub.
2. Jenkins checks out the source code and orchestrates the CI/CD pipeline.
3. SonarQube analyzes the source code and Jenkins checks the configured quality gate.
4. Trivy scans the project filesystem and the built container image for vulnerabilities.
5. Docker builds the application image and pushes it to Docker Hub.
6. Jenkins deploys the application to Amazon EKS using Kubernetes manifests.
7. Kubernetes manages two application replicas across worker nodes.
8. A Kubernetes LoadBalancer Service exposes the application through an AWS Load Balancer.
9. Prometheus collects metrics and Grafana provides monitoring dashboards.

Terraform is used for infrastructure provisioning. It is responsible for creating the AWS resources defined in the Terraform configuration, rather than building or deploying the application itself.

## CI/CD Pipeline Stages

The Jenkins pipeline implemented these stages:

- Clean workspace
- Checkout source code from GitHub
- SonarQube code analysis
- Quality Gate evaluation
- Install application dependencies
- Trivy filesystem scan
- Docker image build and push to Docker Hub
- Trivy image scan
- Deploy application to Kubernetes
- Verify Kubernetes rollout, pods, and Service
- Send build notification by email

The pipeline was successfully executed during the lab. Add screenshots of the successful build and relevant stage outputs below.

## Kubernetes Deployment

The application was deployed to Amazon EKS using Kubernetes Deployment and Service manifests.

**Deployment configuration:**

- Application: YouTube Clone
- Deployment: `youtube-clone-app`
- Replicas: 2
- Container image: `mydockerpersonalwork/youtube-clone`
- Service type: `LoadBalancer`
- Container port: 3000
- Service port: 80

Both application pods were verified in the `Running` state on separate worker nodes during testing. The public application endpoint was also tested during the lab.

The live AWS endpoint is no longer available because the lab infrastructure was terminated.

## Infrastructure and Monitoring

The project included hands-on work with Terraform and AWS infrastructure, plus Prometheus and Grafana monitoring components.

Monitoring tools used in the lab included:

- **Prometheus:** Metrics collection and querying.
- **Grafana:** Monitoring dashboards and visualization.
- **Alertmanager:** Alert routing and management.
- **Node Exporter:** Host-level metrics.
- **kube-state-metrics:** Kubernetes object-state metrics.

Only resources and monitoring configurations that were actually deployed should be represented as completed components in the final project screenshots and documentation.

## Security Considerations

- Used SonarQube for static code quality analysis.
- Used Trivy for filesystem and container-image vulnerability scanning.
- Used Jenkins credentials for integrations that required authentication.
- Practiced AWS infrastructure cleanup to avoid unnecessary cloud costs.

**Note:** Vulnerability scans identify issues that require review; running a scan alone does not mean an application is vulnerability-free.

## Screenshots and Evidence

Add screenshots from the completed lab to a `docs/` directory and link them here.

- [ ] Jenkins successful pipeline
- [ ] SonarQube project analysis
- [ ] Trivy scan output
- [ ] Docker Hub image
- [ ] Kubernetes pods and worker nodes
- [ ] Kubernetes LoadBalancer Service
- [ ] Prometheus and Grafana dashboards
- [ ] Architecture diagram

## Key Learning Outcomes

Through this project, I gained hands-on experience with:

- Building a multi-stage CI/CD pipeline in Jenkins.
- Integrating source code quality analysis and security scanning.
- Building and publishing Docker images.
- Deploying containerized applications to Kubernetes on Amazon EKS.
- Using Kubernetes Deployments, replicas, Services, and rollout verification.
- Provisioning cloud infrastructure with Terraform.
- Understanding monitoring and observability using Prometheus and Grafana.
- Cleaning up AWS infrastructure to manage cloud expenditure.

## Future Improvements

- Automate Jenkins builds through a GitHub webhook.
- Use unique Docker image tags for reproducible deployments.
- Store Kubernetes manifests and the Jenkins pipeline in version control.
- Improve secret management and image-scanning policy enforcement.
- Add an architecture diagram and screenshots of verified results.
- Recreate the environment on demand for demonstrations.

## Attribution

The underlying YouTube Clone application was based on the original project by [Ashfaque-9x](https://github.com/Ashfaque-9x/a-youtube-clone-app). This repository documents my DevOps and DevSecOps learning and implementation work around that application.

## Disclaimer

This repository is a portfolio and educational project. AWS resources used during the lab have been terminated to avoid ongoing charges. A live deployment is not currently maintained.
