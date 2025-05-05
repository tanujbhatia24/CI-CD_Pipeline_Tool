# DevOps CI/CD Pipeline

This project demonstrates a simple **CI/CD pipeline** for automatically deploying changes from a GitHub repository using Python and shell scripting, with support for `nginx` as the web server.
---

## Project Structure

```
CI-CD_Pipeline_Tool/
│-- deploy_sample/
│   ├── check_commits.py     # Script to check for new commits
│   ├── deploy.sh            # Deployment script
│-- .gitignore               # Git ignore file
│-- index.html               # Sample index page
│-- README.md                # Project documentation
```
---

## Features

- **Automated Commit Checking** with `check_commits.py`
- **Automatic Deployment** with `deploy.sh`
- **Cron Job Integration** to run scripts periodically
- **Nginx Configuration** for serving a static `index.html` page
- **Token-Based GitHub Authentication**
- **Logging Support** to track execution
---

## System Requirements

Ensure the following are installed on your Ubuntu/Linux system:

```bash
sudo apt update
sudo apt install -y nginx git python3 pipx
pipx ensurepath
```
---

## Project Setup

1. Set up your SSH keys with GitHub.
2. Clone the repository:
   ```bash
   mkdir -p ~/Devops_CICD && cd ~/Devops_CICD
   git clone <your_repo_url>
   cd CI-CD_Pipeline_Tool
   ```
3. Create a `log` directory:
   ```bash
   mkdir log && chmod 755 log
   ```

4. Copy the provided scripts:
   - `check_commits.py`
   - `deploy.sh`  
   (Refer to `deploy_sample/`)

5. Make both scripts executable:
   ```bash
   chmod 755 check_commits.py deploy.sh
   ```
---

## GitHub Token Setup

### On Ubuntu:
1. Install `python3-dotenv`:
   ```bash
   sudo apt install -y python3-dotenv
   ```
2. Create a `.env` file and add your GitHub token:
   ```python
   GITHUB_TOKEN = "your_github_token"
   ```
3. Ensure `.env` is listed in `.gitignore`.

### On Windows:
1. Install dotenv:
   ```bash
   pip install python-dotenv
   ```
2. Create a `.env` file and add your GitHub token:
   ```python
   GITHUB_TOKEN = "your_github_token"
   ```
3. Ensure `.env` is listed in `.gitignore`.
---

## Cron Job Setup (Every 5 Minutes)

Edit crontab:

```bash
crontab -e
```

Add the following line (adjust paths as needed):

To enable cron:

```bash
sudo systemctl enable cron
sudo systemctl start cron
```

```cron
*/5 * * * * /usr/bin/python3 $HOME/Devops_CICD/check_commits.py >> $HOME/Devops_CICD/log/check_commits.log 2>&1
```

### Validate Cron:

```bash
crontab -l
systemctl status cron
sudo journalctl -u cron --since "1 hour ago"
```
---

## Nginx Setup

1. Update Nginx configuration:

```bash
sudo nano /etc/nginx/sites-available/default
```

Set the root to:

```nginx
root /home/<your_username>/Devops_CICD/CI-CD_Pipeline_Tool/;
```

2. Restart nginx:

```bash
sudo systemctl restart nginx
```

(Optional: allow restart without password)

```bash
echo "$(whoami) ALL=(ALL) NOPASSWD: /bin/systemctl restart nginx" | sudo tee /etc/sudoers.d/nginx_restart
```
---

## Askpass Script (Optional for Sudo Automation)

Create an askpass script for secure sudo:

```bash
nano ~/askpass.sh
```

Add the following:

```bash
#!/bin/bash
echo "your_sudo_password"
```

Make it executable:

```bash
chmod +x ~/askpass.sh
```
---

## ✅ Validation

- **Check Python version**: `python3 --version`
- **Check Git version**: `git --version`
- **Check Nginx**: `sudo systemctl status nginx`
- **Check Cron**: `sudo systemctl status cron`
---

## 📄 License

This project is intended for educational and demonstration purposes. You are welcome to use and adapt it as a reference; however, please ensure that your work represents your own understanding and is not reproduced verbatim.
