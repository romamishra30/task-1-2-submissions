# OverTheWire Bandit Write-up

## Level 0 → Level 1

I logged into the Bandit server using SSH with the provided credentials. After accessing the home directory, I listed the available files using the `ls` command and found a file named `readme`. I used the `cat` command to display its contents, which revealed the password for the next level. This level introduced basic Linux navigation and file reading.

## Level 1 → Level 2

After logging in with the Level 1 password, I listed the files and noticed a file named `-`. Since `-` is treated specially by many Linux commands, using `cat -` did not work as expected. To explicitly reference the file, I used `cat ./-`, which successfully displayed the password. This level demonstrated how special filenames can be accessed using relative paths.

## Level 2 → Level 3

The password was stored inside a file whose name contained spaces. Directly referencing the filename caused issues because the shell interpreted the spaces as separate arguments. I solved this by either escaping the spaces or enclosing the filename within quotes while using the `cat` command. This level helped me understand how the shell handles filenames containing spaces.

## Level 3 → Level 4

After entering the hidden directory using the `cd` command, I used `ls -a` to display hidden files. A hidden file named `.hidden` was present inside the directory. Reading this file with `cat` revealed the next password. This level introduced hidden files and the importance of using `ls -a` when exploring directories.

## Level 4 → Level 5

The level contained multiple files with different formats. To determine which file contained readable data, I used the `file` command on all files in the directory. One file was identified as an ASCII text file, while the others were binary or non-readable formats. Reading the text file with `cat` provided the password. This level taught me how to inspect file types before attempting to read them.

## Level 5 → Level 6

The password was hidden somewhere within a large directory structure. The challenge specified conditions such as file size, ownership, and readability. I used the `find` command with the required filters to search for files matching those conditions. Once the correct file was located, I used `cat` to retrieve the password. This level demonstrated the power of the `find` command for targeted file searches.

## Level 6 → Level 7

The password was stored in a file owned by a specific user and group. I again used the `find` command with ownership filters to identify the correct file. After locating it, I displayed its contents to obtain the password. This reinforced my understanding of Linux file ownership and advanced search filters.

## Level 7 → Level 8

A large text file contained many lines, but only one line started with the keyword “millionth”. I used the `grep` command to search for this unique string and extract the relevant line. The password was present alongside the keyword. This level introduced text searching using pattern matching.

## Level 8 → Level 9

The file contained many repeated lines, with only one unique line appearing once. To identify it, I sorted the file using `sort` and then used `uniq -u` to display the line that occurred only once. That unique line contained the password. This level demonstrated how Unix commands can be combined to process data efficiently.

## Level 9 → Level 10

The file contained mostly binary data with a few human-readable strings. I used the `strings` command to extract readable text and then filtered the results to locate the password. This level showed how useful the `strings` utility is when examining binary files.

## Level 10 → Level 11

The password was encoded using Base64. After viewing the file contents, I decoded the data using `base64 -d`, which revealed the plaintext password. This level introduced data encoding and decoding techniques.

## Level 11 → Level 12

The password was encrypted using ROT13. Since ROT13 shifts every alphabetic character by 13 positions, I used the `tr` command to translate the encoded characters back to their original form. The resulting text contained the password. This level demonstrated character substitution techniques.

## Level 12 → Level 13

This was one of the most challenging levels. The file contained a hexadecimal dump of data that had been repeatedly compressed using different formats. I first converted the hex dump back into binary using `xxd -r`. I then repeatedly used the `file` command to identify the current file type and applied the appropriate extraction utility such as `gunzip`, `bunzip2`, and `tar` until the final text file was obtained. The password was stored inside the resulting file. This level required patience, careful observation, and understanding of multiple compression formats.

## Level 13 → Level 14

The level provided an SSH private key instead of a password. Initially, I faced difficulties understanding how to use the key correctly and encountered authentication issues. After creating a local key file, setting proper permissions, and using the `ssh -i` option, I successfully authenticated as the next user. This level introduced key-based SSH authentication.

## Level 14 → Level 15

The password for the current level had to be submitted to a service running on localhost port 30000. I first retrieved the current password from the protected password file and then used `nc` (netcat) to send it to the specified port. The service validated the password and returned the credentials for the next level. This level introduced basic network communication using command-line tools.
