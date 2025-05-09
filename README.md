# kube-personal-stack

## Prérequis

- **Argo CD** doit être installé et opérationnel dans le namespace `argo-cd` de votre cluster Kubernetes.

Pour installer Argo CD, vous pouvez utiliser le chart Helm officiel : [https://artifacthub.io/packages/helm/argo/argo-cd](https://artifacthub.io/packages/helm/argo/argo-cd)

Exemple d'installation :

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm install argo-cd argo/argo-cd --namespace argo-cd --create-namespace
```

## Déploiement de la stack

Ce dépôt contient une stack d'applications gérées par Argo CD, incluant n8n et Traefik, configurées via des manifests Kubernetes et des projets Argo CD.

### 1. Cloner ce dépôt

```bash
git clone <url-du-repo>
cd kube-personal-stack
```

### 2. Appliquer la stack avec Kustomize

Assurez-vous d'être dans le dossier racine du projet, puis lancez :

```bash
kubectl apply -k .
```

Cela appliquera tous les manifests listés dans `kustomization.yaml` (Applications, AppProjects, Repositories).

### 3. Vérifier dans Argo CD

Rendez-vous sur l'interface web d'Argo CD (habituellement sur `https://<ARGOCD_SERVER>`) pour vérifier que les applications `n8n` et `traefik` sont bien synchronisées et en bonne santé.

## Structure du dépôt

- `kustomization.yaml` : liste des ressources à appliquer
- `Application.*.yaml` : définitions des applications Argo CD
- `AppProject.*.yaml` : définitions des projets Argo CD
- `Repository.*.yaml` : définitions des dépôts Helm utilisés

## Services disponibles

### n8n
n8n est une plateforme d'automatisation de workflows low-code/no-code. Elle permet de connecter différentes applications et services pour automatiser des tâches, orchestrer des processus métiers et manipuler des données. L'interface web de n8n sera accessible via l'URL : http://n8n.localhost (modifiable selon votre configuration d'ingress).

### Traefik
Traefik est un reverse proxy et un contrôleur d'entrée (Ingress Controller) moderne pour Kubernetes. Il gère l'accès aux applications via HTTP/HTTPS, fournit des fonctionnalités de routage, de gestion de certificats et d'observabilité. Le dashboard Traefik sera accessible via l'URL : http://traefik.localhost (modifiable selon votre configuration d'ingress).

### Argo CD
Argo CD est un outil de déploiement continu (CD) pour Kubernetes, permettant de gérer vos applications via GitOps. L'interface web d'Argo CD est accessible via l'URL : http://argocd.localhost (modifiable selon votre configuration d'ingress).

## Notes

- Les namespaces nécessaires (`n8n`, `traefik`) sont créés automatiquement par Argo CD si besoin.
- Les valeurs Helm pour chaque application sont personnalisées dans les manifests correspondants.

---

Pour toute question, ouvrez une issue sur ce dépôt.