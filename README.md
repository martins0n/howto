# Howto

## Bash

### How to find file with defined substring inside
```bash
find . -name '*.ipynb' -exec grep -l 'search_reviews' {} \;
```

### Folder sizes in s3 buckets with s3cmd
```bash
s3cmd ls s3://<bucket-name>/ | awk '{print $2}' | grep 's3' |  xargs -n 1 -I {} s3cmd du -H {}
```
