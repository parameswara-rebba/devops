# GitOps with Argo CD

A small GitOps project: Argo CD watches this folder and keeps a Kubernetes cluster
in sync with it. It uses the **app-of-apps** pattern to deploy a sample nginx web
application to a dev and a prod namespace.

## How it fits together

```text
bootstrap/root-app.yaml          applied once by hand
        │  watches apps/
        ▼
apps/web-dev.yaml ──────► workloads/web/overlays/dev  ──► namespace web-dev  (1 replica, auto-sync)
apps/web-prod.yaml ─────► workloads/web/overlays/prod ──► namespace web-prod (3 replicas, manual sync)
                                   │
                                   └── both build on workloads/web/base (Deployment + Service)
```

| Path | Purpose |
|---|---|
| `bootstrap/project.yaml` | `AppProject` named `web`: limits the workloads to this repo and the two namespaces |
| `bootstrap/root-app.yaml` | Root `Application` that creates everything in `apps/` |
| `apps/` | One `Application` per environment |
| `workloads/web/base` | The Deployment and Service shared by all environments |
| `workloads/web/overlays` | Kustomize overlays with the per-environment differences |

## Environments

| | dev | prod |
|---|---|---|
| Namespace | `web-dev` | `web-prod` |
| Replicas | 1 | 3 |
| Sync | Automatic, with prune and self-heal | Manual |
| CPU / memory limits | 200m / 128Mi | 500m / 256Mi |

## Prerequisites

- A Kubernetes cluster (minikube, kind, AKS, EKS, GKE, ...) and `kubectl` pointing at it
- This repository is public, so Argo CD can read it without credentials

## Setup

1. Install Argo CD:

   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   kubectl wait --for=condition=available deployment --all -n argocd --timeout=300s
   ```

2. Bootstrap this project. This is the only manual `kubectl apply`; everything
   after it is driven by Git:

   ```bash
   kubectl apply -f gitops-argocd/bootstrap/project.yaml
   kubectl apply -f gitops-argocd/bootstrap/root-app.yaml
   ```

3. Open the Argo CD UI:

   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' | base64 -d; echo
   kubectl -n argocd port-forward svc/argocd-server 8080:443
   ```

   Browse to https://localhost:8080 and log in as `admin` with the password printed above.

4. Check the result. `web-dev` syncs by itself; `web-prod` stays `OutOfSync` until
   you press **Sync** in the UI:

   ```bash
   kubectl -n argocd get applications
   kubectl -n web-dev get pods
   kubectl -n web-dev port-forward svc/web 8081:80   # then open http://localhost:8081
   ```

## The GitOps workflow

Change the cluster by changing Git, never with `kubectl edit`:

1. Edit a manifest, for example the replica count in `workloads/web/overlays/dev/kustomization.yaml`.
2. Commit and push to `master` (ideally through a pull request).
3. Argo CD notices within about three minutes and applies the change to dev.
4. For prod, review the diff in the UI and press **Sync**.

To see self-healing, run `kubectl -n web-dev scale deployment web --replicas=5`:
Argo CD puts it back to the value in Git.

### Add another application

1. Put its manifests under `workloads/<name>/`.
2. Add an `Application` file for it in `apps/`.
3. Allow its namespace in `bootstrap/project.yaml` (and re-apply that file), or give it its own project.

## Preview what will be deployed

```bash
kubectl kustomize gitops-argocd/workloads/web/overlays/dev
kubectl kustomize gitops-argocd/workloads/web/overlays/prod
```

## Clean up

```bash
kubectl -n argocd delete application root   # removes the child applications and the workloads
kubectl delete -f gitops-argocd/bootstrap/project.yaml
kubectl delete namespace argocd web-dev web-prod
```

## Notes

- The Applications track the `master` branch of
  `https://github.com/parameswara-rebba/devops.git`. If the repository is renamed or
  forked, update `repoURL` in `bootstrap/` and `apps/`.
- The root Application uses Argo CD's built-in `default` project because it has to
  create `Application` resources in the `argocd` namespace; the workloads use the
  restricted `web` project.
