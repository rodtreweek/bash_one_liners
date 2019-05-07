# Bash One-liners

## List of bash one-liners
* Get a list of failed ssh logins from `/var/log/auth.log`
```
grep "Failed password" /var/log/auth.log | awk ‘{print $11}’ | uniq -c | sort -nr
```
