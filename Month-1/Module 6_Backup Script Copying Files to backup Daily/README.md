# Module 6_Backup Script Copying Files to /backup Daily

## Introduction 
In every organization, protecting data is a top priority. Imagine spending hours working on important files only to lose them in an instant due to a system crash, accidental deletion, or hardware failure. This is why backups are not optional — they are essential. Instead of relying on manual copying, which is slow and unreliable, we can harness the power of Bash scripting to automate the process.
In this project, you will build a backup script that copies files to /backup automatically in real time. By combining the flexibility of Bash with a continuous loop, this solution ensures that every new or updated file in the source directory is backed up immediately, without human intervention. This project not only strengthens your Linux scripting skills but also shows how automation can bring efficiency, reliability, and peace of mind in real-world DevOps environments.

## Statement of the Problem
System data is constantly exposed to risks such as accidental deletion, hardware failures, and unexpected crashes. Losing important files can disrupt daily operations and cause serious setbacks. Relying on manual backups is not a reliable solution because they are often inconsistent, easily forgotten, and vulnerable to human error. To avoid these challenges, there is a need for an automated backup process that runs continuously in the background, copying files to a secure directory (/backup) the moment changes occur. This ensures data is always protected without depending on manual effort.

## Project Objectives
- Write a Bash script that copies files to the /backup directory.
- Automate the process so it runs in real time, not just once per day.
- Demonstrate Bash concepts such as variables, conditions, loops, and directory checks.
- Improve reliability and reduce manual workload in file management by ensuring backups happen immediately after changes.

## Project Steps
Step 1: Create a new Bash script file

