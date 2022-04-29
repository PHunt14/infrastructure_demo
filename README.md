# infrastructure_demo

**starting:**
- _docker 20.10.12_
- _minikube 1.25.2_
- _kubectl 1.19.15_
- _helm v2.14.1_
- _vault 1.4.2_
- _drone 1.7.0_


# helm tiller installation
v2.14.1

# drone-server installation

create drone namespace
`kubectl create namespace drone`

`helm install --name drone --namespace drone drone/drone -f .\drone\drone-values.yml`

after executing the helm install this is required (also presented on-screen)

`kubectl create secret generic drone-server-secrets --namespace=drone --from-literal=clientSecret="<secret-here>"`

`helm upgrade drone --reuse-values --set 'sourceControl.provider=github' --set 'sourceControl.github.clientID=<ID-here>' --set 'sourceControl.secret=drone-server-secrets' drone/drone`

# drone-runner-kube install

`helm install --namespace drone --name drone-runner-kube drone/drone-runner-kube -f .\drone\drone-runner-kube-values.yml`

`helm upgrade drone-runner-kube --namespace drone drone/drone-runner-kube -f .\drone\drone-runner-kube-values.yml`
