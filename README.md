CREATING A POST-COMMIT HOOK

1) Created post-commit script under .git/hooks/

2) Wrote the script that adds to commit-log.md once a commit is made,which is as follows

`
#!/usr/bin/env python

import subprocess
from datetime import datetime

commit_message = subprocess.run(
    ["git", "log", "-1", "--pretty=%B"],
    capture_output=True,
    text=True
).stdout.strip()


commit_timestamp = subprocess.run(
    ["git", "log", "-1", "--pretty=%ci"],
    capture_output=True,
    text=True
).stdout.strip()


log_entry = f"### Commit Timestamp: {commit_timestamp}\n{commit_message}\n\n"

with open("commit-log.md", "a") as log_file:
    log_file.write(log_entry)

print("Commit logged successfully.")

`

3) Changed it into a executable using 'chmod +x .git/hooks/post-commit'

4) The commit details were reflected in commit-log.md once a commit was made

Output:
(base) vashistavallambhatla@vashistas-Air test % git commit -m 'updated Readme.md'
Commit logged successfully.
[main 76813d9] updated Readme.md
2 files changed, 1 insertion(+), 1 deletion(-)
create mode 100644 commit-log.md
