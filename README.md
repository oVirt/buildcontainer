# Build container for GitHub Actions

This repository contains the source files for the build container for oVirt. This container contains the most commonly
used utilities for building oVirt. The image names are:

```
quay.io/ovirt/buildcontainer:el9stream
quay.io/ovirt/buildcontainer:almalinux9
```

You can use it in GitHub Actions as follows:

```yaml
name: build
on:
  push:
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        include:
          - name: el9
            container-name: el9stream
          - name: almalinux9
            container-name: almalinux9
    name: ${{ matrix.name }}
    container:
      image: quay.io/ovirt/buildcontainer:${{ matrix.container-name }}
    steps:
      # Add your steps here
```

## Building

You can build  and push the containers easily using `docker-compose`:

```
docker-compose build
docker-compose push
```
