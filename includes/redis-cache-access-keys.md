tooconnect tooan Azure Redis 快取執行個體，快取用戶端需要 hello 主機名稱、 連接埠和 hello 快取的索引鍵。 某些用戶端可能會稍有不同的名稱來指稱 toothese 項目。 您可以擷取這項資訊在 hello Azure 入口網站，或使用命令列工具，例如 Azure CLI。

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>擷取主機名稱、 連接埠，以及使用 hello Azure 入口網站的存取金鑰
tooretrieve 主機名稱、 連接埠，與使用 hello Azure 入口網站的存取金鑰[瀏覽](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings)tooyour 快取中 hello [Azure 入口網站](https://portal.azure.com)按一下**存取金鑰**和**屬性**在 hello**資源功能表**。 

![Redis 快取設定](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>使用 Azure CLI 來擷取主機名稱、連接埠及存取金鑰
您可以呼叫的 tooretrieve hello 主機名稱和連接埠使用 Azure CLI 2.0 [az redis 顯示](https://docs.microsoft.com/cli/azure/redis#show)，和 tooretrieve hello 金鑰，您可以呼叫[az redis 清單索引鍵](https://docs.microsoft.com/cli/azure/redis#list-keys)。 hello 下列指令碼會呼叫這兩個命令，echos hello 主機名稱、 通訊埠，以及索引鍵 toohello 主控台。

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

如需有關此指令碼的詳細資訊，請參閱[hello 主機名稱、 通訊埠，以及索引鍵取得 Azure Redis 快取](../articles/redis-cache/scripts/cache-keys-ports.md)。 如需有關 Azure CLI 2.0 的詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) 和[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)。
