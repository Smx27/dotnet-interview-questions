1. **What is Git, and why is it used in software development?**

   - **Answer:** 
     - Git is a distributed version control system used for tracking changes in source code during software development.
     - It allows multiple developers to collaborate on a project simultaneously, track changes, manage versions, and merge code changes efficiently.

2. **What is the difference between Git and other version control systems like SVN or CVS?**

   - **Answer:** 
     - Unlike centralized version control systems like SVN or CVS, Git is distributed, meaning that every developer has a complete copy of the repository, including the entire history of changes.
     - Git provides better performance, scalability, and offline capabilities compared to centralized systems.
     - Git offers powerful branching and merging capabilities, allowing for more flexible and efficient collaboration workflows.

3. **Explain the difference between Git's staging area (index) and working directory.**

   - **Answer:** 
     - The working directory is where you modify and create files for your project.
     - The staging area (index) is a temporary space where you prepare changes before committing them to the repository.
     - Files in the working directory are initially untracked, but you can stage them for inclusion in the next commit using the `git add` command.

4. **What is a Git repository, and how do you create one?**

   - **Answer:** 
     - A Git repository is a collection of files and directories tracked by Git, along with metadata about the project's history and changes.
     - You can create a Git repository by running the command `git init` in the root directory of your project.

5. **What is a Git branch, and why is branching important in Git?**

   - **Answer:** 
     - A Git branch is a separate line of development that diverges from the main codebase (usually the `master` branch).
     - Branching allows developers to work on features, bug fixes, or experiments in isolation without affecting the main codebase.
     - Branches can be merged back into the main codebase when the changes are complete and tested.

6. **How do you create and switch between Git branches?**

   - **Answer:** 
     - To create a new branch, you use the `git branch <branch_name>` command.
     - To switch to an existing branch, you use the `git checkout <branch_name>` command.
     - Alternatively, you can create and switch to a new branch simultaneously using the `git checkout -b <branch_name>` command.

7. **What is a Git merge, and how do you perform a merge operation?**

   - **Answer:** 
     - A Git merge is the process of combining changes from one branch (the source branch) into another branch (the target branch).
     - You perform a merge operation using the `git merge <source_branch>` command while on the target branch.

8. **Explain the difference between a Git merge and a Git rebase.**

   - **Answer:** 
     - A Git merge combines the changes from one branch into another branch, creating a new merge commit that preserves the history of both branches.
     - A Git rebase rewrites the commit history of the current branch by replaying each commit on top of another branch, resulting in a linear history without merge commits.

9. **What is a Git remote, and how do you add and manage remote repositories?**

   - **Answer:** 
     - A Git remote is a pointer to a remote repository, typically hosted on a server or code hosting platform like GitHub or GitLab.
     - You can add a remote repository using the `git remote add <name> <url>` command and manage remote repositories using commands like `git remote -v` (to list remotes) and `git remote remove <name>` (to remove a remote).

10. **How do you resolve merge conflicts in Git?**

    - **Answer:** 
      - Merge conflicts occur when Git cannot automatically merge changes from different branches.
      - To resolve merge conflicts, you edit the conflicted files to resolve the conflicting changes manually.
      - After resolving conflicts, you add the modified files to the staging area using `git add` and complete the merge operation using `git merge --continue` or `git commit`.
