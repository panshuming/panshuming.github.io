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
persistentvolumes                 pv                                          false        PersistentVolume
pods                              po                                          true         Pod
podtemplates                                                                  true         PodTemplate
replicationcontrollers            rc                                          true         ReplicationController
resourcequotas                    quota                                       true         ResourceQuota
secrets                                                                       true         Secret
serviceaccounts                   sa                                          true         ServiceAccount
services                          svc                                         true         Service
mutatingwebhookconfigurations                  admissionregistration.k8s.io   false        MutatingWebhookConfiguration
validatingwebhookconfigurations                admissionregistration.k8s.io   false        ValidatingWebhookConfiguration
customresourcedefinitions         crd,crds     apiextensions.k8s.io           false        CustomResourceDefinition
apiservices                                    apiregistration.k8s.io         false        APIService
controllerrevisions                            apps                           true         ControllerRevision
daemonsets                        ds           apps                           true         DaemonSet
deployments                       deploy       apps                           true         Deployment
replicasets                       rs           apps                           true         ReplicaSet
statefulsets                      sts          apps                           true         StatefulSet
tokenreviews                                   authentication.k8s.io          false        TokenReview
localsubjectaccessreviews                      authorization.k8s.io           true         LocalSubjectAccessReview
selfsubjectaccessreviews                       authorization.k8s.io           false        SelfSubjectAccessReview
selfsubjectrulesreviews                        authorization.k8s.io           false        SelfSubjectRulesReview
subjectaccessreviews                           authorization.k8s.io           false        SubjectAccessReview
horizontalpodautoscalers          hpa          autoscaling                    true         HorizontalPodAutoscaler
cronjobs                          cj           batch                          true         CronJob
jobs                                           batch                          true         Job
certificatesigningrequests        csr          certificates.k8s.io            false        CertificateSigningRequest
leases                                         coordination.k8s.io            true         Lease
bgpconfigurations                              crd.projectcalico.org          false        BGPConfiguration
bgppeers                                       crd.projectcalico.org          false        BGPPeer
blockaffinities                                crd.projectcalico.org          false        BlockAffinity
clusterinformations                            crd.projectcalico.org          false        ClusterInformation
felixconfigurations                            crd.projectcalico.org          false        FelixConfiguration
globalnetworkpolicies                          crd.projectcalico.org          false        GlobalNetworkPolicy
globalnetworksets                              crd.projectcalico.org          false        GlobalNetworkSet
hostendpoints                                  crd.projectcalico.org          false        HostEndpoint
ipamblocks                                     crd.projectcalico.org          false        IPAMBlock
ipamconfigs                                    crd.projectcalico.org          false        IPAMConfig
ipamhandles                                    crd.projectcalico.org          false        IPAMHandle
ippools                                        crd.projectcalico.org          false        IPPool
networkpolicies                                crd.projectcalico.org          true         NetworkPolicy
networksets                                    crd.projectcalico.org          true         NetworkSet
endpointslices                                 discovery.k8s.io               true         EndpointSlice
events                            ev           events.k8s.io                  true         Event
ingresses                         ing          extensions                     true         Ingress
ingressclasses                                 networking.k8s.io              false        IngressClass
ingresses                         ing          networking.k8s.io              true         Ingress
networkpolicies                   netpol       networking.k8s.io              true         NetworkPolicy
runtimeclasses                                 node.k8s.io                    false        RuntimeClass
poddisruptionbudgets              pdb          policy                         true         PodDisruptionBudget
podsecuritypolicies               psp          policy                         false        PodSecurityPolicy
clusterrolebindings                            rbac.authorization.k8s.io      false        ClusterRoleBinding
clusterroles                                   rbac.authorization.k8s.io      false        ClusterRole
rolebindings                                   rbac.authorization.k8s.io      true         RoleBinding
roles                                          rbac.authorization.k8s.io      true         Role
priorityclasses                   pc           scheduling.k8s.io              false        PriorityClass
csidrivers                                     storage.k8s.io                 false        CSIDriver
csinodes                                       storage.k8s.io                 false        CSINode
storageclasses                    sc           storage.k8s.io                 false        StorageClass
volumeattachments                              storage.k8s.io                 false        VolumeAttachment
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
authorization.k8s.io/v1beta1
autoscaling/v1
autoscaling/v2beta1
autoscaling/v2beta2
batch/v1
batch/v1beta1
certificates.k8s.io/v1
certificates.k8s.io/v1beta1
coordination.k8s.io/v1
coordination.k8s.io/v1beta1
crd.projectcalico.org/v1
discovery.k8s.io/v1beta1
events.k8s.io/v1
events.k8s.io/v1beta1
extensions/v1beta1
networking.k8s.io/v1
networking.k8s.io/v1beta1
node.k8s.io/v1beta1
policy/v1beta1
rbac.authorization.k8s.io/v1
rbac.authorization.k8s.io/v1beta1
scheduling.k8s.io/v1
scheduling.k8s.io/v1beta1
storage.k8s.io/v1
storage.k8s.io/v1beta1
v1
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

   spec <Object>
     Specification of the desired behavior of the Deployment.

   status       <Object>
     Most recently observed status of the Deployment.
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
      managedFields     <[]Object>
         apiVersion     <string>
         fieldsType     <string>
         fieldsV1       <map[string]>
         manager        <string>
         operation      <string>
         time   <string>
      name      <string>
      namespace <string>
      ownerReferences   <[]Object>
         apiVersion     <string>
         blockOwnerDeletion     <boolean>
         controller     <boolean>
         kind   <string>
         name   <string>
         uid    <string>
      resourceVersion   <string>
      selfLink  <string>
      uid       <string>
   spec <Object>
      minReadySeconds   <integer>
      paused    <boolean>
      progressDeadlineSeconds   <integer>
      replicas  <integer>
      revisionHistoryLimit      <integer>
      selector  <Object>
         matchExpressions       <[]Object>
            key <string>
            operator    <string>
            values      <[]string>
         matchLabels    <map[string]string>
      strategy  <Object>
         rollingUpdate  <Object>
            maxSurge    <string>
            maxUnavailable      <string>
         type   <string>
      template  <Object>
         metadata       <Object>
            annotations <map[string]string>
            clusterName <string>
            creationTimestamp   <string>
            deletionGracePeriodSeconds  <integer>
            deletionTimestamp   <string>
            finalizers  <[]string>
            generateName        <string>
            generation  <integer>
            labels      <map[string]string>
            managedFields       <[]Object>
               apiVersion       <string>
               fieldsType       <string>
               fieldsV1 <map[string]>
               manager  <string>
               operation        <string>
               time     <string>
            name        <string>
            namespace   <string>
            ownerReferences     <[]Object>
               apiVersion       <string>
               blockOwnerDeletion       <boolean>
               controller       <boolean>
               kind     <string>
               name     <string>
               uid      <string>
            resourceVersion     <string>
            selfLink    <string>
            uid <string>
         spec   <Object>
            activeDeadlineSeconds       <integer>
            affinity    <Object>
               nodeAffinity     <Object>
                  preferredDuringSchedulingIgnoredDuringExecution       <[]Object>
                     preference <Object>
                        matchExpressions        <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
                        matchFields     <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
                     weight     <integer>
                  requiredDuringSchedulingIgnoredDuringExecution        <Object>
                     nodeSelectorTerms  <[]Object>
                        matchExpressions        <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
                        matchFields     <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
               podAffinity      <Object>
                  preferredDuringSchedulingIgnoredDuringExecution       <[]Object>
                     podAffinityTerm    <Object>
                        labelSelector   <Object>
                           matchExpressions     <[]Object>
                              key       <string>
                              operator  <string>
                              values    <[]string>
                           matchLabels  <map[string]string>
                        namespaces      <[]string>
                        topologyKey     <string>
                     weight     <integer>
                  requiredDuringSchedulingIgnoredDuringExecution        <[]Object>
                     labelSelector      <Object>
                        matchExpressions        <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
                        matchLabels     <map[string]string>
                     namespaces <[]string>
                     topologyKey        <string>
               podAntiAffinity  <Object>
                  preferredDuringSchedulingIgnoredDuringExecution       <[]Object>
                     podAffinityTerm    <Object>
                        labelSelector   <Object>
                           matchExpressions     <[]Object>
                              key       <string>
                              operator  <string>
                              values    <[]string>
                           matchLabels  <map[string]string>
                        namespaces      <[]string>
                        topologyKey     <string>
                     weight     <integer>
                  requiredDuringSchedulingIgnoredDuringExecution        <[]Object>
                     labelSelector      <Object>
                        matchExpressions        <[]Object>
                           key  <string>
                           operator     <string>
                           values       <[]string>
                        matchLabels     <map[string]string>
                     namespaces <[]string>
                     topologyKey        <string>
            automountServiceAccountToken        <boolean>
            containers  <[]Object>
               args     <[]string>
               command  <[]string>
               env      <[]Object>
                  name  <string>
                  value <string>
                  valueFrom     <Object>
                     configMapKeyRef    <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
                     fieldRef   <Object>
                        apiVersion      <string>
                        fieldPath       <string>
                     resourceFieldRef   <Object>
                        containerName   <string>
                        divisor <string>
                        resource        <string>
                     secretKeyRef       <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
               envFrom  <[]Object>
                  configMapRef  <Object>
                     name       <string>
                     optional   <boolean>
                  prefix        <string>
                  secretRef     <Object>
                     name       <string>
                     optional   <boolean>
               image    <string>
               imagePullPolicy  <string>
               lifecycle        <Object>
                  postStart     <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
                  preStop       <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
               livenessProbe    <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               name     <string>
               ports    <[]Object>
                  containerPort <integer>
                  hostIP        <string>
                  hostPort      <integer>
                  name  <string>
                  protocol      <string>
               readinessProbe   <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               resources        <Object>
                  limits        <map[string]string>
                  requests      <map[string]string>
               securityContext  <Object>
                  allowPrivilegeEscalation      <boolean>
                  capabilities  <Object>
                     add        <[]string>
                     drop       <[]string>
                  privileged    <boolean>
                  procMount     <string>
                  readOnlyRootFilesystem        <boolean>
                  runAsGroup    <integer>
                  runAsNonRoot  <boolean>
                  runAsUser     <integer>
                  seLinuxOptions        <Object>
                     level      <string>
                     role       <string>
                     type       <string>
                     user       <string>
                  seccompProfile        <Object>
                     localhostProfile   <string>
                     type       <string>
                  windowsOptions        <Object>
                     gmsaCredentialSpec <string>
                     gmsaCredentialSpecName     <string>
                     runAsUserName      <string>
               startupProbe     <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               stdin    <boolean>
               stdinOnce        <boolean>
               terminationMessagePath   <string>
               terminationMessagePolicy <string>
               tty      <boolean>
               volumeDevices    <[]Object>
                  devicePath    <string>
                  name  <string>
               volumeMounts     <[]Object>
                  mountPath     <string>
                  mountPropagation      <string>
                  name  <string>
                  readOnly      <boolean>
                  subPath       <string>
                  subPathExpr   <string>
               workingDir       <string>
            dnsConfig   <Object>
               nameservers      <[]string>
               options  <[]Object>
                  name  <string>
                  value <string>
               searches <[]string>
            dnsPolicy   <string>
            enableServiceLinks  <boolean>
            ephemeralContainers <[]Object>
               args     <[]string>
               command  <[]string>
               env      <[]Object>
                  name  <string>
                  value <string>
                  valueFrom     <Object>
                     configMapKeyRef    <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
                     fieldRef   <Object>
                        apiVersion      <string>
                        fieldPath       <string>
                     resourceFieldRef   <Object>
                        containerName   <string>
                        divisor <string>
                        resource        <string>
                     secretKeyRef       <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
               envFrom  <[]Object>
                  configMapRef  <Object>
                     name       <string>
                     optional   <boolean>
                  prefix        <string>
                  secretRef     <Object>
                     name       <string>
                     optional   <boolean>
               image    <string>
               imagePullPolicy  <string>
               lifecycle        <Object>
                  postStart     <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
                  preStop       <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
               livenessProbe    <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               name     <string>
               ports    <[]Object>
                  containerPort <integer>
                  hostIP        <string>
                  hostPort      <integer>
                  name  <string>
                  protocol      <string>
               readinessProbe   <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               resources        <Object>
                  limits        <map[string]string>
                  requests      <map[string]string>
               securityContext  <Object>
                  allowPrivilegeEscalation      <boolean>
                  capabilities  <Object>
                     add        <[]string>
                     drop       <[]string>
                  privileged    <boolean>
                  procMount     <string>
                  readOnlyRootFilesystem        <boolean>
                  runAsGroup    <integer>
                  runAsNonRoot  <boolean>
                  runAsUser     <integer>
                  seLinuxOptions        <Object>
                     level      <string>
                     role       <string>
                     type       <string>
                     user       <string>
                  seccompProfile        <Object>
                     localhostProfile   <string>
                     type       <string>
                  windowsOptions        <Object>
                     gmsaCredentialSpec <string>
                     gmsaCredentialSpecName     <string>
                     runAsUserName      <string>
               startupProbe     <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               stdin    <boolean>
               stdinOnce        <boolean>
               targetContainerName      <string>
               terminationMessagePath   <string>
               terminationMessagePolicy <string>
               tty      <boolean>
               volumeDevices    <[]Object>
                  devicePath    <string>
                  name  <string>
               volumeMounts     <[]Object>
                  mountPath     <string>
                  mountPropagation      <string>
                  name  <string>
                  readOnly      <boolean>
                  subPath       <string>
                  subPathExpr   <string>
               workingDir       <string>
            hostAliases <[]Object>
               hostnames        <[]string>
               ip       <string>
            hostIPC     <boolean>
            hostNetwork <boolean>
            hostPID     <boolean>
            hostname    <string>
            imagePullSecrets    <[]Object>
               name     <string>
            initContainers      <[]Object>
               args     <[]string>
               command  <[]string>
               env      <[]Object>
                  name  <string>
                  value <string>
                  valueFrom     <Object>
                     configMapKeyRef    <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
                     fieldRef   <Object>
                        apiVersion      <string>
                        fieldPath       <string>
                     resourceFieldRef   <Object>
                        containerName   <string>
                        divisor <string>
                        resource        <string>
                     secretKeyRef       <Object>
                        key     <string>
                        name    <string>
                        optional        <boolean>
               envFrom  <[]Object>
                  configMapRef  <Object>
                     name       <string>
                     optional   <boolean>
                  prefix        <string>
                  secretRef     <Object>
                     name       <string>
                     optional   <boolean>
               image    <string>
               imagePullPolicy  <string>
               lifecycle        <Object>
                  postStart     <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
                  preStop       <Object>
                     exec       <Object>
                        command <[]string>
                     httpGet    <Object>
                        host    <string>
                        httpHeaders     <[]Object>
                           name <string>
                           value        <string>
                        path    <string>
                        port    <string>
                        scheme  <string>
                     tcpSocket  <Object>
                        host    <string>
                        port    <string>
               livenessProbe    <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               name     <string>
               ports    <[]Object>
                  containerPort <integer>
                  hostIP        <string>
                  hostPort      <integer>
                  name  <string>
                  protocol      <string>
               readinessProbe   <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               resources        <Object>
                  limits        <map[string]string>
                  requests      <map[string]string>
               securityContext  <Object>
                  allowPrivilegeEscalation      <boolean>
                  capabilities  <Object>
                     add        <[]string>
                     drop       <[]string>
                  privileged    <boolean>
                  procMount     <string>
                  readOnlyRootFilesystem        <boolean>
                  runAsGroup    <integer>
                  runAsNonRoot  <boolean>
                  runAsUser     <integer>
                  seLinuxOptions        <Object>
                     level      <string>
                     role       <string>
                     type       <string>
                     user       <string>
                  seccompProfile        <Object>
                     localhostProfile   <string>
                     type       <string>
                  windowsOptions        <Object>
                     gmsaCredentialSpec <string>
                     gmsaCredentialSpecName     <string>
                     runAsUserName      <string>
               startupProbe     <Object>
                  exec  <Object>
                     command    <[]string>
                  failureThreshold      <integer>
                  httpGet       <Object>
                     host       <string>
                     httpHeaders        <[]Object>
                        name    <string>
                        value   <string>
                     path       <string>
                     port       <string>
                     scheme     <string>
                  initialDelaySeconds   <integer>
                  periodSeconds <integer>
                  successThreshold      <integer>
                  tcpSocket     <Object>
                     host       <string>
                     port       <string>
                  timeoutSeconds        <integer>
               stdin    <boolean>
               stdinOnce        <boolean>
               terminationMessagePath   <string>
               terminationMessagePolicy <string>
               tty      <boolean>
               volumeDevices    <[]Object>
                  devicePath    <string>
                  name  <string>
               volumeMounts     <[]Object>
                  mountPath     <string>
                  mountPropagation      <string>
                  name  <string>
                  readOnly      <boolean>
                  subPath       <string>
                  subPathExpr   <string>
               workingDir       <string>
            nodeName    <string>
            nodeSelector        <map[string]string>
            overhead    <map[string]string>
            preemptionPolicy    <string>
            priority    <integer>
            priorityClassName   <string>
            readinessGates      <[]Object>
               conditionType    <string>
            restartPolicy       <string>
            runtimeClassName    <string>
            schedulerName       <string>
            securityContext     <Object>
               fsGroup  <integer>
               fsGroupChangePolicy      <string>
               runAsGroup       <integer>
               runAsNonRoot     <boolean>
               runAsUser        <integer>
               seLinuxOptions   <Object>
                  level <string>
                  role  <string>
                  type  <string>
                  user  <string>
               seccompProfile   <Object>
                  localhostProfile      <string>
                  type  <string>
               supplementalGroups       <[]integer>
               sysctls  <[]Object>
                  name  <string>
                  value <string>
               windowsOptions   <Object>
                  gmsaCredentialSpec    <string>
                  gmsaCredentialSpecName        <string>
                  runAsUserName <string>
            serviceAccount      <string>
            serviceAccountName  <string>
            setHostnameAsFQDN   <boolean>
            shareProcessNamespace       <boolean>
            subdomain   <string>
            terminationGracePeriodSeconds       <integer>
            tolerations <[]Object>
               effect   <string>
               key      <string>
               operator <string>
               tolerationSeconds        <integer>
               value    <string>
            topologySpreadConstraints   <[]Object>
               labelSelector    <Object>
                  matchExpressions      <[]Object>
                     key        <string>
                     operator   <string>
                     values     <[]string>
                  matchLabels   <map[string]string>
               maxSkew  <integer>
               topologyKey      <string>
               whenUnsatisfiable        <string>
            volumes     <[]Object>
               awsElasticBlockStore     <Object>
                  fsType        <string>
                  partition     <integer>
                  readOnly      <boolean>
                  volumeID      <string>
               azureDisk        <Object>
                  cachingMode   <string>
                  diskName      <string>
                  diskURI       <string>
                  fsType        <string>
                  kind  <string>
                  readOnly      <boolean>
               azureFile        <Object>
                  readOnly      <boolean>
                  secretName    <string>
                  shareName     <string>
               cephfs   <Object>
                  monitors      <[]string>
                  path  <string>
                  readOnly      <boolean>
                  secretFile    <string>
                  secretRef     <Object>
                     name       <string>
                  user  <string>
               cinder   <Object>
                  fsType        <string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
                  volumeID      <string>
               configMap        <Object>
                  defaultMode   <integer>
                  items <[]Object>
                     key        <string>
                     mode       <integer>
                     path       <string>
                  name  <string>
                  optional      <boolean>
               csi      <Object>
                  driver        <string>
                  fsType        <string>
                  nodePublishSecretRef  <Object>
                     name       <string>
                  readOnly      <boolean>
                  volumeAttributes      <map[string]string>
               downwardAPI      <Object>
                  defaultMode   <integer>
                  items <[]Object>
                     fieldRef   <Object>
                        apiVersion      <string>
                        fieldPath       <string>
                     mode       <integer>
                     path       <string>
                     resourceFieldRef   <Object>
                        containerName   <string>
                        divisor <string>
                        resource        <string>
               emptyDir <Object>
                  medium        <string>
                  sizeLimit     <string>
               ephemeral        <Object>
                  readOnly      <boolean>
                  volumeClaimTemplate   <Object>
                     metadata   <Object>
                        annotations     <map[string]string>
                        clusterName     <string>
                        creationTimestamp       <string>
                        deletionGracePeriodSeconds      <integer>
                        deletionTimestamp       <string>
                        finalizers      <[]string>
                        generateName    <string>
                        generation      <integer>
                        labels  <map[string]string>
                        managedFields   <[]Object>
                           apiVersion   <string>
                           fieldsType   <string>
                           fieldsV1     <map[string]>
                           manager      <string>
                           operation    <string>
                           time <string>
                        name    <string>
                        namespace       <string>
                        ownerReferences <[]Object>
                           apiVersion   <string>
                           blockOwnerDeletion   <boolean>
                           controller   <boolean>
                           kind <string>
                           name <string>
                           uid  <string>
                        resourceVersion <string>
                        selfLink        <string>
                        uid     <string>
                     spec       <Object>
                        accessModes     <[]string>
                        dataSource      <Object>
                           apiGroup     <string>
                           kind <string>
                           name <string>
                        resources       <Object>
                           limits       <map[string]string>
                           requests     <map[string]string>
                        selector        <Object>
                           matchExpressions     <[]Object>
                              key       <string>
                              operator  <string>
                              values    <[]string>
                           matchLabels  <map[string]string>
                        storageClassName        <string>
                        volumeMode      <string>
                        volumeName      <string>
               fc       <Object>
                  fsType        <string>
                  lun   <integer>
                  readOnly      <boolean>
                  targetWWNs    <[]string>
                  wwids <[]string>
               flexVolume       <Object>
                  driver        <string>
                  fsType        <string>
                  options       <map[string]string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
               flocker  <Object>
                  datasetName   <string>
                  datasetUUID   <string>
               gcePersistentDisk        <Object>
                  fsType        <string>
                  partition     <integer>
                  pdName        <string>
                  readOnly      <boolean>
               gitRepo  <Object>
                  directory     <string>
                  repository    <string>
                  revision      <string>
               glusterfs        <Object>
                  endpoints     <string>
                  path  <string>
                  readOnly      <boolean>
               hostPath <Object>
                  path  <string>
                  type  <string>
               iscsi    <Object>
                  chapAuthDiscovery     <boolean>
                  chapAuthSession       <boolean>
                  fsType        <string>
                  initiatorName <string>
                  iqn   <string>
                  iscsiInterface        <string>
                  lun   <integer>
                  portals       <[]string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
                  targetPortal  <string>
               name     <string>
               nfs      <Object>
                  path  <string>
                  readOnly      <boolean>
                  server        <string>
               persistentVolumeClaim    <Object>
                  claimName     <string>
                  readOnly      <boolean>
               photonPersistentDisk     <Object>
                  fsType        <string>
                  pdID  <string>
               portworxVolume   <Object>
                  fsType        <string>
                  readOnly      <boolean>
                  volumeID      <string>
               projected        <Object>
                  defaultMode   <integer>
                  sources       <[]Object>
                     configMap  <Object>
                        items   <[]Object>
                           key  <string>
                           mode <integer>
                           path <string>
                        name    <string>
                        optional        <boolean>
                     downwardAPI        <Object>
                        items   <[]Object>
                           fieldRef     <Object>
                              apiVersion        <string>
                              fieldPath <string>
                           mode <integer>
                           path <string>
                           resourceFieldRef     <Object>
                              containerName     <string>
                              divisor   <string>
                              resource  <string>
                     secret     <Object>
                        items   <[]Object>
                           key  <string>
                           mode <integer>
                           path <string>
                        name    <string>
                        optional        <boolean>
                     serviceAccountToken        <Object>
                        audience        <string>
                        expirationSeconds       <integer>
                        path    <string>
               quobyte  <Object>
                  group <string>
                  readOnly      <boolean>
                  registry      <string>
                  tenant        <string>
                  user  <string>
                  volume        <string>
               rbd      <Object>
                  fsType        <string>
                  image <string>
                  keyring       <string>
                  monitors      <[]string>
                  pool  <string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
                  user  <string>
               scaleIO  <Object>
                  fsType        <string>
                  gateway       <string>
                  protectionDomain      <string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
                  sslEnabled    <boolean>
                  storageMode   <string>
                  storagePool   <string>
                  system        <string>
                  volumeName    <string>
               secret   <Object>
                  defaultMode   <integer>
                  items <[]Object>
                     key        <string>
                     mode       <integer>
                     path       <string>
                  optional      <boolean>
                  secretName    <string>
               storageos        <Object>
                  fsType        <string>
                  readOnly      <boolean>
                  secretRef     <Object>
                     name       <string>
                  volumeName    <string>
                  volumeNamespace       <string>
               vsphereVolume    <Object>
                  fsType        <string>
                  storagePolicyID       <string>
                  storagePolicyName     <string>
                  volumePath    <string>
   status       <Object>
      availableReplicas <integer>
      collisionCount    <integer>
      conditions        <[]Object>
         lastTransitionTime     <string>
         lastUpdateTime <string>
         message        <string>
         reason <string>
         status <string>
         type   <string>
      observedGeneration        <integer>
      readyReplicas     <integer>
      replicas  <integer>
      unavailableReplicas       <integer>
      updatedReplicas   <integer>
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

