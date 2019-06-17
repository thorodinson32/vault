#Vault with Docker and Spring Boot

1. **Install vault**
2. **Create Vault container:**  
	*docker run --cap-add=IPC_LOCK \  
    -e 'VAULT_LOCAL_CONFIG={"backend": {"file": {"path": "/vault/file"}}, "default_lease_ttl": "168h", "max_lease_ttl": "720h", "listener": {"tcp": {"address": "0.0.0.0:8200", "tls_disable": 1}}}' \  
    --name vault \  
    -p 8200:8200 \  
    -v {{workspace}}/vault/file:/vault/file \  
    -it vault server*  
3. **Initialize vault:**  
	*vault operator init*
4. **Save the keys generated from init**  
5. **Create environment Variables**
      *export VAULT_ADDR="http://localhost:8200"*
	  *export VAULT_TOKEN="{{root key}}"*  
6. **Enable KV secrets:**
	  *vault secrets enable -path=secret/ kv*
7. **Unseal the vault by running this command with 3 keys:**
	  *vault operator unseal {{key}}*
8. **Insert a secret:**
	   *vault kv put secret/{{appname}}/{{profile}} password=test*

