# Docker images

```bash
pnpm build <repository path>
```

## Options

- `-p`: push image to registry
- `-r <repo>`: set repository other than folder name
- `-t <tag>`: tag image other than latest
- `-u <username>`: username for registry

## Example

### Build and push image to registry

```bash
pnpm build php/php-fpm -p
pnpm build node/node/18-alpine3.16 -p
```
