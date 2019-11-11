### Variant 10
Output the following information:

* Top 10 URLs that caused client errors (code starts with 4)
* The number of errors for each of them
* The percentage of errors for each of them

Sample output:

```
1. /example.com - 50 - 50%
2. /img/image.png - 30 - 30%
3. /robots.txt - 20 - 20%                                      
```
#! /bin/bash
sum=$(cat log.txt | grep -e 'HTTP/1.1" 4' -e 'HTTP/1.0" 4' | wc -l);
cat log.txt | grep -e 'HTTP/1.1" 4' -e 'HTTP/1.0" 4'| cut -f7 -d" " | sort | uniq -c | sort -k1 -r -n | head | cat -n | awk '{print $1 ". " $3 " - " $2 " - " $2*100/"'$sum'" "%"}'
