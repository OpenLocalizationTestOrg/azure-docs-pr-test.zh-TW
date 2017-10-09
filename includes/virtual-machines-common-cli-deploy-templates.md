
* [<span data-ttu-id="28805-101">在 Azure 中快速建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="28805-102">在 Azure 中利用範本部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="28805-103">從自訂映像建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="28805-104">部署使用虛擬網路和負載平衡器的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="28805-105">移除資源群組</span><span class="sxs-lookup"><span data-stu-id="28805-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="28805-106">顯示資源群組部署的 hello 記錄檔</span><span class="sxs-lookup"><span data-stu-id="28805-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="28805-107">顯示虛擬機器的相關資訊</span><span class="sxs-lookup"><span data-stu-id="28805-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="28805-108">Tooa Linux 型虛擬機器連線</span><span class="sxs-lookup"><span data-stu-id="28805-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="28805-109">停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="28805-110">啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="28805-111">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="28805-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="28805-112">準備就緒</span><span class="sxs-lookup"><span data-stu-id="28805-112">Getting ready</span></span>
<span data-ttu-id="28805-113">您可以使用 Azure CLI hello 與 Azure 資源群組之前，您需要 toohave hello 適合 Azure CLI 版本與 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="28805-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="28805-114">如果您沒有 hello Azure CLI[安裝](../articles/cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="28805-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="28805-115">更新您的 Azure CLI 版本 too0.9.0 或更新版本</span><span class="sxs-lookup"><span data-stu-id="28805-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="28805-116">型別`azure --version`toosee 是否已安裝版本 0.9.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="28805-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="28805-117">如果您的版本不是 0.9.0 或更新版本中，您需要 tooupdate 它使用其中一種 hello 原生安裝程式或透過**npm**輸入`npm update -g azure-cli`。</span><span class="sxs-lookup"><span data-stu-id="28805-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="28805-118">您也可以執行的 Docker 容器 Azure CLI，使用 hello 下列[Docker 映像](https://registry.hub.docker.com/u/microsoft/azure-cli/)。</span><span class="sxs-lookup"><span data-stu-id="28805-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="28805-119">Docker 主機時，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="28805-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="28805-120">設定 Azure 帳戶和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="28805-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="28805-121">如果您還沒有 Azure 訂閱帳戶，但是有 MSDN 訂閱帳戶，請啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="28805-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="28805-122">或者申請 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="28805-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="28805-123">現在[以互動方式登入 Azure 帳戶 tooyour](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login)輸入`azure login`並遵循 hello 互動式登入經驗 tooyour Azure 帳戶的提示。</span><span class="sxs-lookup"><span data-stu-id="28805-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="28805-124">如果您有工作或學校識別碼，而且您知道您不需要啟用雙因素驗證，您可以**也**使用`azure login -u`以及 hello 工作或學校中的識別碼 toolog*沒有*互動式工作階段。</span><span class="sxs-lookup"><span data-stu-id="28805-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="28805-125">如果您不要有工作或學校識別碼，您可以[從個人 Microsoft 帳戶所建立的工作或學校識別碼](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toolog hello 中的相同的方式。</span><span class="sxs-lookup"><span data-stu-id="28805-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="28805-126">您的帳戶可能會有一個以上的訂閱帳戶。</span><span class="sxs-lookup"><span data-stu-id="28805-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="28805-127">您可以輸入 `azure account list`，即可列出訂閱帳戶，如以下所示：</span><span class="sxs-lookup"><span data-stu-id="28805-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

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

<span data-ttu-id="28805-128">您可以輸入 hello 下列設定 hello 目前的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28805-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="28805-129">使用 hello 訂用帳戶名稱或 hello ID 具有您想要 toomanage hello 資源。</span><span class="sxs-lookup"><span data-stu-id="28805-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="28805-130">切換 toohello Azure CLI 資源群組模式</span><span class="sxs-lookup"><span data-stu-id="28805-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="28805-131">根據預設，啟動 「 hello 服務管理模式 hello Azure CLI (**asm**模式)。</span><span class="sxs-lookup"><span data-stu-id="28805-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="28805-132">輸入 hello 遵循 tooswitch tooresource 群組模式。</span><span class="sxs-lookup"><span data-stu-id="28805-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="28805-133">了解 Azure 資源範本和資源群組</span><span class="sxs-lookup"><span data-stu-id="28805-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="28805-134">大部分的應用程式在建立時會使用不同資源類型的組合 (例如一或多個 VM 和儲存體帳戶、SQL 資料庫、虛擬網路或內容傳遞網路)。</span><span class="sxs-lookup"><span data-stu-id="28805-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="28805-135">hello 預設 Azure 服務管理 API，而且 hello Azure 傳統入口網站以表示這些項目使用的服務方法。</span><span class="sxs-lookup"><span data-stu-id="28805-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="28805-136">這種方法需要您 toodeploy 和個別管理 hello 個別服務 （或尋找其他工具，這樣做），而不是部署為單一邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="28805-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="28805-137">*Azure 資源管理員範本*，不過，可讓您 toodeploy 和做為一個邏輯的部署單位，以宣告方式管理這些不同的資源。</span><span class="sxs-lookup"><span data-stu-id="28805-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="28805-138">而不是以命令方式告訴 Azure 哪些 toodeploy 一個命令在另一個之後，描述整個部署-所有 hello 資源和相關聯的組態和部署參數-在 JSON 檔案中，並告訴 Azure toodeploy 成為這些資源群組。</span><span class="sxs-lookup"><span data-stu-id="28805-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="28805-139">接著，您可以管理 hello hello 群組的資源，使用 Azure CLI 資源管理命令的整個生命週期：</span><span class="sxs-lookup"><span data-stu-id="28805-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="28805-140">停止、 啟動或同時刪除所有 hello hello 群組內的資源。</span><span class="sxs-lookup"><span data-stu-id="28805-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="28805-141">在其上套用角色型存取控制 (RBAC) 規則 toolock 下安全性權限。</span><span class="sxs-lookup"><span data-stu-id="28805-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="28805-142">稽核作業。</span><span class="sxs-lookup"><span data-stu-id="28805-142">Audit operations.</span></span>
* <span data-ttu-id="28805-143">利用其他中繼資料標記資源，方便追蹤。</span><span class="sxs-lookup"><span data-stu-id="28805-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="28805-144">您可以了解更多關於 Azure 資源群組，以及如何為您在 hello 許多[Azure 資源管理員概觀](../articles/azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="28805-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="28805-145">如果您有興趣了解如何編寫範本，請參閱 [編寫 Azure 資源管理員範本](../articles/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="28805-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="28805-146"><a id="quick-create-a-vm-in-azure"></a>工作：在 Azure 中快速建立 VM</span><span class="sxs-lookup"><span data-stu-id="28805-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="28805-147">有時候您知道在需要時，哪些映像，您現在需要將 VM 從該映像和您不太在意 hello 基礎結構--或許您有 tootest 全新的 VM 上。</span><span class="sxs-lookup"><span data-stu-id="28805-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="28805-148">這是當您想要 toouse hello`azure vm quick-create`命令，然後傳遞 hello 引數需要 toocreate，VM 和它的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="28805-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="28805-149">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="28805-149">First, create your resource group.</span></span>

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

<span data-ttu-id="28805-150">第二，您將需要映像。</span><span class="sxs-lookup"><span data-stu-id="28805-150">Second, you'll need an image.</span></span> <span data-ttu-id="28805-151">toofind 映像以 hello Azure CLI，請參閱[巡覽並選取 Azure 虛擬機器映像使用 PowerShell 和 hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="28805-152">不過在本文中，以下是常用映像的簡要清單。</span><span class="sxs-lookup"><span data-stu-id="28805-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="28805-153">我們會使用 CoreOS 的 Stable 映像，縮短整個建立流程。</span><span class="sxs-lookup"><span data-stu-id="28805-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="28805-154">ComputeImageVersion，您可以也只提供 「 最近的 」 為 hello hello Azure CLI 和這兩個 hello 範本語言中的參數。</span><span class="sxs-lookup"><span data-stu-id="28805-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="28805-155">這可讓您 tooalways 使用 hello hello 映像的最新的和修補版本而不需 toomodify，您的指令碼或範本。</span><span class="sxs-lookup"><span data-stu-id="28805-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="28805-156">如下所示。</span><span class="sxs-lookup"><span data-stu-id="28805-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="28805-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="28805-157">PublisherName</span></span> | <span data-ttu-id="28805-158">提供項目</span><span class="sxs-lookup"><span data-stu-id="28805-158">Offer</span></span> | <span data-ttu-id="28805-159">SKU</span><span class="sxs-lookup"><span data-stu-id="28805-159">Sku</span></span> | <span data-ttu-id="28805-160">版本</span><span class="sxs-lookup"><span data-stu-id="28805-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="28805-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="28805-161">OpenLogic</span></span> |<span data-ttu-id="28805-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="28805-162">CentOS</span></span> |<span data-ttu-id="28805-163">7</span><span class="sxs-lookup"><span data-stu-id="28805-163">7</span></span> |<span data-ttu-id="28805-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="28805-164">7.0.201503</span></span> |
| <span data-ttu-id="28805-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="28805-165">OpenLogic</span></span> |<span data-ttu-id="28805-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="28805-166">CentOS</span></span> |<span data-ttu-id="28805-167">7.1</span><span class="sxs-lookup"><span data-stu-id="28805-167">7.1</span></span> |<span data-ttu-id="28805-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="28805-168">7.1.201504</span></span> |
| <span data-ttu-id="28805-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="28805-169">CoreOS</span></span> |<span data-ttu-id="28805-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="28805-170">CoreOS</span></span> |<span data-ttu-id="28805-171">Beta</span><span class="sxs-lookup"><span data-stu-id="28805-171">Beta</span></span> |<span data-ttu-id="28805-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="28805-172">647.0.0</span></span> |
| <span data-ttu-id="28805-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="28805-173">CoreOS</span></span> |<span data-ttu-id="28805-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="28805-174">CoreOS</span></span> |<span data-ttu-id="28805-175">Stable</span><span class="sxs-lookup"><span data-stu-id="28805-175">Stable</span></span> |<span data-ttu-id="28805-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="28805-176">633.1.0</span></span> |
| <span data-ttu-id="28805-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="28805-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="28805-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="28805-178">DynamicsNAV</span></span> |<span data-ttu-id="28805-179">2015</span><span class="sxs-lookup"><span data-stu-id="28805-179">2015</span></span> |<span data-ttu-id="28805-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="28805-180">8.0.40459</span></span> |
| <span data-ttu-id="28805-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="28805-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="28805-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="28805-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="28805-183">2013</span><span class="sxs-lookup"><span data-stu-id="28805-183">2013</span></span> |<span data-ttu-id="28805-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="28805-184">1.0.0</span></span> |
| <span data-ttu-id="28805-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="28805-185">msopentech</span></span> |<span data-ttu-id="28805-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="28805-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="28805-187">標準</span><span class="sxs-lookup"><span data-stu-id="28805-187">Standard</span></span> |<span data-ttu-id="28805-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="28805-188">1.0.0</span></span> |
| <span data-ttu-id="28805-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="28805-189">msopentech</span></span> |<span data-ttu-id="28805-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="28805-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="28805-191">Enterprise</span><span class="sxs-lookup"><span data-stu-id="28805-191">Enterprise</span></span> |<span data-ttu-id="28805-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="28805-192">1.0.0</span></span> |
| <span data-ttu-id="28805-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="28805-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="28805-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="28805-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="28805-195">Enterprise-Optimized-for-DW</span><span class="sxs-lookup"><span data-stu-id="28805-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="28805-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="28805-196">12.0.2430</span></span> |
| <span data-ttu-id="28805-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="28805-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="28805-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="28805-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="28805-199">Enterprise-Optimized-for-OLTP</span><span class="sxs-lookup"><span data-stu-id="28805-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="28805-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="28805-200">12.0.2430</span></span> |
| <span data-ttu-id="28805-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="28805-201">Canonical</span></span> |<span data-ttu-id="28805-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="28805-202">UbuntuServer</span></span> |<span data-ttu-id="28805-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="28805-203">12.04.5-LTS</span></span> |<span data-ttu-id="28805-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="28805-204">12.04.201504230</span></span> |
| <span data-ttu-id="28805-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="28805-205">Canonical</span></span> |<span data-ttu-id="28805-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="28805-206">UbuntuServer</span></span> |<span data-ttu-id="28805-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="28805-207">14.04.2-LTS</span></span> |<span data-ttu-id="28805-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="28805-208">14.04.201503090</span></span> |
| <span data-ttu-id="28805-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="28805-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-210">WindowsServer</span></span> |<span data-ttu-id="28805-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="28805-211">2012-Datacenter</span></span> |<span data-ttu-id="28805-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="28805-212">3.0.201503</span></span> |
| <span data-ttu-id="28805-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="28805-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-214">WindowsServer</span></span> |<span data-ttu-id="28805-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="28805-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="28805-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="28805-216">4.0.201503</span></span> |
| <span data-ttu-id="28805-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="28805-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="28805-218">WindowsServer</span></span> |<span data-ttu-id="28805-219">Windows-Server-Technical-Preview</span><span class="sxs-lookup"><span data-stu-id="28805-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="28805-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="28805-220">5.0.201504</span></span> |
| <span data-ttu-id="28805-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="28805-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="28805-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="28805-222">WindowsServerEssentials</span></span> |<span data-ttu-id="28805-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="28805-223">WindowsServerEssentials</span></span> |<span data-ttu-id="28805-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="28805-224">1.0.141204</span></span> |
| <span data-ttu-id="28805-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="28805-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="28805-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="28805-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="28805-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="28805-227">2012R2</span></span> |<span data-ttu-id="28805-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="28805-228">4.3.4665</span></span> |

<span data-ttu-id="28805-229">只要建立您的 VM 輸入 hello`azure vm quick-create`命令，並準備就緒的 hello 提示。</span><span class="sxs-lookup"><span data-stu-id="28805-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="28805-230">您應該會看到類似下面的畫面：</span><span class="sxs-lookup"><span data-stu-id="28805-230">It should look something like this:</span></span>

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
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
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

<span data-ttu-id="28805-231">無論身在何處，新的 VM 就在您身邊。</span><span class="sxs-lookup"><span data-stu-id="28805-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="28805-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>工作：在 Azure 中利用範本部署 VM</span><span class="sxs-lookup"><span data-stu-id="28805-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="28805-233">使用這些章節 toodeploy 新的 Azure VM 中的 hello 指示，以 hello Azure CLI 使用範本。</span><span class="sxs-lookup"><span data-stu-id="28805-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="28805-234">此範本所建立單一的虛擬機器中新的虛擬網路與單一子網路，此外，不同於`azure vm quick-create`，可讓您 toodescribe 您想要精確地重複無誤。</span><span class="sxs-lookup"><span data-stu-id="28805-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="28805-235">以下是這個範本建立的內容：</span><span class="sxs-lookup"><span data-stu-id="28805-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="28805-236">步驟 1： 檢查 hello 範本參數的 hello JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="28805-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="28805-237">以下是 hello 的 hello hello 範本的 JSON 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="28805-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="28805-238">(hello 範本也位於[GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json)。)</span><span class="sxs-lookup"><span data-stu-id="28805-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="28805-239">範本是彈性，因此擁有許多的參數選擇 toogive 或只有少數藉由建立多固定範本選擇 toooffer hello 設計工具。</span><span class="sxs-lookup"><span data-stu-id="28805-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="28805-240">在您需要 toopass hello 範本做為參數順序 toocollect hello 資訊，開啟 hello 範本檔案 （本主題具有下列範本內嵌），檢查 hello**參數**值。</span><span class="sxs-lookup"><span data-stu-id="28805-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="28805-241">在此情況下，以下的 hello 範本會要求您：</span><span class="sxs-lookup"><span data-stu-id="28805-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="28805-242">唯一的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="28805-242">A unique storage account name.</span></span>
* <span data-ttu-id="28805-243">Hello VM 系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="28805-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="28805-244">密碼。</span><span class="sxs-lookup"><span data-stu-id="28805-244">A password.</span></span>
* <span data-ttu-id="28805-245">Hello world toouse 外部網域名稱。</span><span class="sxs-lookup"><span data-stu-id="28805-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="28805-246">Ubuntu Server 版本號碼 -- 但只能接受一個清單。</span><span class="sxs-lookup"><span data-stu-id="28805-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="28805-247">進一步了解 [使用者名稱和密碼需求](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm)。</span><span class="sxs-lookup"><span data-stu-id="28805-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="28805-248">一旦您決定對這些值，您正在準備 toocreate 的群組，並將此範本部署到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="28805-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
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
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
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

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="28805-249">步驟 2： 使用 hello 範本來建立 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="28805-250">一旦您準備好的參數值，您必須針對範本部署建立資源群組，然後再部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="28805-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="28805-251">toocreate hello 資源群組、 型別`azure group create <group name> <location>`hello 名稱 hello 群組，您想要 toodeploy hello 資料中心位置。</span><span class="sxs-lookup"><span data-stu-id="28805-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="28805-252">進行速度十分快：</span><span class="sxs-lookup"><span data-stu-id="28805-252">This happens quickly:</span></span>

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

<span data-ttu-id="28805-253">現在 toocreate hello 部署，此時會呼叫`azure group deployment create`並傳遞：</span><span class="sxs-lookup"><span data-stu-id="28805-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="28805-254">hello 範本檔案 （如果您要儲存 JSON 範本 tooa 本機檔案上方的 hello）。</span><span class="sxs-lookup"><span data-stu-id="28805-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="28805-255">範本 （如果您想要在 GitHub 或其他的 web 位址中的 hello 檔案 toopoint） 的 URI。</span><span class="sxs-lookup"><span data-stu-id="28805-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="28805-256">您想在其中 toodeploy hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="28805-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="28805-257">選用部署名稱。</span><span class="sxs-lookup"><span data-stu-id="28805-257">An optional deployment name.</span></span>

<span data-ttu-id="28805-258">系統會提示的 toosupply hello hello JSON 檔案 hello < 參數 > 一節中的參數值。</span><span class="sxs-lookup"><span data-stu-id="28805-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="28805-259">當您已指定所有的 hello 參數值時，就會開始您的部署。</span><span class="sxs-lookup"><span data-stu-id="28805-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="28805-260">下列是一個範例：</span><span class="sxs-lookup"><span data-stu-id="28805-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="28805-261">您會收到 hello 下列類型的資訊：</span><span class="sxs-lookup"><span data-stu-id="28805-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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


## <span data-ttu-id="28805-262"><a id="create-a-custom-vm-image"></a>工作：建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="28805-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="28805-263">您已看過上述範本 hello 基本使用方式，所以現在我們可以使用類似指示 toocreate 自訂 VM 在 Azure 中的特定.vhd 檔案從使用範本，以透過 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="28805-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="28805-264">這裡的 hello 差異在於這個範本會建立單一的虛擬機器，從指定虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="28805-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="28805-265">步驟 1： 檢查 hello hello 範本的 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="28805-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="28805-266">以下是 hello hello 本節使用做為範例的 hello 範本的 JSON 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="28805-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="28805-267">(hello 範本也位於[GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json)。)</span><span class="sxs-lookup"><span data-stu-id="28805-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="28805-268">同樣地，您將需要 toofind hello 值要 tooenter hello 參數沒有預設值。</span><span class="sxs-lookup"><span data-stu-id="28805-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="28805-269">當您執行 hello`azure group deployment create`命令時，Azure CLI hello 會提示您 tooenter 這些值。</span><span class="sxs-lookup"><span data-stu-id="28805-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

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

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="28805-270">步驟 2： 取得 hello VHD</span><span class="sxs-lookup"><span data-stu-id="28805-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="28805-271">很明顯，您需要 .vhd。</span><span class="sxs-lookup"><span data-stu-id="28805-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="28805-272">您可以使用 Azure 現有的 .vhd 或者可以上傳一個 .vhd。</span><span class="sxs-lookup"><span data-stu-id="28805-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="28805-273">Windows 型虛擬機器，請參閱[建立並上傳 Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="28805-274">Linux 型虛擬機器，請參閱[建立和上傳包含 hello Linux 作業系統的虛擬硬碟](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="28805-275">步驟 3： 使用 hello 範本來建立 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="28805-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="28805-276">您現在已經準備好 toocreate hello.vhd 為基礎的新虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="28805-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="28805-277">使用建立置入群組 toodeploy `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="28805-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

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

<span data-ttu-id="28805-278">然後使用 hello 建立 hello 部署`--template-uri`直接 hello 範本中的選項 toocall (或者您可以使用 hello`--template-file`選項 toouse 您已在本機儲存的檔案)。</span><span class="sxs-lookup"><span data-stu-id="28805-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="28805-279">請注意，因為 hello 範本有指定的預設值，系統會提示您只有幾件事。</span><span class="sxs-lookup"><span data-stu-id="28805-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="28805-280">如果您部署在不同的地方 hello 範本，您可能會發現某些命名的衝突發生 hello 預設值 （特別是 hello DNS 名稱建立）。</span><span class="sxs-lookup"><span data-stu-id="28805-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="28805-281">輸出看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="28805-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
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

## <span data-ttu-id="28805-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>工作：部署含多部 VM 的應用程式，它會使用虛擬網路和外部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="28805-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="28805-283">此範本可讓您在負載平衡器下 toocreate 兩個虛擬機器，並設定連接埠 80 上的負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="28805-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="28805-284">這個範本也會部署儲存體帳戶、虛擬網路、公用 IP 位址、可用性集合以及網路介面。</span><span class="sxs-lookup"><span data-stu-id="28805-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="28805-285">請遵循這些步驟 toodeploy hello GitHub 範本儲存機制，透過 Azure PowerShell 命令中使用資源管理員範本中使用虛擬網路和負載平衡器的多部 VM 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28805-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="28805-286">步驟 1： 檢查 hello hello 範本的 JSON 檔案</span><span class="sxs-lookup"><span data-stu-id="28805-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="28805-287">以下是 hello 的 hello hello 範本的 JSON 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="28805-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="28805-288">如果您想 hello 最新版本，它找到[hello GitHub 儲存機制範本](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="28805-289">本主題使用 hello`--template-uri`交換器 toocall hello 範本，但您也可以使用 hello`--template-file`切換 toopass 本機版本。</span><span class="sxs-lookup"><span data-stu-id="28805-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

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
                "description": "Prefix toouse for VM names"
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
                "description": "Size of hello VM"
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

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="28805-290">步驟 2： 使用 hello 範本來建立 hello 部署</span><span class="sxs-lookup"><span data-stu-id="28805-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="28805-291">使用建立資源群組 hello 範本`azure group create <location>`。</span><span class="sxs-lookup"><span data-stu-id="28805-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="28805-292">然後，使用建立部署至資源群組`azure group deployment create`和傳遞 hello 資源群組、 將傳遞為部署名稱，和回應 hello 提示沒有預設值的 hello 範本中的參數。</span><span class="sxs-lookup"><span data-stu-id="28805-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

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

<span data-ttu-id="28805-293">現在使用 hello`azure group deployment create`命令和 hello`--template-uri`選項 toodeploy hello 範本。</span><span class="sxs-lookup"><span data-stu-id="28805-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="28805-294">請在系統提示時備妥您的參數值，如下所示。</span><span class="sxs-lookup"><span data-stu-id="28805-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
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

<span data-ttu-id="28805-295">請注意，這個範本會部署 Windows Server 映像。不過，任何 Linux 映像都可以輕易取代它。</span><span class="sxs-lookup"><span data-stu-id="28805-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="28805-296">想 toocreate Docker 叢集具有多個群集管理員嗎？</span><span class="sxs-lookup"><span data-stu-id="28805-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="28805-297">[您做得到](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/)。</span><span class="sxs-lookup"><span data-stu-id="28805-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="28805-298"><a id="remove-a-resource-group"></a>工作：移除資源群組</span><span class="sxs-lookup"><span data-stu-id="28805-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="28805-299">請注意，您可以重新部署 tooa 資源群組，但如果您完成其中一個，可以刪除使用`azure group delete <group name>`。</span><span class="sxs-lookup"><span data-stu-id="28805-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="28805-300"><a id="show-the-log-for-a-resource-group-deployment"></a>工作： 顯示 hello 記錄檔中的資源群組部署</span><span class="sxs-lookup"><span data-stu-id="28805-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="28805-301">建立或使用範本時，此種情況很常見。</span><span class="sxs-lookup"><span data-stu-id="28805-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="28805-302">hello 呼叫 toodisplay hello 部署記錄檔群組是`azure group log show <groupname>`，其中顯示相當多的了解為什麼指發生-，或未有用的資訊。</span><span class="sxs-lookup"><span data-stu-id="28805-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="28805-303">(如需疑難排解部署及其他問題的詳細資訊，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md))。</span><span class="sxs-lookup"><span data-stu-id="28805-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="28805-304">tootarget 特定失敗，例如，您可能會使用等工具**jq**更精確地說，例如哪些個別失敗您需要 toocorrect tooquery 項目。</span><span class="sxs-lookup"><span data-stu-id="28805-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="28805-305">hello 下列範例會使用**jq** tooparse 部署記錄檔以取得**lbgroup**，尋找失敗。</span><span class="sxs-lookup"><span data-stu-id="28805-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="28805-306">您可以快速發現問題出在哪裡，然後予以修正，最後再試一次。</span><span class="sxs-lookup"><span data-stu-id="28805-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="28805-307">在下列案例的 hello，hello 範本具有已建立兩個 Vm 在 hello hello.vhd 建立鎖定的相同時間。</span><span class="sxs-lookup"><span data-stu-id="28805-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="28805-308">(我們修改 hello 範本之後，hello 快速成功的部署)。</span><span class="sxs-lookup"><span data-stu-id="28805-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="28805-309"><a id="display-information-about-a-virtual-machine"></a>工作：顯示虛擬機器的相關資訊</span><span class="sxs-lookup"><span data-stu-id="28805-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="28805-310">您可以在資源群組中看到特定 Vm 的相關資訊，使用 hello`azure vm show <groupname> <vmname>`命令。</span><span class="sxs-lookup"><span data-stu-id="28805-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="28805-311">如果您有一個以上的 VM 群組中，您需要在群組中的 toolist hello Vm 使用`azure vm list <groupname>`。</span><span class="sxs-lookup"><span data-stu-id="28805-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="28805-312">然後，查閱 myVM1：</span><span class="sxs-lookup"><span data-stu-id="28805-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
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
> <span data-ttu-id="28805-313">如果您想 tooprogrammatically 存放區，且操作 hello 的主控台命令的輸出，您可能會想的 toouse JSON 剖析工具例如 **[jq](https://github.com/stedolan/jq)** 或 **[jsawk](https://github.com/micha/jsawk)** ，或語言比較適合 hello 工作的程式庫。</span><span class="sxs-lookup"><span data-stu-id="28805-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="28805-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>登入 tooa Linux 型虛擬機器的工作：</span><span class="sxs-lookup"><span data-stu-id="28805-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="28805-315">通常 Linux 機器是連線的 toothrough SSH。</span><span class="sxs-lookup"><span data-stu-id="28805-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="28805-316">如需詳細資訊，請參閱[如何透過在 Azure 上的 Linux SSH toouse](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="28805-317"><a id="stop-a-virtual-machine"></a>工作：停止 VM</span><span class="sxs-lookup"><span data-stu-id="28805-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="28805-318">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="28805-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="28805-319">使用此參數 tookeep hello 虛擬 IP (VIP) 的 hello vnet，以便在 hello 該 vnet 中的最後一個 VM。</span><span class="sxs-lookup"><span data-stu-id="28805-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="28805-320">如果您使用 hello`StayProvisioned`參數，您將仍然要支付 hello VM。</span><span class="sxs-lookup"><span data-stu-id="28805-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="28805-321"><a id="start-a-virtual-machine"></a>工作：啟動 VM</span><span class="sxs-lookup"><span data-stu-id="28805-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="28805-322">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="28805-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="28805-323"><a id="attach-a-data-disk"></a>工作：連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="28805-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="28805-324">您還需要 toodecide 是否 tooattach 新磁碟或其中所包含的資料。</span><span class="sxs-lookup"><span data-stu-id="28805-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="28805-325">Hello 命令建立 hello.vhd 檔案並將它附加在 hello 做為新的磁碟，同一個命令。</span><span class="sxs-lookup"><span data-stu-id="28805-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="28805-326">tooattach 新磁碟時，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="28805-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="28805-327">tooattach 現有的資料磁碟，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="28805-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="28805-328">然後您將需要 toomount hello 磁碟，像平常一樣在 Linux 中。</span><span class="sxs-lookup"><span data-stu-id="28805-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28805-329">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28805-329">Next steps</span></span>
<span data-ttu-id="28805-330">如需以 hello Azure CLI 使用方式的更多範例**arm**模式中，請參閱[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](../articles/xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="28805-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="28805-331">toolearn 深入了解 Azure 資源和其概念，請參閱[Azure 資源管理員概觀](../articles/azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="28805-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="28805-332">如需您可以使用的其他範本，請參閱[Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)和[使用範本的應用程式架構](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="28805-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
