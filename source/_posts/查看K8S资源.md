---
title: 查看K8S资源
tags: K8S
categories: K8S
abbrlink: 2928198525
date: 2021-02-02 17:12:33
---


### 查看所有api资源

可以通过命令`kubectl api-resources`来查看索有api资源

```bash
[root@node01 ~]# kubectl api-resources
NAME                              SHORTNAMES   APIGROUP                       NAMESPACED   KIND
bindings                                                                      true         Binding
componentstatuses                 cs                                          false        ComponentStatus
configmaps                        cm                                          true         ConfigMap
endpoints                         ep                                          true         Endpoints
events                            ev                                          true         Event
limitranges                       limits                                      true         LimitRange
namespaces                        ns                                          false        Namespace
nodes                             no                                          false        Node
persistentvolumeclaims            pvc                                         true         PersistentVolumeClaim
。。。
```

除了可以看到资源的对象名称外，还可以看到对象的别名，这时候我们再看到别人的命令如`kubectl get no`这样费解的命令时就可以知道它实际上代表的是`kubectl get nodes`命令

> 查看api的版本，很多yaml配置里都需要指定配置的资源版本，我们经常看到v1、apps/v1这样的配置，到底某个资源的最新版本 是什么呢？

### 查看api版本

可以通过`kubectl api-versions`来查看api的版本

```bash
[root@node01 ~]# kubectl api-versions
admissionregistration.k8s.io/v1
admissionregistration.k8s.io/v1beta1
apiextensions.k8s.io/v1
apiextensions.k8s.io/v1beta1
apiregistration.k8s.io/v1
apiregistration.k8s.io/v1beta1
apps/v1
authentication.k8s.io/v1
authentication.k8s.io/v1beta1
authorization.k8s.io/v1
。。。
```

以上只是整体概况，很多时候我们还想要看到某个api下面都有哪些配置，某一推荐配置的含义等，下面罗列一些查看api的技巧

### 通过`kubectl explain`查看api字段

1. 通过`kubectl explain <资源对象名称>`查看某个资源对象拥有的字段

```bash
[root@node01 ~]# kubectl explain deployment
KIND:     Deployment
VERSION:  apps/v1

DESCRIPTION:
     Deployment enables declarative updates for Pods and ReplicaSets.

FIELDS:
   apiVersion   <string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind <string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata     <Object>
     Standard object metadata.
。。。
```

以上`DESCRIPTION`是对资源对象的简要描述，`FIELDS`则是对所有字段的描述。

2. 列出所有api字段

想要罗列出索有的字段，可以加上`--recursive`来列出索有可能的字段。

```bash
[root@node01 ~]# kubectl explain deployment --recursive
KIND:     Deployment
VERSION:  apps/v1

DESCRIPTION:
     Deployment enables declarative updates for Pods and ReplicaSets.

FIELDS:
   apiVersion   <string>
   kind <string>
   metadata     <Object>
      annotations       <map[string]string>
      clusterName       <string>
      creationTimestamp <string>
      deletionGracePeriodSeconds        <integer>
      deletionTimestamp <string>
      finalizers        <[]string>
      generateName      <string>
      generation        <integer>
      labels    <map[string]string>
。。。
```

以上输出的内容是经过格式化了的，我们可以根据缩进很容易看到某一个字段从属关系

3. 查看具体字段

如果想要知道某一个api名称的详细信息，则可以通过`kubectl explain <资源对象名称.api名称>`的方式来查看

```bash
[root@node01 ~]# kubectl explain deployment.status.updatedReplicas
KIND:     Deployment
VERSION:  apps/v1

FIELD:    updatedReplicas <integer>

DESCRIPTION:
     Total number of non-terminated pods targeted by this deployment that have
     the desired template spec.

```

