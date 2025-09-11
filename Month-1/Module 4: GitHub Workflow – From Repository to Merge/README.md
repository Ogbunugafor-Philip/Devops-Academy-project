# Module 4: GitHub Workflow – From Repository to Merge

## Introduction

In collaborative software development, it is important to have a clear workflow that prevents code conflicts, ensures quality, and makes teamwork smoother. GitHub provides an industry-standard process where developers create repositories, document them with a README file, work on separate branches, and submit Pull Requests (PRs) for review before merging changes into the main branch. This project introduces students to this fundamental GitHub workflow, which is the backbone of modern DevOps and software engineering practices.

## Statement of Problem
Without a structured workflow, developers often overwrite each other’s work, lose track of changes, and introduce errors into the main codebase. Many projects fail because there is no documentation, no process for reviewing code, and no method to keep the project history clean. To solve this, teams need a process where:

- The repository serves as the single source of truth,
- Documentation provides guidance to all contributors,
- New features and fixes are developed in isolated branches, and
- Pull Requests enforce reviews before changes are accepted.

This project addresses these problems by teaching a step-by-step GitHub workflow from repository creation to merging contributions.

## Objectives
i.	To create a GitHub repository with a structured README that describes the project.

ii.	To practice using branches for feature development without affecting the main branch.

iii.	To use Pull Requests (PRs) as a mechanism for reviewing and approving code changes.

iv.	To merge approved changes into the main branch, ensuring a clean and professional workflow.

## Project Steps
Step 1: Register to Github and Create a Repository

Step 2: Create a Branch

Step 3: Make Changes

Step 4: Open a Pull Request (PR)

Step 5: Review and Merge

Step 6: Understanding Git Commands in the Terminal


## Project Implementation 

### Step 1: Register to GitHub and Create a Repository

Before we can collaborate on code, we need a central place to store it. A GitHub repository serves as the single source of truth where all files, commits, and history are tracked. Creating a repo also gives every contributor a starting point with shared documentation.

- Go to https://github.com and sign up for a free account
  <img width="975" height="287" alt="image" src="https://github.com/user-attachments/assets/f20b67f2-2fde-40fe-b827-89a5191db528" />

 
-Create your free account and then log in into your github
<img width="975" height="320" alt="image" src="https://github.com/user-attachments/assets/b70c05df-600c-4d96-9d20-16e4c28be729" />


- Once logged in, click the “+” button → New repository
  <img width="975" height="397" alt="image" src="https://github.com/user-attachments/assets/8ffb213a-6ac0-472c-b42b-3462931c3724" />

 
- Give your repository a name (e.g., github-workflow-demo)
  <img width="933" height="276" alt="image" src="https://github.com/user-attachments/assets/3dfbc760-3fb0-4f13-ad74-23c026838ff0" />

 
- Add a description (optional, but recommended)
  <img width="975" height="132" alt="image" src="https://github.com/user-attachments/assets/5a3ea34a-3de8-4e79-8f54-2334e5048d79" />

 
- Check “Add a README file” so the repository has an initial document
 <img width="975" height="308" alt="image" src="https://github.com/user-attachments/assets/5101c542-1202-471b-91b1-6392a68984fc" />


- Click Create repository
  <img width="975" height="282" alt="image" src="https://github.com/user-attachments/assets/fa48350f-4e4e-4785-a90e-3d78c701f9d9" />

  
 


### Step 2: Create a Branch

Branches allow us to work on new features without touching the main codebase. This prevents mistakes from breaking the main branch and makes it easier to isolate, test, and review changes before merging.

- In your repository, open the branch dropdown (default is main)
  <img width="975" height="296" alt="image" src="https://github.com/user-attachments/assets/c0ea1bd0-ce5c-44f9-b3dc-a8685e25093e" />

 

- Type the name of a new branch, e.g., feature-update-readme
  <img width="611" height="248" alt="image" src="https://github.com/user-attachments/assets/fb10f325-1589-42a4-b33c-8a300927e0ff" />

 
- Click Create branch.
  <img width="794" height="427" alt="image" src="https://github.com/user-attachments/assets/80e3b164-d353-42a2-96a7-48e4dff4983a" />

 


