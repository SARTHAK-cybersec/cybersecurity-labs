# Commands Used — Lab 01

This document records the main Linux commands used during the investigation and explains their purpose.

---

## 1. Check Current Directory

```bash
pwd

Displays the current working directory.

## 2. List Files and Directories
ls -la
Displays files and directories, including hidden files, along with detailed information such as permissions, ownership, and file size.

## 3. Create Directories
mkdir logs evidence suspicious
Creates directories used to organize the investigation environment.

## 4. Create Files
touch logs/auth.log logs/system.log
touch evidence/notes.txt
touch suspicious/temp_data.txt

Creates empty files for the simulated investigation.

## 5. Find Files and Directories
find .

Searches recursively from the current directory and displays files and directories.

## 6. Display File Contents
cat logs/auth.log

Displays the contents of the authentication log.

## 7. Write Data to a File
echo "Successful login: eminem" > logs/auth.log

Writes text to a file.
The > operator overwrites the existing contents of the file.

## 8. Append Data to a File
echo "Failed login: unknown_user" >> logs/auth.log

Adds text to the end of a file without overwriting its existing contents.

The >> operator appends data.

## 9. Search Log Entries
grep "Failed" logs/auth.log

Searches the authentication log for lines containing the word Failed.

## 10. Count Failed Login Attempts
grep "Failed" logs/auth.log | wc -l

Counts the number of lines containing Failed.

The pipe | sends the output of grep to wc.

wc -l counts lines.

Result:
2

## 11. Count Successful Logins
grep "Successful" logs/auth.log | wc -l

Counts successful login entries.

Result:
2

## 12. List Suspicious Files
find suspicious -type f

Searches the suspicious directory for regular files.

## 13. Search for a Specific Filename
find . -name "temp_data.txt"

Searches the investigation directory for a file named temp_data.txt.

## 14. Find Non-Empty Files
find suspicious -type f -size +0c

Finds regular files larger than 0 bytes.

The c represents bytes.

## 15. Identify File Type
file suspicious/temp_data.txt

Identifies the type of data stored in the file.

Result:
ASCII text

## 16. Search File Contents
grep "unknown" suspicious/temp_data.txt

Searches the suspicious file for the word unknown.

## 17. Check File Details
ls -lh suspicious/temp_data.txt

Displays detailed file information including permissions, ownership, size, and modification time.

###Key Linux Concepts Practiced
> = overwrite

>> = append

| = pipe output from one command to another

find = locate files/directories

grep = search text

wc -l = count lines

file = identify file type

ls -lh = view human-readable file information
