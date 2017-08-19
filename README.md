## Git repo on AWS
This is a brief guide to setup git repository in AWS EC2 instance. AWS Free tier has a [limitation](https://aws.amazon.com/free/?sc_ichannel=ha&sc_icampaign=free-tier&sc_icontent=2234) of 5 active users and 10K requests/mo to use [AWS CodeCommit](https://aws.amazon.com/codecommit/) service. Hopefully, this guide will help to get around the limitation and recurring charge although that might be neglible. 

### Step 1. Add security certificate
This step is not mandatory. However it is advisable to add AWS secutiry key to your ssh agent so that you don't need to specify security key with every command to access your EC2 instance.
```bash
$ ssh-add <path to key pair(pem file)>
```

### Step 2. Create remote repo directory
Connect to your EC2 from command line, and set up git [bare repository](https://githowto.com/bare_repositories)
```bash
$ ssh ec2-user@<your EC2 public DNS>
$ mkdir <remote-repo-name>.git
$ cd !$
$ git init --bare
```

### Step 3. Create local repo to push to new remote 
Create local repo and add your work on it, or use your existing local repo to setup its remote origin repo
```bash
$ mkdir <local-repo-name>
$ cd !$
$ git init
$ # Do all your stuffs
$ git add . && git commit -m "<commit message>"
$ git remote add origin ec2-user@<your EC2 public DNS>:<path to remote repo dir>.git
$ git push origin master
```

### To clone remote repository
To clone back the remote repository, use the origin url

```bash
$ git clone ec2-user@<your EC2 public DNS>:<path to remote repo dir>.git
```

