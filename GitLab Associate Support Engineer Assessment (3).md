
# GitLab Associate Support Engineer Assessment
---
# Question 1: Bash Script to List Usernames and Home Directories

To achieve the desired output for this task, we need to create a bash file (list_users.sh) using ``vim list_users.sh`` to create the file and edit it using **vim**.

[![Screenshot-2025-04-30-at-21-39-51.png](https://i.postimg.cc/1X2Y2BLg/Screenshot-2025-04-30-at-21-39-51.png)](https://postimg.cc/kRNctQM9)

The next step is to add the Shebang ( `#!bin/bash`) in the  `test.sh` file followed by the line of code as shownn below:



[![Screenshot-2025-04-25-at-15-59-37.png](https://i.postimg.cc/W47GvzRN/Screenshot-2025-04-25-at-15-59-37.png)](https://postimg.cc/WDhFm2bC)

```bash
#!/bin/bas
cut -d: -f1,6 /etc/passwd
```
**Explanation**:  

- `#!/bin/bash`: This tells the system what interpreter to use in executing the file.
- `cut`: A command-line utility to extract sections from lines of text.
- `-d`: This tells `cut` to use `:` as the delimiter (which is how `/etc/passwd` fields are separated).
- `-f1,6` selects the **username (field 1)** and **home directory (field 6)**.
- `/etc/passwd`: This file contains user account information, with each line structured like this:  
`username:password:UID:GID:GECOS:home_directory:shell`

To run the bash file, we need to give it an execute permission using `chmod +x list_users.sh` command as show below:
[![Screenshot-2025-04-30-at-21-45-57.png](https://i.postimg.cc/ZK01KBHY/Screenshot-2025-04-30-at-21-45-57.png)](https://postimg.cc/RN5Pg022)

Now we can run the script using `./list_users.sh` as shown below:
[![Screenshot-2025-04-30-at-21-49-29.png](https://i.postimg.cc/vmzs6RVG/Screenshot-2025-04-30-at-21-49-29.png)](https://postimg.cc/DW8DtM6N)

**Expected output**:
```
root:/root
daemon:/usr/sbin
nobody:/nonexistent
```
**Screenshoot of Output**:

[![Screenshot-2025-04-30-at-21-50-59.png](https://i.postimg.cc/6pL9X4zj/Screenshot-2025-04-30-at-21-50-59.png)](https://postimg.cc/DS0VQZ9L)

Note: Some accounts like `_apt`, `nobody`, `messagebus`, `syslog` or `mysql` have `/nonexistent` as their home directory because the are **system users**, and not intended to log in interactively.

**Source**:  
- [Linux man pages - `cut`](https://man7.org/linux/man-pages/man1/cut.1.html)

---
 
## Question 2: Git Commit Graph - Reconstructing Command Sequence

The commit graph below illustrates a typical Git workflow involving branching, committing, merging, and post-merge development. 


[![git-history-v3.png](https://i.postimg.cc/BZpS8nz1/git-history-v3.png)](https://postimg.cc/4nKkqssJ)

Below is a command sequence that could have generated this graph:
```bash
# 1. Initialize the repository and make initial commits
git init
echo "first" > file.txt
git add file.txt
git commit -m "first commit"

echo "second" >> file.txt
git commit -am "second commit"

echo "third" >> file.txt
git commit -am "third commit"

# 2. Create and switch to feature branch
git checkout -b feature-branch

echo "feature" >> file.txt
git commit -am "awesome feature"

# 3. Switch back to main and merge feature-branch
git checkout main
git merge feature-branch

# 4. Final commit after merge
echo "final changes" >> file.txt
git commit -am "fourth commit"
```
Using the command `git log --graph --all --decorate`, we can visualise the branches and merges in this git commit graph as show below: 

[![Screenshot-2025-05-01-at-16-41-32.png](https://i.postimg.cc/5NDqs6SH/Screenshot-2025-05-01-at-16-41-32.png)](https://postimg.cc/ykXZd65B)


**Explanation**:  
- `git checkout -b feature-branch` creates a new branch from the third commit on `main`.
- A new commit labeled "awesome feature" is made on this branch.
- The branch is then merged back into `main`.
- Finally, a new commit ("fourth commit") is added to `main`.

**Source**:  
- [Github for Developers](https://githubtraining.github.io/training-manual/#/09_merging_pull_requests)


---

## Question 3: Blog Post – What is Git and What Can It Do for You?

#### Version Control with Git: A Developer’s Best Friend

If you're stepping into the world of coding, development, or any kind of collaborative project, **Git** is a name you’ll hear a lot. But what exactly is it, and why is it so essential?

---

##  What is Git?

**Git** is a free and open-source **version control system**. That’s a fancy way of saying it helps you:

- Track changes in your code or files  
- Work with multiple versions of a project  
- Collaborate with others without overwriting each other's work  

It was originally created by **Linus Torvalds** (the same person behind Linux) back in 2005.

---

## How Does Git Work?

Git stores information as a **snapshot** of your entire project. Each time you make changes and save them (a.k.a. *commit*), Git takes a snapshot and allows you to return to it later.

You typically interact with Git using the terminal, with commands like:

```bash
git init
git add .
git commit -m "Initial commit"
git push
```

---

## What Can Git Do for You?

### 1. **Never Lose Work Again**
With Git, every change is logged. You can go back in time and restore a previous version of your project.

### 2. **Work with Others Smoothly**
You and your teammates can work on the same files, even at the same time. Git will help you merge changes and resolve conflicts if needed.

### 3. **Experiment Without Fear**
Create branches to try new ideas. If something breaks, you can easily switch back to the working version.

### 4. **Deploy and Automate**
Git integrates with services like **GitHub**, **GitLab**, and **Bitbucket** to automate testing, deployment, and even documentation.

---

## Git vs GitHub (and Friends)

Git is the *tool*. GitHub, GitLab, and Bitbucket are **platforms** that host Git repositories online, adding features like:

- Issue tracking  
- Pull/Merge Requests  
- CI/CD pipelines  
- Collaboration tools  

---

## Getting Started with Git

Here’s how you can start using Git on your machine:

```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Create a new repo
mkdir my-project && cd my-project
git init
```

Then just start coding! 

---

## Sources

- [git-scm.com](https://git-scm.com/) — The official Git documentation  
- [GitHub Docs](https://docs.github.com/)  
- Personal experience and examples from developer best practices

---

##  AI Attribution

This blog post was generated with the help of **ChatGPT**, prompted with:

 *"Generate a markdown formatted blog post – What is Git and What Can It Do for You?"*

All content was reviewed and edited for clarity and accuracy by the author.

---




 
## Question 4: Debugging Experience – CI Pipeline Failing Due to Incorrect Runner Tags

A customer reached out reporting that their GitLab CI/CD pipeline was stuck in a “Pending” state and wouldn’t start executing. This was blocking their deployment workflow and causing team delays.

#### **Investigation**

I began by reviewing the `.gitlab-ci.yml` file to verify the pipeline configuration. I noticed that the job in question specified a `tags:` key:

```yaml
deploy_job:
  stage: deploy
  script:
    - ./deploy.sh
  tags:
    - prod-runner
```

The use of the `prod-runner` tag implied that the job required a specific GitLab Runner with that tag. I then navigated to the **Admin Area > Runners** section to cross-check available runners and their tags.

There were no runners registered with the `prod-runner` tag. The available shared runners had different tags — or none at all — which explained why the job was pending: no eligible runner could pick it up.

#### **Resolution**

I provided the customer with two options:
1. **Update the Runner**: Tag their existing GitLab Runner with `prod-runner` to match the job requirements.
2. **Update the CI Configuration**: Remove or change the `tags:` entry in the `.gitlab-ci.yml` file to match an available runner.

They opted to tag an existing runner appropriately. Once that was done, the next pipeline ran successfully.

#### **Tools and Resources Consulted**
- GitLab UI: *Admin Area > Runners*
- GitLab Documentation: [GitLab Runner Tags](https://docs.gitlab.com/ci/yaml/#tags)
- GitLab CI/CD Docs: [`.gitlab-ci.yml` syntax reference](https://docs.gitlab.com/ee/ci/yaml/)
- Git & Github Tutorial: [Git & Github Tutorial by Net Ninja ](https://www.youtube.com/watch?v=3RjQznt-8kE&list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR)
- AI Tool: ChatGPT (OpenAI GPT-4)  
  - **Prompt used**: *"Create a simple CI/CD debuggable script involving GitLab runners and pipeline tags, in the deploy stage."*

#### **Takeaway**

This experience reinforced how important clear documentation and matching runner configurations are in CI/CD workflows. It also highlighted the need to educate customers about how GitLab runners and tags interact, especially in shared or hybrid environments.

