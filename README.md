

1) CHERRY-PICKING 

-> I created a new branch called 'cherry' from the main branch.
-> Switched to that branch and made some changes and commited (git switch cherry or git checkout cherry) 
-> "git add ." followed by "git commit -m 'Cherry branch commit' "
-> Switched back to main branch and cherry picked the "cherry" branch

Results:

(base) vashistavallambhatla@vashistas-Air test % git branch
* cherry
  main
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Cherry-branch-text%                                                                                  
(base) vashistavallambhatla@vashistas-Air test % git checkout main 
Switched to branch 'main'
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Main-branch-text%                                                                                    
(base) vashistavallambhatla@vashistas-Air test % git cherry-pick cherry
[main 7e94552] cherry-commit
 Date: Fri Nov 15 12:20:33 2024 +0530
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) vashistavallambhatla@vashistas-Air test % git branch
  cherry
* main
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Cherry-branch-text% 

2) STASHING AND CLEANING

-> I made changes to the main branch and stashed the changes using "git stash".
-> The changes got stashed temporarily resulting in retreival of commited content.
-> Used "git clean -f" resulting in deletion of untracked files.
-> Used "git stash apply" to get the stashed content back.

(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Commit-text

-> uncomplete text meant to be stashed%                                                              
(base) vashistavallambhatla@vashistas-Air test % git stash 
Saved working directory and index state WIP on main: 2f718e5 stashing and cleaning
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Commit-text%    
(base) vashistavallambhatla@vashistas-Air test % git clean -f
(base) vashistavallambhatla@vashistas-Air test % git stash apply
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file.txt

no changes added to commit (use "git add" and/or "git commit -a")
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Commit-text

-> uncomplete text meant to be stashed%   

4) UNDOING CHANGES 

-> I made changes by doing "echo "Changes made" >> file.txt" in file.txt
-> Staged and committed the changes
-> Used "git revert HEAD" which resulted in a new commit that reverted back to the state before the current commit (Inverse)


(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Prevoius commit %                                                                                    
(base) vashistavallambhatla@vashistas-Air test % echo "Changes made" >> file.txt 
(base) vashistavallambhatla@vashistas-Air test % git add .
(base) vashistavallambhatla@vashistas-Air test % git commit -m "Current commit"
[main 1b2ad51] Current commit
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) vashistavallambhatla@vashistas-Air test % git revert HEAD
[main f32ee54] Revert "Current commit"
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
Prevoius commit % 

5) GIT RESET

-> Created a new commit by changing the file's content from 1 to 2
-> staged and committed the changes
-> Used "git reset --hard HEAD^" which resulted in going back to the previous commit entirely. No new commits were made,only the changes were reversed.

(base) vashistavallambhatla@vashistas-Air test % cat file.txt
1% 
(base) vashistavallambhatla@vashistas-Air test % git add .
(base) vashistavallambhatla@vashistas-Air test % git commit -m '1'
[main 0a65240] 1
 2 files changed, 5 insertions(+), 1 deletion(-)
(base) vashistavallambhatla@vashistas-Air test % echo '2' > file.txt 
(base) vashistavallambhatla@vashistas-Air test % git add .
(base) vashistavallambhatla@vashistas-Air test % git commit -m '2'
[main b1b0593] 2
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) vashistavallambhatla@vashistas-Air test % git log --oneline -n 3
b1b0593 (HEAD -> main) 2
0a65240 1
c2111e3 Three tasks done
(base) vashistavallambhatla@vashistas-Air test % git reset --hard HEAD
HEAD is now at b1b0593 2
(base) vashistavallambhatla@vashistas-Air test % git reset --hard HEAD^
HEAD is now at 0a65240 1
(base) vashistavallambhatla@vashistas-Air test % git log --oneline -n 3
0a65240 (HEAD -> main) 1
c2111e3 Three tasks done
2f718e5 stashing and cleaning
(base) vashistavallambhatla@vashistas-Air test % cat file.txt
1%   

6) GIT SHOW

-> Upon using git show on the HEAD I got back commit metadata (commit hash,branch,    author,date,commit message) and Diff Output compared to parent commit.

(base) vashistavallambhatla@vashistas-Air test % git show
commit 0a6524001857aeeb6000abb614aea212e03a768d (HEAD -> main)
Author: vashista <vashista.vallambhatla@gmail.com>
Date:   Fri Nov 15 12:59:42 2024 +0530

    1

diff --git a/README.md b/README.md
index 968d506..268e1ed 100644
--- a/README.md
+++ b/README.md
@@ -75,6 +75,10 @@ Prevoius commit %
 (base) vashistavallambhatla@vashistas-Air test % cat file.txt
 Prevoius commit % 
 
+5) GIT RESET
+
+
+
 
 
 
diff --git a/file.txt b/file.txt
index 198b443..56a6051 100644
--- a/file.txt
+++ b/file.txt
@@ -1 +1 @@


7) GIT REBASE

-> Used "git rebase -i HEAD~3" to squash three commits together
-> Changed "pick" to "squash" of the commits that were to be squashed in vim
-> Reafactored the commit message as it popped up right after squashing 

(base) vashistas-Air:test vashistavallambhatla$ git reflog
ca9f8a5 (HEAD -> main) HEAD@{0}: checkout: moving from squash to main
95f1518 (squash) HEAD@{1}: rebase (finish): returning to refs/heads/squash
95f1518 (squash) HEAD@{2}: rebase (squash): s1
cc2e828 HEAD@{3}: rebase (squash): # This is a combination of 2 commits.
c516b28 HEAD@{4}: rebase (start): checkout HEAD~3
04f497f HEAD@{5}: rebase (abort): returning to refs/heads/squash
04f497f HEAD@{6}: rebase (abort): returning to refs/heads/squash
04f497f HEAD@{7}: commit: s3
2009f23 HEAD@{8}: commit: s2
c516b28 HEAD@{9}: commit: s1
ca9f8a5 (HEAD -> main) HEAD@{10}: checkout: moving from main to squash

8) REFLOG

-> Used "git reset --hard HEAD^ " to delete a commit.
-> The commit was no longer visible in from git log.
-> Used "git reflog" to get the hash of deleted commit
-> Used "git reset" to get back to the deleted commit.

(base) vashistas-Air:test vashistavallambhatla$ git add .
(base) vashistas-Air:test vashistavallambhatla$ git commit -m 'reflog'
[main 799a041] reflog
 2 files changed, 20 insertions(+), 3 deletions(-)
(base) vashistas-Air:test vashistavallambhatla$ git reset --hard HEAD^
HEAD is now at ca9f8a5 current

(base) vashistas-Air:test vashistavallambhatla$ git reflog
ca9f8a5 (HEAD -> main) HEAD@{0}: reset: moving to HEAD^
799a041 HEAD@{1}: commit: reflog
.
.
.

(base) vashistas-Air:test vashistavallambhatla$ git reset --hard 799a041
HEAD is now at 799a041 reflog





