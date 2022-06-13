`helm install --name vault incubator/vault`

installed v0.23.9

but then the pods were all ready and deployed?  No need to unseal?  I probably didn't do the backend storage properly, if I were to guess.

bastardizing
https://learn.hashicorp.com/tutorials/vault/kubernetes-minikube-consul


`helm search stable/consul --col-width 240`

was able to get consul installed and then vault containers running:

`helm install --namespace vault --name consul stable/consul -f vault/helm-consul-values.yaml`
`helm install --namespace vault --name vault incubator/vault -f vault/vault-values.yaml --version 0.22.0`

vault operator init -key-shares=1 -key-threshold=1 -format=json -address=http://127.0.0.1:8200

vault operator unseal -address=http://127.0.0.1:8200 "xxxxxxxxxxxxx"