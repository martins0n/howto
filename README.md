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

### Content of deleted git files
```bash

# Fetch the list of deleted file paths
files=$(git diff --name-status master..HEAD | awk '$1 == "D" {print $2}')

# Loop over each file and output its contents from the master branch
for file in $files; do
    echo "Filename: $file" >> removed_files_content.txt
    git show master:"$file" >> removed_files_content.txt
    echo "-----------------------" >> removed_files_content.txt
done

```