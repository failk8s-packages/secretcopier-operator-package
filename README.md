# package-secretcopier-operator

This package provides secret copy config and injection of image pull secrets into serviceaccounts functionality using [failk8s-operator](https://github.com/failk8s/failk8s-operator).

## Components

* secretcopier-operator

## Configuration

The following configuration values can be set to customize the secretcopier-operator installation.

### Global

| Value | Required/Optional | Description |
|-------|-------------------|-------------|
| `namespace` | Optional | The namespace in which to deploy secretcopier-operator. Default: `failk8s-operator` |
| `wildcard.create` | Required | Boolean. Should it install a wildcard secret copier configuration Default: `True` |
| `wildcard.name` | Optional | The name of the original wildcard secret to copy. Default: `failk8s-operator` |
| `wildcard.namespace` | Optional | The namespace of the original wildcard secret to copy. Default: `REPLACE_ME` |


## Usage Example

This walkthrough guides you through using secretcopier-operator...

## Test

To validate this config:
```
ytt -f config -v wildcard.namespace=projectcontour -v namespace=developer --data-value-yaml wildcard.create=False
```

## Develop checklist

1. Update your [config.json](./config.json) with the package info
2. Update your [vendir.yml](./src/bundle/vendir.yml) with your upstreams
3. `vendir sync` in `src/bundle` to fetch your new upstream files
4. Add [overlays](./src/bundle/config/overlays/) and [values](./src/bundle/config/values.yaml)
5. Update your [bundle.yml](./src/bundle/.imgpkg/bundle.yml) file
6. Test your bundle: `ytt -f config`
7. Lock images used: `kbld -f . --imgpkg-lock-output .imgpkg/images.yml`
8. Publish your bundle: `imgpkg push --bundle quay.io/failk8s/secretcopier-operator-package:develop --file .`. These steps can be done via [hack/build-package.sh](./hack/build-package.sh)
9. Package up your k8s manifests and test in k8s [hack/package-manifests.sh](./hack/package-manifests.sh). The files will be in `target` folder.
