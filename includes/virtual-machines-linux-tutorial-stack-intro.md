## <a name="create-a-resource-group"></a><span data-ttu-id="1d197-101">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1d197-101">Create a resource group</span></span>

<span data-ttu-id="1d197-102">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1d197-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1d197-103">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="1d197-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1d197-104">下列範例會在 eastus 位置建立名為 myResourceGroup 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1d197-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="1d197-105">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1d197-105">Create a virtual machine</span></span>

<span data-ttu-id="1d197-106">使用 [az vm create](/cli/azure/vm#create) 命令來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="1d197-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="1d197-107">下列範例會建立名為 myVM 的 VM，並建立 SSH 金鑰 (如果它們不存在於預設金鑰位置)。</span><span class="sxs-lookup"><span data-stu-id="1d197-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="1d197-108">若要使用一組特定金鑰，請使用 `--ssh-key-value` 選項。</span><span class="sxs-lookup"><span data-stu-id="1d197-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="1d197-109">建立 VM 後，Azure CLI 會顯示類似下列範例的資訊。</span><span class="sxs-lookup"><span data-stu-id="1d197-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="1d197-110">記下 `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="1d197-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="1d197-111">此位址用來存取 VM。</span><span class="sxs-lookup"><span data-stu-id="1d197-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="1d197-112">針對 Web 流量開啟連接埠 80</span><span class="sxs-lookup"><span data-stu-id="1d197-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="1d197-113">依預設只能透過 SSH 連線至 Azure 中部署的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="1d197-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="1d197-114">因為此 VM 即將成為 Web 伺服器，所以您需要從網際網路開啟連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="1d197-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="1d197-115">使用 [az vm open-port](/cli/azure/vm#open-port) 命令來開啟所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1d197-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="1d197-116">透過 SSH 連線到您的 VM</span><span class="sxs-lookup"><span data-stu-id="1d197-116">SSH into your VM</span></span>


<span data-ttu-id="1d197-117">如果您還不知道您 VM 的公用 IP 位址，請執行 [az network public-ip list](/cli/azure/network/public-ip#list) 命令：</span><span class="sxs-lookup"><span data-stu-id="1d197-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="1d197-118">使用下列命令，建立與虛擬機器的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="1d197-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="1d197-119">替換為您虛擬機器的正確公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1d197-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="1d197-120">在此範例中，IP 位址是 *40.68.254.142*。</span><span class="sxs-lookup"><span data-stu-id="1d197-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

