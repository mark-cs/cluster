# Configure k3s and cert-manager with the CA Certificate

## Deploy cert-manager using arkade

[arkade](https://github.com/alexellis/arkade), written by Alex Ellis, just makes this easy!

Install it by running (warning SUDO!):

```bash
curl -sLS https://dl.get-arkade.dev | sudo sh
```

Then install cert-manager as follows:

```bash
arkade install cert-manager
```

## Deploy the CA certificate and create Cluster Issuer

Add `ca_crt` and `ca_key` variables to the Ansible variables.
The values should be the base64 encoded versions of the `ca.pem` and `ca-key.pem` files from the output of the previous step.

The required yaml to create a secret in the cluster with the CA key and certificate can be produced with:

```bash
TLS_CRT=`cat ../ca/ca.pem | base64`
TLS_KEY=`cat ../ca/ca-key.pem | base64`
sed -e "s/\${tls.key}/$TLS_KEY/" -e "s/\${tls.crt}/$TLS_CRT/" certificate.tpl.yml > certificate.yml 
```

Create CA Secret and Cluster Issuer in k3s cluster, verifying results.

```bash
kubectl apply -f certificate.yml
kubectl apply -f cluster-issuer.yml

kubectl get secrets -n cert-manager
kubectl get clusterissuer -n cert-manager
```