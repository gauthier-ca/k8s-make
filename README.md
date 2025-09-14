# k8s-make

Simple convenience makefiles to build and deploy apps seemlessly to multiple k8s using kustomize manifests. Use only what you need, and override as needed.

## Usage
To start you need an app repository containing a Dockerfile and a kustomize manifest. You also need a kubernetes cluster, e.g. Docker Desktop, and GNU make installed. With that available, clone this repository. Then, in your own app repository, add a Makefile containing:

```
include ../k8s-make/targets/base
include ../k8s-make/targets/build
include ../k8s-make/targets/run
include ../k8s-make/targets/stop
include ../k8s-make/targets/clean
```
Change the relative paths as needed. You can now build and run your app with:
```
make
```

## Targets

The following targets are available:

<dl>
  <dt>all (default)</dt>
  <dd>Build and run the app.</dd>
  <dt>build</dt>
  <dd>Build the image.</dd>
  <dt>clean</dt>
  <dd>Remove all resources and images.</dd>
  <dt>config</dt>
  <dd>Dump the makefile config variables.</dd>
  <dt>deploy</dt>
  <dd>Deploy resources to k8s.</dd>
  <dt>help</dt>
  <dd>List the available targets.</dd>
  <dt>login</dt>
  <dd>Login to the registry.</dd>
  <dt>push</dt>
  <dd>Push to the registry.</dd>
  <dt>repo</dt>
  <dd>Create the initial ECR repo (for AWS ECR).</dd>
  <dt>run</dt>
  <dd>Deploy, then test.</dd>
  <dt>stop</dt>
  <dd>Remove all non persistent resources.</dd>
  <dt>test</dt>
  <dd>Run tests.</dd>
</dl>

Persistent resources are defined by adding `metadata.labels.delete: persist` in their manifest. Commands can be combined, e.g.:
```
make clean build run
```

## Variables

The following variables are available:

<dl>
  <dt>overlays</dt>
  <dd>Set the path to the kustomize overlays directory. Defaults to `k8s/overlays`.</dd>
  <dt>stage</dt>
  <dd>Specify a specific overlay. Defaults to dev.</dd>
</dl>

`make` Variables can be set on the command line, e.g.:
```
make run stage=prod
```
