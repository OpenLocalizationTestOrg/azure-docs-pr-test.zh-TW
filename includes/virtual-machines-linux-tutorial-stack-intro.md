## <a name="create-a-resource-group"></a><span data-ttu-id="81686-101">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="81686-101">Create a resource group</span></span>

<span data-ttu-id="81686-102">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="81686-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="81686-103">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="81686-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="81686-104">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="81686-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="81686-105">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="81686-105">Create a virtual machine</span></span>

<span data-ttu-id="81686-106">建立 VM 以 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="81686-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="81686-107">hello 下列範例會建立名為的 VM *myVM*並建立 SSH 金鑰，如果它們原本不在預設索引鍵位置。</span><span class="sxs-lookup"><span data-stu-id="81686-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="81686-108">toouse 一組特定的金鑰，請使用 hello`--ssh-key-value`選項。</span><span class="sxs-lookup"><span data-stu-id="81686-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="81686-109">建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="81686-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="81686-110">記下 hello `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="81686-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="81686-111">此位址為使用的 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="81686-111">This address is used tooaccess hello VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="81686-112">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="81686-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="81686-113">依預設只能透過 SSH 連線至 Azure 中部署的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="81686-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="81686-114">由於此 VM 即將 toobe web 伺服器，您必須從 hello tooopen 連接埠 80 網際網路。</span><span class="sxs-lookup"><span data-stu-id="81686-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="81686-115">使用 hello [az vm 開啟通訊埠](/cli/azure/vm#open-port)命令 tooopen hello 所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="81686-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="81686-116">透過 SSH 連線到您的 VM</span><span class="sxs-lookup"><span data-stu-id="81686-116">SSH into your VM</span></span>


<span data-ttu-id="81686-117">如果您不知道 hello VM 的公用 IP 位址，請執行 hello [az 網路公用 ip 清單](/cli/azure/network/public-ip#list)命令：</span><span class="sxs-lookup"><span data-stu-id="81686-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="81686-118">使用 hello 下列命令 toocreate 與 hello 虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="81686-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="81686-119">取代 hello 正確公用 IP 位址的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="81686-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="81686-120">在此範例中，hello IP 位址是*40.68.254.142*。</span><span class="sxs-lookup"><span data-stu-id="81686-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