Step 2: Add the shebang (#!/bin/bash) to specify the shell

Step 3: Define source and destination directories

Step 4: Add commands to copy files into /backup

Step 5: Add a check to create /backup if it doesn’t exist

Step 6: Make the script executable

Step 7: Test run the script to confirm file copies

Step 8: Add Real-Time Backup with a Loop


## Project Implementation

### Step 1: Create a new Bash script file

Before writing any code, we first need to create a script file that will hold our backup instructions. This ensures we have a dedicated place to build and test the automation.

- Open Git Bash.
 <img width="975" height="296" alt="image" src="https://github.com/user-attachments/assets/dd586fdb-b954-4200-8329-293076c85ef5" />
 
 

- Navigate to a safe location for your project (e.g., Documents). Run;
```bash
cd Documents
```
<img width="920" height="270" alt="image" src="https://github.com/user-attachments/assets/3205f4a6-68b8-4f31-9cf8-367c3d80b291" />


- Create a project folder in the just moved document and move into it. Run these commands one after another
```bash
mkdir backup_project
cd backup_project
``` 
<img width="975" height="275" alt="image" src="https://github.com/user-attachments/assets/8ffee704-83d0-44f7-9157-28e943b7d18c" />


- Create a backup directory in the backup_project where files will be stored. Run;
```bash
mkdir backup
```
<img width="975" height="180" alt="image" src="https://github.com/user-attachments/assets/3cf92a24-2b1c-4954-a774-b5ea4df3ee03" />
 

- Create an empty script file named daily_backup.sh. Run;
```bash
touch daily_backup.sh
``` 
<img width="975" height="176" alt="image" src="https://github.com/user-attachments/assets/14fa474d-9f32-408e-a448-bfc5c55ae957" />


### Step 2: Add the shebang (#!/bin/bash) to specify the shell
Every Bash script needs to tell the system which program should run it. This is done with a shebang (#!) line at the very top of the script. By writing #!/bin/bash, we ensure that the Bash shell is used to interpret and execute all commands in the script.

- Open your script file in the vi editor. Vi is a powerful, modal text editor found on all Unix/Linux systems that operates in different modes for navigation and text entry. It's essential for system administration since it's universally available. Run;
```bash
vi daily_backup.sh
```
<img width="975" height="466" alt="image" src="https://github.com/user-attachments/assets/d7d5dc09-4878-4f47-a4f7-80a0e20d0b29" />


- Press i to enter INSERT mode (you’ll see -- INSERT -- at the bottom of the terminal).
  <img width="975" height="369" alt="image" src="https://github.com/user-attachments/assets/85601ba5-e8f0-4378-86fa-521f4a9b6f7e" />

 

- Type the below line at the very top of the file.
```bash
#!/bin/bash
```
<img width="975" height="334" alt="image" src="https://github.com/user-attachments/assets/4d76e7ae-9df9-44d9-9ec8-c1db89de658c" />
 

- Press Esc to leave INSERT mode, then save and exit the editor by typing the below
```bash
:wq!
```
<img width="975" height="374" alt="image" src="https://github.com/user-attachments/assets/841c021a-5c53-4a0f-9d6d-057c5142b90c" />

 

### Step 3: Define source and destination directories

To make the backup script flexible and reusable, we shouldn’t hard-code file paths directly into the copy command. Instead, we define variables for the source (where the files are coming from) and the destination (where they’ll be copied). This way, we can easily change the backup folders in one place without editing the whole script.

- Open your script file again in vi. Run;
```bash
vi daily_backup.sh
``` 

- Press i to enter INSERT mode.

- Below the shebang line, add these two variables.
```bash
# Define source and destination directories using absolute paths
SOURCE="$(pwd)/source_files"
DEST="$(pwd)/backup" 
```
<img width="975" height="126" alt="image" src="https://github.com/user-attachments/assets/018487ca-469a-4061-b21a-a7bc882fa1db" />

Explanation

  - SOURCE → the folder where your files to be backed up are stored (you can create this folder if it              doesn’t exist yet).
    
  - DEST → the backup folder we created earlier.

  
- Press Esc to leave INSERT mode, then save and exit the editor by typing the below
```bash
:wq!
```

- Create the source_files folder so you have something to back up later. Run;
```
mkdir source_files
``` 
<img width="975" height="171" alt="image" src="https://github.com/user-attachments/assets/34e670f9-d52e-43f8-ab5e-a6097d8c7bfd" />

### Step 4: Add commands to copy files into /backup

Now that we have defined the source and destination directories, the next step is to actually copy the files. In Bash, the cp command is used to copy files from one directory to another. By combining it with our variables (SOURCE and DEST), the script will always copy files from the source folder into the backup folder.

- Open your script file in vi. Run;
```
vi daily_backup.sh
```

- Press i to enter INSERT mode

- Below the directory variables, add the copy command.
```
# Copy files from source to destination
cp -r "$SOURCE"/* "$DEST"/
```
<img width="644" height="65" alt="image" src="https://github.com/user-attachments/assets/ae153dc3-26c4-4c53-8602-645e8cb8d7a1" />


Explanation:
- cp → copy command
- 	-r → recursive, so it copies directories and their contents too
- $SOURCE/* → everything inside the source folder
- $DEST/ → where the files will be placed

- Press Esc to leave INSERT mode, then save and exit the editor by typing the below
```
:wq!
```

### Step 5: Add a check to create /backup if it doesn’t exist

To make the script reliable, ensure the destination folder exists before copying. If it doesn’t, create it so the backup never fails.

- Open the script, run;
```
vi daily_backup.sh
```

- Press i to enter INSERT mode.

- Above the cp line, add this block
```
# Ensure destination directory exists
if [ ! -d "$DEST" ]; then
  mkdir -p "$DEST"
fi 
```
<img width="975" height="354" alt="image" src="https://github.com/user-attachments/assets/20a028ab-927f-400d-b47a-04d703f99bae" />

Explanation
- If the destination folder exists → continue normally.
- If it doesn’t exist → create it automatically.

- Press Esc to leave INSERT mode, then save and exit the editor by typing the below
```
:wq!
```

### Step 6: Make the script executable

Right now, your script is just a text file. To be able to run it directly as a program, you need to give it execute permissions. On Linux (and Git Bash), this is done with the chmod command. Once executable, you can run the script with ./daily_backup.sh instead of calling it through bash.

- In your Git Bash terminal, make the script executable. Run;
```
chmod +x daily_backup.sh
``` 
<img width="975" height="181" alt="image" src="https://github.com/user-attachments/assets/2ac370c9-19a1-4e4e-90ec-0d94c928aad6" />

Explanation
- chmod → change file permissions
- +x → adds execute permission
- daily_backup.sh → the file to update

- Verify the permission change by listing files. Run;
```
ls -l
``` 
<img width="975" height="166" alt="image" src="https://github.com/user-attachments/assets/8b7f2d84-b32a-4eeb-91a6-39f5a730cd5d" />

### Step 7: Test run the script to confirm file copies
Now that your script is executable, it’s time to test it. We’ll place some sample files in the source folder and then run the script. If everything works, the files should appear in the backup folder. This test ensures the script performs the actual backup before we automate it later.

- Add test files to the source folder. Run;
```
echo "This is file 1" > source_files/file1.txt
echo "This is file 2" > source_files/file2.txt
``` 
<img width="975" height="263" alt="image" src="https://github.com/user-attachments/assets/2f9e6319-ee5e-4c64-bcb7-94a9fc41570f" />

This creates two sample text files inside source_files/

- Run your script. Run;
```
./daily_backup.sh
```
<img width="975" height="179" alt="image" src="https://github.com/user-attachments/assets/c7992b5e-c50f-4b95-a4eb-b559f394445c" />


- Run this command to list the backup folder.
```
ls backup
```
<img width="975" height="100" alt="image" src="https://github.com/user-attachments/assets/acf62c30-d402-46da-b7d2-e26053f83579" />


Our script ran successfully; everything created on our source folder is now in our backup folder after we ran the script.


### Step 8: Add Real-Time Backup with a Loop

So far, the script runs only when you execute it manually. But in real DevOps environments, you often need backups to happen automatically without any user action. Instead of scheduling it once per day with cron jobs, we’ll improve the script to continuously monitor the source folder. Using a while loop, the script will repeatedly check the folder and immediately copy new or updated files into the backup directory. This creates a real-time sync system.

- Open your script in vi. Run;
```
vi daily_backup.sh
```
- Press i to enter INSERT mode.

- Replace the single copy command with this loop
```
# Copy files from source to destination
echo "Starting real-time backup... Watching $SOURCE"
while true; do
  cp -ru "$SOURCE"/. "$DEST"/
  sleep 5
done
``` 
<img width="975" height="396" alt="image" src="https://github.com/user-attachments/assets/44bcd65c-d330-4237-a486-e8aa98058354" />

Explanation
- cp -ru instead of rsync
- -r → recursive (copies directories)
- -u → only copies files that are new or updated (prevents unnecessary overwriting)
- The loop (while true) still checks every 5 seconds.


- Press Esc to leave INSERT mode, then save and exit the editor by typing the below
```
:wq!
```

- Run the script;
```
./daily_backup.sh
```
<img width="975" height="270" alt="image" src="https://github.com/user-attachments/assets/ef0af3a1-9fdc-454d-a1df-4a7dba0b9d03" />
 

Now your script is running in real-time mode. That means it’s actively watching your source_files folder and looping every 5 seconds.


Now, let us test. We would allow the scripts to be running and open another git bash window to test if it copies automatically

- Let us open another git bash terminal. Windows Start button; type Git Bash in the search box; click Git Bash → it opens a new terminal window.
<img width="975" height="293" alt="image" src="https://github.com/user-attachments/assets/aa8d050a-6835-4005-a3af-10a0080d618a" />
 

- Run these commands to go to our project folder;
```
cd Documents
cd backup_project
```
<img width="975" height="271" alt="image" src="https://github.com/user-attachments/assets/c2a50ee2-0708-4807-9850-a08c79650e7d" />
 
- Add a new file to the source folder. Run;
```
echo "Auto backup test" > source_files/file4.txt
``` 
<img width="975" height="213" alt="image" src="https://github.com/user-attachments/assets/73c582d1-101e-41e7-9a1b-e5ae41794bd9" />

- Wait a few seconds, then check the backup folder. Run;
```
ls backup
``` 
<img width="975" height="164" alt="image" src="https://github.com/user-attachments/assets/96da155d-aff6-4d54-b671-9c2081d6c1df" />

## Conclusion
In this project, we successfully designed and implemented a Bash script to automate file backups into a dedicated /backup directory. Beginning with the basics of script creation and shebang usage, we built a structured solution that defined source and destination directories, ensured directory existence, and handled file copying reliably.
While traditional automation often relies on scheduled jobs (like cron), we improved the design by introducing a continuous while loop that runs in real time. This enhancement allows the script to automatically detect and copy new or updated files within seconds, ensuring data is always protected without requiring manual intervention.
Through this project, we demonstrated practical Bash concepts such as variables, conditions, loops, and directory management. More importantly, we saw how automation improves reliability and reduces human error in file management — a principle that lies at the heart of DevOps. This project not only strengthens scripting skills but also highlights the importance of proactive, real-time solutions in safeguarding critical data.

