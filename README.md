
# Setting Up SSH Authentication for GitHub Repository

This guide provides step-by-step instructions to switch from HTTPS to SSH authentication in your GitHub repository to avoid repeatedly entering your username and password.

## 1️⃣ Check Current Git Remote
To verify whether your repository is using HTTPS, run the following command:
```bash
git remote -v
```
If it returns an output like this, it means your repository is using HTTPS:
```
origin  https://github.com/your-organization/repository.git (fetch)
origin  https://github.com/your-organization/repository.git (push)
```

## 2️⃣ Generate an SSH Key (If Not Already Created)
First, check if you already have an SSH key:
```bash
ls -al ~/.ssh
```
If `id_rsa` and `id_rsa.pub` are not present, generate a new SSH key:
```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```
Press **Enter** to accept the default location.

## 3️⃣ Add the SSH Key to GitHub
Copy your public SSH key:
```bash
cat ~/.ssh/id_rsa.pub
```
1. Go to **GitHub → Settings → SSH and GPG Keys** ([Direct Link](https://github.com/settings/keys)).
2. Click **New SSH Key**.
3. **Paste the copied key** into the "Key" field and save it.

## 4️⃣ Add SSH Key to SSH Agent
Run the following commands to ensure your SSH key is loaded:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

## 5️⃣ Change Git Remote to SSH
Navigate to your repository:
```bash
cd ~/path-to-your-repository
```
Change the remote URL to SSH:
```bash
git remote set-url origin git@github.com:your-organization/repository.git
```
Verify the change:
```bash
git remote -v
```
The output should now be:
```
origin  git@github.com:your-organization/repository.git (fetch)
origin  git@github.com:your-organization/repository.git (push)
```

## 6️⃣ Test SSH Connection
Run:
```bash
ssh -T git@github.com
```
If successful, you should see:
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

## 7️⃣ Pull and Push Without Password Prompt
Now, you can pull or push changes without being asked for a username or password:
```bash
git pull origin main  # or 'master' depending on your branch
```
```bash
git push origin main
```

## ✅ Conclusion
You have successfully switched from HTTPS to SSH authentication for your GitHub repository. You will no longer be prompted to enter your GitHub username and password when pulling or pushing changes.

---
_Last updated: March 4, 2025_
