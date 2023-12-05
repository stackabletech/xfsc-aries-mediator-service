## Create manifests

### Namespace and secret

```
kubectl create namespace pcm-mediator && \
kubectl -n pcm-mediator apply -f postgres-secret.yaml
```

### Postgresql Database
```
helm install mediator-postgresql \
--namespace pcm-mediator \
--version 12.5.6 \
-f helm-bitnami-postgresql-values.yaml \
--repo https://charts.bitnami.com/bitnami postgresql
```

### Mediator agent
```
# cd deployment/helm
helm dependency build && \
helm install --create-namespace --namespace pcm-mediator \
--generate-name --set "service.type=ClusterIP" .
```

#### Error
```
2023-12-05 14:43:45,978 indy.libindy.native.indystrgpostgres.postgres_storage DEBUG     src/postgres_storage.rs:666 | connecting to postgres, url_base: "postgresql://mediator:%EF%BF%BD%EF%BF%BD%2D%EF%BF%BD%EF%BF%BD%EF%BF%BD@mediator-postgresql:5432/postgres"
2023-12-05 14:43:45,984 indy.libindy.native.indystrgpostgres ERROR     src/lib.rs:190 | Create storage failed: IOError("IO error during storage operation: database error")
2023-12-05 14:43:45,984 indy.libindy DEBUG _get_error_details: >>>
2023-12-05 14:43:45,984 indy.libindy DEBUG _get_error_details: <<< error_details: {'backtrace': '', 'message': 'Error: Wallet storage error occurred\n  Caused by: Plugin returned error\n'}
```
