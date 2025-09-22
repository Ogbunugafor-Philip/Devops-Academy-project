# Module 5_Track Tasks with GitHub Projects (with Git Terminal Integration)

## Introduction
In real-world DevOps practice, version control and task management go hand-in-hand. GitHub provides a powerful platform that combines source code management with project tracking through GitHub Projects. While many beginners start by using GitHub’s web interface to commit changes, create issues, and manage boards, DevOps engineers are expected to master Git commands directly in the terminal.
This project teaches how to track tasks with GitHub Projects while simultaneously reinforcing Git command-line operations such as git clone, git add, git commit, git push, and git pull. By integrating task tracking with hands-on Git terminal usage, learners will gain the confidence to manage projects professionally — just like in enterprise DevOps environments.

## Statement of Problem
Many beginners rely heavily on GitHub’s web interface without understanding the underlying Git commands. This creates several challenges:

- Limited practical readiness: Depending only on web clicks leaves learners unprepared for real-world DevOps, where terminal commands like clone, branch, push, and pull are essential.
- Poor workflow and automation skills: Without practicing Git in the terminal, students fail to connect task tracking with version control and miss the foundation needed for scripting and CI/CD pipelines.

This project addresses these issues by combining GitHub Projects (for task tracking) with Git terminal usage (for version control).

## Objectives
- To create and configure a GitHub repository as the foundation for version control.
- To clone the repository locally and establish a working connection between the local machine and GitHub.
- To practice essential Git terminal operations (clone, add, commit, push, pull) in a real project.
- To build confidence in managing beginner DevOps projects using GitHub and the terminal.

## Project Steps

i.	Set up a GitHub Repository

ii.	Clone the Repository Locally

iii.	Perform Git Operations via Terminal



## Project Implementation

### Step 1: Set up a GitHub Repository
To begin, you need a GitHub repository that will serve as the central location for your project’s code and documentation. Initializing it with a README.md provides a starting point and ensures the repository is not empty. In our last project, we learnt how to create and log on to github repository.

- Log in to your github, click the “+” button → New repository
  <img width="975" height="397" alt="image" src="https://github.com/user-attachments/assets/0ed4a4e8-c8cc-4cac-8659-3684b031f2c5" />

 
- Give your repository a name (e.g., github-workflow-demo)
  <img width="933" height="276" alt="image" src="https://github.com/user-attachments/assets/7233de77-23cc-4e5b-aa22-912c84b59cfe" />

 
- Add a description (optional, but recommended)
  <img width="975" height="132" alt="image" src="https://github.com/user-attachments/assets/be78d932-9484-4676-9249-dbe60c760fab" />

 
- Check “Add a README file” so the repository has an initial document
  <img width="975" height="246" alt="image" src="https://github.com/user-attachments/assets/e6444682-91a6-48bc-87bd-617f66673420" />

 

- Click Create repository
  <img width="975" height="282" alt="image" src="https://github.com/user-attachments/assets/27fa694f-5a11-44ba-b913-d10412e045be" />

 

### Step 2: Clone the Repository Locally
Cloning a repository means creating a local copy of the GitHub repository on your computer. This is important because real-world DevOps engineers rarely edit code directly on GitHub’s website. Instead, they work from their local development environment, use Git commands in the terminal, and then synchronize changes back to GitHub. Cloning establishes the link between your local system and the remote repository, allowing you to perform operations such as git add, git commit, git push, and git pull.

- Go to your repository on GitHub
  <img width="974" height="322" alt="image" src="https://github.com/user-attachments/assets/54501efa-ef2e-49e3-a9cd-8f99f2638b2a" />

 - Click the green Code button.
   <img width="975" height="304" alt="image" src="https://github.com/user-attachments/assets/7d0fcedf-b013-4786-8ad1-6fabf9966c43" />

 
- Choose HTTPS and copy the repository link.
  <img width="562" height="214" alt="image" src="https://github.com/user-attachments/assets/9b264cd7-7f38-441b-ad46-ffdf9e6eac91" />

 
- On your local machine, open your Git Bash
  <img width="940" height="215" alt="image" src="https://github.com/user-attachments/assets/abb925ac-d171-4c14-88d7-fc2907e82274" />

 
- Use the git clone command followed by the repository URL you copied.
  ``` bash
  git clone https://github.com/Ogbunugafor-Philip/github-workflow-demo.git
 ``
<img width="975" height="336" alt="image" src="https://github.com/user-attachments/assets/e41e7b03-64de-4e85-9723-5ff4e5b2f48a" />
 

### Step 3: Perform Git Operations via Terminal

Once the repository has been cloned locally, the real DevOps practice begins. Engineers don’t rely on GitHub’s web interface for everyday work; instead, they use Git commands in the terminal. These commands control the entire workflow: adding new files, committing changes, pushing updates to GitHub, and pulling the latest code from the remote repository. By practicing these operations, learners gain confidence in managing source code directly from the terminal, just like in enterprise environments.

- Navigate into the Repository. Run;
```bash
cd github-workflow-demo
``` 
<img width="975" height="234" alt="image" src="https://github.com/user-attachments/assets/ba8ab651-1a60-42ab-bf90-0dab9c227f44" />

- To check Repository Status (See which files are new, modified, or staged), run;
```bash
git status
```
 <img width="975" height="279" alt="image" src="https://github.com/user-attachments/assets/4e8e7822-28f4-4573-9696-3cfd87a78ca8" />


- Create a new file named notes.txt and paste a sentence in it. Run;
```bash
echo "This is my first DevOps Academy Git operation." > notes.txt
``` 
<img width="975" height="196" alt="image" src="https://github.com/user-attachments/assets/59de7ac1-882d-4cfd-90d9-0edaddd144f0" />


- Stage the File notes.txt just created. Run;
```bash
git add notes.txt
```
<img width="975" height="142" alt="image" src="https://github.com/user-attachments/assets/650fada0-2bfa-4f9c-93f6-480b8902e864" />

- Commit the Changes. Save changes locally with a descriptive message. Run;
```bash
git commit -m "Added notes.txt with first message"
```
<img width="975" height="151" alt="image" src="https://github.com/user-attachments/assets/e1644020-cd44-4f3b-9229-7a21205fcc3a" />


- Push Changes to GitHub. Send your local commits to the remote repository. Run;
```bash
git push origin main
``` 
<img width="975" height="248" alt="image" src="https://github.com/user-attachments/assets/0ee34021-394a-4813-8415-bdd2485eba62" />

- Pull Updates from GitHub. If someone else made changes (or you updated from GitHub web), pull the latest updates. Run; 
```bash
git pull origin main
```
<img width="975" height="233" alt="image" src="https://github.com/user-attachments/assets/6aec4e6b-4ce1-4b25-bba2-24417e8b2ef3" />



	

## Conclusion
This project has demonstrated how DevOps engineers can effectively combine task tracking with GitHub Projects and hands-on Git terminal operations. By setting up a repository, cloning it locally, and performing essential Git commands (git add, git commit, git push, git pull), learners have experienced the real workflow used in enterprise environments.
For beginners, this module builds the foundation for:

- Working confidently with Git in the terminal.
- Keeping project tasks organized and connected to real version control actions.
- Understanding how professional DevOps workflows bridge planning (boards) and execution (Git commands).

With this knowledge, students are better prepared to manage projects independently and are one step closer to advanced DevOps practices like branching strategies, collaboration workflows, and CI/CD automation.





