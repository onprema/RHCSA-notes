## Finding Files with Locate and Find
- `find . -mtime -3` find all files in CWD that have been Modified within the last 3 days
- `find . -mtime +3` find all files in CWD that have been Modified greater than 3 days ago
- `find / -user jeff -type f -exec stat {} \;` -- V.POWERFUL. This will find all files owned by 'jeff' and then execute `stat` on each one. Note that the "\;" is part of the syntax.
