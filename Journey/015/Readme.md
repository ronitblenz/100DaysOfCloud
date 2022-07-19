![placeholder image](https://user-images.githubusercontent.com/91361382/179404737-ee14686e-cc7a-4b3e-a249-e0c355a8e005.png)

# Git for DevOps

## Introduction

Git is software for tracking changes in any set of files, usually used for coordinating work among programmers collaboratively developing source code during software development. Its goals include speed, data integrity, and support for distributed, non-linear workflows.

 - Now the first question that arises is, we relate to ```version controlling``` while defining Git, so what is version controlling?
   - The purpose of version control is to allow software teams track changes to the code, while enhancing communication and collaboration between team members. Version control facilitates a continuous, simple way to develop software.

 - In one sentence, Git handles the Version Control System for a piece of Code which is present in local machine as well as on GitHub or GitLab.
 - Now new words come into play, ```GitHub``` and ```GitLab```
   - GitHub provides code hosting services that allow developers to build software for open-source and private projects in organizations.
   - GitLab does the same, while in addition, it has Continuous Integration/Continuous Delivery (CI/CD) and DevOps workflows built-in.
**(FUN FACT : GitHub is acquired by Microsoft, that's why GitLab transferred their database from Microsoft Azure to Google Cloud Provider, just competitor things, haha!)**

 - For our convenience as a cloud/DevOps engineer, We will work with GitLab in this case.

## Basic Git Commands

### Setup

 - ```git config --global user.name “[firstname lastname]”``` <br>
(set a name that is identifiable for credit when review version history)

 - ```git config --global user.email “[valid-email]”``` <br>
(set an email address that will be associated with each history marker)

### Initialise

 - ```git init``` <br>
(initialize an existing directory as a Git repository)

 - ```git clone [url]``` <br>
(retrieve an entire repository from a hosted location via URL)

### Stage & Snapshot

 - ```git status``` <br>
(show modified files in working directory, staged for your next commit)

 - ```git add [file]``` <br>
(add a file as it looks now to your next commit)

 - ```git reset [file]``` <br>
(unstage a file while retaining the changes in working directory)

 - ```git diff``` <br>
(diff of what is changed but not staged)

 - ```git diff --staged``` <br>
(diff of what is staged but not yet commited)

 - ```git commit -m “[descriptive message]”``` <br>
(commit your staged content as a new commit snapshot)

### Branch and Merge

 - ```git branch``` <br>
(list your branches. a * will appear next to the currently active branch)

 - ```git branch [branch-name]``` <br>
(create a new branch at the current commit)

 - ```git checkout [branch-name]``` <br>
(switch to another branch and check it out into your working directory)

 - ```git merge [branch]``` <br>
(merge the specified branch’s history into the current one)

 - ```git log```
(show all commits in the current branch’s history)

 
 
