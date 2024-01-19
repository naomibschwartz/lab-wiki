---
title: GitHub
linktitle: GitHub
type: book
date: '2019-05-05T00:00:00+01:00'
# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
summary: >
  GitHub is an open-sourced code hosting platform that is great for containing, organizing, and sharing code amongst lab members. Below will be some general Git resources, along with basic instructions pertaining to Lab Website/Wiki editing.
---
## SETTING UP GIT LOCALLY

As shown in the cheat sheet, you must first configure your git account on the local end to be able to create remote connections, and this means you MUST have a Git account before proceeding. Two great documents that will help you with setting up Git are:
-	<ins> https://docs.github.com/en/get-started/getting-started-with-git </ins>
-	<ins> https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup </ins>

Once you have created a Git account, you are now able to set up a remote connection, which will allow you to host and edit Git projects on your own computer (Yay!). To set this up:

1.	Open up your Terminal (Mac and Linux) or Git Bash (Windows)
2.	Now you can set a Git* username, to do this type:

```
git config --global user.name “[Your User Name]”
```

To confirm that your Git user is set up correctly you can type:

```
git config –global user.name
```

If all went well you should be able to move onto the next sections discussing remote connections, specifically cloning environments into your local system.

## CLONING ENVIRONMENTS

Once you have established your connection locally, you can begin to clone repositories from online sources through either HTTPS or SSH Cloning, these will be explained more below. 

In my opinion, if you will be working with Git extensively, setting up SSH cloning is more useful, where you will not need to be continuously asked to login to your account, instead a more secure connection can be made through more work spent at the beginning which will save you time down the line.

Before cloning, ensure that you have changed your working directory to the folder where you wish to host your project, you can do this through the ‘cd’ command followed by your folder path.

### HTTPS CLONING
If you are using a MacOS (or Linux) system it may be a good idea to install the Homebrew package, which will install many packages your system may be missing that are useful for Git and coding in general – this includes a Git Credential Manager.

1.	You will need to first install homebrew using this command:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
	
2.	Once installed, you can then use Homebrew to install git, with this command:

```
brew install git
```

3.	Install Git Credential Manager using Homebrew – this will allow you to sign into your account through a browser window to allow for cloning of environments

```
Brew install --cask git-credential-manager
```

**For other systems Homebrew is incompatible so may need to look at other options*

Now that you should have your credentials set up, you should be able to move onto actually cloning a repository!

To do this you will need to find the repositories HTTPS url, which can be found under code while in the repository. To actually add this remote connection you will need to type in your Terminal:
	
```
git remote add origin <REMOTE_URL>
```

Where <REMOTE_URL> is replaced with the HTTPS url for your desired repository, e.g., 
<ins>https://github.com/naomibschwartz/naomibschwartz.github.io.git</ins>

### SSH CLONING
While the HTTPS method for cloning repositories is said to be easier, if you are planning on pulling multiple repositories and working frequently on the website or other Git projects it may be beneficial to instead switch to the SSH (Secure Shell Protocol) methods.

This process is a bit more extensive, but in my experience it has worked more seamlessly than the HTTPS option.

First you will need to generate a new key, you can do this either locally or through the Git website, but below will have instructions for local generation

1.	Open your Terminal or Git Bash
2.	Paste

```
ssh-keygen -t ed25519 -C "[YOUR EMAIL]"
```

3.	This will cause a prompt, “Enter a file in which to save the key”, press ENTER if you accept the default location
4.	Type a secure passphrase when prompted, or leave blank if you don’t want to tie a passphrase with it (WOULD RECOMMEND AGAINST THIS)

You should now be able to add your SSH key to an ssh-agent, which will allow you to store the passwords and its key on your local system. On Mac’s (after Sierra 10.12.2), you can do this by:
 
1.	Checking that you have a configuring file within your ssh program

```
open ~/.ssh/config
```

  - If the file doesn’t exist, create one:

```
touch ~/.ssh/config
```

2.	Open this file (through the ‘open’ command above) and modify the file so it features:
```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```
For Windows, you should first set-up the ssh-agent, by:

1.	Opening your ~/.profile or ~/.bashrc file in a Git shell, and copying:

```
env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env
```

2.	Add your SSH private key to the ssh-agent by typing (replace id_ed25519 with your key name if different):

```
ssh-add /c/Users/YOU/.ssh/id_ed25519
```

To test the connection, you can do so through Terminal or Git Bash by typing:

```
ssh -T git@github.com
```

it should return a message like this one: Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access. 

Now you can clone the repository! To do this, you follow the same steps of the HTTPS cloning:

To do this you will need to find the repositories SSH url, which can be found under code while in the repository. To actually add this remote connection you will need to type in your Terminal:
	
```
git remote add origin <REMOTE_URL>
```

Where <REMOTE_URL> is replaced with the HTTPS url for your desired repository, e.g., 
git@github.com:naomibschwartz/naomibschwartz.github.io.git

## Adding, Committing, and Pushing Edits
### Adding Edits
First use ```git status``` to see what edits are queued for a push – edits will show in red if they have yet to be committed.

The easiest way to add the edits are to type ```git add .``` the '.' means that all changes (noted in red) will be added to the push – the edits should be in green if we type the ```git status```

### Committing Edits
When committing its beneficial to tie a message to your edits so that the Git Manager can see what edits have been done when accepting the merge between your edits to the main branch, and when trying to find where conflicts are emerging from. 

So once you have added your edits, you simply type ```git commit -m [MESSAGE]``` the '-m' means you want to tie a message. Try to make it concise, so that the manager is able to see quickly what was done, because other than that the code will speak for itself!

### Pushing Edits
Now that your edits have been added, and committed, you can now push them upstream to the Git Repository. To do this type ```git push origin [branch-name]```. This will create a copy of your branch in the Git Repo that the manager can then merge with the main branch if all looks to be correct.
 
For larger commits, it may take a bit longer to push, so no worries if it doesn’t immediately happen – we can then check on the main Git Repo to see if our edits have made it there. 

We can see they have with the creation of the pull request! This will be where the manager can compare and merge the branches if there are no conflicts, and your edits can now be implemented into the website. 
  - It will take a couple moments for the website to merge and publish the edits, so don’t worry if it doesn’t appear right away – if there is an issue you will see a little alert at the top of the Repository

