## Project description
The research team at my organization needs to update the file permissions for certain files and directories within the `projects` directory. The permissions do not currently reflect the level of authorization that should be given. Checking and updating these permissions will help keep their system secure. To complete this task, I performed the following tasks:

## Check file and directory details
I used the `ls` command with the `-la` option to display a detailed listing of the file contents that also returned hidden files. The output of my command indicates that there is one directory named drafts, one hidden file named `.project_x.txt`, and five other project files.
```
researcher2@1a11feec0c46:~/projects$ ls -la /home/researcher2/projects
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 17:51 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 19:03 ..
-rw--w---- 1 researcher2 research_team   46 Oct 20 17:51 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Oct 20 17:51 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Oct 20 17:51 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Oct 20 17:51 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_r.txt
```

 ## Change file permissions
 The `chmod` command changes the permissions on files and directories. The first argument indicates what permissions should be changed, and the second argument specifies the file or directory. 
 
 In this example, I removed write permissions from other for the `project_k.txt file`. After this, I used `ls -l` to review the updates I made.
```
researcher2@1a11feec0c46:~/projects$ chmod o-w project_k.txt
researcher2@1a11feec0c46:~/projects$ ls -l /home/researcher2/projects
total 20
drwx--x--- 2 researcher2 research_team 4096 Oct 20 17:51 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Oct 20 17:51 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_t.txt
```

## Change file permissions on a hidden file
The research team at my organization recently archived `project_x.txt`. They do not want anyone to have write access to this project, but the user and group should have read access. 

The following code demonstrates how I used Linux commands to change the permissions:
```
researcher2@1a11feec0c46:~/projects$ chmod u-w,g-w,g+r .project_x.txt
researcher2@1a11feec0c46:~/projects$ ls -la /home/researcher2/projects
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 17:51 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 19:03 ..
-r--r----- 1 researcher2 research_team   46 Oct 20 17:51 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Oct 20 17:51 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_k.txt
-rw------- 1 researcher2 research_team   46 Oct 20 17:51 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_t.txt
```
`.project_x.txt` is a hidden file because it starts with a period `(.)`. In this example, I removed write permissions from the user and group, and added read permissions to the group. I removed write permissions from the user with u-w. Then, I removed write permissions from the group with `g-w`, and added read permissions to the group with `g+r`.

## Change directory permissions
My organization only wants the `researcher2` user to have access to the drafts directory and its contents. This means that no one other than `researcher2` should have execute permissions.
```
researcher2@1a11feec0c46:~/projects$ chmod g-x drafts
researcher2@1a11feec0c46:~/projects$ ls -la /home/researcher2/projects
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 17:51 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct 20 19:03 ..
-r--r----- 1 researcher2 research_team   46 Oct 20 17:51 .project_x.txt
drwx------ 2 researcher2 research_team 4096 Oct 20 17:51 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_k.txt
-rw------- 1 researcher2 research_team   46 Oct 20 17:51 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct 20 17:51 project_t.txt
researcher2@1a11feec0c46:~/projects$ 
```
I previously determined that the group had execute permissions, so I used the `chmod` command to remove them. The `researcher2` user already had execute permissions, so they did not need to be added.
