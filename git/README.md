<div align="center">

# **Git**

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

    
