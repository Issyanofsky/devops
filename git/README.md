<div align="center">

# **Git**

![Git](./pic/git.gif)
</div>

## clone
  git clone https:/...<repository address> 
  sync folder (local) to the git repository

## add
  git add . 
  add files (and folders) to be sync to the trpository

## status
  git status
  show files (folder) that witing to be sync.

## commit
  git commit -m "<some text>"
  commit the changes to git with a description

## push
  git push 
  git push - u origin <branch name> - push the files to a specific branch

## merge
  git merge <branch> <second branch>
  merge branches

## pull
  git pull origin <branch-name>
  pull to the folder (local) from a specific branch

# branches
  git branch - display a list of all branches in the repository, with an asterisk (*) next to the currently active branch.
  
  git branch -a - lists all branches in the Git repository, both local and remote. 
  
  git branch <branch-Name> - create branch
  
  git checkout <branch-Name> - switch branches.
  
  git switch <branch_Name> - switch branches (like checkout - new command).
  
  git diff - show the differences between files in your working directory, staged changes, or between commits.

  git branch -f <brance_Name> HEAD~2 - change the branch's reference to a different commit without creating a new branch.

# HEAD

  where you currently are in your repository history.
  
  git checkout HEAD~1 - The parent commit of the current commit.

    (git diff HEAD~1 HEAD)
  
    (git reset --hard HEAD~1) - Reset HEAD (undo the last commit).

    (git reset --soft HEAD~1) - keep changes in your working directory but move HEAD to an earlier commit.

## reset

  git reset --soft/hard/mixed HEAD~2 - undo changes by moving the current HEAD (and possibly the index and working directory) to a specific state.

## revert

  git revert <commit_hash> - undo changes without disrupting others.
  
## cherry-pick

  git cherry-pick <commit_hash> - merging commit (or range of commit) from one branch to another (add it as a new commit).

## rebase

 main has new commits that you don’t have in your feature-xyz branch, and you want to update your branch with those changes.
 
  git rebase main 

  (git rebase -i HEAD~5) - Clean Up Commit History

## log

  git log - view the commit history of a Git repository.

## Blame

  show what revision and author last modified each line of a file. It helps you track changes, find out who made a specific modification, and investigate the history of a file.

  git blame <file>

## clean  

   used to remove untracked files or directories from your working directory. This is helpful when you want to clean up files that are not being tracked by Git but are still present in your local repository (e.g., temporary build files, editor backups, or other files that are not part of the version-controlled project).

   git clean [options]

  (git clean -f) - remove untracked files (not directories).

  (git clean -fd) - remove untracked directories as well.

## bisect

  ommand used to help you find the commit that introduced a bug or issue in your code. It uses a binary search algorithm to efficiently narrow down the problematic commit by testing a series of commits.

  bisect works:

    git bisect start - Start the Bisect Process: You tell Git which commit is "good" and which one is "bad."
    git bisect bad <bad_commit>   # Bad commit (where the bug exists)
    git bisect good <good_commit> # Good commit (where everything worked)
    ......
      git bisect good/bad
    ......
    git bisect reset - End the Bisect Process. This will return you to your original working branch and state 
  

# GitHub CI

  method - testing, security, build images (packaging). all kind of test and packaging of the code.

  after passing the CI phase the process can continue to the CD stage (production).

  ## GitHub Action 

    allows you to automate workflows like testing, building, and deploying your code directly from a GitHub repository.

    location: .github/workflows 

    type: YAML file type.

    ## Workflow syntax and structure

      [YAML]
      name: workflow name (optional).
      on: the event that trigger the workflow (push, pull...)
      jobs: a list of jobs running
      steps: a list of steps within the job.

      ## example 

      name: Python CI
      
      on:
        push:
          branches:
            - main  # Trigger the action when there is a push to the `main` branch
          pull_request:
            branches:
            - main  # Trigger when a pull request is made to the `main` branch

    jobs:
      test:
        runs-on: ubuntu-latest  # Use the latest Ubuntu image for the runner

        steps:
        #Step 1: Checkout the code from the repository
          - name: Checkout code
            uses: actions/checkout@v2

        #Step 2: Set up Python
          - name: Set up Python
            uses: actions/setup-python@v2
            with:
              python-version: '3.8'  # Set Python version

        #Step 3: Install dependencies
          - name: Install dependencies
            run: |
              python -m pip install --upgrade pip
              pip install -r requirements.txt  # Install dependencies from `requirements.txt`

        #Step 4: Run tests
          - name: Run tests
            run: |
            pytest  # Run your tests using pytest or any other test framework

