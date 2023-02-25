# Debian base

Base image used for debian based instances.

### Notes

`massas_debian` is added with a default UID

### Building and Pushing

For multiple platforms at the same time:

```
docker buildx build --platform linux/amd64,linux/arm64 -t elmassas/debian:v1 --push .
```
