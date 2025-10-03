# Hippo

## Helm
### [1] Run hippo helm via kubtectl command

In this section, we want to deploy our application on kubernetes cluster (locally). We have decided to show a simulated real work Kubernetes deployment.  
So, we need at least three environments to deploy, it means. `dev`, `testing`, and `production`.

Before doing anything else, we should create three mentioned namespaces. Thurefore, run the following commands:

```
> kubectl create namespace dev
> kubectl create namespace testing
> kubectl create namespace prod
```

Then, we should execute `helm` command to run our deoloyments.

**Note**: This issue is so important that we have defined three customized `values`
files for each namespace. Moreover, to run our application for every environment, we shuld set 
`--values` parameter and pass our specific values file for that namespace. Therefore, run the 
following commands:

```
> cd /path/to/project/helm/dir
> helm install webpp-release-prod --namespace prod --values values-prod.yaml helm-webapp/
> helm install webpp-release-testing --namespace testing --values values-testing.yaml helm-webapp/
> helm install webpp-release-dev --namespace dev --values values-dev.yaml helm-webapp/
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

### [2] Run hippo helm via ArgoCD
In order to run and execute this project via ArgoCD, first, we should clone 
the project:
```
> git clone https://github.com/rezaharasani/hippo.git
```

Then, change directory to hippo project:
```
> cd /path/to/project/.../hippo
```

Because this project is just defined to work with helm, so, we do not have seprate directory. Thurefore, we define our argocd parameter, like the 
following commands:

```
> argocd app create hipp-[NS] \
  --repo --repo https://github.com/rezaharasani/hippo.git \
  --path helm-webapp/ \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace [NS]
  --values values-[NS].yaml
```
`NS` means your namespace. (You can run the project under your namespace, like prod, dev, testing).

**Note**: If you are into the `helm-webapp` directory, you can set value `--path` parameter 
with `.` (`dot` means the current directory, means all helm configs are placed in the current 
directory).  

After installation, we can connect to the installed service like the above instructions.


## Kustomize
### [1] Run hippo kustomize via kubtectl command
### [2] Run hippo kustomize via ArgoCD