## Step 3: Make Changes
Now that we’re on a branch, we can safely edit files or add new ones without affecting the main project. This keeps experiments and new features separate until they’re ready.

- On your new branch, open the README.md file.
  <img width="975" height="293" alt="image" src="https://github.com/user-attachments/assets/8c1a5b41-a26d-48fc-9122-d8ce1263bd68" />
 
- Click the pencil ✏️ icon to edit the file
  <img width="975" height="366" alt="image" src="https://github.com/user-attachments/assets/b3d284dd-f0a2-4046-833e-fb2d468a3d11" />

 
- Add a line such as: “This is an update made from the feature branch”
  <img width="822" height="355" alt="image" src="https://github.com/user-attachments/assets/391fdf41-b19b-43f2-815e-dd81e748cf76" />

 

- Write a commit message (e.g., Updated README with feature branch note)
  <img width="975" height="196" alt="image" src="https://github.com/user-attachments/assets/f6e57590-98d1-4d14-bfea-22a583a02bb1" />

 
- Make sure Commit directly to the feature-update-readme branch is selected. Click Commit changes.
  <img width="706" height="372" alt="image" src="https://github.com/user-attachments/assets/634ad632-e0b4-4bf8-980d-b314f39931eb" />


 

### Step 4: Open a Pull Request (PR)

Pull Requests are a way to propose changes and get feedback before merging them into the main branch. This step allows for review, discussion, and quality control, which are all standard practices in real-world teams.

- After committing, GitHub will suggest opening a Pull Request. Click Compare & pull request.
  <img width="975" height="235" alt="image" src="https://github.com/user-attachments/assets/d7394d8b-a1ef-4d01-9fc2-78467941937c" />



- Add a title (e.g., “Update README from feature branch”).
- <img width="975" height="126" alt="image" src="https://github.com/user-attachments/assets/079ad53b-7d76-4219-b702-43410580a83c" />

 
- Write a short description of what you changed
 <img width="975" height="228" alt="image" src="https://github.com/user-attachments/assets/77b0c736-dc52-46c5-aded-0abcdbf0cce3" />


- Review the differences between your branch and the main branch

- Click Create Pull Request
 

### Step 5: Review and Merge

Merging is the final step that brings your branch changes into the main codebase. Reviewing first ensures that mistakes are caught early, and merging keeps the history clean and traceable.

- Open your Pull Request
 <img width="975" height="341" alt="image" src="https://github.com/user-attachments/assets/7b5530f4-2b49-4769-a9e9-234b5e8c7e93" />


- Review the changes (or ask a teammate to review)

- Once satisfied, click Merge pull request
 <img width="975" height="448" alt="image" src="https://github.com/user-attachments/assets/ab45a2c2-8baa-430d-9cd9-5742c3201cdf" />

- Confirm by clicking Confirm merge
  <img width="975" height="359" alt="image" src="https://github.com/user-attachments/assets/e1d5dba8-5642-4c2a-b946-bbab4b4baa0d" />

 

### Step 6: Understanding Git Commands in the Terminal

While GitHub’s web interface is useful, most DevOps engineers work directly in the terminal. These are the most important Git commands to practice and understand:

- git clone <repository-url> → Download a repository from GitHub to your computer.
- git branch → Show all branches in your project.
- git checkout -b <branch-name> → Create and switch to a new branch.
- git add <filename> → Stage a file for commit.
- git commit -m "message" → Save changes with a description.
- git push origin <branch-name> → Upload your branch and changes to GitHub.
- git checkout <main> → Switch back to the main branch.
- git merge <branch-name> → Merge a feature branch into the main branch.
- git pull origin <main> → Update your local project with the latest changes from GitHub.

## Conclusion
By completing this project, you’ve learned the end-to-end GitHub workflow that underpins modern collaborative development. You now understand how to create repositories, branch off for safe feature development, make commits that document your changes, and open Pull Requests that encourage peer review and maintain quality. Beyond the web interface, you also practiced essential Git commands in the terminal — the true language of DevOps engineers.
This workflow ensures that every project you work on is structured, traceable, and professional. Whether you are working alone or on a large team, following this process helps avoid conflicts, improves code quality, and keeps your history clean. Mastering it is a vital step toward becoming a confident DevOps practitioner ready for real-world projects.

