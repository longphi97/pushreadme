# Training Git
#### _Nguyen Van Phi Long_
[![](https://wiki.tino.org/wp-content/uploads/2021/05/word-image-214.png)](https://github.com/)
[![](https://blog.cloud365.vn/images/img-gitlab/gitlab-00.jpeg)](https://gitlab.com/)
1. __What is Git?__  
    Git is a free and open-source version control system, originally created by Linus Torvalds in 2005. Unlike older centralized version control systems such as SVN and CVS, Git is distributed: every developer has the full history of their code repository locally. This makes the initial clone of the repository slower, but subsequent operations such as commit, blame, diff, merge, and log dramatically faster.
    Git also has excellent support for branching, merging, and rewriting repository history, which has led to many innovative and powerful workflows and tools. Pull requests are one such popular tool that allows teams to collaborate on Git branches and efficiently review each other's code. Git is the most widely used version control system in the world today and is considered the modern standard for software development.
2. __How Git Works?__  
Here is a basic overview of how Git works:
    - Create a "repository" (project) with a git hosting tool (like Bitbucket)
    - Copy (or clone) the repository to your local machine
    - Add a file to your local repo and "commit" (save) the changes
    - "Push" your changes to your main branch
    - Make a change to your file with a git hosting tool and commit
    - "Pull" the changes to your local machine
    - Create a "branch" (version), make a change, commit the change
    - Open a "pull request" (propose changes to the main branch)
    - "Merge" your branch to the main branch
3. __About SSH?__  
An SSH key is an access credential for the SSH (secure shell) network protocol. This authenticated and encrypted secure network protocol is used for remote communication between machines on an unsecured open network. SSH is used for remote file transfer, network management, and remote operating system access. The SSH acronym is also used to describe a set of tools used to interact with the SSH protocol.
SSH uses a pair of keys to initiate a secure handshake between remote parties. The key pair contains a public and private key. The private vs public nomenclature can be confusing as they are both called keys. It is more helpful to think of the public key as a "lock" and the private key as the "key". You give the public 'lock' to remote parties to encrypt or 'lock' data. This data is then opened with the 'private' key which you hold in a secure place.
4. __How to Create an SSH Key__  
SSH keys are generated through a public key cryptographic algorithm, the most common being RSA or DSA. At a very high level SSH keys are generated through a mathematical formula that takes 2 prime numbers and a random seed variable to output the public and private key. This is a one-way formula that ensures the public key can be derived from the private key but the private key cannot be derived from the public key.
SSH keys are created using a key generation tool. The SSH command line tool suite includes a keygen tool. Most git hosting providers offer guides on how to create an SSH Key.
5. __Generate an SSH Key on Mac and Linux__  
Both OsX and Linux operating systems have comprehensive modern terminal applications that ship with the SSH suite installed. The process for creating an SSH key is the same between them.
    1. execute the following to begin the key creation  
    ```ssh-keygen -t rsa -b 4096 -C "your_email@example.com"```  
    This command will create a new SSH key using the email as a label
    2.  You will then be prompted to "Enter a file in which to save the key."
You can specify a file location or press “Enter” to accept the default file location.  
    ```> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]```  
    3. The next prompt will ask for a secure passphrase.
    A passphrase will add an additional layer of security to the SSH and will be required anytime the SSH key is used. If someone gains access to the computer that private keys are stored on, they could also gain access to any system that uses that key. Adding a passphrase to keys will prevent this scenario.  
    ```> Enter passphrase (empty for no passphrase): [Type a passphrase]```  
    ```> Enter same passphrase again: [Type passphrase again]```  
At this point, a new SSH key will have been generated at the previously specified file path.
    4. Add the new SSH key to the ssh-agent
    The ssh-agent is another program that is part of the SSH toolsuite. The ssh-agent is responsible for holding private keys. Think of it like a keychain. In addition to holding private keys it also brokers requests to sign SSH requests with the private keys so that private keys are never passed around unsecurly.
Before adding the new SSH key to the ssh-agent first ensure the ssh-agent is running by executing:  
```$ eval "$(ssh-agent -s)"```  
```> Agent pid 59566```
    Once the ssh-agent is running the following command will add the new SSH key to the local SSH agent.  
    ```ssh-add -K /Users/you/.ssh/id_rsa```  
    The new SSH key is now registered and ready to use!  
6. __What is a Git repository?__  
A Git repository is a virtual storage of your project. It allows you to save versions of your code, which you can access when needed.  
7. __Initializing a new repository: git init__    
    To create a new repo, you'll use the git init command. git init is a one-time command you use during the initial setup of a new repo. Executing this command will create a new .git subdirectory in your current working directory. This will also create a new main branch.  
    Versioning an existing project with a new git repository
    This example assumes you already have an existing project folder that you would like to create a repo within. You'll first cd to the root project folder and then execute the git init command.  
```cd /path/to/your/existing/code```  
```git init```  
Pointing git init to an existing project directory will execute the same initialization setup as mentioned above, but scoped to that project directory.  
```git init <project directory>```
8. __Cloning an existing repository: git clone__  
    If a project has already been set up in a central repository, the clone command is the most common way for users to obtain a local development clone. Like git init, cloning is generally a one-time operation. Once a developer has obtained a working copy, all version control operations are managed through their local repository.  
    ```git clone <repo url>```  
    git clone is used to create a copy or clone of remote repositories. You pass git clone a repository URL. Git supports a few different network protocols and corresponding URL formats. In this example, we'll be using the Git SSH protocol. Git SSH URLs follow a template of: ```git@HOSTNAME:USERNAME/REPONAME.git```  
    An example Git SSH URL would be: ```git@bitbucket.org:rhyolight/javascript-data-store.git``` where the template values match:  
    - HOSTNAME: bitbucket.org  
    - USERNAME: rhyolight  
    - REPONAME: javascript-data-store  
    When executed, the latest version of the remote repo files on the main branch will be pulled down and added to a new folder. The new folder will be named after the REPONAME in this case javascript-data-store. The folder will contain the full history of the remote repository and a newly created main branch. 
9. __How to Delete, Checkout, Create, and Rename a branch in Git__
    1. Git Branch  
    Git’s branching functionality lets you create new branches of a project to test ideas, isolate new features, or experiment without impacting the main project  
    2. View Branches  
    To view the branches in a Git repository, run the command:  
    ```git branch```  
    To view both remote-tracking branches and local branches, run the command:  
    ```git branch -a```  
    There will be an asterisk (*) next to the branch that you’re currently on.   
    There are a number of different options you can include with git branch to see different information. For more details about the branches, you can use the -v (or -vv, or --verbose) option. The list of branches will include the SHA-1 value and commit subject line for the HEAD of each branch next to its name.  
    You can use the -a (or --all) option to show the local branches as well as any remote branches for a repository. If you only want to see the remote branches, use the -r (or --remotes) option  
    3. Checkout a Branch  
    To checkout an existing branch, run the command:  
    ```git checkout BRANCH-NAME```  
    Generally, Git won’t let you checkout another branch unless your working directory is clean, because you would lose any working directory changes that aren’t committed. You have three options to handle your changes:  
        1. trash them  
        2. commit them  
        3. stash them  
    4. Create a New Branch  
    To create a new branch, run the command:  
    ```git branch NEW-BRANCH-NAME```
    Note that this command only creates the new branch. You’ll need to run git checkout NEW-BRANCH-NAME to switch to it.  
    There’s a shortcut to create and checkout a new branch at once. You can pass the -b option (for branch) with git checkout. The following commands do the same thing:  
        1. Two-step method  
        ```git branch NEW-BRANCH-NAME```  
        ```git checkout NEW-BRANCH-NAME```  
        2. Shortcut  
        ```git checkout -b NEW-BRANCH-NAME```  
        When you create a new branch, it will include all commits from the parent branch. The parent branch is the branch you’re on when you create the new branch.  
    5. Rename a Branch  
    To rename a branch, run the command:  
    ```git branch -m OLD-BRANCH-NAME NEW-BRANCH-NAME```  
    ```git branch --move OLD-BRANCH-NAME NEW-BRANCH-NAM```  
    6. Delete a Branch  
    Git won’t let you delete a branch that you’re currently on. You first need to checkout a different branch, then run the command:  
    ```git branch -d BRANCH-TO-DELETE```  
    ```git branch --delete BRANCH-TO-DELETE```  
    The branch that you switch to makes a difference. Git will throw an error if the changes in the branch you’re trying to delete are not fully merged into the current branch. You can override this and force Git to delete the branch with the -D option (note the capital letter) or using the --force option with -d or --delete:  
    ```git branch -D BRANCH-TO-DELETE```  
    ```git branch -d --force BRANCH-TO-DELETE```  
    ```git branch --delete --force BRANCH-TO-DELETE```  
    7. Compare Branches  
    You can compare branches with the git diff command:  
    ```git diff FIRST-BRANCH..SECOND-BRANCH```  
    You’ll see colored output for the changes between branches. For all lines that have changed, the SECOND-BRANCH version will be a green line starting with a ”+”, and the FIRST-BRANCH version will be a red line starting with a ”-“. If you don’t want Git to display two lines for each change, you can use the --color-words option. Instead, Git will show one line with deleted text in red, and added text in green.  
    If you want to see a list of all the branches that are completely merged into your current branch (in other words, your current branch includes all the changes of the other branches that are listed), run the command  
    ```git branch --merged.```  
    8. Help with Git Branch  
    If you forget how to use an option, or want to explore other functionality around the git branch command, you can run any of these commands:  
    ```git help branch```  
    ```git branch --help```  
    ```man git-branch```  
10. __Git Merge vs Git Rebase__  
    1. What is Git Merge?  
    Git merge is a command that allows you to merge branches from Git.
    Merging is a common practice for developers. Whether branches are created for testing, bug fixes, or other reasons, merging commits changes to another branch. It takes the contents of a source branch and integrates it with a target branch.  
    When you use Git merge, only the target branch is changed. The source branch history remains. Advocates of it like it because it preserves the history of a branch  
    2. What is Git Rebase?  
    Git rebase is a command that allows developers to integrate changes from one branch to another.  
    Git rebase compresses all the changes into a single “patch.” Then it integrates the patch onto the target branch. Unlike merging, rebasing flattens history. It transfers the completed work from one branch to another. In the process, unwanted history is eliminated.  
    Advocates of Git rebase like it because it simplifies their review process.  
    *Git Rebase vs. Git Merge: Similarities and Differences:*  
    Git rebase and merge both integrate changes from one branch into another. Where they differ is how it's done. Git rebase moves a feature branch into a master. Git merge adds a new commit, preserving the history.  
    *What Is the Difference Between Git Merge and Git Rebase?*  
        *Git Rebase:*  
        - Streamlines a potentially complex history.  
        - Avoids merge commit “noise” in busy repos with busy branches.  
        - Cleans intermediate commits by making them a single commit, which can be helpful for DevOps teams.  
          
        *Git Merge:*   
        - Simple and familiar.  
        - Preserves complete history and chronological order.  
        - Maintains the context of the branch.



    









