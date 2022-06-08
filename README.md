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

`helm repo add drone https://charts.drone.io`

https://docs.drone.io/server/provider/github/

setup github OAuth app, note Client ID and Secret
https://docs.github.com/en/developers/apps/building-oauth-apps/creating-an-oauth-app
Create an RPC secret and note this
`openssl rand -hex 16`

complete the `drone\drone-values.yml` with your above information

create drone namespace
`kubectl create namespace drone`

`helm install --name drone --namespace drone drone/drone -f .\drone\drone-values.yml`

# drone-runner-kube install

complete the `drone\drone-runner-kube-values.yml` with your shared secret

`helm install --namespace drone --name drone-runner-kube drone/drone-runner-kube -f .\drone\drone-runner-kube-values.yml`
