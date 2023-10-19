##Create Azure Policy

``` json
# Mount the OIDC auth method
path "sys/auth/oidc" {
  capabilities = [ "create", "read", "update", "delete", "sudo" ]
}

# Configure the OIDC auth method
path "auth/oidc/*" {
  capabilities = [ "create", "read", "update", "delete", "list" ]
}

# Write ACL policies
path "sys/policies/acl/*" {
  capabilities = [ "create", "read", "update", "delete", "list" ]
}

# List available secrets engines to retrieve accessor ID
path "sys/mounts" {
  capabilities = [ "read" ]
}

# Manage secrets engines
path "sys/mounts/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# List, create, update, and delete key/value secrets
path "secret/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}


```

##Setup the Azure config in Vault via the CLI

```
vault write auth/oidc/config \
    oidc_discovery_url="https://login.microsoftonline.com/<azure-tenant-id>/v2.0" \
    oidc_client_id="<azure-client-id>" \
    oidc_client_secret="<azure-secret>" \
    default_role="azure-developers"
```  
   
##Create the Vault role that will work with Azurel]=
```
vault write auth/oidc/role/azure-developers \
    user_claim="email" \
    groups_claim="groups" \
    role_type="oidc" \
    oidc_scopes="https://graph.microsoft.com/.default" \
    allowed_redirect_uris=""http://localhost:8250/oidc/callback",https://<url-redirect >.us/ui/vault/auth/oidc/oidc/callback"
    policies="azure-developers" \
    ttl=1h  
```    