# Important
* `sudo apt update`
* `sudo apt install <package_name>`
<br> <br>
# 60+ Commands from NetworkChuck
**Source**: [NetworkChuck's Video](https://www.youtube.com/watch?v=gd7BXuUQ91w)
1. `ssh <username>@<ip>`
2. 
    * `ls` 
    * `ls -a`
    * `ls -h`
    * `ls -l`
3. `pwd`
4. * `cd <path>`    
   * `cd`
   * `cd ..`
5. * `touch <file.txt>`
    * `touch <linode{0..100}>`
6. `echo 'hello world' > <new_file.txt>`
7. `nano <file.txt>`
8. `vim <file.txt>`
9. `cat <file.txt>`
10. `shred <file.txt`
11. `mkdir <new_dir>`
12. `cp <file.txt> <path>`
13. `mv <file.txt> <path`
14. `rm <file.txt>`
15. `rm -r <dir>`
16. `ln -s <file.txt> <alinktothefile>` : Creates a soft link
17. `clear`
18. `whoami`
19. `sudo useradd <user>`
20. `sudo adduser <user>` : More interactive
21. `su <different_user>` : Switches to a different user
22. `sudo passwd <username>` : Changes user password
23. `man <command>`
24. `whatis <something>`
25. `wget <url>` : Download
26. `curl <url> > <download.extension>`
27. `zip <zipped.zip> <to_be_zippe.extension>`
28. `unzip <zip_file.zip>`
29. `less <file.txt>` : Gives you one page at a time
30. `head <file.txt>` : Beginnning of your file
31. `tail <file.txt>` : End of your file
32. `cmp <file_1.txt> <file_2.txt>` : Compares two files
33. `diff <file_1.txt> <file_2.txt>` : Tells us the exact difference 
34. `sort <file.txt>` : Sorts a file in alphabetical order
35. * `find <path> -name <file_name>`
    * `sudo find <path> -type f -name ".*"` : Finds hidden files
    * `find <path> -type f -empty` : Finds empty directories
    * `find <path> -perm /a=x`
36. `chmod +x <file>` : Making the file executable
37. `chown <user> <file>` : Changing ownership of a file
38. `ifconfig` : Finds IP Info (Install with `sudo apt install net-tools`)
39.  `ip address`
40. `grep <text_to_find> <file_where_to_look>` : Finds a text in a file
41. `awk '{print $1}'`
42. `resolvectl status` : Finds the DNS Server
43. * `ping www.google.com`
    * `ping -c <how_many_pings> www.google.com`
    * `ping -s <size_of_the_packet> www.google.com`
44. `traceroute www.google.com`
45. * `netstat`
    * `netstat -tulpn`
46. * `ss`
    * `ss -tulpn`
47. * `sudo ufw allow 80` : Firewall
    * `sudo ufw status`
    * `sudo ufw enable` : Activate the firewall
48. `uname -a` : Know about your system
49. `neofetch` : Prettier version (Install using `sudo apt install neofetch`)
50. `cal` : Calender
51. `echo "4+5+6` | bc` : Calculator
52. * `free` : How much free memory you have
    * `free -h` : Better Format
53. * `df` : How much disk space you have
    * `df -H` : Better format
54. * `ps` : Learn about your system processes
    * `ps -aux` : More detailed
55. `top` : Top processes
56. `htop` : Prettier way
57. `kill -9 <process_id>` : Force kill a process
58. `pkill -f <process_name>` : Force kill using the process name
59. * `sudo systemctl start <service>` : Start a service
    * `sudo systemctl stop <service>` : Stop a service
60. `history` : History of all the commands
61. `sudo reboot`
62. * `sudo shutdown`
    * `sudo shutdown -h now` : Shutdown now
63. `exit`
