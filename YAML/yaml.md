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

# Table Format:-

| Tool | YAML file ka use |
| :--- | :--- |
| **Docker Compose** | `docker-compose.yml` – multi-container apps define karne ke liye |
| **Kubernetes** | Pod, Deployment, Service definitions (`deployment.yaml`, `service.yaml`) |
| **Ansible** | Playbooks (`playbook.yaml`) – server automation ke steps define karte hain |
| **GitLab CI/CD** | `.gitlab-ci.yml` – pipeline stages define karte hain |
| **CircleCI** | `.circleci/config.yml` |
| **Helm (K8s package manager)** | `values.yaml`, `Chart.yaml` |
| **AWS CloudFormation / Serverless Framework** | Infrastructure as Code templates |
| **Prometheus** | `prometheus.yml` – monitoring config |
| **Spring Boot (Java)** | `application.yml` – app configuration |
| **Swagger/OpenAPI** | API documentation specs |


# 6. Docker Compose Example (practical + production style)
version: "3.8"

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      - ENV=production
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: secret123
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:

# Breakdown:
- version → Compose file format version
- services → root key, har service ek key hai (web, db)
- image → kaunsi Docker image use karni hai
- ports → host:container port mapping
- volumes → data persistence
- environment → env variables container ke andar
- depends_on → startup order define karta hai

# 7. Common Interview Questions
1. YAML aur JSON me kya difference hai?
2. YAML indentation ke liye tabs kyu allowed nahi hai?
3. Anchors (&) aur aliases (*) kis liye use hote hain?
4. | aur > block scalars me kya difference hai?
5. Ek invalid YAML file ko kaise debug karoge?
6. Docker Compose me depends_on aur health checks ka relation kya hai?

# 8. Beginner Mistakes (jo tum avoid karo)
- Tabs use karna (hamesha spaces)
- Inconsistent indentation levels
- Colon ke baad space bhoolna
- List items ke beech missing dash
- Boolean values ko quotes me likhna jab zaroorat na ho ("true" string ban jayega, boolean nahi)

# 9. Best Practices
- Hamesha 2-space indentation consistent rakho
- Ek YAML linter use karo (yamllint) validate karne ke liye
- Complex configs ko multiple files me split karo (readability ke liye)
- Sensitive data (passwords) ko YAML me hardcode mat karo — secrets manager use karo

# 10. Memory Trick
- "YAML = You Always Mind Lines"** — matlab hamesha line ka indentation aur spacing dhyan se dekho, kyunki YAML whitespace-sensitive language hai.
- Simple mnemonic: "Dash for list, Colon for pair, Indent for nest"