# Alpine base

Base image used for alpine based instances.

### Notes

`massas_alpine` is added with a default UID

### Building and Pushing

For multiple platforms at the same time:

```
docker buildx build --platform linux/amd64,linux/arm64 -t elmassas/alpine:v1 --push .
```
