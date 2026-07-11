# ❓ Frequently Asked Interview Questions – Git & GitHub

## Question 1: What is a Version Control System (VCS), and why is it critical in a DevOps lifecycle?
Answer: A Version Control System is a software tool that tracks, records, and manages evolutionary changes made to source code over time. In a DevOps lifecycle, it is critical because it enables continuous collaboration among multi-tenant developer teams. It prevents code overwrites, maintains a detailed historical log of changes (who, what, and when), and allows teams to seamlessly roll back or revert to older stable states if a faulty deployment occurs.

## Question 2: Can you explain the structural difference between Centralized (CVCS) and Distributed Version Control Systems (DVCS)?
Answer: Centralized VCS (e.g., SVN, CVS): It relies on a single central server that stores the entire version history. Developers check out only working copies of specific files. The major limitation is that it creates a Single Point of Failure (SPOF)—if the central server goes down or loses network connectivity, developers can neither commit code nor access historical logs.

Distributed VCS (e.g., Git): Every developer's local machine maintains a complete mirror clone of the repository, including its full commit history, metadata, and branches. Developers can work, commit, and view logs completely offline. If the remote tracking server crashes, any developer's local copy can be used to fully restore the entire system.

## Question 3: What is the technical difference between Git and GitHub?
Answer: Git is an open-source, local command-line software tool that performs the actual core engine operations of version control on your machine. GitHub is a cloud-based hosting platform built on top of Git. It provides a Graphical User Interface (GUI), access management, and extra collaboration features such as Pull Requests, Issue Trackers, and CI/CD pipeline integrations (GitHub Actions).

## Question 4: What is the practical difference between a Git Fork and a Git Clone?
Answer: Git Fork: This is a GitHub platform feature (not a native Git command). It creates a server-side duplicate copy of a remote repository under your personal GitHub profile. It is widely used in open-source projects so you can make modifications without affecting the original master repository.

Git Clone: This is a native Git CLI command (git clone <URL>). It downloads a copy of an existing remote repository onto your local physical machine environment so you can begin working on the code locally.
