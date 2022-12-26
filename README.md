# HowtoGithub
Basic Myself knowledge About Git to do Push commit edit files.

# Basic

To Configure username and email:
```
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```
To view current Status on current local session happening.
```
git status
```
To clone a repo 
```
git clone <urlofrepo>
```
## After making changes

And all file which edited recently:
```
git add --all
```
Write a message about changes made:
```
git commit -m "CommitPurposeMessage"
```
To upload all file to github
```
git push -u origin main
```


# To create github pages : 
Refer : https://pages.github.com/


# local to remote in cli:

## …or create a new repository on the command line
```
echo "# sfr" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/iamvk1437k/sfr.git
git push -u origin main
```
## …or push an existing repository from the command line
```
git remote add origin https://github.com/iamvk1437k/sfr.git
git branch -M main
git push -u origin main
```

# AddLicenceForExistRepo
 If you release it with a license, you allow people to use it as the licence describes. You can't just say "no I changed my mind I don't want it to be under GPL". Of course your future release may be in another license (GPL forces other people's modified versions to be GPL, but you, as the creator, may release new versions of your work under a new license).

Amendment
Websites like choosealicense.com may help you to choose a suitable license. The license picker provides some templates that can be committed to your repository; for an existing repository you can bring it back this way:

* browse to your repository at GitHub.com
* create a new file by pressing the blue + icon (updated to: New File button)
* name it LICENSE.md or LICENSE.txt to show up the license picker again
* choose a template

| [Reference](https://stackoverflow.com/questions/20243214/how-to-change-the-license-for-a-project-at-github) |

# How to configure automatic password handling for git commands


Setting the credential.helper config option to store should definitely do what you're asking for. You'll still have to enter your username and password at least once for [git-credential-store](http://git-scm.com/docs/git-credential-store) to store it in a file (~/.git-credentials by default), but then you shouldn't need to anymore.

Note that the file storing your credentials won't be encrypted and anybody managing to read it would then get the user's permissions on the repository, so it might a good idea to set up a read-only user especially for this and not globally set the credential.helper config option to store.

If you're using a web interface to your repository (Github, Bitbucket, Gitlab, etc), you might also have the (preferred, imho) possibility to set up a SSH deploy key through the repository settings to provide secure, read-only access.

| [Reference](https://superuser.com/questions/812931/how-to-configure-automatic-password-handling-for-git-commands) |


## Dev = 1'43
This guide is maintained by [**1437k**](https://github.com/iamvk1437k).

[![1437k](https://github.com/iamvk1437k.png?size=100)](https://github.com/iamvk1437k) |
--- |
[1437k](https://github.com/iamvk1437k) |

## License

[GNU GENERAL PUBLIC LICENSE](./LICENSE)
