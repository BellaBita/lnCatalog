# LENA Session Server

[LENA](http://devon.lgcns.com/html/lena.html) is is an open source implementation of the Java Servlet, JavaServer Pages, Java Expression Language and Java WebSocket technologies.

## Introduction

This Chart is made from Helm Tomcat 0.2.0 template.
This chart creates a [LENA session server](http://http://devon.lgcns.com/html/lena.html) Deployment, plus Internal Services for the server.
The chart offers an optimization for session service for LENA application servers. 


## Prerequisites

- Kubernetes 1.8+ 

## Provider-specific Prerequisites


## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release stable/tomcat
```

This command deploys a tomcat dedicated server with sane defaults.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the tomcat chart and their default values.

Parameter                       | Description                           | Default
------------------------------- | ------------------------------------- | ----------------------------------------------------------
`image.lena.repository`         | LENA image source repository name     | `lenasupport/lena-session-dev`
`image.lena.tag`                | LENA release tag.                     | `1.3.0e.1-cent7-openjdk8`
`image.pullPolicy`              | Image pull policy                     | `IfNotPresent`
`image.pullSecrets`             | Image pull secrets                    | `[]`
`service.name`                  | LENA session service name             | `lena-session`
`service.externalPort`          | Kubernetes service port               | `6000`
`service.internalPort`          | Tomcat front port                     | `6000`
`service.type`                  | Kubernetes service type               | `ClusteIP`
`resources`                     | CPU/Memory resource requests/limits   | `{}`
`nodeSelector`                  | Node affinity                         | `{}`
`tolerations`                   | Node tolerations                      | `{}`
`lenaManagerIp`                 | LENA Manager IP                       | `127.0.0.1`
`lenaManagerPort`               | LENA Manager Port                     | `7700`

Refer to [values.yaml](values.yaml) for the full run-down on defaults. These are a mixture of Kubernetes and tomcat-related directives that map to environment variables. 

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set Values.someval=My Server,ImageTag=1.0 \
    stable/tomcat
```

The above command deploys Tomcat dedicated with a server name of `My Server` and docker-tomcat image version `1.0`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/stable
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

> *"An emptyDir volume is first created when a Pod is assigned to a Node, and exists as long as that Pod is running on that node. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted forever."*

