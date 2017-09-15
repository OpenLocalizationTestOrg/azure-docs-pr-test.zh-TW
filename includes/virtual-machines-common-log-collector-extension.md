
<span data-ttu-id="9bde1-101">要診斷 Microsoft Azure 雲端服務的問題，必須在問題發生時收集服務在虛擬機器上的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9bde1-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span></span> <span data-ttu-id="9bde1-102">您可以視需要使用 AzureLogCollector 延伸模組，從一或多個雲端服務 VM (從 Web 角色和背景工作角色) 執行一次性的記錄收集作業，並將收集到的檔案傳輸到 Azure 儲存體帳戶，完全不必遠端登入任何 VM。</span><span class="sxs-lookup"><span data-stu-id="9bde1-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="9bde1-103">大部分的記錄資訊描述位於 http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp。</span><span class="sxs-lookup"><span data-stu-id="9bde1-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="9bde1-104">根據要收集的檔案類型，會有兩種收集模式。</span><span class="sxs-lookup"><span data-stu-id="9bde1-104">There are two modes of collection dependent on the types of files to be collected.</span></span>

* <span data-ttu-id="9bde1-105">僅限 Azure 客體代理程式記錄檔 (GA)。</span><span class="sxs-lookup"><span data-stu-id="9bde1-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="9bde1-106">此收集模式包含所有與 Azure 客體代理程式和其他 Azure 元件相關的記錄。</span><span class="sxs-lookup"><span data-stu-id="9bde1-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span></span>
* <span data-ttu-id="9bde1-107">所有的記錄檔 (完整)。</span><span class="sxs-lookup"><span data-stu-id="9bde1-107">All Logs (Full).</span></span> <span data-ttu-id="9bde1-108">此收集模式將會收集 GA 模式中的所有檔案，外加：</span><span class="sxs-lookup"><span data-stu-id="9bde1-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="9bde1-109">系統和應用程式事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="9bde1-109">system and application event logs</span></span>
  * <span data-ttu-id="9bde1-110">HTTP 錯誤記錄檔</span><span class="sxs-lookup"><span data-stu-id="9bde1-110">HTTP error logs</span></span>
  * <span data-ttu-id="9bde1-111">IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="9bde1-111">IIS Logs</span></span>
  * <span data-ttu-id="9bde1-112">安裝記錄檔</span><span class="sxs-lookup"><span data-stu-id="9bde1-112">Setup logs</span></span>
  * <span data-ttu-id="9bde1-113">其他系統記錄檔</span><span class="sxs-lookup"><span data-stu-id="9bde1-113">other system logs</span></span>

<span data-ttu-id="9bde1-114">在這兩種收集模式中，都可以使用下列結構的集合來指定其他資料收集資料夾：</span><span class="sxs-lookup"><span data-stu-id="9bde1-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span></span>

