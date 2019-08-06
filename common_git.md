## Configure Git username/email

To set your global username/email configuration:
Set your username:
```
git config --global user.name "FIRST_NAME LAST_NAME"
```
Set your email address:
```
git config --global user.email "MY_NAME@example.com"
```
To set repository-specific username/email configuration:
From the command line, change into the repository directory.
Set your username:
```
git config user.name "FIRST_NAME LAST_NAME"
```
Set your email address:
```
git config user.email "MY_NAME@example.com"
```
Verify your configuration by displaying your configuration file:
```
cat .git/config
```

## changing/adding a remote:

to add a new remote:
```
git remote add origin git@github.com:User/UserRepo.git
```
to change the url of an existing remote repository:
```
git remote set-url origin git@github.com:User/UserRepo.git
```

below will push your code to the master branch of the remote repository defined with origin and -u let you point your current local branch to the remote master branch:
```
git push -u origin master
```

## delete a commit in git, local and remote
(see https://ncona.com/2011/07/how-to-delete-a-commit-in-git-local-and-remote/ for details)

see your commits:
```
git log --pretty=oneline --abbrev-commit
```

initiate interactive rebase (~2 sets depth to 2 commits):
```
git rebase -i HEAD~2
```

just delete the line that corresponds to the commit you want to delete and save the file

To remove a commit you already pushed to your origin or to another remote repository you have to first delete it locally like in the previous step and then push your changes to the remote.
```
git push origin +master
```

## Changing author info

see https://help.github.com/en/articles/changing-author-info

## ignore everything except a few files:
(https://stackoverflow.com/questions/987142/make-gitignore-ignore-everything-except-a-few-files)
An optional prefix ! which negates the pattern; any matching file excluded by a previous pattern will become included again. If a negated pattern matches, this will override lower precedence patterns sources.

gitignore:

```
# Ignore everything
*

# But not these files...
!.gitignore
!script.pl
!template.latex
# etc...

# ...even if they are in subdirectories
!*/

# if the files to be tracked are in subdirectories
!*/a/b/file1.txt
!*/a/b/c/*
```