## Triggers and Events

  events or actions that cause a workflow to run.

  - push - Runs when a commit is pushed to a branch.
  - pull_request - Runs when a pull request is created, synchronized, or reopened.
  - workflow_dispatch - Allows you to manually trigger a workflow.
  - schedule - Runs workflows on a schedule (similar to a cron job).
  - release - Runs when a release is published, created, or deleted.
  - create - Runs when a new branch or tag is created.
  
## jobs & Runners

  Runner - the environment (or machine) where the jobs run.

    jobs:
      test:
        runs-on: ubuntu-latest  # This job runs on a GitHub-hosted runner with Ubuntu

  Jobs - set of steps that execute as part of a workflow.

    jobs:
      test:
        runs-on: ubuntu-latest  # The job runs on a GitHub-hosted runner with Ubuntu
        steps:
          - name: Checkout code
            uses: actions/checkout@v2  # Step 1: Checkout the code
          - name: Install dependencies
            run: |
              python -m pip install --upgrade pip
              pip install -r requirements.txt  # Step 2: Install dependencies
          - name: Run tests
            run: pytest  # Step 3: Run tests using pytest

## need

  used to control the order in which jobs run within a workflow. It allows you to specify dependencies between jobs, meaning that one job should only run after another job has successfully completed.

  refer to another job in the workflow (will execute only if another job as accomplished).

## step & Actions

  steps - a single task that is part of a job in a GitHub Actions workflow. 

  Action -  reusable block of code or a pre-built functionality that can be used within a step. 
    
    -  uses: actions/checkout@v2  # This uses a GitHub-hosted action to check out the repository code.
    -  uses: actions/setup-python@v2  # This uses a GitHub-hosted action to set up a Python environment.
    -  uses: actions/github-script@v5  # This uses a GitHub-hosted action to run a custom script.
    

## Environment Variabls 

  Default Environment Variables (provided by GitHub): 

    - GITHUB_REPOSITORY - The name of the repository.
    - GITHUB_ACTOR - The username of the person who triggered the workflow.
    - GITHUB_REF - The branch or tag that triggered the workflow (e.g., refs/heads/main).
    - GITHUB_SHA - The commit SHA that triggered the workflow.
    - RUNNER_OS - The operating system of the runner (e.g., Ubuntu, Windows).

  Custom Environment Variables (User-Defined):
    
    jobs:
      build:
        runs-on: ubuntu-latest
        env:  # Define environment variables at the job level
          MY_VARIABLE: "Hello, World!"
        steps:
          - name: Show environment variable
            run: echo $MY_VARIABLE  # Output: Hello, World!

  Secret Environment Variables:

    Setting and Using Secrets in GitHub Actions:
    To use secrets:

      - Go to your repository's Settings.
      - Navigate to Secrets.
      - Add your secret key-value pair.


# caching Dependencies

  powerful feature in GitHub Actions that helps to speed up workflows by reusing dependencies or other files that do not change frequently. For example, if your workflow involves installing dependencies (e.g., via npm install or pip install), these dependencies do not change unless you update them.

# Notification

  set up notifications to alert you or your team members about the status of your workflow runs, such as when a job succeeds, fails, or completes. Notifications can be sent through various channels such as email, Slack, or other integrated services.


# Debugging

  use echo command inside the workflow to debug the process.

    
      - name: Output debug value
        run: echo "Debug Output: ${{ steps.debug-step.outputs.debug_value }}"
