# Intro git
Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"


$ git status

#To view current Status on current local session happening.

$ git clone <urlofrepo>

#Clone a Autorized repo to make changes

#After making changes

$ git add * ; git add --all

#Add all file to commit

$ git commit -m "CommitPurposeMessage"

#Write a Message About commit

$ git push -u origin main

finally push or upload all 

To create github pages : 
Ref : https://pages.github.com/


#local to remote in cli:

…or create a new repository on the command line

echo "# repo-name" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/username/repo-name".git
git push -u origin main

…or push an existing repository from the command line

git remote add origin https://github.com/username/repo-name".git
git branch -M main
git push -u origin main
