## <a name="overview"></a><span data-ttu-id="32313-101">概觀</span><span class="sxs-lookup"><span data-stu-id="32313-101">Overview</span></span>
<span data-ttu-id="32313-102">當您建立新的虛擬機器 (VM) 的資源群組中的部署映像從[Azure Marketplace](https://azure.microsoft.com/marketplace/)，hello 預設作業系統磁碟機是 127 GB。</span><span class="sxs-lookup"><span data-stu-id="32313-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="32313-103">即使它可能 tooadd 資料磁碟 toohello VM （hello SKU 多少根據您選擇），此外建議的 tooinstall 應用程式和在這些增補磁碟上的 CPU 密集型工作負載會有時候客戶必須 tooexpand hello OS磁碟機 toosupport 特定案例，例如下列：</span><span class="sxs-lookup"><span data-stu-id="32313-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="32313-104">支援將元件安裝在作業系統磁碟機上的舊型應用程式。</span><span class="sxs-lookup"><span data-stu-id="32313-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="32313-105">從具有較大作業系統磁碟機的內部部署移轉實體電腦或虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="32313-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32313-106">Azure 建立和處理資源的部署模型有二種：資源管理員和傳統。</span><span class="sxs-lookup"><span data-stu-id="32313-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="32313-107">本文件涵蓋使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="32313-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="32313-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="32313-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="32313-109">調整 hello 作業系統磁碟機</span><span class="sxs-lookup"><span data-stu-id="32313-109">Resize hello OS drive</span></span>
<span data-ttu-id="32313-110">本文章中我們將完成的調整大小 hello 作業系統磁碟機使用的資源管理員模組 hello 工作[Azure Powershell](/powershell/azureps-cmdlets-docs)。</span><span class="sxs-lookup"><span data-stu-id="32313-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="32313-111">在系統管理模式中開啟您的 Powershell ISE 或 Powershell 視窗，並依照下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="32313-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="32313-112">登入 tooyour Microsoft Azure 帳戶中資源管理模式，並選取您的訂用帳戶，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="32313-113">設定資源群組名稱和 VM 名稱，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="32313-114">取得參考 tooyour VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="32313-115">停止 hello VM，然後再調整 hello 磁碟大小，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="32313-116">與以下是我們所期待的 hello 目前 ！</span><span class="sxs-lookup"><span data-stu-id="32313-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="32313-117">設定 hello hello OS 磁碟 toohello 預期值的大小及更新 hello VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="32313-118">hello 新大小應該大於 hello 現有的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="32313-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="32313-119">hello 允許最大值為 1023 GB。</span><span class="sxs-lookup"><span data-stu-id="32313-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="32313-120">更新 hello VM 可能需要幾秒鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="32313-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="32313-121">一旦 hello 命令完成執行後，重新啟動 hello VM，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="32313-122">這樣就大功告成了！</span><span class="sxs-lookup"><span data-stu-id="32313-122">And that’s it!</span></span> <span data-ttu-id="32313-123">現在 RDP 到 hello VM，開啟 電腦管理 （或磁碟管理），並展開 hello 磁碟機使用 hello 新配置的空間。</span><span class="sxs-lookup"><span data-stu-id="32313-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="32313-124">摘要</span><span class="sxs-lookup"><span data-stu-id="32313-124">Summary</span></span>
<span data-ttu-id="32313-125">在本文中，我們會使用 Azure 資源管理員的 Powershell tooexpand hello IaaS 虛擬機器的作業系統磁碟機的模組。</span><span class="sxs-lookup"><span data-stu-id="32313-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="32313-126">重現下面是供您參考 hello 完整的指令碼：</span><span class="sxs-lookup"><span data-stu-id="32313-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="32313-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32313-127">Next Steps</span></span>
<span data-ttu-id="32313-128">在本文中，我們會著重於擴充的 hello VM hello OS 磁碟，但 hello 開發的指令碼也可用擴充 hello 資料磁碟附加的 toohello VM，藉由變更一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="32313-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="32313-129">例如，tooexpand hello 第一個資料磁碟附加的 toohello VM，取代 hello```OSDisk```物件```StorageProfile```與```DataDisks```陣列並使用數值索引 tooobtain 參考 toofirst 附加的資料磁碟，如下所示：</span><span class="sxs-lookup"><span data-stu-id="32313-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="32313-130">同樣地，您便可以參考其他資料磁碟附加的 toohello VM，如上所示，使用索引上，或者 hello ```Name``` hello 磁碟，如下所示的屬性：</span><span class="sxs-lookup"><span data-stu-id="32313-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="32313-131">如果您想 toofind 出 tooattach 磁碟 tooan Azure 資源管理員 VM 的方式，請檢查這[文章](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32313-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

