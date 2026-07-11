# Git and GitHub Architecture Exploration

This sandbox repository mirrors the core architectural insights presented on Day 9 of the DevOps Zero to Hero course. It highlights why modern technology firms prioritize Distributed Version Control over old Centralized paradigms.

## 🏗️ Architectural Differences Visualized

### Centralized VCS Framework (SVN/CVS)
  [ Developer A Workspace ] ──(Requires Active Network)──┐
                                                          ▼
  [ Developer B Workspace ] ──────────────────────> [ CENTRAL SERVER ] (Single Point of Failure)

### Distributed VCS Framework (Git)
  [ Developer A Workspace ] <───(Peer Clone)───> [ Developer B Workspace ]
            │                                               │
    (Full Local History)                            (Full Local History)
            │                                               │
            └───────────────> [ GITHUB / REMOTE ] <─────────┘


### Git diagnostic commands
# View all hidden repository footprints (Locating the hidden .git directory)
ls -la

# Checking local history without needing internet access
git log

# Analyzing granular code level changes
git diff