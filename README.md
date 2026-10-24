# Python CI/CD with GitHub and Jenkins

This is a simple Python application with automated checks using GitHub and Jenkins.

## Project structure

- app.py - application code
- requirements.txt - Python dependencies
- tests/test_app.py - unit tests
- Jenkinsfile - Jenkins pipeline

## Run locally

```bash
python -m venv venv
source venv/bin/activate   # Linux/macOS
# or venv\Scripts\activate  # Windows
pip install -r requirements.txt
pytest -q
```

## Jenkins setup

1. Install Jenkins.
2. Install plugins: GitHub, Git, Pipeline, Build Trigger, Warnings, etc.
3. Create a new Pipeline job.
4. Point Jenkins to this GitHub repository.
5. Enable `GitHub hook trigger for GITScm polling` or use a GitHub webhook.
6. Jenkins will automatically run when a new commit is pushed.

## GitHub setup

1. Create a GitHub repository.
2. Push the project to GitHub.
3. Add a webhook:
   - Payload URL: `http://<jenkins-server-ip>:8080/github-webhook/`
   - Content type: `application/json`
   - Select `Just the push event`
4. Commit code changes to GitHub.
5. Jenkins will detect the push and run the pipeline.

## Pipeline behavior

- Checkout source code
- Install dependencies
- Run tests with `pytest`
- Mark build success or failure

## Example workflow

```bash
git add .
git commit -m "Update app logic"
git push origin main
```

After pushing, Jenkins automatically checks the repository and runs tests.
