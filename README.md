# git
repository for notes about how git works and how you can work with it

### content

- create local git
- create remote git


### how to implement a git post-receive hook for auto-deployment

*on localhost:*

create new local git repository by initiate a new git with `git init` or clone an exisiting from your git server by `git clone git@githubcom:racoon63/test.git
on your server where you want to auto-deploy your repository and your files in it.

*on the server:*

*STEP 1:*
create an empty directory (for i.e. test_hook):

```bash
mkdir /home/git/test_hook
```
*STEP 2:*
change into that newly created directory:

```bash
cd /home/git/test_hook
```
*STEP 3:*
and create a new bare git by typing:

```bash
git init --bare
```

*STEP :*
verify your remote repository on the git server. There will be none if you inititated a new one locally. When you cloned a remote repository there will appear a remote repoitory address like `origin git@github.$
```bash
git remote add origin git@github.com:racoon63/test.git
```

*STEP :*
create a post-receive bash script (without .sh at the end) that will be executed everytime we push something to our git repository

```bash
nano /home/git/test_hook/hooks/post-receive
```
*STEP :*
add the following lines to the file:

```bash
#!/bin/bash
working_tree="/home/git/test"
target_branch="master"
GIT_WORK_TREE=$working_tree git checkout $target_branch -f
```

*STEP :*
save the file with `STGR + O` and close it with `STGR + X`
give execution permissions for the file:

```bash
chmod +x /home/git/test-hook/hooks/post-receive
```

*STEP :*
create a new directory with a normal git in it (i.e. test) that will hold our files/config etc. later:

```bash
mkdir /home/git/test/
cd /home/git/test/
git init
```

*STEP :*
add remote repository address:
```bash
git remote add origin git@github.com:racoon63/test.git
```

*Verification that the process works:*
create or edit a file on your local machine, add it to stage, commit the files and push it/them to your remote repository.
Now list the content of the directory that should hold your files:

```bash
ls -l /home/git/test/
```

when the files will be listed, everything works. You can edit your post-receive script if you'd like.
