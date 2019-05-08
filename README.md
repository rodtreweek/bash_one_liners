# Bash One-liners

## List of bash one-liners
* You can use the following to display a rough list of all IP addresses that tried and failed to log in to the SSH server alongside the number of failed attempts of each IP address (additional filtering would be required to exclude "illegal users"):
```
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort -nr | uniq -c
```
If you want to filter out the "illegal user" lines, you could use:
```
grep "Failed password" /var/log/auth.log | grep -v "Failed password for illegal" | awk '{print $11}' | sort -nr | uniq -c
```
Or you could use the following regex pattern with grep (grep -Po only works w/ GNU grep, not MacOS):
```
grep "Failed password" /var/log/auth.log | grep -Po "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" | sort -nr | uniq -c
```
Note: On newer Linux distributions you can query the runtime log file maintained by Systemd daemon via journalctl command. In order to display all failed SSH login attempts you should pipe the result via grep filter:
```
# journalctl _SYSTEMD_UNIT=ssh.service | egrep "Failed|Failure"
# journalctl _SYSTEMD_UNIT=sshd.service | egrep "Failed|Failure"  #In RHEL, CentOS 
```
