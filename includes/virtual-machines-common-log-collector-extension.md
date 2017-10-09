
<span data-ttu-id="d4651-101">診斷問題的 Microsoft Azure 雲端服務需要 hello 問題發生時收集 hello 服務的虛擬機器上的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d4651-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="d4651-102">您可以使用 hello AzureLogCollector 延伸隨 tooperfom 單次收集記錄檔從一或多個雲端服務 Vm （從 web 角色和背景工作角色） 和傳送嗨收集檔案 tooan Azure 儲存體帳戶 – 完全不需要從遠端登入tooany 的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="d4651-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="d4651-103">可以在 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp 找到大部分的 hello 記錄資訊的描述。</span><span class="sxs-lookup"><span data-stu-id="d4651-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="d4651-104">有兩個模式的集合收集檔案 toobe hello 類型而定。</span><span class="sxs-lookup"><span data-stu-id="d4651-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="d4651-105">僅限 Azure 客體代理程式記錄檔 (GA)。</span><span class="sxs-lookup"><span data-stu-id="d4651-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="d4651-106">這個收集模式包含所有 hello 記錄相關的 tooAzure 客體代理程式及其他 Azure 元件。</span><span class="sxs-lookup"><span data-stu-id="d4651-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="d4651-107">所有的記錄檔 (完整)。</span><span class="sxs-lookup"><span data-stu-id="d4651-107">All Logs (Full).</span></span> <span data-ttu-id="d4651-108">此收集模式將會收集 GA 模式中的所有檔案，外加：</span><span class="sxs-lookup"><span data-stu-id="d4651-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="d4651-109">系統和應用程式事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4651-109">system and application event logs</span></span>
  * <span data-ttu-id="d4651-110">HTTP 錯誤記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4651-110">HTTP error logs</span></span>
  * <span data-ttu-id="d4651-111">IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4651-111">IIS Logs</span></span>
  * <span data-ttu-id="d4651-112">安裝記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4651-112">Setup logs</span></span>
  * <span data-ttu-id="d4651-113">其他系統記錄檔</span><span class="sxs-lookup"><span data-stu-id="d4651-113">other system logs</span></span>

