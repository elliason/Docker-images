# Docker images

```bash
pnpm build <repository path>
```

## Options

- `-p, --push`: push image to registry
- `-r, --repository <repo>`: set repository other than folder name
- `-t, --tag <tag>`: tag image other than latest
- `-u, --user <username>`: username for registry
- `--platform <platforms>`: comma-separated list of platforms (default: `linux/amd64,linux/arm64`)
- `--load`: load the image into docker after build (only works with single platform)

## Examples

### Build and push multiplatform images (default behavior)

```bash
# Build for default platforms (linux/amd64, linux/arm64) and push
pnpm build php/php-fpm -p
pnpm build node/22-bullseye -p
```

### Build for custom platforms

```bash
# Build for ARM64 only and load locally
pnpm build node/22-bullseye --platform linux/arm64 --load

# Build for additional platforms
pnpm build node/22-bullseye --platform linux/amd64,linux/arm64,linux/arm/v7 -p

# Build for a single platform
pnpm build node/22-bullseye --platform linux/amd64 --load
```

**Note**: When building for multiple platforms, you must use `-p` to push to a registry. Use `--load` only for single-platform builds to load the image locally into Docker.
