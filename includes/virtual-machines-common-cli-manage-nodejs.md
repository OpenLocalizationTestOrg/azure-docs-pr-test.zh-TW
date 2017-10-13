<span data-ttu-id="63c22-101">您可以使用之前 hello Azure CLI 與資源管理員命令和範本 toodeploy Azure 資源和工作負載使用資源群組，您必須使用 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63c22-101">Before you can use hello Azure CLI with Resource Manager commands and templates toodeploy Azure resources and workloads using resource groups, you will need an account with Azure.</span></span> <span data-ttu-id="63c22-102">如果您沒有帳戶，可以取得 [此處免費試用的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="63c22-102">If you do not have an account, you can get a [free Azure trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="63c22-103">如果您尚未安裝 hello Azure CLI 連線的 tooyour 訂用帳戶，請參閱[安裝 hello Azure CLI](../articles/cli-install-nodejs.md)太設定 hello 模式`arm`與`azure config mode arm`，並以 hello 連接 tooAzure`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="63c22-103">If you haven't already installed hello Azure CLI and connected tooyour subscription, see [Install hello Azure CLI](../articles/cli-install-nodejs.md) set hello mode too`arm` with `azure config mode arm`, and connect tooAzure with hello `azure login` command.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="63c22-104">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="63c22-104">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="63c22-105">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="63c22-105">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="63c22-106">Azure CLI 10 – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="63c22-106">Azure CLI 10 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="63c22-107">[Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="63c22-107">[Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a><span data-ttu-id="63c22-108">Azure CLI 中的基本 Azure Resource Manager 命令</span><span class="sxs-lookup"><span data-stu-id="63c22-108">Basic Azure Resource Manager commands in Azure CLI</span></span>
<span data-ttu-id="63c22-109">本文涵蓋基本的命令，您會想要使用 Azure CLI toomanage toouse 並與其互動您 Azure 訂用帳戶中的資源 (主要 Vm)。</span><span class="sxs-lookup"><span data-stu-id="63c22-109">This article covers basic commands you will want toouse with Azure CLI toomanage and interact with your resources (primarily VMs) in your Azure subscription.</span></span>  <span data-ttu-id="63c22-110">如需詳細說明使用特定的命令列參數和選項，您可以使用 hello 線上命令說明和選項輸入`azure <command> <subcommand> --help`或`azure help <command> <subcommand>`。</span><span class="sxs-lookup"><span data-stu-id="63c22-110">For more detailed help with specific command line switches and options, you can use hello online command help and options by typing `azure <command> <subcommand> --help` or `azure help <command> <subcommand>`.</span></span>

> [!NOTE]
> <span data-ttu-id="63c22-111">這些範例不包含以範本為基礎的作業，這些作業一般建議在資源管理員中針對 VM 部署使用。</span><span class="sxs-lookup"><span data-stu-id="63c22-111">These examples don't include template-based operations which are generally recommended for VM deployments in Resource Manager.</span></span> <span data-ttu-id="63c22-112">資訊，請參閱[使用 hello Azure CLI 與 Azure 資源管理員](../articles/xplat-cli-azure-resource-manager.md)和[部署和管理虛擬機器使用的 Azure Resource Manager 範本和 hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="63c22-112">For information, see [Use hello Azure CLI with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) and [Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

| <span data-ttu-id="63c22-113">Task</span><span class="sxs-lookup"><span data-stu-id="63c22-113">Task</span></span> | <span data-ttu-id="63c22-114">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63c22-114">Resource Manager</span></span> |
| --- | --- | --- |
| <span data-ttu-id="63c22-115">建立 hello 最基本的 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-115">Create hello most basic VM</span></span> |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/><span data-ttu-id="63c22-116">(取得 hello`image-urn`從 hello`azure vm image list`命令。</span><span class="sxs-lookup"><span data-stu-id="63c22-116">(Obtain hello `image-urn` from hello `azure vm image list` command.</span></span> <span data-ttu-id="63c22-117">如需範例，請參閱[這篇文章](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。)</span><span class="sxs-lookup"><span data-stu-id="63c22-117">See [this article](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for examples.)</span></span> |
| <span data-ttu-id="63c22-118">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="63c22-118">Create a Linux VM</span></span> |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| <span data-ttu-id="63c22-119">建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="63c22-119">Create a Windows VM</span></span> |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| <span data-ttu-id="63c22-120">列出 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-120">List VMs</span></span> |`azure  vm list [options]` |
| <span data-ttu-id="63c22-121">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="63c22-121">Get information about a VM</span></span> |`azure  vm show [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-122">啟動 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-122">Start a VM</span></span> |`azure vm start [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-123">停止 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-123">Stop a VM</span></span> |`azure vm stop [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-124">解除配置 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-124">Deallocate a VM</span></span> |`azure vm deallocate [options] <resource-group> <name>` |
| <span data-ttu-id="63c22-125">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-125">Restart a VM</span></span> |`azure vm restart [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-126">刪除 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-126">Delete a VM</span></span> |`azure vm delete [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-127">擷取 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-127">Capture a VM</span></span> |`azure vm capture [options] <resource_group> <name>` |
| <span data-ttu-id="63c22-128">從使用者映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-128">Create a VM from a user image</span></span> |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| <span data-ttu-id="63c22-129">從特殊化磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="63c22-129">Create a VM from a specialized disk</span></span> |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| <span data-ttu-id="63c22-130">新增資料磁碟 tooa VM</span><span class="sxs-lookup"><span data-stu-id="63c22-130">Add a data disk tooa VM</span></span> |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| <span data-ttu-id="63c22-131">從 VM 移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="63c22-131">Remove a data disk from a VM</span></span> |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| <span data-ttu-id="63c22-132">加入泛型擴充 tooa VM</span><span class="sxs-lookup"><span data-stu-id="63c22-132">Add a generic extension tooa VM</span></span> |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| <span data-ttu-id="63c22-133">新增 VM 存取延伸 tooa VM</span><span class="sxs-lookup"><span data-stu-id="63c22-133">Add VM Access extension tooa VM</span></span> |`azure vm reset-access [options] <resource-group> <name>` |
| <span data-ttu-id="63c22-134">將 Docker 擴充功能 tooa VM</span><span class="sxs-lookup"><span data-stu-id="63c22-134">Add Docker extension tooa VM</span></span> |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| <span data-ttu-id="63c22-135">移除 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="63c22-135">Remove a VM extension</span></span> |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| <span data-ttu-id="63c22-136">取得 VM 資源的使用量</span><span class="sxs-lookup"><span data-stu-id="63c22-136">Get usage of VM resources</span></span> |`azure vm list-usage [options] <location>` |
| <span data-ttu-id="63c22-137">取得所有可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="63c22-137">Get all available VM sizes</span></span> |`azure vm sizes [options]` |

## <a name="next-steps"></a><span data-ttu-id="63c22-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63c22-138">Next steps</span></span>
* <span data-ttu-id="63c22-139">除了基本 VM 管理之外的 hello CLI 命令的其他範例，請參閱[使用 hello Azure CLI 與 Azure 資源管理員](../articles/virtual-machines/azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="63c22-139">For additional examples of hello CLI commands going beyond basic VM management, see [Using hello Azure CLI with Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).</span></span>