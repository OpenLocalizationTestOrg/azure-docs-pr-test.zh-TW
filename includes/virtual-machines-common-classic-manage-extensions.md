


## <a name="using-vm-extensions"></a><span data-ttu-id="27fba-101">使用 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-101">Using VM Extensions</span></span>
<span data-ttu-id="27fba-102">Azure VM 延伸模組實作行為或功能，是協助 Azure Vm 上使用其他程式 (例如，hello **WebDeployForVSDevTest**延伸模組可讓 Visual Studio tooWeb 部署解決方案上的 Azure VM)，或提供hello 能力 toointeract hello VM toosupport 與其他的行為 （例如，您可以使用從 PowerShell、 hello Azure CLI 和 REST 用戶端 tooreset hello VM 存取擴充功能或修改 Azure VM 上的遠端存取值）。</span><span class="sxs-lookup"><span data-stu-id="27fba-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="27fba-103">依其支援的 hello 功能的擴充功能的完整清單，請參閱[Azure VM 延伸模組和功能](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="27fba-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="27fba-104">因為每個 VM 延伸模組支援特定功能，完全什麼您可以與具有副檔名無法執行的動作取決於 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="27fba-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="27fba-105">因此，在修改之前您的 VM，請確定您已閱讀 hello 文件以 hello 想 toouse VM 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="27fba-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="27fba-106">不支援移除一些 VM 擴充功能。其他則具有已設定來大幅變更 VM 行為的屬性。</span><span class="sxs-lookup"><span data-stu-id="27fba-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="27fba-107">hello 最常見的工作如下：</span><span class="sxs-lookup"><span data-stu-id="27fba-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="27fba-108">尋找可用的擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="27fba-109">更新已載入的擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="27fba-110">加入擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-110">Adding Extensions</span></span>
4. <span data-ttu-id="27fba-111">移除擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="27fba-112">尋找可用的擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-112">Find Available Extensions</span></span>
<span data-ttu-id="27fba-113">您可以使用下列各項找到擴充功能和其他資訊：</span><span class="sxs-lookup"><span data-stu-id="27fba-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="27fba-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27fba-114">PowerShell</span></span>
* <span data-ttu-id="27fba-115">Azure 跨平台命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="27fba-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="27fba-116">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="27fba-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="27fba-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="27fba-117">Azure PowerShell</span></span>
<span data-ttu-id="27fba-118">有些延伸模組包含 PowerShell cmdlet 的特定 toothem，可能會建立其組態從 PowerShell 更容易。但 hello 下列 cmdlet 適用於所有 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="27fba-119">您可以使用下列 cmdlet tooobtain 資訊可用擴充功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="27fba-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="27fba-120">執行個體的 web 角色或背景工作角色，您可以使用 hello [Get-azureserviceavailableextension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="27fba-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="27fba-121">執行個體的虛擬機器，您可以使用 hello [Get-azurevmavailableextension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="27fba-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="27fba-122">例如，下列程式碼範例顯示如何來 hello toolist hello 的資訊**IaaSDiagnostics**使用 PowerShell 的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="27fba-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="27fba-123">Azure 命令列介面 (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="27fba-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="27fba-124">有些延伸模組包含特定 toothem Azure CLI 命令 （hello Docker VM 擴充功能是一個例子），這可能會讓其組態更容易。但 hello 下列命令的所有 VM 擴充功能的運作。</span><span class="sxs-lookup"><span data-stu-id="27fba-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="27fba-125">您可以使用 hello **azure vm 延伸模組清單**命令 tooobtain 資訊可用擴充功能，並使用 hello **--json**選項 toodisplay 一或多個擴充功能的相關的所有可用的資訊。</span><span class="sxs-lookup"><span data-stu-id="27fba-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="27fba-126">如果您未使用的副檔名，hello 命令傳回的 JSON 描述所有可用的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="27fba-127">例如，hello 下列程式碼範例顯示如何 toolist hello 資訊 hello **IaaSDiagnostics**延伸模組使用 hello Azure CLI **azure vm 延伸模組清單**命令，並使用 hello **--json**選項 tooreturn 完整資訊。</span><span class="sxs-lookup"><span data-stu-id="27fba-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="27fba-128">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="27fba-128">Service Management REST APIs</span></span>
<span data-ttu-id="27fba-129">您可以使用下列 REST Api tooobtain 資訊可用擴充功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="27fba-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="27fba-130">執行個體的 web 角色或背景工作角色，您可以使用 hello[列出可用擴充功能](https://msdn.microsoft.com/library/dn169559.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="27fba-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="27fba-131">toolist hello 版本中可用的擴充功能，您可以使用[列出擴充功能版本](https://msdn.microsoft.com/library/dn495437.aspx)。</span><span class="sxs-lookup"><span data-stu-id="27fba-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="27fba-132">執行個體的虛擬機器，您可以使用 hello[列出資源擴充功能](https://msdn.microsoft.com/library/dn495441.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="27fba-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="27fba-133">toolist hello 版本中可用的擴充功能，您可以使用[列出資源擴充功能版本](https://msdn.microsoft.com/library/dn495440.aspx)。</span><span class="sxs-lookup"><span data-stu-id="27fba-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="27fba-134">加入、更新或停用擴充功能</span><span class="sxs-lookup"><span data-stu-id="27fba-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="27fba-135">建立執行個體時，或者可以將它們加入 tooa 執行執行個體，可以加入擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="27fba-136">可以更新、停用或移除擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="27fba-137">您可以使用 Azure PowerShell cmdlet 或使用 hello 服務管理 REST API 作業來執行這些動作。</span><span class="sxs-lookup"><span data-stu-id="27fba-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="27fba-138">參數是必要的 tooinstall 和設定部分擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="27fba-139">擴充功能支援公用和私人參數。</span><span class="sxs-lookup"><span data-stu-id="27fba-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="27fba-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="27fba-140">Azure PowerShell</span></span>
<span data-ttu-id="27fba-141">使用 Azure PowerShell cmdlet 是 hello 最簡單方式 tooadd 和更新擴充功能。</span><span class="sxs-lookup"><span data-stu-id="27fba-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="27fba-142">當您使用 hello 延伸模組的 cmdlet 時，為您完成大部分的 hello 擴充的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="27fba-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="27fba-143">有時候，您可能需要 tooprogrammatically 加入延伸模組。</span><span class="sxs-lookup"><span data-stu-id="27fba-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="27fba-144">當您需要 toodo 此時，您必須提供 hello 擴充的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="27fba-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="27fba-145">您可以使用下列 cmdlet tooknow 擴充功能需要公用和私人參數的組態是否 hello:</span><span class="sxs-lookup"><span data-stu-id="27fba-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="27fba-146">執行個體的 web 角色或背景工作角色，您可以使用 hello **Get-azureserviceavailableextension** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="27fba-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="27fba-147">執行個體的虛擬機器，您可以使用 hello **Get-azurevmavailableextension** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="27fba-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="27fba-148">服務管理 REST API</span><span class="sxs-lookup"><span data-stu-id="27fba-148">Service Management REST APIs</span></span>
<span data-ttu-id="27fba-149">當您使用 hello REST Api 擷取可用擴充功能清單時，您會收到 hello 延伸模組的 toobe 設定方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="27fba-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="27fba-150">傳回的 hello 資訊可能會顯示由公用結構描述和私人結構描述表示的參數資訊。</span><span class="sxs-lookup"><span data-stu-id="27fba-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="27fba-151">關於 hello 執行個體的查詢會傳回公用參數值。</span><span class="sxs-lookup"><span data-stu-id="27fba-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="27fba-152">不會傳回私用參數值。</span><span class="sxs-lookup"><span data-stu-id="27fba-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="27fba-153">您可以使用下列 REST Api tooknow 擴充功能需要公用和私人參數的組態是否 hello:</span><span class="sxs-lookup"><span data-stu-id="27fba-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="27fba-154">針對 web 角色或背景工作角色執行個體 hello **PublicConfigurationSchema**和**PrivateConfigurationSchema**元素包含 hello hello 回應 hello 資訊[清單可用的擴充功能](https://msdn.microsoft.com/library/dn169559.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="27fba-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="27fba-155">針對虛擬機器的執行個體 hello **PublicConfigurationSchema**和**PrivateConfigurationSchema**元素包含 hello hello 回應 hello 資訊[清單資源擴充功能](https://msdn.microsoft.com/library/dn495441.aspx)作業。</span><span class="sxs-lookup"><span data-stu-id="27fba-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="27fba-156">擴充功能也可以使用 JSON 所定義的組態。</span><span class="sxs-lookup"><span data-stu-id="27fba-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="27fba-157">當使用這些類型的擴充功能時，只有 hello **SampleConfig**使用項目。</span><span class="sxs-lookup"><span data-stu-id="27fba-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

