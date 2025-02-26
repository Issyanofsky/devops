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

git reset --soft/hard/mixed HEAD~2 - undo changes by moving the current HEAD (and possibly the index and working directory) to a specific state.

git revert <commit_hash> - undo changes without disrupting others.
  
