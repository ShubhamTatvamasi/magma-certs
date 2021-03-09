# magma-certs

Install cert-manager:
```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update

helm install cert-manager jetstack/cert-manager \
  --create-namespace \
  --namespace cert-manager \
  --set installCRDs=true
```
---

Install magma-certs:
```bash
helm install magma-certs .
```

We will get all these secrets:
```
magma-certs-admin-operator-tls
magma-certs-bootstrapper-key
magma-certs-certifier-tls
magma-certs-controller-tls
magma-certs-fluentd-tls
magma-certs-root-tls
```

Check the certificate:
```bash
kubectl get secrets magma-certs-admin-operator-tls \
  -o jsonpath='{.data.tls\.crt}' | \
  base64 -d | openssl x509 -text -noout -in -
```
