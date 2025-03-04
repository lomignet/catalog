# Golangci Lint

This Task is a Golang task to validate Go projects.

## Install the task

```
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/main/task/golangci-lint/0.2/golangci-lint.yaml

```

### Parameters

* **package**: base package under validation
* **context**: path to the directory to use as context (default: .)
* **flags**: flags to use for `golangci-lint` command (_default:_--verbose)
* **version**: golangci-lint version to use (_default:_ v1.16)
* **GOOS**: operating system target (_default:_ linux)
* **GOARCH**: architecture target (_default:_ amd64)
* **GO111MODULE**: value of module support (_default:_ auto)
* **GOCACHE**: value for go caching path (_default:_ "")
* **GOMODCACHE**: value for go module caching path (_default:_ "")
* **GOLANGCI_LINT_CACHE**: value for golangci-lint caching path (_default:_ "")

### Workspaces

* **source**: A [Workspace](https://github.com/tektoncd/pipeline/blob/main/docs/workspaces.md) containing the source to build.

## Platforms

The Task can be run on `linux/amd64` platform.

## Usage

This TaskRun runs the Task to validate
[`tektoncd/pipeline`](https://github.com/tektoncd/pipeline) `pkg` package with
`golangci-lint`.

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: lint-my-code
spec:
  taskRef:
    name: golangci-lint
  workspaces:
  - name: source
    persistentVolumeClaim:
      claimName: my-source
  params:
  - name: package
    value: github.com/tektoncd/pipeline
  - name: flags
    value: --verbose
```
