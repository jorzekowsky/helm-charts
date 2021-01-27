# helm-charts

## mundialis helm repo

    helm repo add mundialis https://mundialis.github.io/helm-charts/
    helm repo update
    helm search repo mundialis -l

## commit changes to chart

    helm lint charts/*   
    helm package -u charts/*

    # change branch to helm-repo
    # (move helm packages to helm-repo)

    helm repo index --url https://mundialis.github.io/helm-charts/ .

    git add . && git commit -m "pages commit"
    git push origin helm-repo

## examples

### prerequisites
    helm repo add mundialis https://mundialis.github.io/helm-charts/
    helm repo update

### install actinia with default values
    helm upgrade --install actinia mundialis/actinia

### install actinia with persistence
    helm upgrade --install actinia mundialis/actinia --set "persistence.enabled=true" --set "redis.master.persistence.enabled=true"

### install actinia with ingress enabled
    helm upgrade --install actinia mundialis/actinia --set "ingress.enabled=true"

#### example ingress config

    ingress
      enabled: true
      annotations:
        kubernetes.io/ingress.class: nginx
        kubernetes.io/tls-acme: "true"
      hosts:
        - host: chart-example.local
          paths: [ "/" ]
      tls:
        - secretName: chart-example-tls
          hosts:
            - chart-example.local
