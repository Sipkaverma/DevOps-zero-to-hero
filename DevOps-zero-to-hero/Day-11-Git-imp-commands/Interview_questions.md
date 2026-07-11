Interview Questions Covered

### **Q1. What is a Merge Conflict in Git, and how do you resolve it?**
* **Answer:** A merge conflict happens when Git cannot automatically determine which changes to keep—usually when two people modify the same line in the same file on different branches. To resolve it, you must open the conflicted file, locate the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`), manually edit the file to keep the correct code, remove the markers, and then stage (`git add`) and commit the resolved file.

### **Q2. Why do we use branching in Git instead of working directly on the Master/Main branch?**
* **Answer:** Working directly on `main` can break the production-ready code if a bug is introduced. Branching allows multiple developers to work on features or fixes simultaneously in isolation without disturbing the stable codebase. Once verified, the code goes through a Pull Request (PR) review before merging.

### **Q3. What is the difference between `git fetch` and `git pull`?**
* **Answer:** `git fetch` only downloads the latest metadata and changes from the remote repository to your local system but does not merge them into your working files. `git pull` is a combination of two commands: it does a `git fetch` followed immediately by a `git merge`, updating your current local branch with the remote changes.

### **Q4. Explain the standard Git workflow in a DevOps environment.**
* **Answer:** 
  1. Clone the repository (`git clone`).
  2. Create a specific feature or bug-fix branch (`git checkout -b feature/xyz`).
  3. Make code changes, stage them (`git add`), and commit them locally (`git commit`).
  4. Push the branch to the remote repository (`git push origin feature/xyz`).
  5. Raise a Pull Request (PR) / Merge Request for senior review and automated CI/CD pipeline checks.
  6. Once approved, merge it into the main branch.