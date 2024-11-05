# Week 2: Git and Cloud Architecture

This week, we focused on **Git** and **Cloud Architecture**, reviewing familiar concepts and learning new ones.

## Git
We explored **version control** using Git, covering commands like `git init` and `git checkout -b dev`, and discussed using Git for managing cloud projects.

### Git Repository Creation & Strategy
We created the repository using `git init` and pushed it to GitHub. We’ll follow a branching strategy, creating feature branches for each module to avoid conflicts.

## Cloud Architecture
We covered components like:
- **Frontend:** UI and client-side logic.
- **Backend:** Server-side logic and infrastructure.
- **Cloud Infrastructure:** Platforms like AWS and Azure for scalable solutions.
- **Networking:** Ensures secure, reliable data transfer.

### AWS S3 Bucket Creation
We used AWS CLI commands to create an S3 bucket and upload objects:
- **Create a new S3 bucket:**
  ```bash
  aws s3 mb s3://[cloud-bootcamp]
  aws s3 cp [C:\Users\jshoo\Documents\test] s3://[cloud-bootcamp]


