# PES-VCS Project

## Student Details
Name: Soumya  
SRN: PES1UG24CS628  

---

## Phase 1: Object Storage

In this phase, I implemented the basic object storage system. 
It stores blobs using SHA-256 hashing and organizes them inside `.pes/objects`.

### Screenshot 1A: Test Objects Output
![Phase1_1A](screenshots/phase1_1A.jpeg)

### Screenshot 1B: Object Storage Structure
![Phase1_1B](screenshots/phase1_1B.jpeg)

---

## Phase 2: Tree Objects

Here, I worked on tree objects which represent directory structure. 
The tree is built from entries and then serialized and stored.

### Screenshot 2A: Test Tree Output
![Phase2_2A](screenshots/phase2_2A.jpeg)

### Screenshot 2B: Raw Tree Object
![Phase2_2B](screenshots/phase2_2B.jpeg)

---

## Phase 3: Index (Staging Area)

In this phase, I implemented the staging area (index). 
It keeps track of files that are added before committing.

### Screenshot 3A: Init → Add → Status
![Phase3_3A](screenshots/phase3_3A.jpeg)

### Screenshot 3B: Index File Content
![Phase3_3B](screenshots/phase3_3B.jpeg)

---

## Phase 4: Commits and History

This phase handles commit creation and history tracking. 
Each commit stores metadata like author, message, and tree reference.

### Screenshot 4A: Log Output
![Phase4_4A](screenshots/phase4_4A.jpeg)

### Screenshot 4B: Object Growth
![Phase4_4B](screenshots/phase4_4B.jpeg)

### Screenshot 4C: HEAD and Branch Reference
![Phase4_4C](screenshots/phase4_4C.jpeg)

---

## Final Integration Test

This shows that all components (object, tree, index, commit) are working together.

![Final](screenshots/final.jpeg)

---

## Phase 5 & 6: Analysis Questions

### Q5.1 Branch & Checkout
In this system, a branch is basically a file that stores the latest commit hash.  
When we do checkout, we update the HEAD to point to that branch and change the working directory to match the files of that commit.

---

### Q5.2 Switching Branches
Before switching branches, we should check if there are any unsaved changes.  
If there are changes in the working directory, switching should not be allowed.  
This can be checked by comparing the working directory with the index and the index with HEAD.

---

### Q5.3 Detached HEAD
Detached HEAD means HEAD is pointing directly to a commit instead of a branch.  
If we make commits in this state, they are not linked to any branch and may be lost unless we create a new branch.

---

### Q6.1 Garbage Collection
Garbage collection removes objects that are no longer used.  
We start from branch heads and traverse all commits, trees, and blobs.  
Any object that is not reachable from these is considered unused and can be deleted.

---

### Q6.2 GC Race Condition
If garbage collection runs at the same time as a commit, it might delete objects that are still being created.  
This can cause errors. Git avoids this by using locking and safe file operations.
