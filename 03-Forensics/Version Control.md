# Version Control

Using git version control to find any valuable information

## Tools

- Linux terminal
- GIT

## How to Use

When getting a git repository into the terminal, one way it can be done is by cloning it with a git link

`git clone <gitlink>` is one example

Another way is installing a zip file with a git repository

For this case, `git_backup.zip` is an example that would be use

Once the zip file in the terminal use `unzip git_backup.zip` to unzip to your directory

Access the directory that was unzip, `git_backup` for instance

The .git in the directory will allow the usage of git commands

### Finding Information Using Git

Use `git log` to find information on any commits that been made

Information could be shown are:
 - Commit hash
 - The person or author with the email provided that made the commit
 - The date and time the commit was made
 - Commit message

Use `git show <commithash>` for additional information on what was commited

For this case `git show f28a0c2e4ef9bdc2cd6e780abdbd8695485c7083`

Information shown in there are a txt file and a employees assign flag

### Switching Git Branches
 
Use `git branch` to check if the repository have multiple branches

Use `git checkout <branchname>` or `git switch <branchname>` to switch branches

For this example, this repository has two branches, master and next branch

Use `git checkout next` to switch to another branch

Repository with branches will at times have file contents not found on main or other branches

Next branch has a `password.txt` not found on the main or master branch

