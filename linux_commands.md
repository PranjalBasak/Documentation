# Resources and Online Tools
* [Crontab Generator](https://crontab-generator.org/)
* [Cron Guru](https://crontab.guru/)

# Important
* `sudo apt update`
* `sudo apt install <package_name>`
<br> <br>
# 60+ Commands from NetworkChuck (Personally Added More!)
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
    * `find <path> -user <user> -group <group> -size <size>c 2>/dev/null
36. `chmod +x <file>` : Making the file executable
37. `chown <user> <file>` : Changing ownership of a file
38. `ifconfig` : Finds IP Info (Install with `sudo apt install net-tools`)
39.  `ip address`
40. * `egrep <pattern_to_match> <file_where_to_look>` : Finds a text in a file
    * `egrep -v <pattern_to_not_match> <file.txt>` : Inverts matching
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
64. `crontab -e`

# Awk CheatSheet
`awk` has a `BEGIN` block, a codeblock and an `END` block <br><br>
**Format** : `awk 'BEGIN {print "Starting"} {print $1} END {print "Ending"}' {file.txt}`
1. `awk '{print $1}' <file.txt>` : prints the first column taking space as the seperator by default
2. `awk -F ":" '{print $1}' /etc/passwd` : prints the first column taking colon(:) as the field seperator
3. `awk -F ":" '{print $1"\t"$3"\t"$5}' /etc/passwd` : Using "\t" inbetween to seperate the columns in output
4. `awk {/^/ print} <file>`
5. `awk -f <code.awk> <file.txt>`
6. `awk --profile <code> file.txt` : Generates a `awkprof.out` file
7. `BEGIN{FS=","}` : Input field seperator changed to comma
8. `awk 'BEGIN{FS=":'; OFS=","} {print $1,$2}' <file.txt>` : Using both input and output field seperator
9. `BEGIN{RS="|"}` : An input record seperator
10. `BEGIN{ORS=","}` : An output record seperator
11. `{print NF}` : Prints number of fields by record
12. `{print NR}` : Prints number of records
13. `awk 'BEGIN{OFS="\t"} {print $2, $3}' data.txt | sort -n -k1`

## Regex
1. ^ -> Start of the line
2. $ -> End of the line
3. Dot(.) -> Match on any symbol
4. a* = b, a, aa, aaa : Matches 0 or more occurrences
5. a+ = a, aa, aaa... : Matches 1 or more occurrences
6. a? = a, b but not aa : Matches 0 or 1 occurrence
7. * `/da{2,3}ta/` : daata, daaata
    * `/da{2,}ta/` : 2 or more a's
    * `/da{,3}ta/` : 3 or less a's
    * `/da{2}/` : daata / exactly 2 a's
8. `awk '/^.*$/ {print}` <file>: Matches everything 
9. `(aa)` : It is a group
10. `(aa)+` : aa, aaaa, aaaaaa (2,4,6)
11. * The pattern `[aeiou]` matches any single vowel.
    * The pattern `[0-9]` matches any single digit.
    * The pattern `[a-z]` matches any single lowercase letter.
    * The pattern `[A-Z]` matches any single uppercase letter.
12. Escape character is backslash(\). '\.' will match dot(.).
13. `\n` matches a new line
14. `\t` matches a tab
15. `/[a-zA-Z0-9]/`
16. `awk $1 ~ \is\ {print $1}` : If the first column contains "is", print the first column
17. `!~` means the opposite
18. `^a-z` : Anything but characters in the range a-z
19. `\d` : Any digit
20. `\D` : Any non-digit
21. `\b` : Word boundary
22. `\w` : Word (Any unicode character). Alternative to [a-zA-Z0-9]
23. `\W` : Not a word

### Practice Regex
* https://regex101.com/
* https://regexr.com/


