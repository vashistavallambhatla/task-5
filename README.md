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





