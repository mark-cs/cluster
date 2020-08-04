# Test Service

This is a test service (expects cert-manager to be configured).
It runs in the `example` namespace.

To run it:

```bash
kubectl create namespace example
kubectl apply -f hello.yml
```