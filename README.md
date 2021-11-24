# weka-kubernetes

Demo project to show how to use weka with kubernetes

## Requisites

- Docker
- microk8s
- kubectl

## How to use

create the docker image
```
docker build -t localhost:32000/weka-kubernetes .
```

test image by running it on docker container

```
docker run localhost:32000/weka-kubernetes java -cp weka.jar weka.classifiers.trees.J48 -t elecNormNew.arff
```

enable microk8s registry
```
microk8s enable registry
```

push image to the registry

```
docker push localhost:32000/weka-kubernetes
```

start a pod using the image

```
microk8s kubectl run wekakube --image localhost:32000/teste-git --namespace default -- java -cp weka.jar weka.classifiers.trees.J48 -t elecNormNew.arff
```

after a few seconds, check the result

```
microk8s kubectl logs wekakube
```
