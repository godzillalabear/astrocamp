# git cheatsheet

| command | features |
| --- | --- |
| git status | view now status |
| git add . | move file from working directory to staging area |
| git commit -m"message" | copy file from staging area to repository |
| git log | view hole project record |
| git blame [filename] | view code writer line by line|
| git log -p [filename] | see single file record |
| git branch [branchname] | create new branch |
| git branch | view resent branches |
| git checkout [branchname] | change HEAD branch |
| git checkout [filename] | restore removed file |
| git merge [branchname] | merge two branches |
| git branch -d [branchname] | delete unmerged branch |
| git reset [reference] -mixed | turn to any specific commit (uncommit files go to working directory) |
| git reset [or] -softed | uncommit files go to staging area |
| git reset [branchname] -hard | kill all uncommit files |
| git reflog | view reference record |
| git branch [branchname] [reference] | tag branch on specific commit |
