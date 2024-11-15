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





