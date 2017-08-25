## Step-by-step guide

Command | Description
---     |---
git checkout develop | get the work of all developers ... 
git pull | … from the remote repository
git branch myFeature | create a new feature branch ...
git checkout myFeature | … and start working with it. code in eclipse, write tests, ... . if you have made changes in any javascript file, don't forget to run >> build.py << to make your changes available in the compressed version of our javascript files.
git status | list all files, that have been created, modified or deleted
git add <file1> <file2> | add one or more files for a commit. "add ." add all files. "add -u" add all modified files
git commit -m "reasonable message" | commit it into the local feature branch. coding, adding, committing may happen many times. All changes are local. | now everything is committed, the work is done, others should take advantage of your work
git checkout develop | you need to know, what others have done since your branch. Thus: get their work ...
git pull | … from the remote repository. No problem here.
git checkout myFeature | you have to check, whether work of others conflicts with your work
git rebase develop | this is the crucial part. Read the comment about rebasing! We assume, that the rebase finished successfully. Run all unit tests. If errors pop up, goto *
git checkout develop ; git merge myFeature | Hurry to checkout develop and merge your changes. If the rebase terminated with "fast forward", there should be no problem. The merge will terminate with "fast forward", too.
git push | push it to the remote repository
git branch -d myFeature | delete your feature branch. You may save it, protoype something with it. Don't care. Your work is saved in "develop".

### The benefit of rebasing

Consider the following situation: you have got all resources from the common remote repository you start to change resources to implement your new feature but other devloper do the same sometimes they are faster than you and push their changes to the common remote repository before you do. now you have a problem: is there a conflict between their work and your's?

In this situation you would consider it a big advantage, if you had started your work after the other developers had pushed their changes. Thus you may ask the question: when I would apply my changes (i.e. my commits) on top of the actual develop branch, do conflicts arise or are my changes and the changes of the others compatible?

Exactly this question is answered by the command "git rebase develop". You are working in your branch "myFeature". GIT returns to a common ancestor commit of both branches (that must exist!), saves all changes you have committed in your branch "myFeature". Then it takes the branch "develop" and applies your changes one after the other. There are two outcomes:

   + no didn't change something that the other developers changed and the other developers didn't change anything you changed.
   + you are lucky, nothing to remedy
   + GIT says "fast forward" to express that.
   + you will get accustomed to feel lucky when you read "fast forward"
   + your branch "myFeature" is rebuild in a way, that it originates from the current develop
   + the other developers and you changed the same resource
       + GIT complains about a conflict
       + use the merge-tool builtin into eclipse to solve the conflict by copying, ignoring or editing the resources one after the other
       + then commit your edit. This will complete the rebase. You have solved the problem.
       + now your branch originates from the current develop, too.

If you have rebased or merged branches, do not forget to run all tests! Really.