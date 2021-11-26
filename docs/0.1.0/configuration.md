# Configuration

```hcl
component "argocd" {
  namespace = "argocd"

  # Params default values

  publicURL = "" # required
  git = {
    repo = ""    # required
  }

  adminGroup = "" # optional

  credentialsSecret = {
    store = {
      name = "default"
      kind = "ClusterSecretStore"
    }
    key = ""      # required
    type = "ssh"  # values: ssh or password
  }

  secret = {
    store = {
      name = "default"
      kind = "ClusterSecretStore"
    }
    key = ""      # required
  }

  # override this section only if you are using
  # a different Dex instance than the default one
  dex = {
    name = "dex"
    namespace = "dex"
  }

  # override this section only if you are NOT using Dex
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
}
```

## Secrets

Secretas referenced by the configuration must be provisioned in the backend service of your choice before installing ArgoCD. 

Unless you changed the configuration of the External Secret component or manually provisioned a custom `SecretStore` resource, you don't need to override the `store` section of each secret reference.