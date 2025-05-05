# DevOps Pipeline

This project contains a **CICD pipeline** setup for automating deployments.

## Project Structure

```
Devops_pipeline/
│-- deploy_sample/
│   ├── check_commits.py   # Script to check for new commits
│   ├── deploy.sh          # Deployment script
│-- .gitignore             # Git ignore file
│-- index.html             # Sample index page
│-- README.md              # This is a documentation file
│-- requirements.txt       # Contains setup and usage instructions
```

## Features
- **Automated commit checking** using `check_commits.py`
- **Automatic deployment** using `deploy.sh`
- **Nginx configuration** for serving `index.html`

## Troubleshooting
If you encounter permission issues with Nginx, run:
```bash
sudo systemctl restart nginx
```

For GitHub authentication issues, ensure your **GITHUB_TOKEN** is correctly set.

---

## Key Contributor
1. Tanuj
2. Minnath
3. Shraddha
4. Harjeet
5. Jasmine
6. Aniruddha
7. Ankit

