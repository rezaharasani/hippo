# Helm Configuration

In this section, we want to deploy our application on kubernetes cluster (locally). We have decided to show a simulated real work Kubernetes deployment.
So, we need at least three environments to deploy, it means. `dev`, `testing`,
and `production`.

Before doing anything else, we should create three mentioned namespaces. Thurefore, run the following commands:

```
> kubectl create namespace dev
> kubectl create namespace testing
> kubectl create namespace prod
```

Then, we should execute `helm` command to run our deoloyments.

Note: This issue is so important that we have defined three customized `values`
files for each namespace. Moreover, to run our application for every environment, we shuld set `--values` parameter and pass our specific values file for that namespace. Therefore, run the following commands:

```
> cd /path/to/project/helm/dir
> helm install webpp-release-prod --namespace prod --values values-prod.yaml .
> helm install webpp-release-testing --namespace testing --values values-testing.yaml .
> helm install webpp-release-dev --namespace dev --values values-dev.yaml .
```

Subsequently, at the end, we can connect to our application in diffrent 
environments via their spefic port for each.

```
Production:
http://127.0.0.1:9000

Development:
http://127.0.0.1:9001

Testing:
http://127.0.0.1:9002
```