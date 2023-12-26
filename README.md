# Manage-Authorization-in-Linux

<h2>Activity overview</h2>

In this lab activity, I’ll use Linux commands to configure authorization in Linux.

Authorization is the concept of granting access to specific resources in a system. It's important because without authorization any user could access and modify all files belonging to other users or system files. This would certainly be a security risk.

In Linux, file and directory permissions are used to specify who has access to specific files and directories. I’ll explore file and directory permissions and change the ownership of a file and a directory to limit who can access them.

As a security analyst, setting appropriate access permissions is critical to protecting sensitive information and maintaining the overall security of a system.

<h2>Scenario</h2>

In this scenario, I must examine and manage the permissions on the files in the ```/home/researcher2/projects``` directory for the ```researcher2``` user.

The ```researcher2``` user is part of the ```research_team``` group.

I must check the permissions for all files in the directory, including any hidden files, to make sure that permissions align with the authorization that should be given. When it doesn't, I must change the permissions.

Here’s how I’ll do this task: First, I’ll check the user and group permissions for all files in the ```projects``` directory using the ```ls -la``` command. Next, you’ll check whether any files have incorrect permissions and change the permissions as needed. Finally, I’ll check the permissions of the ```/home/researcher2/projects/drafts``` directory and modify these permissions, using the ```chmod``` command to remove any unauthorized access.

<h2>Task 1. Check file and directory details</h2>

In this task, I must explore the permissions of the ```projects``` directory and the files it contains. The lab starts with ```/home/researcher2``` as the current working directory. This is because I’m changing permissions for files and directories belonging to the ```researcher2``` user.

1. Navigate to the ```projects``` directory.
2. List the contents and permissions of the ```projects``` directory.

The permissions of the files in the projects directory are as follows:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/6ddff568-b93e-4bd3-9e36-60f2c6348d84)

A 10-character string begins each entry and indicates how the permissions on the file are set. For instance, a directory with full permissions for all owner types would be ```drwxrwxrwx```:

- The 1st character indicates the file type. The ```d``` indicates it’s a ```directory```. When this character is a hyphen (```-```), it's a ```regular file```.
- The 2nd-4th characters indicate the read (```r```), write (```w```), and execute (```x```) permissions for the user. When one of these characters is a hyphen (```-```) instead, it indicates that this permission is not granted to the ```user```.
- The 5th-7th characters indicate the read (```r```), write (```w```), and execute (```x```) permissions for the ```group```. When one of these characters is a hyphen (```-```) instead, it indicates that this permission is not granted for the ```group```.
- The 8th-10th characters indicate the read (```r```), write (```w```), and execute (```x```) permissions for the owner type of other. This owner type consists of all other users on the system apart from the user and the group. When one of these characters is a hyphen (```-```) instead, that indicates that this permission is not granted for other.

The second block of text in the expanded directory listing is the user who owns the file. The third block of text is the group owner of the file.

Here I can see that research_team is the name of the group that owns the files in the ```projects``` directory:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/533caf16-7a6b-4eec-b524-f552776ce4bd)

3. Check whether any hidden files exist in the ```projects``` directory. Hidden files have a . before their filename.

Here I can see ```.project_x.txt``` is a hidden file:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/ec300dc5-4e95-40d1-978e-b4419280521e)

<h2>Task 2. Change file permissions</h2>

In this task, I must determine whether any files have incorrect permissions and then change the permissions as needed. This action will remove unauthorized access and strengthen security on the system.

None of the files should allow the other users to write to files.

1. Check whether any files in the ```projects``` directory have write permissions for the owner type of other.

Here I can see that ```project_k.txt``` grants other users write permissions when it shouldn’t:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/d24fc7f9-7434-461c-b92f-c29580cea95b)

2. Change the permissions of the file identified in the previous step so that the owner type of other doesn’t have write permissions using ```chmod o-w project_k.txt```.

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/81b8ac56-3102-4f99-a965-debcf652fa90)

Note: Permissions are granted for three different types of owners, namely user, group, and other. In the ```chmod``` command ```u``` sets the permissions for the user who owns the file,```g``` sets the permissions for the group that owns the file, and ```o``` sets the permissions for others.

3. The file ```project_m.txt``` is a restricted file and should not be readable or writable by the group or other; only the user should have these permissions on this file. List the contents and permissions of the current directory and check if the group has read or write permissions.

Here I can see that the group has read permissions on the ```project_m.txt``` file when they shouldn’t:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/8d7c6884-5226-4938-af13-280efd189ab5)

4. Use the ```chmod``` command to change permissions of the ```project_m.txt``` file so that the group doesn’t have read or write permissions.

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/22c83c4d-c3fe-475a-97e0-6448e694bc5a)

<h2>Task 3. Change file permissions on a hidden file</h2>

In this task, I must determine if a hidden file has incorrect permissions and then change the permissions as needed. This action will further remove unauthorized access and strengthen security on the system.

The file ```.project_x.txt``` is a hidden file that has been archived and should not be written to by anyone. (The user and group should still be able to read this file.)

1. Check the permissions of the hidden file ```.project_x.txt``` 

Here I can see the user and the group has incorrect write permissions:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/282e9e8a-9f63-40d4-a77c-7cf184aee7ad)

2. Change the permissions of the file .project_x.txt so that both the user and the group can read, but not write to, the file.

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/132e12c0-283d-4480-97d6-b13b5006bc9f)

<h2>Task 4. Change directory permissions</h2>

In this task, I must change the permissions of a directory. First, I’ll check the group permissions of the ```/home/researcher2/projects/drafts``` directory and then modify the permissions as required. (I should be in the ```projects``` directory while managing the permissions of its subdirectory ```drafts```.)

Only the ```researcher2``` user should be allowed to access the ```drafts``` directory and its contents. (This means that only ```researcher2``` should have execute privileges.)

1. Check the permissions of the ```drafts``` directory 

Here I can see the group has permissions set to access the drafts directory:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/979b95d8-8086-4310-86f9-b47f57c7f535)

2. Remove the execute permission for the group from the ```drafts``` directory.

Here I removed the execute permission from the group:

![image](https://github.com/n8som/Manage-Authorization-in-Linux/assets/110139109/3b6413e5-4073-4b95-b916-653861a295d7)

<H2>Conclusion</H2>

I now have practical experience in using basic Linux Bash shell commands to

- examine file and directory permissions using ```ls -la```,
- using ```chmod``` change permissions on files, and
- change permissions on directories.

This is an important milestone on my journey toward managing authorization in Linux!

