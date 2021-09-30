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
2. Add [overlays](./src/bundle/config/overlays/) and [values](./src/bundle/config/values.yaml)
3. Test your bundle: `ytt --data-values-file src/example-values/minikube.yaml  -f target/bundle/config` providing a sample values file from [example-values](./src/examples-values/)
4. Build your bundle `./hack/build.sh`
5. Add it to the [failk8s-repo](https://github.com/failk8s-packages/failk8s-repo) and publish the new repo and test the package from there, or [test with local files](./target/test)

**NOTE**: `develop` versions will not be image locked and will have a version of 0.0.0+develop to comply with semver.