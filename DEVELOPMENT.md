# Developing

## Getting started

1. Create [a GitHub account](https://github.com/join)
1. Setup
   [GitHub access via SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)
1. [Create and checkout a repo fork](#checkout-your-fork)
1. Set up your [shell environment](#environment-setup)
1. Install [requirements](#requirements)
1. [Set up a Kubernetes cluster](#kubernetes-cluster)
1. [Running Tests](#Running-Tests)

Then you can [iterate](#iterating).

### Checkout your fork

The Go tools require that you clone the repository to the
`src/github.com/openshift-pipelines/tektoncd-pruner` directory in your
[`GOPATH`](https://github.com/golang/go/wiki/SettingGOPATH).

To check out this repository:

1. Create your own
   [fork of this repo](https://help.github.com/articles/fork-a-repo/)
1. Clone it to your machine:

```shell
mkdir -p ${GOPATH}/src/github.com/openshift-pipelines
cd ${GOPATH}/src/github.com/openshift-pipelines
git clone git@github.com:${YOUR_GITHUB_USERNAME}/tektoncd-pruner.git
cd tektoncd-pruner
git remote add upstream git@github.com:openshift-pipelines/tektoncd-pruner.git
git remote set-url --push upstream no_push
```

_Adding the `upstream` remote sets you up nicely for regularly
[syncing your fork](https://help.github.com/articles/syncing-a-fork/)._

### Requirements

You must install these tools:

1. [`go`](https://golang.org/doc/install): The language Tekton
   Pruner is built in
1. [`git`](https://help.github.com/articles/set-up-git/): For source control
1. [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
   (optional): For interacting with your kube cluster

## Kubernetes cluster

To setup a Kubernetes cluster for development, see the Tekton Pipelines [documentation](https://github.com/tektoncd/pipeline/blob/master/DEVELOPMENT.md#kubernetes-cluster).

## Environment Setup

To build the Tekton Pruner project, you'll need to set `GO111MODULE=on`
environment variable to force `go` to use [go
modules](https://github.com/golang/go/wiki/Modules#quick-start).

## Iterating

## Install Pruner

You can stand up a version of this controller on-cluster (to your `kubectl
config current-context`):

```shell
ko apply -f config/
```

### Observability Setup

For development with monitoring and metrics, use the observability setup script:

```shell
./hack/setup-observability-dev.sh
```

This sets up a Kind cluster with Tekton Pruner, Prometheus, and Jaeger. Access via:
- Prometheus: http://localhost:9091
- Jaeger: http://localhost:16686  
- Pruner Metrics: http://localhost:9090/metrics

### Redeploy controller

As you make changes to the code, you can redeploy your controller with:

```shell
ko apply -f config/controller.yaml
```

### Tear it down

You can clean up everything with:

```shell
ko delete -f config/
```

## Accessing logs

To look at the controller logs, run:

```shell
kubectl -n tekton-pipelines logs deployment/tekton-pruner-controller
```

## Running Tests

Pruner uses the standard go testing framework.
Unit tests can be run with:

TO BE UPDATED

Integration tests require a running cluster and Pruner to be installed.
These are protected by a build tag "e2e".
To run integration tests:

TO BE UPDATED