<span data-ttu-id="d4651-114">在這兩個集合模式中，使用下列結構的 hello 的集合可以指定其他資料集合資料夾：</span><span class="sxs-lookup"><span data-stu-id="d4651-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="d4651-115">**名稱**: hello 名稱 hello 集合將用於做為子資料夾內 hello zip 檔案 toobe hello 名稱的收集。</span><span class="sxs-lookup"><span data-stu-id="d4651-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="d4651-116">**位置**: hello 路徑 toohello 資料夾 hello 虛擬機器上的收集檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="d4651-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="d4651-117">**SearchPattern**: hello 模式的檔案 toobe hello 名稱的收集。</span><span class="sxs-lookup"><span data-stu-id="d4651-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="d4651-118">預設值為 "*"</span><span class="sxs-lookup"><span data-stu-id="d4651-118">Default is “*”</span></span>
* <span data-ttu-id="d4651-119">**遞迴**： 如果將會收集的遞迴 hello 資料夾下的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4651-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4651-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4651-120">Prerequisites</span></span>
* <span data-ttu-id="d4651-121">您需要 toohave 儲存體帳戶的延伸模組產生的 toosave zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="d4651-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="d4651-122">您必須確定使用的是 Azure PowerShell Cmdlet V0.8.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d4651-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="d4651-123">如需詳細資訊，請參閱 [Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="d4651-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="d4651-124">加入 hello 擴充功能</span><span class="sxs-lookup"><span data-stu-id="d4651-124">Add hello extension</span></span>
<span data-ttu-id="d4651-125">您可以使用[Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet 或[服務管理 REST Api](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d4651-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="d4651-126">雲端服務的 hello 現有的 Azure Powershell cmdlet， **Set-azureserviceextension**，可以是雲端服務角色執行個體上的使用的 tooenable hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d4651-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="d4651-127">每次透過這個 cmdlet 會啟用這項擴充功能，所選角色的 hello 選取角色執行個體觸發記錄檔集合。</span><span class="sxs-lookup"><span data-stu-id="d4651-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="d4651-128">虛擬機器的 hello 現有的 Azure Powershell cmdlet，**組 AzureVMExtension**，可以是虛擬機器上的使用的 tooenable hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d4651-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="d4651-129">每次透過 hello cmdlet 會啟用此延伸模組，每個執行個體觸發記錄檔集合。</span><span class="sxs-lookup"><span data-stu-id="d4651-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="d4651-130">就內部而言，此延伸模組所使用的 JSON 型 PublicConfiguration hello 和 PrivateConfiguration。</span><span class="sxs-lookup"><span data-stu-id="d4651-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="d4651-131">hello 以下是範例 JSON 公用和私用組態的 hello 版面配置。</span><span class="sxs-lookup"><span data-stu-id="d4651-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="d4651-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4651-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="d4651-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d4651-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="d4651-134">此延伸模組不需要 **privateConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="d4651-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="d4651-135">您可以只提供空的結構 hello **– PrivateConfiguration**引數。</span><span class="sxs-lookup"><span data-stu-id="d4651-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="d4651-136">您可以遵循下列其中一個 hello 兩個步驟 tooadd hello AzureLogCollector tooone 或雲端服務或虛擬機器的觸發程序 hello 上每個 VM toorun 集合和傳送嗨收集檔案 tooAzure 帳戶所選角色的多個執行個體指定。</span><span class="sxs-lookup"><span data-stu-id="d4651-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="d4651-137">新增為服務延伸模組</span><span class="sxs-lookup"><span data-stu-id="d4651-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="d4651-138">請遵循 hello 指示 tooconnect Azure PowerShell tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4651-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="d4651-139">指定 hello 服務名稱、 位置、 角色和角色執行個體 toowhich tooadd 並啟用 hello AzureLogCollector 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="d4651-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="d4651-140">指定要收集檔案的 hello 其他資料資料夾 （這是選擇性步驟）。</span><span class="sxs-lookup"><span data-stu-id="d4651-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="d4651-141">您可以使用語彙基元`%roleroot%`toospecify hello 角色根磁碟機因為它不會使用固定磁碟機。</span><span class="sxs-lookup"><span data-stu-id="d4651-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="d4651-142">提供將上傳 hello Azure 儲存體帳戶名稱和金鑰 toowhich 收集檔案。</span><span class="sxs-lookup"><span data-stu-id="d4651-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="d4651-143">雲端服務，如下所示 tooenable hello AzureLogCollector 延伸模組為呼叫 hello SetAzureServiceLogCollector.ps1 （包含在 hello hello 文章結尾處）。</span><span class="sxs-lookup"><span data-stu-id="d4651-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="d4651-144">Hello 執行完成後，您可以找到下的 hello 上傳檔案`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="d4651-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="d4651-145">hello 下列是 hello 傳遞 toohello 指令碼的 hello 參數定義。</span><span class="sxs-lookup"><span data-stu-id="d4651-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="d4651-146">(也可以從下方加以複製。)</span><span class="sxs-lookup"><span data-stu-id="d4651-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="d4651-147">*ServiceName*：您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="d4651-148">*Roles*：一份角色清單，例如 “WebRole1” 或 ”WorkerRole1”。</span><span class="sxs-lookup"><span data-stu-id="d4651-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="d4651-149">*執行個體*： 逗號分隔清單的 hello 角色執行個體名稱--請使用 hello 萬用字元字串 ("*") 的所有角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="d4651-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="d4651-150">*Slot*：位置名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-150">*Slot*: Slot name.</span></span> <span data-ttu-id="d4651-151">「生產」或「預備」。</span><span class="sxs-lookup"><span data-stu-id="d4651-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="d4651-152">*Mode*：收集模式。</span><span class="sxs-lookup"><span data-stu-id="d4651-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="d4651-153">「完整」或「GA」。</span><span class="sxs-lookup"><span data-stu-id="d4651-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="d4651-154">*StorageAccountName*：用來儲存收集之資料的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="d4651-155">*StorageAccountKey*：Azure 儲存體帳戶金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="d4651-156">*AdditionalDataLocationList*: hello 下列結構的清單：</span><span class="sxs-lookup"><span data-stu-id="d4651-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="d4651-157">新增為 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="d4651-157">Adding as a VM Extension</span></span>
<span data-ttu-id="d4651-158">請遵循 hello 指示 tooconnect Azure PowerShell tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d4651-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="d4651-159">指定 hello 服務名稱、 VM 和 hello 收集模式。</span><span class="sxs-lookup"><span data-stu-id="d4651-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="d4651-160">提供將上傳 hello Azure 儲存體帳戶名稱和金鑰 toowhich 收集檔案。</span><span class="sxs-lookup"><span data-stu-id="d4651-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="d4651-161">雲端服務，如下所示 tooenable hello AzureLogCollector 延伸模組為呼叫 hello SetAzureVMLogCollector.ps1 （包含在 hello hello 文章結尾處）。</span><span class="sxs-lookup"><span data-stu-id="d4651-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="d4651-162">Hello 執行完成後，您可以找到下 https://YouareStorageAccountName.blob.core.windows.net/vmlogs hello 上傳檔案</span><span class="sxs-lookup"><span data-stu-id="d4651-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="d4651-163">hello 下列是 hello 傳遞 toohello 指令碼的 hello 參數定義。</span><span class="sxs-lookup"><span data-stu-id="d4651-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="d4651-164">(也可以從下方加以複製。)</span><span class="sxs-lookup"><span data-stu-id="d4651-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="d4651-165">ServiceName：您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="d4651-166">VMName hello hello VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="d4651-167">Mode：收集模式。</span><span class="sxs-lookup"><span data-stu-id="d4651-167">Mode: Collection mode.</span></span> <span data-ttu-id="d4651-168">「完整」或「GA」。</span><span class="sxs-lookup"><span data-stu-id="d4651-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="d4651-169">StorageAccountName：用來儲存收集之資料的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="d4651-170">StorageAccountKey：Azure 儲存體帳戶金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="d4651-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="d4651-171">AdditionalDataLocationList: Hello 下列結構的清單：</span><span class="sxs-lookup"><span data-stu-id="d4651-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="d4651-172">延伸模組 PowerShell 指令碼檔案</span><span class="sxs-lookup"><span data-stu-id="d4651-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="d4651-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="d4651-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="d4651-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="d4651-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="d4651-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4651-175">Next Steps</span></span>
<span data-ttu-id="d4651-176">現在，您可以從一個非常簡單的位置檢查或複製您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="d4651-176">Now you can examine or copy your logs from one very simple location.</span></span>

