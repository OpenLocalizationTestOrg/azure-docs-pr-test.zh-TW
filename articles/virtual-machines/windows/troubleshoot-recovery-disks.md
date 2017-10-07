---
title: "Windows 疑難排解 VM 使用 Azure PowerShell aaaUse |Microsoft 文件"
description: "了解如何 tootroubleshoot Windows VM 在 Azure 中藉由來發出連接 hello OS 磁碟 tooa 復原 VM 使用 Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="32f67-103">疑難排解 Windows VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="32f67-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="32f67-104">如果 Windows 虛擬機器 (VM) 在 Azure 中會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。</span><span class="sxs-lookup"><span data-stu-id="32f67-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="32f67-105">常見範例是防止 hello VM 可以 tooboot 成功失敗的應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="32f67-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="32f67-106">此發行項詳細資料時，如何 toouse Azure PowerShell tooconnect 您的虛擬硬碟 tooanother Windows VM toofix 任何錯誤，然後重新建立原始 VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="32f67-107">復原程序概觀</span><span class="sxs-lookup"><span data-stu-id="32f67-107">Recovery process overview</span></span>
<span data-ttu-id="32f67-108">hello 疑難排解程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="32f67-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="32f67-109">刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="32f67-110">附加和掛接 hello Windows VM 的虛擬硬碟 tooanother 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="32f67-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="32f67-111">連接 toohello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="32f67-112">編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。</span><span class="sxs-lookup"><span data-stu-id="32f67-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="32f67-113">取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="32f67-114">使用建立 VM hello 原始虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="32f67-115">請確定您有[hello 最新 Azure PowerShell](/powershell/azure/overview)安裝並登入 tooyour 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="32f67-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="32f67-116">在 hello 下列範例中，會取代您自己的值的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="32f67-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="32f67-117">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="32f67-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="32f67-118">判斷開機問題</span><span class="sxs-lookup"><span data-stu-id="32f67-118">Determine boot issues</span></span>
<span data-ttu-id="32f67-119">您可以在 Azure 中檢視您的 VM 的螢幕擷取畫面 toohelp 開機問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="32f67-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="32f67-120">這個螢幕擷取畫面可以協助您找出 VM 失敗 tooboot 的原因。</span><span class="sxs-lookup"><span data-stu-id="32f67-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="32f67-121">hello 下列範例會取得 hello 螢幕擷取畫面來自 hello 名為 Windows VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="32f67-122">檢閱 hello 螢幕擷取畫面 toodetermine hello VM 失敗 tooboot 的原因。</span><span class="sxs-lookup"><span data-stu-id="32f67-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="32f67-123">請注意任何特定的錯誤訊息或提供的錯誤代碼。</span><span class="sxs-lookup"><span data-stu-id="32f67-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="32f67-124">檢視現有的虛擬硬碟詳細資料</span><span class="sxs-lookup"><span data-stu-id="32f67-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="32f67-125">您可以將附加您的虛擬硬碟 tooanother VM 之前，您會需要 tooidentify hello hello 虛擬硬碟 (VHD) 名稱。</span><span class="sxs-lookup"><span data-stu-id="32f67-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="32f67-126">hello 下列範例會取得名為 VM hello 資訊`myVM`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="32f67-127">尋找`Vhd URI`內 hello `StorageProfile` hello 輸出中的 hello 上述命令 > 一節。</span><span class="sxs-lookup"><span data-stu-id="32f67-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="32f67-128">hello 下列截斷的範例輸出顯示 hello`Vhd URI`朝向 hello hello 程式碼區塊的結尾：</span><span class="sxs-lookup"><span data-stu-id="32f67-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="32f67-129">刪除現有的 VM</span><span class="sxs-lookup"><span data-stu-id="32f67-129">Delete existing VM</span></span>
<span data-ttu-id="32f67-130">虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。</span><span class="sxs-lookup"><span data-stu-id="32f67-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="32f67-131">虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。</span><span class="sxs-lookup"><span data-stu-id="32f67-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="32f67-132">hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。</span><span class="sxs-lookup"><span data-stu-id="32f67-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="32f67-133">每個虛擬硬碟已連接時，指派租用 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="32f67-134">雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="32f67-135">hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。</span><span class="sxs-lookup"><span data-stu-id="32f67-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="32f67-136">hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。</span><span class="sxs-lookup"><span data-stu-id="32f67-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="32f67-137">刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="32f67-138">刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="32f67-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="32f67-139">下列範例刪除 hello hello 名為 VM`myVM`從名為 hello 資源群組`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="32f67-140">請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="32f67-141">hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。</span><span class="sxs-lookup"><span data-stu-id="32f67-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="32f67-142">附加現有的虛擬硬碟 tooanother VM</span><span class="sxs-lookup"><span data-stu-id="32f67-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="32f67-143">如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="32f67-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="32f67-144">附加 hello 疑難排解 VM toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。</span><span class="sxs-lookup"><span data-stu-id="32f67-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="32f67-145">此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。</span><span class="sxs-lookup"><span data-stu-id="32f67-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="32f67-146">選擇或建立另一個 VM toouse 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="32f67-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="32f67-147">當您附加 hello 現有虛擬硬碟時，指定在 hello 上述中取得的 hello URL toohello 磁碟`Get-AzureRmVM`命令。</span><span class="sxs-lookup"><span data-stu-id="32f67-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="32f67-148">hello 下列範例會附加疑難排解名為 VM 的現有虛擬硬碟 toohello `myVMRecovery` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="32f67-149">新增磁碟需要 toospecify hello hello 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="32f67-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="32f67-150">因為我們連接現有的磁碟，hello`-DiskSizeInGB`指定為`$null`。</span><span class="sxs-lookup"><span data-stu-id="32f67-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="32f67-151">此值可確保正確連接 hello 資料磁碟，而且沒有 hello 需要 toodetermine hello 資料磁碟大小，則為 true。</span><span class="sxs-lookup"><span data-stu-id="32f67-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="32f67-152">掛接 hello 連接的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="32f67-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="32f67-153">RDP tooyour 疑難排解 VM 使用 hello 適當的認證。</span><span class="sxs-lookup"><span data-stu-id="32f67-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="32f67-154">hello 下列範例會下載 hello hello 名為 VM 的 RDP 連線檔案`myVMRecovery`hello 資源群組中名為`myResourceGroup`，並將它下載太`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="32f67-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="32f67-155">自動偵測並附加 hello 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="32f67-156">檢視連接的磁碟區 toodetermine hello 的磁碟機代號 hello 清單如下所示：</span><span class="sxs-lookup"><span data-stu-id="32f67-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="32f67-157">下列範例輸出的 hello 可讓您顯示 hello 虛擬硬碟連接磁碟**2**。</span><span class="sxs-lookup"><span data-stu-id="32f67-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="32f67-158">(您也可以使用`Get-Volume`tooview hello 磁碟機代號):</span><span class="sxs-lookup"><span data-stu-id="32f67-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="32f67-159">修正原始虛擬硬碟的問題</span><span class="sxs-lookup"><span data-stu-id="32f67-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="32f67-160">與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。</span><span class="sxs-lookup"><span data-stu-id="32f67-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="32f67-161">一旦解決 hello 問題之後，繼續進行步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="32f67-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="32f67-162">卸載並中斷連結原始虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="32f67-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="32f67-163">一旦解決的錯誤，您會卸載，並中斷您疑難排解的 VM 中的 hello 現有虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="32f67-164">您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。</span><span class="sxs-lookup"><span data-stu-id="32f67-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="32f67-165">從您的 RDP 工作階段內卸載 hello 資料磁碟上您將復原 VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="32f67-166">您需要從 hello hello 磁碟編號先前`Get-Disk`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="32f67-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="32f67-167">然後，使用`Set-Disk`tooset hello 磁碟為離線狀態：</span><span class="sxs-lookup"><span data-stu-id="32f67-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="32f67-168">確認 hello 磁碟現在已設定為離線使用`Get-Disk`一次。</span><span class="sxs-lookup"><span data-stu-id="32f67-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="32f67-169">hello 下列範例輸出顯示 hello 磁碟現在已設定為離線：</span><span class="sxs-lookup"><span data-stu-id="32f67-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="32f67-170">結束您的 RDP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="32f67-170">Exit your RDP session.</span></span> <span data-ttu-id="32f67-171">從您的 Azure PowerShell 工作階段移除 hello 疑難排解 VM 中的 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="32f67-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="32f67-172">從原始硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="32f67-172">Create VM from original hard disk</span></span>
<span data-ttu-id="32f67-173">toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="32f67-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="32f67-174">hello 實際的 JSON 範本位於 hello 下列連結：</span><span class="sxs-lookup"><span data-stu-id="32f67-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="32f67-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="32f67-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="32f67-176">hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。</span><span class="sxs-lookup"><span data-stu-id="32f67-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="32f67-177">hello 下列範例會將部署 hello 範本 toohello 資源群組名稱`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="32f67-178">回應 hello 提示 hello 範本，例如 VM 名稱、 OS 類型與 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="32f67-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="32f67-179">hello `osDiskVhdUri` hello 如先前附加時會使用 hello 疑難排解 VM 現有虛擬硬碟 toohello 相同。</span><span class="sxs-lookup"><span data-stu-id="32f67-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="32f67-180">重新啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="32f67-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="32f67-181">當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="32f67-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="32f67-182">hello 下列範例會啟用 hello hello 名為 VM 上的診斷延伸模組`myVMDeployed`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="32f67-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="32f67-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32f67-183">Next steps</span></span>
<span data-ttu-id="32f67-184">如果您有連接 tooyour VM 的問題，請參閱[疑難排解 RDP 連線 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32f67-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="32f67-185">如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Windows VM 上的應用程式連線問題進行疑難排解](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32f67-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="32f67-186">如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32f67-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
