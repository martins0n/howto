# Howto

## Bash

### How to find file with defined substring inside
```bash
find . -name '*.ipynb' -exec grep -l 'search_reviews' {} \;
```
