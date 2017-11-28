


## <a name="using-vm-extensions"></a><span data-ttu-id="b93ad-101">使用 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-101">Using VM Extensions</span></span>
<span data-ttu-id="b93ad-102">Azure VM 延伸模組會實作行為或功能，以協助其他程式在 Azure VM 上運作 (例如， **WebDeployForVSDevTest** 延伸模組可讓 Visual Studio 在您的 Azure VM 上進行 Web 部署解決方案)，或是讓您能夠與 VM 互動以支援一些其他行為 (例如，您可以使用 PowerShell 的 VM 存取延伸模組、Azure CLI 和 REST 用戶端，來重設或修改 Azure VM 上的遠端存取值)。</span><span class="sxs-lookup"><span data-stu-id="b93ad-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b93ad-103">如需所支援功能的完整延伸模組清單，請參閱[Azure VM 延伸模組與功能](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b93ad-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b93ad-104">因為每個 VM 擴充功能支援特定功能，您確切可以及不可以使用擴充功能做到的事取決於擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b93ad-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="b93ad-105">因此，在修改 VM 之前，請確定您已閱讀想要使用之 VM 擴充功能的文件。</span><span class="sxs-lookup"><span data-stu-id="b93ad-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="b93ad-106">不支援移除一些 VM 擴充功能。其他則具有已設定來大幅變更 VM 行為的屬性。</span><span class="sxs-lookup"><span data-stu-id="b93ad-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="b93ad-107">最常見的工作如下：</span><span class="sxs-lookup"><span data-stu-id="b93ad-107">The most common tasks are:</span></span>

1. <span data-ttu-id="b93ad-108">尋找可用的擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="b93ad-109">更新已載入的擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="b93ad-110">加入擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-110">Adding Extensions</span></span>
4. <span data-ttu-id="b93ad-111">移除擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="b93ad-112">尋找可用的擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-112">Find Available Extensions</span></span>
<span data-ttu-id="b93ad-113">您可以使用下列各項找到擴充功能和其他資訊：</span><span class="sxs-lookup"><span data-stu-id="b93ad-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="b93ad-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b93ad-114">PowerShell</span></span>
* <span data-ttu-id="b93ad-115">Azure 跨平台命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="b93ad-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="b93ad-116">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="b93ad-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b93ad-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b93ad-117">Azure PowerShell</span></span>
<span data-ttu-id="b93ad-118">有些擴充功能有特有的 PowerShell Cmdlet，這可能會使其更容易從 PowerShell 進行設定。但下列 Cmdlet 適用於所有的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b93ad-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="b93ad-119">您可以使用下列 Cmdlet 來取得可用擴充功能的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="b93ad-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="b93ad-120">針對 Web 角色或背景工作角色的執行個體，您可以使用 [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b93ad-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="b93ad-121">針對虛擬機器的執行個體，您可以使用 [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b93ad-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="b93ad-122">例如，下列程式碼範例示範如何使用 PowerShell 來列出 **IaaSDiagnostics** 延伸模組的資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="b93ad-123">Azure 命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="b93ad-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="b93ad-124">有些延伸模組有特有的 Azure CLI 命令 (Docker VM 延伸模組便是一個例子)，這可能會讓其更容易進行設定。但下列命令適用於所有的 VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="b93ad-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="b93ad-125">您可以使用 **azure vm extension list** 命令來取得可用延伸模組的相關資訊，並使用 **–-json** 選項來顯示有關一或多個延伸模組的所有可用資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="b93ad-126">如果您不使用擴充功能名稱，命令會傳回所有可用擴充功能的 JSON 描述。</span><span class="sxs-lookup"><span data-stu-id="b93ad-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="b93ad-127">例如，下列程式碼範例示範如何使用 Azure CLI **azure vm extension list** 命令列出 **IaaSDiagnostics** 延伸模組的資訊，並使用 **–-json** 選項傳回完整資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="b93ad-128">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="b93ad-128">Service Management REST APIs</span></span>
<span data-ttu-id="b93ad-129">您可以使用下列 REST API 來取得可用擴充功能的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="b93ad-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="b93ad-130">針對 Web 角色或背景工作角色的執行個體，您可以使用 [列出可用延伸模組](https://msdn.microsoft.com/library/dn169559.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="b93ad-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="b93ad-131">若要列出可用延伸模組的版本，您可以使用 [列出延伸模組版本](https://msdn.microsoft.com/library/dn495437.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b93ad-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="b93ad-132">針對虛擬機器的執行個體，您可以使用 [列出資源延伸模組](https://msdn.microsoft.com/library/dn495441.aspx) 作業。</span><span class="sxs-lookup"><span data-stu-id="b93ad-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="b93ad-133">若要列出可用延伸模組的版本，您可以使用 [列出資源延伸模組版本](https://msdn.microsoft.com/library/dn495440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b93ad-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="b93ad-134">加入、更新或停用擴充功能</span><span class="sxs-lookup"><span data-stu-id="b93ad-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="b93ad-135">擴充功能可以在建立執行個體或是它們可以加入執行中的執行個體時加入。</span><span class="sxs-lookup"><span data-stu-id="b93ad-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="b93ad-136">可以更新、停用或移除擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b93ad-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="b93ad-137">您可以使用 Azure PowerShell Cmdlet 或使用服務管理 REST API 作業來執行這些動作。</span><span class="sxs-lookup"><span data-stu-id="b93ad-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="b93ad-138">安裝和設定部分擴充功能時需要參數。</span><span class="sxs-lookup"><span data-stu-id="b93ad-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="b93ad-139">擴充功能支援公用和私人參數。</span><span class="sxs-lookup"><span data-stu-id="b93ad-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b93ad-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b93ad-140">Azure PowerShell</span></span>
<span data-ttu-id="b93ad-141">使用 Azure PowerShell Cmdlet 是加入與更新擴充功能最簡單的方式。</span><span class="sxs-lookup"><span data-stu-id="b93ad-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="b93ad-142">當您使用擴充功能 Cmdlet 時，會為您完成大部分的擴充功能組態。</span><span class="sxs-lookup"><span data-stu-id="b93ad-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="b93ad-143">有時您可能需要以程式設計方式加入擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b93ad-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="b93ad-144">需要如此做時，必須提供擴充功能的組態。</span><span class="sxs-lookup"><span data-stu-id="b93ad-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="b93ad-145">您可以使用下列 Cmdlet 來了解擴充功能是否需要公用和私用參數的組態：</span><span class="sxs-lookup"><span data-stu-id="b93ad-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="b93ad-146">針對 Web 角色或背景工作角色的執行個體，您可以使用 **Get-AzureServiceAvailableExtension** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b93ad-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="b93ad-147">針對虛擬機器的執行個體，您可以使用 **Get-AzureVMAvailableExtension** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b93ad-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="b93ad-148">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="b93ad-148">Service Management REST APIs</span></span>
<span data-ttu-id="b93ad-149">當您使用 REST API 擷取可用擴充功能清單時，會收到擴充功能設定方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="b93ad-150">傳回的資訊可能會顯示由公用結構描述和私用結構描述代表的參數資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="b93ad-151">關於執行個體的查詢會傳回公用參數值。</span><span class="sxs-lookup"><span data-stu-id="b93ad-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="b93ad-152">不會傳回私用參數值。</span><span class="sxs-lookup"><span data-stu-id="b93ad-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="b93ad-153">您可以使用下列 REST API 來了解擴充功能是否需要公用和私用參數的組態：</span><span class="sxs-lookup"><span data-stu-id="b93ad-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="b93ad-154">針對 Web 角色或背景工作角色的執行個體，**PublicConfigurationSchema** 和 **PrivateConfigurationSchema** 元素包含來自[列出可用延伸模組](https://msdn.microsoft.com/library/dn169559.aspx)作業回應的資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="b93ad-155">針對虛擬機器的執行個體，**PublicConfigurationSchema** 和 **PrivateConfigurationSchema** 元素包含來自[列出資源延伸模組](https://msdn.microsoft.com/library/dn495441.aspx)作業回應的資訊。</span><span class="sxs-lookup"><span data-stu-id="b93ad-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="b93ad-156">擴充功能也可以使用 JSON 所定義的組態。</span><span class="sxs-lookup"><span data-stu-id="b93ad-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="b93ad-157">使用這些類型的延伸模組時，只會使用 **SampleConfig** 元素。</span><span class="sxs-lookup"><span data-stu-id="b93ad-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

