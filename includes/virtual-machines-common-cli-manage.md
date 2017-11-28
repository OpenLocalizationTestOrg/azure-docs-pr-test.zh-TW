<span data-ttu-id="d58c2-101">Azure CLI 2.0 可讓您建立及管理 macOS、Linux 和 Windows 上的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="d58c2-101">The Azure CLI 2.0 allows you to create and manage your Azure resources on macOS, Linux, and Windows.</span></span> <span data-ttu-id="d58c2-102">本文會詳細說明一些最常用來建立和管理虛擬機器 (VM) 的命令。</span><span class="sxs-lookup"><span data-stu-id="d58c2-102">This article details some of the most common commands to create and manage virtual machines (VMs).</span></span>

<span data-ttu-id="d58c2-103">本文需要 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d58c2-103">This article requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d58c2-104">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="d58c2-104">Run `az --version` to find the version.</span></span> <span data-ttu-id="d58c2-105">如果您需要升級，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d58c2-105">If you need to upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="d58c2-106">您也可以從瀏覽器使用 [Cloud Shell](/azure/cloud-shell/quickstart)。</span><span class="sxs-lookup"><span data-stu-id="d58c2-106">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="d58c2-107">Azure CLI 中的基本 Azure Resource Manager 命令</span><span class="sxs-lookup"><span data-stu-id="d58c2-107">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="d58c2-108">如需特定命令列參數和選項的詳細說明，您可以輸入 `az <command> <subcommand> --help` 來使用線上命令說明和選項。</span><span class="sxs-lookup"><span data-stu-id="d58c2-108">For more detailed help with specific command line switches and options, you can use the online command help and options by typing `az <command> <subcommand> --help`.</span></span>

### <a name="create-vms"></a><span data-ttu-id="d58c2-109">建立 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-109">Create VMs</span></span>
| <span data-ttu-id="d58c2-110">工作</span><span class="sxs-lookup"><span data-stu-id="d58c2-110">Task</span></span> | <span data-ttu-id="d58c2-111">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="d58c2-111">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="d58c2-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="d58c2-112">Create a resource group</span></span> | `az group create --name myResourceGroup --location eastus` |
| <span data-ttu-id="d58c2-113">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-113">Create a Linux VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| <span data-ttu-id="d58c2-114">建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-114">Create a Windows VM</span></span> | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a><span data-ttu-id="d58c2-115">管理 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="d58c2-115">Manage VM state</span></span>
| <span data-ttu-id="d58c2-116">工作</span><span class="sxs-lookup"><span data-stu-id="d58c2-116">Task</span></span> | <span data-ttu-id="d58c2-117">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="d58c2-117">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="d58c2-118">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-118">Start a VM</span></span> | `az vm start --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-119">停止 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-119">Stop a VM</span></span> | `az vm stop --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-120">解除配置 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-120">Deallocate a VM</span></span> | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-121">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-121">Restart a VM</span></span> | `az vm restart --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-122">重新部署 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-122">Redeploy a VM</span></span> | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-123">刪除 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-123">Delete a VM</span></span> | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a><span data-ttu-id="d58c2-124">取得 VM 資訊</span><span class="sxs-lookup"><span data-stu-id="d58c2-124">Get VM info</span></span>
| <span data-ttu-id="d58c2-125">工作</span><span class="sxs-lookup"><span data-stu-id="d58c2-125">Task</span></span> | <span data-ttu-id="d58c2-126">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="d58c2-126">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="d58c2-127">列出 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-127">List VMs</span></span> | `az vm list` |
| <span data-ttu-id="d58c2-128">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="d58c2-128">Get information about a VM</span></span> | `az vm show --resource-group myResourceGroup --name myVM` |
| <span data-ttu-id="d58c2-129">取得 VM 資源的使用量</span><span class="sxs-lookup"><span data-stu-id="d58c2-129">Get usage of VM resources</span></span> | `az vm list-usage --location eastus` |
| <span data-ttu-id="d58c2-130">取得所有可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="d58c2-130">Get all available VM sizes</span></span> | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a><span data-ttu-id="d58c2-131">磁碟和映像</span><span class="sxs-lookup"><span data-stu-id="d58c2-131">Disks and images</span></span>
| <span data-ttu-id="d58c2-132">工作</span><span class="sxs-lookup"><span data-stu-id="d58c2-132">Task</span></span> | <span data-ttu-id="d58c2-133">Azure CLI 命令</span><span class="sxs-lookup"><span data-stu-id="d58c2-133">Azure CLI commands</span></span> |
| --- | --- |
| <span data-ttu-id="d58c2-134">將資料磁碟新增至 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-134">Add a data disk to a VM</span></span> | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| <span data-ttu-id="d58c2-135">從 VM 移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="d58c2-135">Remove a data disk from a VM</span></span> | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| <span data-ttu-id="d58c2-136">調整磁碟大小</span><span class="sxs-lookup"><span data-stu-id="d58c2-136">Resize a disk</span></span> | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| <span data-ttu-id="d58c2-137">製作磁碟的快照集</span><span class="sxs-lookup"><span data-stu-id="d58c2-137">Snapshot a disk</span></span> | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| <span data-ttu-id="d58c2-138">建立 VM 的映像</span><span class="sxs-lookup"><span data-stu-id="d58c2-138">Create image of a VM</span></span> | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| <span data-ttu-id="d58c2-139">從映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="d58c2-139">Create VM from image</span></span> | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a><span data-ttu-id="d58c2-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d58c2-140">Next steps</span></span>
<span data-ttu-id="d58c2-141">如需 CLI 命令的其他範例，請參閱[使用 Azure CLI 建立和管理 Linux VM](../articles/virtual-machines/linux/tutorial-manage-vm.md) 教學課程。</span><span class="sxs-lookup"><span data-stu-id="d58c2-141">For additional examples of the CLI commands, see the [Create and Manage Linux VMs with the Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) tutorial.</span></span>

