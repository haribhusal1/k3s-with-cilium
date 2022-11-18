# Role voidengineer.rancher.cilium

This role installs Cilium as CNI provider.

## Supported variables

For default values see [cilium_role_defaults](defaults/main.yml).

```yaml
cilium:
  enabled:            whether cilium should be used as CNI provider (default: false)

  helm:
    name:             name of the Helm application
    chart:            HTTPS URL to chart archive
    target_namespace: namespace of the Helm application

  config:             cilium configuration (all settings of the Helm Chart are supported; sytnax is exactly like in `values.yaml`)
```

For all supported configuration settings see [values.yaml](https://github.com/cilium/cilium/blob/v1.11.4/install/kubernetes/cilium/values.yaml)
