# 📈 Enterprise Use-Cases covered
Uber Case Study: Separating legacy stable modules (Cabs Engine) away from upcoming prototype pipelines (Bikes & Intercity features).

Kubernetes Workflow: Handling massive multi-tenant contribution frameworks (3,300+ developers) asynchronously using structured release staging.

# 🎯 DevOps Interview Questions Discussed by Abhishek Sir

In this video, Abhishek Sir explains that if questions about Git come up during an interview, there is a **90% chance** that one of them will be from this list. Pay close attention to these questions:

### Question 1: What is a Git Branching Strategy and why is it critical for an organization?
* **Answer Guide:** A branching strategy is a clear set of rules defining when developers create branches, how they are named, and how they are merged into the main codebase. It is critical because it ensures new features are delivered to customers safely and on time, without breaking the existing application.

### Question 2: From which branch do you usually perform production releases?
* **Answer Guide:** Releases are always performed from **Release Branches** (e.g., `release-v1.0`), not directly from the `master` or `main` branch. The `master` branch undergoes continuous code changes, whereas a release branch is created to "freeze" the code, allowing only final production-level testing to take place.

### Question 3: What is a Hotfix branch, and what is its specific merging rule?
* **Answer Guide:** When a critical bug appears in a live application running in production, we create a temporary, short-lived branch—called a **Hotfix branch**—to fix it urgently.
* **The Golden Rule:** Once the hotfix code is ready, it **must be merged into both** the **Master Branch** and the active **Release Branch**. This ensures the live application is fixed and the bug does not reappear in future releases.

### Question 4: What is a Feature branch and when do you delete it?
* **Answer Guide:** A feature branch is created to provide an isolated environment whenever work needs to be done on new functionality or when introducing a major or breaking change to the core application. Once development and testing are fully successful and the code is merged into the main branch (`master`) via a pull request, the feature branch is deleted for cleanup.