# Bash One-liners

## List of bash one-liners
* Display a list of all IP addresses that tried and failed to log in to the SSH server alongside the number of failed attempts of each IP address:
```
grep "Failed password" /var/log/auth.log | awk ‘{print $11}’ | uniq -c | sort -nr
```
