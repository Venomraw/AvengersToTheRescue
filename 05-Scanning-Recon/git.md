# Git

For this challenge, we will be using a terminal. **I will be using WSL Ubuntu**. We must also install Git if we have not already by typing `sudo apt install git`.

## Cloning the Repository

In the challenge, there is a GitLab link. However, when trying to clone it, we will get the following error

```
~ git clone git@gitlab.com:cybergit4823/my-awesome-flag-project.git

Cloning into 'my-awesome-flag-project'...
git@gitlab.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

We do not have permission. The reason why is because the link is for an SSH. We cannot add an SSH key to the account, so we have to find the HTTPS link. To do this, we take the link we were given and change it around. Since we already know that the repository is on GitLab we will use `https://www.gitlab.com`. Then we just add `/cybergit4823/my-awesome-flag.git`. Now we enter the following command and it should clone.

```
git clone https://gitlab.com/cybergit4823/my-awesome-flag-project.git
```
---