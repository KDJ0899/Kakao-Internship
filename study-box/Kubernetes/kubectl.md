## **kubectl**

Kybectl은 쿠버네티스 클러스터에 명령을 내리는 CLI(command line interface)입니다.



### Kubectl 문법

kubectl [COMMAND] [TYPE] [NAME] [FLAGS]

- COMMAND : create, get, describe와 같이 하나 혹은 여러개의 리소스에 대한 operation 종류를 선언합니다.

- TYPE : [resource type](https://kubernetes.io/docs/reference/kubectl/overview/#resource-types)에 대해 선언합니다. 리소스 타입은 case-sensitive하고 아래와 같이 선언 가능합니다.

```
$ kubectl get pod pod1
$ kubectl get pods pod1
$ kubectl get po pod1
```

- NAME : 특정 리소스의 이름을 선언합니다. 이름은 case-sensitive합니다. 만약 모든 리소스에 대한 내용을 보고싶다면 아래와 같이 선언합니다.

```java
$ kubectl get pods 
```

만약 여러 리소스들에 대해 한번에 명령을 내리고 싶다면 아래와 같이 선언하면 됩니다.



(1) 똑같은 operation을 여러 같은 type의 리소스에 명령할 경우 : *TYPE1 name1 name2 ...*

```java
$ kubectl get pod example-pod1 example-pod
```

(2) 똑같은 operation을 각기 다른 type의 리소스에 명령할 경우 : *TYPE1/name1 TYPE1/name2 TYPE2/name3 ...*

```java
$ kubectl get pod/example-pod1 replicationcontroller/example-rc1 
```

(3) 똑같은 operation을 여러 다른 file의 리소스에 명령할 경우 : *-f file1 -f file2 ...*

```java
$ kubectl get pod -f ./pod.yaml
```

 

\- FLAGS : 추가적인 option을 선언합니다. 

