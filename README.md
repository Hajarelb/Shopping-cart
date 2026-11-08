# Shopping Cart: DevOps labs

Lab repository from my **Master in DevOps & Cloud Computing** (DevOps I, 2025 – 2026).

This is a fork of [Mlamrini/Shopping-cart](https://github.com/Mlamrini/Shopping-cart), a Spring Boot (Java, Maven) e-commerce demo application provided by my professor. **The application code is not mine.** This fork holds the DevOps work I built around it.

## What I added

- **Ansible**: `ansible.cfg`, `inventory.ini` and `ansible/deploy.yml`. The playbook connects over SSH to a containerized target node and checks it (connectivity, system, Python, hostname).
- **Monitoring**: Spring Boot Actuator and Micrometer dependencies in `pom.xml`, and management endpoints in `application.properties` (`/prometheus`, `/health`, `/metrics` on port 8071), scraped by Prometheus and displayed in Grafana.
- **Build fixes**: AspectJ weaver dependency and `maven-jar-plugin` version.

## Labs run on this application

| Lab | What I built |
|---|---|
| Jenkins CI/CD | Pipeline: Maven build, OWASP Dependency-Check, SonarQube analysis, Docker image build and push to Docker Hub |
| Jenkins + Ansible | The same pipeline extended with a stage that runs the Ansible playbook on the target nodes |
| Monitoring | Prometheus and Grafana: system metrics (Node Exporter), application metrics (Actuator/Micrometer) and Jenkins metrics, plus Health Check and Metrics Check stages in the pipeline |

The Jenkins pipelines were configured in the Jenkins interface during the labs.

## Repository content

| Path | Description |
|---|---|
| `src/`, `pom.xml` | Spring Boot application (from the original project) |
| `Dockerfile`, `docker/Dockerfile` | Image definitions (from the original project) |
| `scripts/run_docker.sh` | Build and run in Docker (from the original project) |
| `deploymentservice.yml` | Kubernetes Deployment and Service (from the original project) |
| `ansible/`, `ansible.cfg`, `inventory.ini` | My Ansible setup for the lab nodes |

## Run it locally

```bash
mvn clean package
docker build -t shopping-cart .
docker run -p 8070:8070 shopping-cart
```

The application listens on `http://localhost:8070`, and metrics on port 8071.

> The default admin account in `application.properties` is a demo account from the original project, for lab use only. Never reuse these credentials.
