# 4. Execution Flow (jab YAML file use hoti hai)

- Tum .yml/.yaml file likhte ho (config define karte ho)
- Tool/platform (Docker, Kubernetes, GitHub Actions, Ansible) us file   ko parse karta hai — YAML ko internally JSON-like data structure (key-value objects) me convert karta hai
- Us parsed data ke basis pe engine actions execute karta hai (container start karna, pipeline run karna, pod deploy karna, etc.)


# 5. Real-World Use Cases (GitHub Actions ke alawa) — ye tumhare interview ke liye important hai
> Tool                        YAML file ka use
- Docker Compose              docker-compose.yml — multi-container apps define karne ke liye
- Kubernetes                  Pod, Deployment, Service definitions (deployment.yaml, service.yaml)
- Ansible                     Playbooks (playbook.yml) — server automation ke steps define karte hain
- GitLab CI/CD               .gitlab-ci.yml — pipeline stages define karte hain
- CircleCI                   .circleci/config.yml
- Helm (K8s package manager)  values.yaml, Chart.yaml
- AWS CloudFormation /        Infrastructure as Code templates
  Serverless Framework 
- Prometheus                  prometheus.yml — monitoring config
- Spring Boot (Java)          application.yml — app configuration
- Swagger/OpenAPI             API documentation specs


DevOps interview angle: Interviewer ye zaroor pucheg — "YAML kaha kaha use hota hai apki knowledge me?" — to Kubernetes aur Ansible ka naam zaroor lena, kyunki wahan YAML ki depth zyada dikhani padti hai.


