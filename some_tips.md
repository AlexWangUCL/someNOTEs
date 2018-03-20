## 1. error: src refspec master does not match any.
error message:
```
error: src refspec master does not match any.
error: failed to push some refs to 'git@github ... .git'
```
and it solved by executing the following commands:
```
touch README
git add README

git add (all other files)
git commit -m 'reinitialized files'
git push origin master --force  # <- caution, --force can delete others work.
```
That's it, hope this helps. From [here](https://stackoverflow.com/questions/4181861/src-refspec-master-does-not-match-any-when-pushing-commits-in-git).