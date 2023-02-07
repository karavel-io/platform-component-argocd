# Configuration

```hcl
component "argocd" {
  namespace = "argocd" # optional

  # Params default values

  publicURL = "" # required, the full URL to reach the Argo instance, e.g. https://deploy.company.com
  git = {
    repo = ""    # required, the git URL containing the Karavel code, e.g. git@github.com:example-company/cloud-infrastructure.git
  }

  adminGroup = "" # optional, the OIDC group that should be given full admin powers

  credentialsSecret = {
    # override this section only if you are not using the default store from the external-secrets component
    store = {
      name = "default"
      kind = "ClusterSecretStore"
    }
    key = ""          # required, should be the store-specific key to the secret, e.g. the Vault or AWS Secrets Manager key
    type = "ssh"      # optional, values: ssh or password
    url = ""          # optional, overrides git.repo in the credential secret
    template = false  # optional, configures the secret as a credentials template, allowing to pass a git namespace as the url above when true (e.g. git@github.com:my-org)
  }

  secret = {
    # override this section only if you are not using the default store from the external-secrets component
    store = {
      name = "default"
      kind = "ClusterSecretStore"
    }
    key = ""     # required, should be the store-specific key to the secret, e.g. the Vault or AWS Secrets Manager key
  }

  # override this section only if you are using
  # a different Dex instance than the default one
  dex = {
    name = "dex"
    namespace = "dex"
  }

  # override this section only if you are NOT using the Dex component
  oidc = {
    config = {
      name = "SSO"
      issuer = ""                         # required
      clientID = ""                       # required
      clientSecret = "$oidc.clientSecret" # see https://argo-cd.readthedocs.io/en/stable/operator-manual/user-management/#sensitive-data-and-sso-client-secrets
      cliClientID = ""                    # optional
      requestedScopes = [
        "openid",
        "profile",
        "email",
        "groups",
      ]
    }
  }

  tracing = {
    enabled = false                                       # optional, automatically enabled by the Tempo component
    endpoint = "tempo.monitoring.svc.cluster.local:4317"  # optional, the OTLP address to use.
  }
}
```

## Secrets

Secrets referenced by the configuration must be provisioned in the backend service of your choice before installing ArgoCD. 

Unless you changed the configuration of the External Secret component or manually provisioned a custom `SecretStore` resource, you don't need to override the `store` section of each secret reference.
