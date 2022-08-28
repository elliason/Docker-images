# Docker images
### Usage
```bash
yarn build <repository path>
```
#### Options
- `-p`: push image to registry
- `-r <repo>`: set repository other than folder name
- `-t <tag>`: tag image other than latest
- `-u <username>`: username for registry

## Example
```bash
yarn build php/php-fpm -p
```