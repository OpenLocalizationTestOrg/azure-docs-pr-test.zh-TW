
* [<span data-ttu-id="b346e-101">在 Azure 中快速建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="b346e-102">在 Azure 中利用範本部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="b346e-103">從自訂映像建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="b346e-104">部署使用虛擬網路和負載平衡器的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="b346e-105">移除資源群組</span><span class="sxs-lookup"><span data-stu-id="b346e-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="b346e-106">顯示資源群組部署記錄檔</span><span class="sxs-lookup"><span data-stu-id="b346e-106">Show the log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="b346e-107">顯示虛擬機器的相關資訊</span><span class="sxs-lookup"><span data-stu-id="b346e-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="b346e-108">連線至 Linux 型虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-108">Connect to a Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="b346e-109">停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="b346e-110">啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="b346e-111">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b346e-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="b346e-112">準備就緒</span><span class="sxs-lookup"><span data-stu-id="b346e-112">Getting ready</span></span>
<span data-ttu-id="b346e-113">在您能夠搭配 Azure 資源群組使用 Azure CLI 之前，必須備妥正確的 Azure CLI 版本以及 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b346e-113">Before you can use the Azure CLI with Azure resource groups, you need to have the right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="b346e-114">如果沒有 Azure CLI，請 [安裝它](../articles/cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="b346e-114">If you don't have the Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-to-090-or-later"></a><span data-ttu-id="b346e-115">將 Azure CLI 版本更新為 0.9.0 或更新版本</span><span class="sxs-lookup"><span data-stu-id="b346e-115">Update your Azure CLI version to 0.9.0 or later</span></span>
<span data-ttu-id="b346e-116">輸入 `azure --version` ，即可查看您是否已經安裝 0.9.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b346e-116">Type `azure --version` to see whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="b346e-117">如果您的版本不是 0.9.0 或更新版本，則必須使用其中一個原生安裝程式或是藉由輸入 `npm update -g azure-cli` 透過 **npm** 來進行版本更新。</span><span class="sxs-lookup"><span data-stu-id="b346e-117">If your version is not 0.9.0 or later, you need to update it by using one of the native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="b346e-118">您也可以藉由使用下列 [Docker 映像](https://registry.hub.docker.com/u/microsoft/azure-cli/)，執行 Azure CLI 做為 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="b346e-118">You can also run Azure CLI as a Docker container by using the following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="b346e-119">從 Docker 主機中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b346e-119">From a Docker host, run the following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="b346e-120">設定 Azure 帳戶和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b346e-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="b346e-121">如果您還沒有 Azure 訂閱帳戶，但是有 MSDN 訂閱帳戶，請啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="b346e-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="b346e-122">或者申請 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b346e-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="b346e-123">現在，輸入 `azure login` 並遵循提示來進行 Azure 帳戶的互動式登入體驗，[以互動方式登入您的 Azure 帳戶](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)。</span><span class="sxs-lookup"><span data-stu-id="b346e-123">Now [log in to your Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following the prompts for an interactive login experience to your Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="b346e-124">如果您有公司或學校識別碼，而且知道尚未啟用雙因素驗證，則您「也」可以使用 `azure login -u` 再加上公司或學校識別碼，在「沒有」互動式工作階段的情況下進行登入。</span><span class="sxs-lookup"><span data-stu-id="b346e-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with the work or school ID to log in *without* an interactive session.</span></span> <span data-ttu-id="b346e-125">如果沒有公司或學校識別碼，您可以[從個人 Microsoft 帳戶建立公司或學校識別碼](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，使用相同方式來登入。</span><span class="sxs-lookup"><span data-stu-id="b346e-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to log in the same way.</span></span>
>
>

<span data-ttu-id="b346e-126">您的帳戶可能會有一個以上的訂閱帳戶。</span><span class="sxs-lookup"><span data-stu-id="b346e-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="b346e-127">您可以輸入 `azure account list`，即可列出訂閱帳戶，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="b346e-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="b346e-128">若要設定目前的 Azure 訂用帳戶，請輸入下列內容。</span><span class="sxs-lookup"><span data-stu-id="b346e-128">You can set the current Azure subscription by typing the following.</span></span> <span data-ttu-id="b346e-129">使用訂用帳戶名稱或識別碼 (有您想管理的資源)。</span><span class="sxs-lookup"><span data-stu-id="b346e-129">Use the subscription name or the ID that has the resources you want to manage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-to-the-azure-cli-resource-group-mode"></a><span data-ttu-id="b346e-130">切換至 Azure CLI 資源群組模式</span><span class="sxs-lookup"><span data-stu-id="b346e-130">Switch to the Azure CLI resource group mode</span></span>
<span data-ttu-id="b346e-131">根據預設，Azure CLI 會在服務管理模式 (**asm** 模式) 下啟動。</span><span class="sxs-lookup"><span data-stu-id="b346e-131">By default, the Azure CLI starts in the service management mode (**asm** mode).</span></span> <span data-ttu-id="b346e-132">輸入下列內容以切換至資源群組模式。</span><span class="sxs-lookup"><span data-stu-id="b346e-132">Type the following to switch to resource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="b346e-133">了解 Azure 資源範本和資源群組</span><span class="sxs-lookup"><span data-stu-id="b346e-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="b346e-134">大部分的應用程式在建立時會使用不同資源類型的組合 (例如一或多個 VM 和儲存體帳戶、SQL 資料庫、虛擬網路或內容傳遞網路)。</span><span class="sxs-lookup"><span data-stu-id="b346e-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="b346e-135">預設 Azure 服務管理 API 和 Azure 傳統入口網站可使用 service-by-service 方法代表這些項目。</span><span class="sxs-lookup"><span data-stu-id="b346e-135">The default Azure service management API and the Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="b346e-136">這個方法會要求您部署和個別管理個別服務 (或尋找執行這項作業的其他工具)，而不是做為部署的單一邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="b346e-136">This approach requires you to deploy and manage the individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="b346e-137">不過，您可以利用「Azure 資源管理員範本」，將這些不同的資源宣告為一個邏輯部署單元，然後就能進行部署和管理。</span><span class="sxs-lookup"><span data-stu-id="b346e-137">*Azure Resource Manager templates*, however, make it possible for you to deploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="b346e-138">請不要以命令方式告訴 Azure 逐一部署命令，您應該在 JSON 檔案描述整個部署過程 -- 所有資源和相關設定以及部署參數 -- 然後告訴 Azure 將這些資源視為一個群組加以部署。</span><span class="sxs-lookup"><span data-stu-id="b346e-138">Instead of imperatively telling Azure what to deploy one command after another, you describe your entire deployment in a JSON file -- all of the resources and associated configuration and deployment parameters -- and tell Azure to deploy those resources as one group.</span></span>

<span data-ttu-id="b346e-139">然後您可以使用 Azure CLI 資源管理命令執行以下動作，即可管理群組的資源整體生命週期：</span><span class="sxs-lookup"><span data-stu-id="b346e-139">You can then manage the overall life cycle of the group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="b346e-140">一次性停止、啟動或刪除群組內的所有資源。</span><span class="sxs-lookup"><span data-stu-id="b346e-140">Stop, start, or delete all of the resources within the group at once.</span></span>
* <span data-ttu-id="b346e-141">將角色型存取控制 (RBAC) 規則套用至鎖定它們的安全權限。</span><span class="sxs-lookup"><span data-stu-id="b346e-141">Apply Role-Based Access Control (RBAC) rules to lock down security permissions on them.</span></span>
* <span data-ttu-id="b346e-142">稽核作業。</span><span class="sxs-lookup"><span data-stu-id="b346e-142">Audit operations.</span></span>
* <span data-ttu-id="b346e-143">利用其他中繼資料標記資源，方便追蹤。</span><span class="sxs-lookup"><span data-stu-id="b346e-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="b346e-144">如需深入了解 Azure 資源群組及其功能，請參閱[Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b346e-144">You can learn lots more about Azure resource groups and what they can do for you in the [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b346e-145">如果您有興趣了解如何編寫範本，請參閱 [編寫 Azure 資源管理員範本](../articles/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="b346e-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="b346e-146"><a id="quick-create-a-vm-in-azure"></a>工作：在 Azure 中快速建立 VM</span><span class="sxs-lookup"><span data-stu-id="b346e-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="b346e-147">有時候您知道需要何種映像，而且您現在需要該映像的 VM，並且不太在意基礎結構 -- 或許您必須在全新的 VM 上進行某些測試。</span><span class="sxs-lookup"><span data-stu-id="b346e-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about the infrastructure -- maybe you have to test something on a clean VM.</span></span> <span data-ttu-id="b346e-148">當您想要使用 `azure vm quick-create` 命令，然後傳遞必要引數來建立 VM 和基礎結構的時候。</span><span class="sxs-lookup"><span data-stu-id="b346e-148">That's when you want to use the `azure vm quick-create` command, and pass the arguments necessary to create a VM and its infrastructure.</span></span>

<span data-ttu-id="b346e-149">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="b346e-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="b346e-150">第二，您將需要映像。</span><span class="sxs-lookup"><span data-stu-id="b346e-150">Second, you'll need an image.</span></span> <span data-ttu-id="b346e-151">若要利用 Azure CLI 尋找映像，請參閱[利用 PowerShell 和 Azure CLI 瀏覽和選取 Azure 虛擬機器映像](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b346e-151">To find an image with the Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and the Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b346e-152">不過在本文中，以下是常用映像的簡要清單。</span><span class="sxs-lookup"><span data-stu-id="b346e-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="b346e-153">我們會使用 CoreOS 的 Stable 映像，縮短整個建立流程。</span><span class="sxs-lookup"><span data-stu-id="b346e-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="b346e-154">對於 ComputeImageVersion，您也可以只提供 'latest' 做為範本語言和 Azure CLI 中的參數。</span><span class="sxs-lookup"><span data-stu-id="b346e-154">For ComputeImageVersion, you can also simply supply 'latest' as the parameter in both the template language and in the Azure CLI.</span></span> <span data-ttu-id="b346e-155">這可讓您永遠使用最新且經過修補的映像版本，而不必修改您的指令碼或範本。</span><span class="sxs-lookup"><span data-stu-id="b346e-155">This will allow you to always use the latest and patched version of the image without having to modify your scripts or templates.</span></span> <span data-ttu-id="b346e-156">如下所示。</span><span class="sxs-lookup"><span data-stu-id="b346e-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="b346e-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="b346e-157">PublisherName</span></span> | <span data-ttu-id="b346e-158">提供項目</span><span class="sxs-lookup"><span data-stu-id="b346e-158">Offer</span></span> | <span data-ttu-id="b346e-159">SKU</span><span class="sxs-lookup"><span data-stu-id="b346e-159">Sku</span></span> | <span data-ttu-id="b346e-160">版本</span><span class="sxs-lookup"><span data-stu-id="b346e-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b346e-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b346e-161">OpenLogic</span></span> |<span data-ttu-id="b346e-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="b346e-162">CentOS</span></span> |<span data-ttu-id="b346e-163">7</span><span class="sxs-lookup"><span data-stu-id="b346e-163">7</span></span> |<span data-ttu-id="b346e-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="b346e-164">7.0.201503</span></span> |
| <span data-ttu-id="b346e-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b346e-165">OpenLogic</span></span> |<span data-ttu-id="b346e-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="b346e-166">CentOS</span></span> |<span data-ttu-id="b346e-167">7.1</span><span class="sxs-lookup"><span data-stu-id="b346e-167">7.1</span></span> |<span data-ttu-id="b346e-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="b346e-168">7.1.201504</span></span> |
| <span data-ttu-id="b346e-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b346e-169">CoreOS</span></span> |<span data-ttu-id="b346e-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b346e-170">CoreOS</span></span> |<span data-ttu-id="b346e-171">Beta</span><span class="sxs-lookup"><span data-stu-id="b346e-171">Beta</span></span> |<span data-ttu-id="b346e-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="b346e-172">647.0.0</span></span> |
| <span data-ttu-id="b346e-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b346e-173">CoreOS</span></span> |<span data-ttu-id="b346e-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b346e-174">CoreOS</span></span> |<span data-ttu-id="b346e-175">Stable</span><span class="sxs-lookup"><span data-stu-id="b346e-175">Stable</span></span> |<span data-ttu-id="b346e-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="b346e-176">633.1.0</span></span> |
| <span data-ttu-id="b346e-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="b346e-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="b346e-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="b346e-178">DynamicsNAV</span></span> |<span data-ttu-id="b346e-179">2015</span><span class="sxs-lookup"><span data-stu-id="b346e-179">2015</span></span> |<span data-ttu-id="b346e-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="b346e-180">8.0.40459</span></span> |
| <span data-ttu-id="b346e-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="b346e-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="b346e-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="b346e-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="b346e-183">2013</span><span class="sxs-lookup"><span data-stu-id="b346e-183">2013</span></span> |<span data-ttu-id="b346e-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b346e-184">1.0.0</span></span> |
| <span data-ttu-id="b346e-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="b346e-185">msopentech</span></span> |<span data-ttu-id="b346e-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="b346e-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="b346e-187">標準</span><span class="sxs-lookup"><span data-stu-id="b346e-187">Standard</span></span> |<span data-ttu-id="b346e-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b346e-188">1.0.0</span></span> |
| <span data-ttu-id="b346e-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="b346e-189">msopentech</span></span> |<span data-ttu-id="b346e-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="b346e-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="b346e-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="b346e-191">Enterprise</span></span> |<span data-ttu-id="b346e-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="b346e-192">1.0.0</span></span> |
| <span data-ttu-id="b346e-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="b346e-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="b346e-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="b346e-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="b346e-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="b346e-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="b346e-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="b346e-196">12.0.2430</span></span> |
| <span data-ttu-id="b346e-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="b346e-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="b346e-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="b346e-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="b346e-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="b346e-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="b346e-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="b346e-200">12.0.2430</span></span> |
| <span data-ttu-id="b346e-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="b346e-201">Canonical</span></span> |<span data-ttu-id="b346e-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b346e-202">UbuntuServer</span></span> |<span data-ttu-id="b346e-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="b346e-203">12.04.5-LTS</span></span> |<span data-ttu-id="b346e-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="b346e-204">12.04.201504230</span></span> |
| <span data-ttu-id="b346e-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="b346e-205">Canonical</span></span> |<span data-ttu-id="b346e-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b346e-206">UbuntuServer</span></span> |<span data-ttu-id="b346e-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="b346e-207">14.04.2-LTS</span></span> |<span data-ttu-id="b346e-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="b346e-208">14.04.201503090</span></span> |
| <span data-ttu-id="b346e-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b346e-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-210">WindowsServer</span></span> |<span data-ttu-id="b346e-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="b346e-211">2012-Datacenter</span></span> |<span data-ttu-id="b346e-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="b346e-212">3.0.201503</span></span> |
| <span data-ttu-id="b346e-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b346e-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-214">WindowsServer</span></span> |<span data-ttu-id="b346e-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="b346e-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="b346e-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="b346e-216">4.0.201503</span></span> |
| <span data-ttu-id="b346e-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="b346e-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="b346e-218">WindowsServer</span></span> |<span data-ttu-id="b346e-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="b346e-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="b346e-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="b346e-220">5.0.201504</span></span> |
| <span data-ttu-id="b346e-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b346e-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="b346e-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b346e-222">WindowsServerEssentials</span></span> |<span data-ttu-id="b346e-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="b346e-223">WindowsServerEssentials</span></span> |<span data-ttu-id="b346e-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="b346e-224">1.0.141204</span></span> |
| <span data-ttu-id="b346e-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="b346e-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="b346e-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="b346e-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="b346e-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="b346e-227">2012R2</span></span> |<span data-ttu-id="b346e-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="b346e-228">4.3.4665</span></span> |

<span data-ttu-id="b346e-229">只要輸入 `azure vm quick-create` 命令，然後根據系統提示執行，就可以建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b346e-229">Just create your VM by entering the `azure vm quick-create` command and being ready for the prompts.</span></span> <span data-ttu-id="b346e-230">您應該會看到類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="b346e-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up the VM "coreos"
info:    Using the VM Size "Standard_A1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in the region "westus", trying to create new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up the storage account cli9fd3fce49e9a9b3d14302
+ Looking up the NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up the virtual network "coreo-westu-1430261891570-vnet"
+ Looking up the subnet "coreo-westu-1430261891570-snet" under the virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up the VM "coreos"
+ Looking up the NIC "coreo-westu-1430261891570-nic"
+ Looking up the public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="b346e-231">無論身在何處，新的 VM 就在您身邊。</span><span class="sxs-lookup"><span data-stu-id="b346e-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="b346e-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>工作：在 Azure 中利用範本部署 VM</span><span class="sxs-lookup"><span data-stu-id="b346e-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="b346e-233">請按照以下各節描述的操作方法，使用 Azure CLI 搭配範本來部署新的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="b346e-233">Use the instructions in these sections to deploy a new Azure VM by using a template with the Azure CLI.</span></span> <span data-ttu-id="b346e-234">這個範本會在只有單一子網路的新虛擬網路中建立單一虛擬機器，而不同於 `azure vm quick-create`，它可以讓您精確描述想要的內容，而且重複使用時也不會發生任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="b346e-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you to describe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="b346e-235">以下是這個範本建立的內容：</span><span class="sxs-lookup"><span data-stu-id="b346e-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-the-json-file-for-the-template-parameters"></a><span data-ttu-id="b346e-236">步驟 1：檢查 JSON 檔案的範本參數。</span><span class="sxs-lookup"><span data-stu-id="b346e-236">Step 1: Examine the JSON file for the template parameters</span></span>
<span data-ttu-id="b346e-237">以下是範本的 JSON 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="b346e-237">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="b346e-238">(這個範本也位於 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json)中)。</span><span class="sxs-lookup"><span data-stu-id="b346e-238">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="b346e-239">範本可彈性運用，所以這位設計人員可能已經決定提供很多的參數給您，或者決定建立一個更固定的範本，而只提供幾個參數給您。</span><span class="sxs-lookup"><span data-stu-id="b346e-239">Templates are flexible, so the designer may have chosen to give you lots of parameters or chosen to offer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="b346e-240">為了收集資訊，請您將這個範本以參數的形式傳遞，然後開啟範本檔案 (這個主題內嵌一個範本)，接下來檢查 [參數]  值。</span><span class="sxs-lookup"><span data-stu-id="b346e-240">In order to collect the information you need to pass the template as parameters, open the template file (this topic has a template inline, below) and examine the **parameters** values.</span></span>

<span data-ttu-id="b346e-241">在這個案例中，系統會要求您提供下列範本：</span><span class="sxs-lookup"><span data-stu-id="b346e-241">In this case, the template below will ask for:</span></span>

* <span data-ttu-id="b346e-242">唯一的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="b346e-242">A unique storage account name.</span></span>
* <span data-ttu-id="b346e-243">VM 的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b346e-243">An admin user name for the VM.</span></span>
* <span data-ttu-id="b346e-244">密碼。</span><span class="sxs-lookup"><span data-stu-id="b346e-244">A password.</span></span>
* <span data-ttu-id="b346e-245">讓外界使用的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="b346e-245">A domain name for the outside world to use.</span></span>
* <span data-ttu-id="b346e-246">Ubuntu Server 版本號碼 -- 但只能接受一個清單。</span><span class="sxs-lookup"><span data-stu-id="b346e-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="b346e-247">進一步了解 [使用者名稱和密碼需求](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="b346e-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="b346e-248">決定這些值之後，就可以開始建立群組，然後將這個範本部署到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b346e-248">Once you decide on these values, you're ready to create a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the storage account where the virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for the virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for the virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for the public IP used to access the virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="b346e-249">步驟 2：使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-249">Step 2: Create the virtual machine by using the template</span></span>
<span data-ttu-id="b346e-250">準備好參數值之後，您必須建立一個部署範本時會用到的資源群組，然後再部署範本。</span><span class="sxs-lookup"><span data-stu-id="b346e-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy the template.</span></span>

<span data-ttu-id="b346e-251">若要建立資源群組，請輸入 `azure group create <group name> <location>` 和您所需群組的名稱，以及要部署到哪一個資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="b346e-251">To create the resource group, type `azure group create <group name> <location>` with the name of the group you want and the datacenter location into which you want to deploy.</span></span> <span data-ttu-id="b346e-252">進行速度十分快：</span><span class="sxs-lookup"><span data-stu-id="b346e-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="b346e-253">現在要建立部署，請呼叫 `azure group deployment create` 並傳遞：</span><span class="sxs-lookup"><span data-stu-id="b346e-253">Now to create the deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="b346e-254">範本檔案 (如果您會將上述 JSON 範本儲存到本機檔案)。</span><span class="sxs-lookup"><span data-stu-id="b346e-254">The template file (if you saved the above JSON template to a local file).</span></span>
* <span data-ttu-id="b346e-255">範本 URI (如果您想指向 GitHub 中的檔案或其他網址)。</span><span class="sxs-lookup"><span data-stu-id="b346e-255">A template URI (if you want to point at the file in GitHub or some other web address).</span></span>
* <span data-ttu-id="b346e-256">部署的目標資源群組。</span><span class="sxs-lookup"><span data-stu-id="b346e-256">The resource group into which you want to deploy.</span></span>
* <span data-ttu-id="b346e-257">選用部署名稱。</span><span class="sxs-lookup"><span data-stu-id="b346e-257">An optional deployment name.</span></span>

<span data-ttu-id="b346e-258">系統會提示您輸入 JSON 檔案的 "parameters" 區段中的參數值。</span><span class="sxs-lookup"><span data-stu-id="b346e-258">You will be prompted to supply the values of parameters in the "parameters" section of the JSON file.</span></span> <span data-ttu-id="b346e-259">指定好所有的參數值後，就會開始部署。</span><span class="sxs-lookup"><span data-stu-id="b346e-259">When you have specified all the parameter values, your deployment will begin.</span></span>

<span data-ttu-id="b346e-260">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="b346e-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="b346e-261">您會收到下列類型的資訊：</span><span class="sxs-lookup"><span data-stu-id="b346e-261">You will receive the following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="b346e-262"><a id="create-a-custom-vm-image"></a>工作：建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="b346e-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="b346e-263">您已基本了解上述範本的用法，那麼現在我們可以使用類似的操作方法，透過 Azure CLI 使用範本從 Azure 中的特定 .vhd 檔案建立自訂 VM。</span><span class="sxs-lookup"><span data-stu-id="b346e-263">You've seen the basic usage of templates above, so now we can use similar instructions to create a custom VM from a specific .vhd file in Azure by using a template via the Azure CLI.</span></span> <span data-ttu-id="b346e-264">其中的差別就是這個範本會從指定的虛擬硬碟 (VHD) 建立單一虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b346e-264">The difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="b346e-265">步驟 1：檢查範本的 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="b346e-265">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="b346e-266">以下是本章節舉例說明時，範本的 JSON 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="b346e-266">Here are the contents of the JSON file for the template that this section uses as an example.</span></span> <span data-ttu-id="b346e-267">(這個範本也位於 [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json)中)。</span><span class="sxs-lookup"><span data-stu-id="b346e-267">(The template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="b346e-268">再說一次，參數如果沒有預設值，就必須找出您想輸入的值。</span><span class="sxs-lookup"><span data-stu-id="b346e-268">Again, you will need to find the values you want to enter for the parameters that do not have default values.</span></span> <span data-ttu-id="b346e-269">當您執行 `azure group deployment create` 命令時，Azure CLI 會提示您輸入這些值。</span><span class="sxs-lookup"><span data-stu-id="b346e-269">When you run the `azure group deployment create` command, the Azure CLI will prompt you to enter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-the-vhd"></a><span data-ttu-id="b346e-270">步驟 2：取得 VHD</span><span class="sxs-lookup"><span data-stu-id="b346e-270">Step 2: Obtain the VHD</span></span>
<span data-ttu-id="b346e-271">很明顯，您需要 .vhd。</span><span class="sxs-lookup"><span data-stu-id="b346e-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="b346e-272">您可以使用 Azure 現有的 .vhd 或者可以上傳一個 .vhd。</span><span class="sxs-lookup"><span data-stu-id="b346e-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="b346e-273">若是 Windows 型虛擬機器，請參閱[建立 Windows Server VHD 並上傳至 Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b346e-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD to Azure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b346e-274">如需了解 Linux 架構的虛擬機器，請參閱[建立及上傳包含 Linux 作業系統的虛擬硬碟](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b346e-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains the Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-the-virtual-machine-by-using-the-template"></a><span data-ttu-id="b346e-275">步驟 3：使用範本建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-275">Step 3: Create the virtual machine by using the template</span></span>
<span data-ttu-id="b346e-276">現在您已準備利用 .vhd 建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b346e-276">Now you're ready to create a new virtual machine based on the .vhd.</span></span> <span data-ttu-id="b346e-277">使用 `azure group create <location>` 建立一個要在其中部署的群組：</span><span class="sxs-lookup"><span data-stu-id="b346e-277">Create a group to deploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="b346e-278">然後使用 `--template-uri` 選項直接呼叫範本 (或者利用 `--template-file` 選項來使用您本機儲存的檔案)，開始建立部署。</span><span class="sxs-lookup"><span data-stu-id="b346e-278">Then create the deployment by using the `--template-uri` option to call in the template directly (or you can use the `--template-file` option to use a file that you have saved locally).</span></span> <span data-ttu-id="b346e-279">請注意，因為範本已指定預設值，所以只會提示您只輸入幾項資料。</span><span class="sxs-lookup"><span data-stu-id="b346e-279">Note that because the template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="b346e-280">如果將範本部署到幾個不同的地方，可能會發現某些名稱與預設值衝突 (特別是您建立的 DNS 名稱)。</span><span class="sxs-lookup"><span data-stu-id="b346e-280">If you deploy the template in different places, you may find that some naming collisions occur with the default values (particularly the DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="b346e-281">您會看到類似下列輸出：</span><span class="sxs-lookup"><span data-stu-id="b346e-281">Output looks something like the following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment to complete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="b346e-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>工作：部署含多部 VM 的應用程式，它會使用虛擬網路和外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b346e-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="b346e-283">您可以利用這個範本，在一個負載平衡器上建立兩個虛擬機器，然後在連接埠 80 設定負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="b346e-283">This template allows you to create two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="b346e-284">這個範本也會部署儲存體帳戶、虛擬網路、公用 IP 位址、可用性集合以及網路介面。</span><span class="sxs-lookup"><span data-stu-id="b346e-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="b346e-285">按照下列步驟部署一個多重 VM 應用程式，它會透過 Azure PowerShell 命令使用 GitHub 範本儲存機制中的 Resource Manager 範本，然後就可以使用虛擬網路和負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b346e-285">Follow these steps to deploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in the GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-the-json-file-for-the-template"></a><span data-ttu-id="b346e-286">步驟 1：檢查範本的 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="b346e-286">Step 1: Examine the JSON file for the template</span></span>
<span data-ttu-id="b346e-287">以下是範本的 JSON 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="b346e-287">Here are the contents of the JSON file for the template.</span></span> <span data-ttu-id="b346e-288">如果您想要最新的版本，可在[範本的 GitHub 存放庫](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json)取得。</span><span class="sxs-lookup"><span data-stu-id="b346e-288">If you want the most recent version, it's located [at the GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="b346e-289">這個主題使用 `--template-uri` 參數來呼叫範本，不過您也可以使用 `--template-file` 參數來傳遞本機版本。</span><span class="sxs-lookup"><span data-stu-id="b346e-289">This topic uses the `--template-uri` switch to call in the template, but you can also use the `--template-file` switch to pass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix to use for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of the VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-the-deployment-by-using-the-template"></a><span data-ttu-id="b346e-290">步驟 2：使用範本建立部署</span><span class="sxs-lookup"><span data-stu-id="b346e-290">Step 2: Create the deployment by using the template</span></span>
<span data-ttu-id="b346e-291">使用 `azure group create <location>`來建立範本的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b346e-291">Create a resource group for the template by using `azure group create <location>`.</span></span> <span data-ttu-id="b346e-292">然後，使用 `azure group deployment create` 並傳遞資源群組、傳遞部署名稱，並為範本中沒有預設值的參數回應提示，就可以在資源群組中建立部署。</span><span class="sxs-lookup"><span data-stu-id="b346e-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing the resource group, passing a deployment name, and answering the prompts for parameters in the template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="b346e-293">現在使用 `azure group deployment create` 命令和 `--template-uri` 選項來部署範本。</span><span class="sxs-lookup"><span data-stu-id="b346e-293">Now use the `azure group deployment create` command and the `--template-uri` option to deploy the template.</span></span> <span data-ttu-id="b346e-294">請在系統提示時備妥您的參數值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b346e-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for the following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment to complete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="b346e-295">請注意，這個範本會部署 Windows Server 映像。不過，任何 Linux 映像都可以輕易取代它。</span><span class="sxs-lookup"><span data-stu-id="b346e-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="b346e-296">想要建立一個具備多個 swarm 管理員的 Docker 叢集嗎？</span><span class="sxs-lookup"><span data-stu-id="b346e-296">Want to create a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="b346e-297">[您做得到](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/)。</span><span class="sxs-lookup"><span data-stu-id="b346e-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="b346e-298"><a id="remove-a-resource-group"></a>工作：移除資源群組</span><span class="sxs-lookup"><span data-stu-id="b346e-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="b346e-299">請記住，您可以重新部署至資源群組，但若其中有一個不再使用，則可使用 `azure group delete <group name>`加以刪除。</span><span class="sxs-lookup"><span data-stu-id="b346e-299">Remember that you can redeploy to a resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="b346e-300"><a id="show-the-log-for-a-resource-group-deployment"></a>工作：顯示資源群組部署記錄檔</span><span class="sxs-lookup"><span data-stu-id="b346e-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show the log for a resource group deployment</span></span>
<span data-ttu-id="b346e-301">建立或使用範本時，此種情況很常見。</span><span class="sxs-lookup"><span data-stu-id="b346e-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="b346e-302">您可以使用 `azure group log show <groupname>` 呼叫來顯示群組的部署記錄檔，它會顯示相當多的實用資訊，協助您了解發生某些狀況的原因，或是未發生某些狀況的原因</span><span class="sxs-lookup"><span data-stu-id="b346e-302">The call to display the deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="b346e-303">(如需疑難排解部署及其他問題的詳細資訊，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md))。</span><span class="sxs-lookup"><span data-stu-id="b346e-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="b346e-304">例如，為了查明某些異常狀況，您可以使用 **jq** 此類的工具，就可以更清楚掌握前因後果，例如您需要更正的異常狀況。</span><span class="sxs-lookup"><span data-stu-id="b346e-304">To target specific failures, for example, you might use tools like **jq** to query things a bit more precisely, such as which individual failures you need to correct.</span></span> <span data-ttu-id="b346e-305">下列範例會使用 **jq** 剖析 **lbgroup** 的部署記錄檔，找出各種異常狀況。</span><span class="sxs-lookup"><span data-stu-id="b346e-305">The following example uses **jq** to parse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="b346e-306">您可以快速發現問題出在哪裡，然後予以修正，最後再試一次。</span><span class="sxs-lookup"><span data-stu-id="b346e-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="b346e-307">在下列情況中，範本已經同時建立兩個 VM，這樣會造成 .vhd 被鎖定。</span><span class="sxs-lookup"><span data-stu-id="b346e-307">In the following case, the template had been creating two VMs at the same time, which created a lock on the .vhd.</span></span> <span data-ttu-id="b346e-308">(修改範本後，很快就部署成功)。</span><span class="sxs-lookup"><span data-stu-id="b346e-308">(After we modified the template, the deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"The resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed to acquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="b346e-309"><a id="display-information-about-a-virtual-machine"></a>工作：顯示虛擬機器的相關資訊</span><span class="sxs-lookup"><span data-stu-id="b346e-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="b346e-310">您可以使用 `azure vm show <groupname> <vmname>` 命令來了解資源群組中特定 VM 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b346e-310">You can see information about specific VMs in your resource group by using the `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="b346e-311">如果您的群組中有多個 VM，可能需要先使用 `azure vm list <groupname>`來列出群組中的 VM。</span><span class="sxs-lookup"><span data-stu-id="b346e-311">If you have more than one VM in your group, you might first need to list the VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="b346e-312">然後，查閱 myVM1：</span><span class="sxs-lookup"><span data-stu-id="b346e-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up the VM "myVM1"
+ Looking up the NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="b346e-313">如果您想要以程式設計方式儲存和操作主控台命令的輸出，可以使用 JSON 剖析工具，例如 **[jq](https://github.com/stedolan/jq)** 或 **[jsawk](https://github.com/micha/jsawk)** 或適用於該工作的語言程式庫。</span><span class="sxs-lookup"><span data-stu-id="b346e-313">If you want to programmatically store and manipulate the output of your console commands, you may want to use a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for the task.</span></span>
>
>

## <span data-ttu-id="b346e-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>工作：登入 Linux 架構的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b346e-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on to a Linux-based virtual machine</span></span>
<span data-ttu-id="b346e-315">通常 Linux 機器是透過 SSH 連接的。</span><span class="sxs-lookup"><span data-stu-id="b346e-315">Typically Linux machines are connected to through SSH.</span></span> <span data-ttu-id="b346e-316">如需詳細資訊，請參閱[如何在 Azure 上搭配使用 SSH 與 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b346e-316">For more information, see [How to use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="b346e-317"><a id="stop-a-virtual-machine"></a>工作：停止 VM</span><span class="sxs-lookup"><span data-stu-id="b346e-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="b346e-318">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="b346e-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="b346e-319">萬一它是 Vnet 的最後一個 VM，您可以使用這個參數來保留 Vnet 的虛擬 IP (VIP)。</span><span class="sxs-lookup"><span data-stu-id="b346e-319">Use this parameter to keep the virtual IP (VIP) of the vnet in case it's the last VM in that vnet.</span></span> <br><br> <span data-ttu-id="b346e-320">如果您使用 `StayProvisioned` 參數，仍需支付 VM 的費用。</span><span class="sxs-lookup"><span data-stu-id="b346e-320">If you use the `StayProvisioned` parameter, you'll still be billed for the VM.</span></span>
>
>

## <span data-ttu-id="b346e-321"><a id="start-a-virtual-machine"></a>工作：啟動 VM</span><span class="sxs-lookup"><span data-stu-id="b346e-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="b346e-322">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="b346e-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="b346e-323"><a id="attach-a-data-disk"></a>工作：連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b346e-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="b346e-324">您也需要決定是否要附加新的磁碟或附加已經包含資料的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b346e-324">You'll also need to decide whether to attach a new disk or one that contains data.</span></span> <span data-ttu-id="b346e-325">如果是新的磁碟，這個命令會建立 .vhd 檔案，然後將它附加在同一個命令中。</span><span class="sxs-lookup"><span data-stu-id="b346e-325">For a new disk, the command creates the .vhd file and attaches it in the same command.</span></span>

<span data-ttu-id="b346e-326">若要附加新的磁碟，請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="b346e-326">To attach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="b346e-327">若要附加現有的資料磁碟，請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="b346e-327">To attach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="b346e-328">然後您必須先掛接磁碟，就像在 Linux 掛接磁碟一樣。</span><span class="sxs-lookup"><span data-stu-id="b346e-328">Then you'll need to mount the disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b346e-329">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b346e-329">Next steps</span></span>
<span data-ttu-id="b346e-330">如需其他有關 Azure CLI 搭配 **arm** 模式使用的範例，請參閱 [搭配 Azure 資源管理員使用適用於 Mac、Linux 和 Windows 的 Azure CLI](../articles/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="b346e-330">For far more examples of Azure CLI usage with the **arm** mode, see [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="b346e-331">若要深入了解 Azure 資源和概念，請參閱[AAzure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b346e-331">To learn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="b346e-332">如需您可以使用的其他範本，請參閱[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)和[使用範本的應用程式架構](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b346e-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
