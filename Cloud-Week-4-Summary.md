# Week 4: Linux and Bash

This week, we explored **Linux** and **Bash** commands, focusing on basic system navigation, file management, editing, and managing permissions in the context of an EC2 instance on AWS. Below are the key learnings and exercises we completed:

## Setting Up an EC2 Instance
- Launched an **EC2 instance** in AWS using the IAM user **Jeremy** (created in Week 1).
- **IAM Role** modification for the EC2 instance to grant permissions to S3.

## Linux Directory Structure
We explored key Linux directories:
- **/etc**: Configuration files.
- **/var**: Variable files, including logs.
- **/bin**: Essential binaries.
- **/lib**: Libraries essential for system boot.
- **/tmp**: Temporary files.

## Basic Navigation and Bash Commands
We practiced several important commands for navigating and managing files:
- **pwd**: Print the current working directory.
- **cd**: Change directory.
- **ls**: List directory contents.
  - **ls -l**: List files with detailed information.
  - **ls -a**: Show hidden files.
- **touch**: Create a new file.
  ```bash
  touch myfile.txt
  ```

## Editing Files with Nano and Vim
- Used **nano** to edit text files:
  - Created and added text to `myfile.txt`, saved, and exited using the commands:
    - **Ctrl + O** (write out/save) and **Ctrl + X** (exit).
- Edited files using **vim**:
  - Entered **Insert Mode** with `i`, added text, saved, exited using `:wq`, and revisited the file for further edits.

## Exercise: Creating and Editing Files
1. **Create a New File**: 
   ```bash
   touch class_notes.txt
   ```
   Created a new file named `class_notes.txt` in the home directory.
   
2. **Edit the File** with **nano** or **vim**:
   - Opened the file using either editor:
     ```bash
     nano class_notes.txt
     ```
     or
     ```bash
     vi class_notes.txt
     ```
   - Added our name, the date, and some notes on what we learned so far.
   - Saved and exited using the relevant commands for each editor.

## Modifying IAM Role and Uploading to S3
- Created and attached an **IAM Role** (ECS2-S3) to the EC2 instance to allow access to **S3**.
- Uploaded the `myfile.txt` to the **S3 bucket** created in a previous week.

## Changing File Permissions
We learned about **file permissions** in Linux, particularly the format:
- Example output from `ls -l`:
  ```bash
  -rw-r--r-- 1 ec2-user ec2-user 33 Sep 22 18:15 my-file.txt
  ```
  - **Owner, Group, and Others** permissions represented as:
    - `r` = Read (4), `w` = Write (2), `x` = Execute (1).
- **chmod** was used to change file permissions using both symbolic and numeric modes:
  ```bash
  chmod 755 my-file.txt
  ```
  - The file permissions after applying `chmod 755`:
    ```
    -rwxr-xr-x 1 ec2-user ec2-user 33 Sep 22 18:15 my-file.txt
    ```

## Terminating the EC2 Instance
After completing the exercises, we terminated the instance to avoid unnecessary costs.

---