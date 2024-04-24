# Kubernetes

## Simple

`kustomization.yaml`:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
metadata:
  name: opengist

resources:
  - https://github.com/thomiceli/opengist/deploy/
```

## Customize

`kustomization.yaml`:

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
metadata:
  name: opengist

resources:
  - https://github.com/thomiceli/opengist/deploy/

images:
  - name: ghcr.io/thomiceli/opengist
    newTag: v1.7.1

patches:
  # Add your ingress host and ingress classs
  - patch: |-
      - op: add
        path: /spec/rules/0/host
        value: opengist.mydomain.com
      - op: add
        path: /spec/ingressClassName
        value: nginx
    target:
      group: networking.k8s.io
      version: v1
      kind: Ingress
      name: opengist
```
