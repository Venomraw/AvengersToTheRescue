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

## Challenges

**We will now be using the terminal from this point on**

1. What is the display name of the author of this git project?

    - Change your directory to the repository you cloned
    - Type `git log`
    - Find the author in the commits

2. What is the short commit hash (first 8 characters) of the initial commit?

    - Type `git log`
    - The commits will be in the order from bottom to top based on when they were commited. Find the commit with the comment `Inital commit`

3. What is flag #1?

    - Type `cat README.md`

4. What is flag #2?

    - Type `git branch -a` to show all branches in the repository
    - Type `git checkout flag2`
    - Type `cat flag2.txt`
    - Type `git checkout master` when you are done

5. What is flag #3?

    - Type `cat flag3.txt`

6. What is flag #4?

    - Type `git log`
    - Find the commit with the comment `Added flag4` and copy the hash
    - Type `git show [commit hash]` (Flag will be in green text)

7. What is flag #5?

    - Type `git log`
    - Flag will be in a comment
