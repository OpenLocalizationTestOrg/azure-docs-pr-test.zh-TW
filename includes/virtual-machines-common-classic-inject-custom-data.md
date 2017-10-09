


<span data-ttu-id="0525f-101">本主題將說明如何：</span><span class="sxs-lookup"><span data-stu-id="0525f-101">This topic describes how to:</span></span>

* <span data-ttu-id="0525f-102">將資料插入正在佈建的 Azure 虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="0525f-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="0525f-103">針對 Windows 和 Linux 進行擷取。</span><span class="sxs-lookup"><span data-stu-id="0525f-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="0525f-104">使用某些系統 toodetect 上可用的特殊工具和自訂資料會自動處理。</span><span class="sxs-lookup"><span data-stu-id="0525f-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="0525f-105">本文說明如何自訂資料可插入所使用的 hello Azure 服務管理 API 以建立 VM。</span><span class="sxs-lookup"><span data-stu-id="0525f-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="0525f-106">如何 toouse hello Azure 資源管理 API，請參閱的 toosee [hello 範例範本](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata)。</span><span class="sxs-lookup"><span data-stu-id="0525f-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="0525f-107">將自訂資料插入 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0525f-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="0525f-108">這項功能目前只支援 hello [Azure 命令列介面](https://github.com/Azure/azure-xplat-cli)。</span><span class="sxs-lookup"><span data-stu-id="0525f-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="0525f-109">我們在這裡建立`custom-data.txt`檔案，其中包含我們的資料，然後插入，在 toohello VM 佈建期間。</span><span class="sxs-lookup"><span data-stu-id="0525f-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="0525f-110">雖然您可以使用任何 hello 選項 hello`azure vm create`命令 hello 以下示範非常基本的其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="0525f-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="0525f-111">在 hello 虛擬機器中使用自訂資料</span><span class="sxs-lookup"><span data-stu-id="0525f-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="0525f-112">如果您的 Azure VM 都是 windows VM，則 hello 自訂的資料檔會儲存太`%SYSTEMDRIVE%\AzureData\CustomData.bin`。</span><span class="sxs-lookup"><span data-stu-id="0525f-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="0525f-113">雖然它是 base64 編碼 tootransfer hello 本機電腦 toohello 從新的 VM，它會自動解碼，可開啟或立即使用。</span><span class="sxs-lookup"><span data-stu-id="0525f-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="0525f-114">如果 hello 檔案存在，則會覆寫。</span><span class="sxs-lookup"><span data-stu-id="0525f-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="0525f-115">hello hello 目錄安全性設定得**System： 完全控制**和**Administrators： 完全控制**。</span><span class="sxs-lookup"><span data-stu-id="0525f-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="0525f-116">如果 Azure VM 都是 linux VM，然後 hello 自訂資料檔案將位於 hello 下列其中一種將視您 distro 而定。</span><span class="sxs-lookup"><span data-stu-id="0525f-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="0525f-117">hello 資料可能會以 base64 編碼，因此您可能需要 toodecode hello 資料第一次：</span><span class="sxs-lookup"><span data-stu-id="0525f-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="0525f-118">Azure 上的 Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="0525f-118">Cloud-init on Azure</span></span>
<span data-ttu-id="0525f-119">如果您的 Azure VM 從 Ubuntu 或 CoreOS 映像，您可以使用 CustomData toosend 雲端組態 toocloud init。</span><span class="sxs-lookup"><span data-stu-id="0525f-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="0525f-120">或者，如果您的自訂資料檔案是指令碼，則 cloud-init 只能執行它。</span><span class="sxs-lookup"><span data-stu-id="0525f-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="0525f-121">Ubuntu 雲端映像</span><span class="sxs-lookup"><span data-stu-id="0525f-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="0525f-122">在大部分的 Azure Linux 映像，您會編輯 「 / etc/waagent.conf"tooconfigure hello 暫存資源的磁碟和交換檔。</span><span class="sxs-lookup"><span data-stu-id="0525f-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="0525f-123">如需詳細資訊，請參閱[Azure Linux 代理程式使用者指南](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0525f-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="0525f-124">不過，hello Ubuntu 雲端映像，您必須使用雲端 init tooconfigure hello 資源磁碟 （也就是 hello 「 暫時 」 磁碟），並切換資料分割。</span><span class="sxs-lookup"><span data-stu-id="0525f-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="0525f-125">請參閱 hello 遵循頁面上 hello Ubuntu wiki，如需詳細資訊： [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)。</span><span class="sxs-lookup"><span data-stu-id="0525f-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="0525f-126">後續步驟：使用 cloud-init</span><span class="sxs-lookup"><span data-stu-id="0525f-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="0525f-127">如需詳細資訊，請參閱 hello [Ubuntu 雲端初始化文件](https://help.ubuntu.com/community/CloudInit)。</span><span class="sxs-lookup"><span data-stu-id="0525f-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="0525f-128">加入角色服務管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="0525f-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="0525f-129">Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="0525f-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

