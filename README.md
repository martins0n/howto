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


### Compress
https://gist.github.com/Kautenja/af670104f13c94f92b69ce054ee96b42

```shell
tar cf - <files> -P | pv -s $(du -sb <files> | awk '{print $1}') | gzip > <some .tar.gz file>
```

where:

-   `<files>` is the root-mounted (i.e. starts with /) path to the files
-   `<some .tar.gz file>` is the output tarball to create

### Decompress
https://gist.github.com/Kautenja/af670104f13c94f92b69ce054ee96b42

```shell
pv <some .tar.gz file> | tar -xvzf - -C <some directory>
```

where:

-   `<some .tar.gz file>` is the path to the tarball to extract
-   `<some directory>` is the directory to extract the tarball to 
