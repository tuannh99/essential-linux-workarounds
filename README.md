# EssentialLinuxWorkarounds

Welcome to **EssentialLinuxWorkarounds**, a comprehensive guide to alternative Linux commands. When standard commands are unavailable or missing from your environment, this repository provides you with "hacky" yet effective alternatives to achieve your goals. It's a valuable resource for developers, system administrators, and researchers.

## Introduction

Linux is powerful, flexible, and, most of all, incredibly diverse in its applications. However, sometimes, due to various constraints like restricted environments, missing packages, or even broken installations, one might find themselves unable to use their go-to commands. **EssentialLinuxWorkarounds** comes to the rescue in such situations, offering alternative commands and techniques to accomplish tasks seamlessly.

## Commands and Alternatives

Below is the curated list of 50 essential Linux commands alongside their alternatives for those times when the conventional options aren’t within reach.

1. `ls` alternative: `echo *`
   - Lists the non-hidden files and directories in the current directory.
   
2. `cd` alternative: Not easily replaceable, but for scripts, you can use `(cd /desired/directory && someCommand)` to change directory temporarily.
   
3. `pwd` alternative: `echo $PWD`
   - Prints the current directory using the environment variable.
   
4. `cat` alternative: `more <filename>` or `less <filename>`
   - Displays the contents of a file, albeit in a paginated way.
   
5. `echo` alternative: `printf "Your text here\n"`
   - Prints text to the terminal.
   
6. `grep` alternative: `awk '/search_pattern/ { print }' file`
   - Searches for patterns in files using AWK.
   
7. `find` alternative: `ls -R | grep "search_pattern"`
   - Recursively lists all files in directories and filters them by pattern.
   
8. `cp` alternative: `rsync -av source destination`
   - Copies files and directories using Rsync.
   
9. `mv` alternative: (Using `cp` and `rm`): `cp source destination && rm source`
   - Moves a file by copying it then deleting the original.
   
10. `rm` alternative: `find . -name "filename" -exec rm {} \;`
    - Finds and removes a specified file.
    
11. `chmod` alternative: `setfacl -m u:username:rwx file`
    - Changes file permissions using Access Control Lists (ACLs).
    
12. `chown` alternative: Not directly replaceable, but you can create a copy of the file, change ownership during the copy process, then replace the original file if necessary.
    
13. `kill` alternative: `pkill -f process_name`
    - Kills processes by name.
    
14. `top` alternative: `ps aux | sort -nrk 3,3 | head -n 5`
    - Lists the top 5 CPU-consuming processes.
    
15. `man` alternative: `pinfo command`
    - Displays the info pages, somewhat similar to man pages.
    
16. `df` alternative: `du -sh /*`
    - Estimates the space used by each directory at the root level.
    
17. `du` alternative: `find . -type f -exec ls -s {} \; | sort -n`
    - Lists files with sizes and sorts them.
    
18. `ps` alternative: `top -bn1 | head -n 10`
    - Displays a snapshot of the current processes using top.
    
19. `touch` alternative: `echo "" >> file`
    - Appends nothing to a file, creating it if it doesn't exist.
    
20. `tar` alternative: `cpio -o < files | gzip > out.gz`
    - Creates a compressed archive using cpio and gzip.

21. `wget` alternative: `curl -O URL`
    - Downloads files from the internet.
    
22. `curl` alternative: `(echo > /dev/tcp/HOST/PORT) >& /dev/null && echo "Success" || echo "Failure"`
    - Checks if a port is open on a given host.
    
23. `ssh` alternative: `telnet HOST PORT`
    - For remote access, though less secure and with different functionality.
    
24. `scp` alternative: `rsync -avz source destination`
    - Securely transfers files between hosts over SSH.
    
25. `tar` (extraction) alternative: `gzip -dc archive.tar.gz | cpio -id`
    - Extracts .tar.gz archives.
    
26. `diff` alternative: `comm file1 file2`
    - Compares files line by line.
    
27. `awk` alternative: `sed -n '/pattern/p' file`
    - Processes and analyzes text files.
    
28. `sed` alternative: `awk '{ gsub(/pattern/, "replacement"); print }' file`
    - Stream editor for filtering and transforming text.
    
29. `mount` alternative: `(echo '/path /mountpoint type options 0 0' >> /etc/fstab) && mount /mountpoint`
    - Mounts filesystems. Requires root/sudo and is permanent through reboots due to fstab entry.
    
30. `umount` alternative: `fuser -km /mountpoint; mountpoint -q /mountpoint && umount /mountpoint`
    - Unmounts filesystems. The first command kills processes using the mount.
    
31. `df` (for a specific filesystem) alternative: `findmnt -n -o SIZE /dev/sda1`
    - Shows size of a specific filesystem.
    
32. `date` alternative: `echo "$(awk '{print strftime("%Y-%m-%d %H:%M:%S", $1)}' <<<$(date +%s))"`
    - Displays current date and time.
    
33. `watch` alternative: `while true; do clear; command; sleep 2; done`
    - Executes a command repeatedly, showing the output.
    
34. `alias` alternative: `function myalias(){ command_to_run; }`
    - Creates a shortcut for a command.
    
35. `unalias` alternative: `unset -f myalias`
    - Removes an alias created with a function.
    
36. `hostname` alternative: `cat /etc/hostname`
    - Shows the system's network hostname.
    
37. `useradd` alternative: `echo "username:x:UID:GID:comment:/home/username:/bin/bash" >> /etc/passwd`
    - Adds a new user (requires manual setup for the home directory and password).
    
38. `passwd` alternative: `(echo password; echo password) | passwd username`
    - Changes the user's password (requires root).
    
39. `cron` (editing crontab) alternative: `echo "0 5 * * * /path/to/command" >> mycrontab; crontab mycrontab`
    - Schedules periodic tasks.
    
40. `at` alternative: `echo "/path/to/command" | at now + 2 minutes`
    - Executes commands at a later time.
    
41. `free` alternative: `grep Mem /proc/meminfo`
    - Shows memory usage.
    
42. `uname` alternative: `cat /proc/version`
    - Shows the system information.
    
43. `ping` alternative: `curl -I http://example.com`
    - Checks if a host is reachable over HTTP.
    
44. `ftp` alternative: `curl -u user:pass -T file ftp://ftp.example.com/upload/`
    - Transfers files over FTP.
    
45. `nano` or `vi` alternative: `ed`
    - A line-oriented text editor. Not user-friendly, but works in a pinch.
    
46. `sync` alternative: `echo 3 > /proc/sys/vm/drop_caches`
    - Flushes filesystem buffers.
    
47. `shutdown` alternative: `echo o > /proc/sysrq-trigger`
    - Shuts down the system immediately (requires root).
    
48. `reboot` alternative: `echo b > /proc/sysrq-trigger`
    - Reboots the system immediately (requires root).
    
49. `netstat` alternative: `ss -tulwn`
    - Shows network statistics.
    
50. `wall` alternative: `echo "Your message" | tee /dev/pts/*`
    - Sends a message to all logged-in users.

## Contributing

Your contributions are what make community-driven projects like **EssentialLinuxWorkarounds** truly valuable. Whether it's adding more command alternatives, improving existing ones, or fixing errors, we welcome your participation.

Please refer to [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to contribute.

## License

This project is open source and available under the [MIT License](LICENSE).

## Acknowledgements

- Thanks to all contributors who help in maintaining, updating, and expanding this repository.
- Special thanks to the Linux community around the world for the endless inspiration and support.

## Contact

For queries, suggestions, or discussions regarding **EssentialLinuxWorkarounds**, feel free to open an issue or a pull request.

---

Happy Hacking!
