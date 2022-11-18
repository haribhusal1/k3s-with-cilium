# Role voidengineer.rancher.helm

This role installs Helm binaries and defines reusable tasks.

## Supported variables

For default values see [helm_role_defaults](defaults/main.yml).

```yaml
helm:
  install:
    version:            version of Helm to install
    download_base_url:  base URL from where to download Helm

  target_namespace:     default namespace to deploy Helm Charts
  bootstrap:            default value for Charts deployed with k3s helm-controller
```

## Resusable tasks

### chart

This tasks install a HelmChart with k3s [helm-controller](https://rancher.com/docs/k3s/latest/en/helm/).

```yaml
- ansible.builtin.include_role:
    name: voidengineer.rancher.helm
    tasks_from: public/chart
  vars:
    name: <Helm Chart name>
    chart: <Helm Chart name in repository, or complete HTTPS URL to chart archive (.tgz)>
    version: <Helm Chart version (when installing from repository)>
    repo: <Helm Chart repository URL (when installing from repository)>
    target_namespace: <Helm chart target namespace (optional, defaults to variable `helm.target_namespace`)>
    bootstrap: <set to `true` if this chart is needed to bootstrap the cluster>
    values_content: <override complex default Chart values via YAML>
```

### template

This tasks call `helm template` with the given `values_content` and automatically deploy the resulting Kubernetes manifest with k3s [helm-controller](https://rancher.com/docs/k3s/latest/en/helm/#automatically-deploying-manifests-and-helm-charts).

```yaml
- ansible.builtin.include_role:
    name: voidengineer.rancher.helm
    tasks_from: public/template
  vars:
    name: <Helm Chart name>
    chart: <complete HTTPS URL to chart archive (.tgz)>
    target_namespace: <Helm chart target namespace (optional, defaults to variable `helm.target_namespace`)>
    values_content: <override complex default Chart values via YAML>
```
