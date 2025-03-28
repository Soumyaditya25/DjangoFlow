# DjangoFlow

**DjangoFlow** is a single‐page Django application scaffolded for fully automated CI/CD. It demonstrates how to wire up:

- **Jenkins** (via `Jenkinsfile`) for build, test & deploy  
- **GitLab CI** (via `.gitlab-ci.yml`) for parallel pipelines  
- **Docker/Docker Compose** to containerize web, worker, and database  
- **Celery** & **Redis** for background tasks  
- **Batch** jobs directory for scheduled scripts  
- Production‐grade tooling: automated migrations, linting, testing, and versioning


## 🚀 Features

- **Zero-touch deployments**  
  Push to `main` → Jenkins picks it up → spins up new containers → runs migrations → health checks → traffic switch  
- **Multi‐environment support**  
  Local, QA, Staging, Production all use the same pipeline definitions  
- **Containerized stack**  
  - Django web (`app/`)  
  - PostgreSQL (`database/`)  
  - Redis & Celery worker (`celery/`)  
  - Optional batch jobs (`batch/`)  
- **DevOps best practices**  
  - Linting & formatting (Black, Flake8, Ruff)  
  - Type checking (mypy)  
  - Automated tests (pytest)  
  - Semantic versioning & changelog generation  
  - Health checks & rolling updates  


## 📁 Repository Structure

```

.
├── .gitignore
├── Jenkinsfile
├── .gitlab-ci.yml
├── requirements.txt
├── dockerfiles/          # Dockerfiles for each service
├── scripts/              # Utility & deployment scripts
├── app/                  # Django project & apps
├── celery/               # Celery configuration & tasks
├── batch/                # Cron-like/one-off batch jobs
└── database/             # DB init scripts & migrations

````

---

## 🔧 Getting Started

### Prerequisites

- **Docker & Docker Compose**  
- **Jenkins** (with Docker permissions)  
- **GitLab Runner** (optional, if using GitLab CI)  

### Clone & Configure

```bash
git clone https://github.com/Soumyaditya25/DjangoFlow.git
cd DjangoFlow
````

Create a `.env` in project root:

```env
# .env
DJANGO_SECRET_KEY=your-secret-key
POSTGRES_DB=djangoflow
POSTGRES_USER=django
POSTGRES_PASSWORD=securepassword
REDIS_URL=redis://redis:6379/0
```

### Local Development

Build and start all services:

```bash
docker-compose up --build
```

* Django will be available at [http://localhost:8000](http://localhost:8000)
* Celery worker logs in your terminal
* Batch scripts can be run via `docker-compose run batch <script-name>`

Run tests:

```bash
docker-compose run web pytest
```

---

## ⚙️ CI/CD Pipelines

### Jenkins

* **`Jenkinsfile`** defines stages: **checkout → build → lint → test → dockerize → deploy**
* Automatically triggered on push to `main`
* Uses Docker agents; jobs run in containers

### GitLab CI

* **`.gitlab-ci.yml`** mirrors Jenkins stages, with parallel jobs & caching
* Good for organizations standardizing on GitLab

---

## 🛠️ Adding New Services

1. Create a new Dockerfile in `dockerfiles/`
2. Add its service to `docker-compose.yml`
3. Extend the Jenkins/GitLab pipeline to build & deploy

---


## Created with ♥️ by Soumyaditya.

