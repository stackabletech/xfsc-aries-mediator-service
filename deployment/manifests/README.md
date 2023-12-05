helm install mediator-postgresql \
--namespace pcm-mediator \
--create-namespace \
--version 12.5.6 \
-f helm-bitnami-postgresql-values.yaml \
--repo https://charts.bitnami.com/bitnami postgresql