* <span data-ttu-id="9bde1-115">**名稱**：集合的名稱，將做為要收集之 zip 檔案內的子資料夾名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span></span>
* <span data-ttu-id="9bde1-116">**位置**：將要收集檔案的資料夾在虛擬機器上的路徑。</span><span class="sxs-lookup"><span data-stu-id="9bde1-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span></span>
* <span data-ttu-id="9bde1-117">**SearchPattern**：要收集之檔案的名稱模式。</span><span class="sxs-lookup"><span data-stu-id="9bde1-117">**SearchPattern**: The pattern of the names of files to be collected.</span></span> <span data-ttu-id="9bde1-118">預設值為 "*"</span><span class="sxs-lookup"><span data-stu-id="9bde1-118">Default is “*”</span></span>
* <span data-ttu-id="9bde1-119">**遞迴**：如果要以遞迴方式收集資料夾下的檔案。</span><span class="sxs-lookup"><span data-stu-id="9bde1-119">**Recursive**: if the files will be collected recursively under the folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bde1-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="9bde1-120">Prerequisites</span></span>
* <span data-ttu-id="9bde1-121">您必須有儲存體帳戶可進行擴充，以儲存產生的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="9bde1-121">You need to have a storage account for extension to save generated zip files.</span></span>
* <span data-ttu-id="9bde1-122">您必須確定使用的是 Azure PowerShell Cmdlet V0.8.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9bde1-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="9bde1-123">如需詳細資訊，請參閱 [Azure 下載](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="9bde1-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-the-extension"></a><span data-ttu-id="9bde1-124">新增延伸模組</span><span class="sxs-lookup"><span data-stu-id="9bde1-124">Add the extension</span></span>
<span data-ttu-id="9bde1-125">您可以使用 [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) Cmdlet 或[服務管理 REST API](https://msdn.microsoft.com/library/ee460799.aspx)，來新增 AzureLogCollector 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9bde1-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span></span>

<span data-ttu-id="9bde1-126">對於雲端服務，可以使用現有的 Azure Powershell Cmdlet **Set-AzureServiceExtension**來啟用雲端服務角色執行個體上的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9bde1-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span></span> <span data-ttu-id="9bde1-127">每次透過此 Cmdlet 啟用此延伸模組時，都會在所選角色的選定角色執行個體上觸發記錄檔收集。</span><span class="sxs-lookup"><span data-stu-id="9bde1-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span></span>

<span data-ttu-id="9bde1-128">對於虛擬機器，可以使用現有的 Azure Powershell Cmdlet **Set-AzureVMExtension**來啟用虛擬機器上的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9bde1-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span></span> <span data-ttu-id="9bde1-129">每次透過這些 Cmdlet 啟用此延伸模組時，都會在每個執行個體上觸發記錄檔收集。</span><span class="sxs-lookup"><span data-stu-id="9bde1-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="9bde1-130">就內部而言，此延伸模組會使用以 JSON 為基礎的 PublicConfiguration 和 PrivateConfiguration。</span><span class="sxs-lookup"><span data-stu-id="9bde1-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="9bde1-131">以下是公用和私人組態的範例 JSON 配置。</span><span class="sxs-lookup"><span data-stu-id="9bde1-131">The following is the layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="9bde1-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="9bde1-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri to your storage account with sp=wl",
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

### <a name="privateconfiguration"></a><span data-ttu-id="9bde1-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9bde1-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="9bde1-134">此延伸模組不需要 **privateConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="9bde1-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="9bde1-135">您可以只提供 **–PrivateConfiguration** 引數的空結構。</span><span class="sxs-lookup"><span data-stu-id="9bde1-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="9bde1-136">您可以依照下列兩個步驟之一，將 AzureLogCollector 新增至所選角色的一或多個雲端服務或虛擬機器執行個體，這會在每個 VM 上觸發收集的執行，並將收集到的檔案傳送至指定的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bde1-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="9bde1-137">新增為服務延伸模組</span><span class="sxs-lookup"><span data-stu-id="9bde1-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="9bde1-138">依照指示將 Azure PowerShell 連接到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bde1-138">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>
2. <span data-ttu-id="9bde1-139">指定要新增並啟用 AzureLogCollector 延伸模組的服務名稱、位置、角色和角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="9bde1-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify the slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified the roles on which the extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify the instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="9bde1-140">指定收集檔案的其他資料夾 (此步驟是選擇性的)。</span><span class="sxs-lookup"><span data-stu-id="9bde1-140">Specify the additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="9bde1-141">您可以使用權杖 `%roleroot%` 來指定角色的根磁碟機，因為它不會使用固定磁碟機。</span><span class="sxs-lookup"><span data-stu-id="9bde1-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="9bde1-142">提供收集到的檔案要上傳到的 Azure 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="9bde1-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="9bde1-143">依照下列方式呼叫 SetAzureServiceLogCollector.ps1 (包含在本文結尾處)，以啟用雲端服務的 AzureLogCollector 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9bde1-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="9bde1-144">執行完成後，您可以在 `https://YouareStorageAccountName.blob.core.windows.net/vmlogs` 找到上傳的檔案</span><span class="sxs-lookup"><span data-stu-id="9bde1-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="9bde1-145">以下是傳遞至指令碼之參數的定義。</span><span class="sxs-lookup"><span data-stu-id="9bde1-145">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="9bde1-146">(也可以從下方加以複製。)</span><span class="sxs-lookup"><span data-stu-id="9bde1-146">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="9bde1-147">*ServiceName*：您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="9bde1-148">*Roles*：一份角色清單，例如 “WebRole1” 或 ”WorkerRole1”。</span><span class="sxs-lookup"><span data-stu-id="9bde1-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="9bde1-149">*Instances*：一份以逗號分隔的角色執行個體名稱 -- 所有角色執行個體皆使用萬用字元字串 ("*")。</span><span class="sxs-lookup"><span data-stu-id="9bde1-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="9bde1-150">*Slot*：位置名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-150">*Slot*: Slot name.</span></span> <span data-ttu-id="9bde1-151">「生產」或「預備」。</span><span class="sxs-lookup"><span data-stu-id="9bde1-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="9bde1-152">*Mode*：收集模式。</span><span class="sxs-lookup"><span data-stu-id="9bde1-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="9bde1-153">「完整」或「GA」。</span><span class="sxs-lookup"><span data-stu-id="9bde1-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="9bde1-154">*StorageAccountName*：用來儲存收集之資料的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="9bde1-155">*StorageAccountKey*：Azure 儲存體帳戶金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="9bde1-156">*AdditionalDataLocationList*：下列結構的清單：</span><span class="sxs-lookup"><span data-stu-id="9bde1-156">*AdditionalDataLocationList*: A list of the following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="9bde1-157">新增為 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="9bde1-157">Adding as a VM Extension</span></span>
<span data-ttu-id="9bde1-158">依照指示將 Azure PowerShell 連接到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bde1-158">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>

1. <span data-ttu-id="9bde1-159">指定服務名稱、VM 和收集模式。</span><span class="sxs-lookup"><span data-stu-id="9bde1-159">Specify the service name, VM, and the collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify the VM name
        $VMName = "'YourVMName'"
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify the additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="9bde1-160">提供收集到的檔案要上傳到的 Azure 儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="9bde1-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="9bde1-161">依照下列方式呼叫 SetAzureVMLogCollector.ps1 (包含在本文結尾處)，以啟用雲端服務的 AzureLogCollector 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="9bde1-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="9bde1-162">一旦完成執行，您可以在 https://YouareStorageAccountName.blob.core.windows.net/vmlogs 底下找到上傳的檔案</span><span class="sxs-lookup"><span data-stu-id="9bde1-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="9bde1-163">以下是傳遞至指令碼之參數的定義。</span><span class="sxs-lookup"><span data-stu-id="9bde1-163">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="9bde1-164">(也可以從下方加以複製。)</span><span class="sxs-lookup"><span data-stu-id="9bde1-164">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="9bde1-165">ServiceName：您的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="9bde1-166">VMName：VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-166">VMName The name of the VM.</span></span>
* <span data-ttu-id="9bde1-167">Mode：收集模式。</span><span class="sxs-lookup"><span data-stu-id="9bde1-167">Mode: Collection mode.</span></span> <span data-ttu-id="9bde1-168">「完整」或「GA」。</span><span class="sxs-lookup"><span data-stu-id="9bde1-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="9bde1-169">StorageAccountName：用來儲存收集之資料的 Azure 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="9bde1-170">StorageAccountKey：Azure 儲存體帳戶金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="9bde1-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="9bde1-171">AdditionalDataLocationList：下列結構的清單：</span><span class="sxs-lookup"><span data-stu-id="9bde1-171">AdditionalDataLocationList: A list of the following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="9bde1-172">延伸模組 PowerShell 指令碼檔案</span><span class="sxs-lookup"><span data-stu-id="9bde1-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="9bde1-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="9bde1-173">SetAzureServiceLogCollector.ps1</span></span>

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
    else  #For all instances if not specified.  The value should be a space or *
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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
    #This is an optional step: generate a sasUri to the container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "The container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="9bde1-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="9bde1-174">SetAzureVMLogCollector.ps1</span></span>

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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
                #We will check the VM status to find if operation by extension has been completed or not. The completion of the operation,either succeed or fail, can be indicated by
                #the presence of SubstatusList field.
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
                              Write-Output "Waiting for operation to complete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access to the file, we can generate a read-only SasUri directly to the file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "The uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove the extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, the extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, the extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="9bde1-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bde1-175">Next Steps</span></span>
<span data-ttu-id="9bde1-176">現在，您可以從一個非常簡單的位置檢查或複製您的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="9bde1-176">Now you can examine or copy your logs from one very simple location.</span></span>

