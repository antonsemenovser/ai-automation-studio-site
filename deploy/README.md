# Deploy — static site on the kotkan k8s cluster

Same convention as `retif/kotkanagrilli.fi`: `Containerfile` + Helm chart +
Woodpecker; Flux rolls it out; the subdomain comes from the Ingress `host`.

## What's here
- `Containerfile` — `nginxinc/nginx-unprivileged` serving the static site on
  `:8080` (non-root, k8s-friendly). Verified locally: builds and serves the
  site with HTTP 200.
- `chart/` — Deployment + Service + **Ingress** (`host: studio.kotkanagrilli.fi`,
  `kube-system-traefik`). `helm template` renders clean.
- `.woodpecker.yaml` — CI: build `--platform linux/arm64` → push image, package
  + push chart to the Gitea OCI registry.

## What the operator (Сашко) provisions once
1. **Mirror to Gitea + Woodpecker** with `gitea_clone_token` /
   `gitea_packages_token` (as the kotkanagrilli pipeline).
2. **`gitea-registry-creds`** pull secret in the namespace.
3. **DNS** for the chosen subdomain (`studio.kotkanagrilli.fi` or another) →
   Cloudflare → cluster, plus a TLS cert if Traefik doesn't issue it
   automatically.
4. **Flux HelmRelease** → `oci://git.oleks.space/oleks/charts/ai-studio-site`.

Change the subdomain in `chart/values.yaml` (`ingress.host`).

## Build/run locally
```
docker build -f deploy/Containerfile -t ai-studio-site .
docker run --rm -p 8080:8080 ai-studio-site   # http://localhost:8080
```
