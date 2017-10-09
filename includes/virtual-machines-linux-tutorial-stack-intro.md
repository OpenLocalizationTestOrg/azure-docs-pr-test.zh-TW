## <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。 Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>建立虛擬機器

建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。 

hello 下列範例會建立名為的 VM *myVM*並建立 SSH 金鑰，如果它們原本不在預設索引鍵位置。 toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 記下 hello `publicIpAddress`。 此位址為使用的 tooaccess hello VM。

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a>針對 Web 流量開啟連接埠 80 

依預設只能透過 SSH 連線至 Azure 中部署的 Linux VM。 由於此 VM 即將 toobe web 伺服器，您必須從 hello tooopen 連接埠 80 網際網路。 使用 hello [az vm 開啟通訊埠](/cli/azure/vm#open-port)命令 tooopen hello 所需的連接埠。  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>透過 SSH 連線到您的 VM


如果您不知道 hello VM 的公用 IP 位址，請執行 hello [az 網路公用 ip 清單](/cli/azure/network/public-ip#list)命令：


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。 取代 hello 正確公用 IP 位址的虛擬機器。 在此範例中，hello IP 位址是*40.68.254.142*。

```bash
ssh azureuser@40.68.254.142
```

