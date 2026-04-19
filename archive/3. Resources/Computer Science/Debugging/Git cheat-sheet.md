```bash
git checkout SHA-HASH -- file/file-path
```
```
git difftool
```

``git ls-files`` ---------------------- tracked files in git

git rm --cached <file> ------------ to unstage a file

git reset HEAD <file> ------------- to unstage a file without changing the contents of the file

git restore --staged new.txt ------ to unstage a file

git restore new.txt --------------- to restore untracked changes

git mv example.txt demo.txt ------- rename a file

git rm demo.txt ------------------- delete a file

git add -u ------------------------ add updated to staging area

git add -A ------------------------ add all

git merge feature-branch ---------- merge any branch to current branch

git branch -d feature-branch ------ delete an existing branch

git checkout -- <file>

git checkout -b feature-branch

git config --global alias.hist "log --oneline --graph --decorate --all" ------ alias

git config --global --list

git log --oneline --graph --decorate --all ---------- logs

git tag <tag-name> ---------------- give tag name

git tag -d <tag-name> ------------- delete a tag anme

git tag -a <tag_name> -m "Commit Message"

  

git reset <commit id> --hard ----- Changes head and removes files

git reset <commit id> --mixed ---- Changes head and unstages

git reset <commit id> --soft ----- Changes head

  

git stash ------------------------- create a stash

git stash pop

git stash list

  

git remote add origin https://github.com/viraj20/demo.git -- add a remote repository

git remote -v --------------------------------------------- check remote repository

  

git push -u origin master --tags --------------------------- to push changes to remote repo

  

ssh-keygen -t rsa -C "virajbharvada20@gmail.com"

git fetch

git pull

git show <commit_id>

  

git remote set-url <name_of_the_repo> <url_of_the_repo>

git remote show <name_of_the_repo>