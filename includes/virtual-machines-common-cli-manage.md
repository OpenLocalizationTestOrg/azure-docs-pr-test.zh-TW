<span data-ttu-id="9b667-101">hello Azure CLI 2.0 可讓您 toocreate 和管理您的 Azure 資源上 macOS、 Linux 及 Windows。</span><span class="sxs-lookup"><span data-stu-id="9b667-101">hello Azure CLI 2.0 allows you toocreate and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="9b667-102">這篇文章詳細說明一些最常見命令 toocreate hello 和管理虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="9b667-102">This article details some of hello most common commands toocreate and manage virtual machines (VMs).</span></span>

<span data-ttu-id="9b667-103">這篇文章需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9b667-103">This article requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9b667-104">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9b667-104">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9b667-105">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9b667-105">If you need tooupgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="9b667-106">您也可以在瀏覽器中使用 [Cloud Shell](/azure/cloud-shell/quickstart)。</span><span class="sxs-lookup"><span data-stu-id="9b667-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="9b667-107">Azure CLI 中的基本 Azure Resource Manager 命令</span><span class="sxs-lookup"><span data-stu-id="9b667-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="9b667-108">如需詳細說明使用特定的命令列參數和選項，您可以使用 hello 線上命令說明和選項輸入`az <command> <subcommand> --help`。</span><span class="sxs-lookup"><span data-stu-id="9b667-108">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="9b667-109">建立 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-109">Create VMs</span></span>
| <span data-ttu-id="9b667-110">工作</span><span class="sxs-lookup"><span data-stu-id="9b667-110">Task</span></span> | <span data-ttu-id="9b667-111">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="9b667-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9b667-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="9b667-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="9b667-113">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="9b667-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="9b667-114">建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="9b667-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="9b667-115">管理 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="9b667-115">Manage VM state</span></span>
| <span data-ttu-id="9b667-116">工作</span><span class="sxs-lookup"><span data-stu-id="9b667-116">Task</span></span> | <span data-ttu-id="9b667-117">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="9b667-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9b667-118">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-119">停止 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-120">解除配置 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-121">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-122">重新部署 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-123">刪除 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="9b667-124">取得 VM 資訊</span><span class="sxs-lookup"><span data-stu-id="9b667-124">Get VM info</span></span>
| <span data-ttu-id="9b667-125">工作</span><span class="sxs-lookup"><span data-stu-id="9b667-125">Task</span></span> | <span data-ttu-id="9b667-126">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="9b667-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9b667-127">列出 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="9b667-128">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="9b667-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="9b667-129">取得 VM 資源的使用量</span><span class="sxs-lookup"><span data-stu-id="9b667-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="9b667-130">取得所有可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="9b667-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="9b667-131">磁碟和映像</span><span class="sxs-lookup"><span data-stu-id="9b667-131">Disks and images</span></span>
| <span data-ttu-id="9b667-132">工作</span><span class="sxs-lookup"><span data-stu-id="9b667-132">Task</span></span> | <span data-ttu-id="9b667-133">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="9b667-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="9b667-134">新增資料磁碟 tooa VM</span><span class="sxs-lookup"><span data-stu-id="9b667-134">Add a data disk tooa VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="9b667-135">從 VM 移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="9b667-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="9b667-136">調整磁碟大小</span><span class="sxs-lookup"><span data-stu-id="9b667-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="9b667-137">製作磁碟的快照集</span><span class="sxs-lookup"><span data-stu-id="9b667-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="9b667-138">建立 VM 的映像</span><span class="sxs-lookup"><span data-stu-id="9b667-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="9b667-139">從映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="9b667-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="9b667-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b667-140">Next steps</span></span>
<span data-ttu-id="9b667-141">如需其他 hello CLI 命令的範例，請參閱 hello[建立和管理 Linux Vm 以 hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="9b667-141">For additional examples of hello CLI commands, see hello [Create and Manage Linux VMs with hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

