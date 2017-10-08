---
title: "aaaAdding VM 映像 tooAzure 堆疊 |Microsoft 文件"
description: "加入您的組織自訂 Windows 或 Linux VM 映像的租用戶 toouse"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="fe7f6-103">在 Azure Stack 中提供自訂虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="fe7f6-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="fe7f6-104">Azure 的堆疊可讓雲端系統管理員 toomake 自訂虛擬機器映像可用 tootheir 使用者。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-104">Azure Stack enables cloud administrators toomake custom virtual machine images available tootheir users.</span></span> <span data-ttu-id="fe7f6-105">這些映像可以參考 Azure 資源管理員範本，或加入 toothe Azure Marketplace UI hello 建立 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-105">These images can be referenced by Azure Resource Manager templates or added toothe Azure Marketplace UI with hello creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a><span data-ttu-id="fe7f6-106">新增 VM 映像 toomarketplace 使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe7f6-106">Add a VM image toomarketplace with PowerShell</span></span>

<span data-ttu-id="fe7f6-107">執行下列必要條件 hello 從 hello[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 的外部用戶端如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span><span class="sxs-lookup"><span data-stu-id="fe7f6-107">Run hello following prerequisites either from hello [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="fe7f6-108">[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-108">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="fe7f6-109">下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-109">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="fe7f6-110">準備 VHD 格式 (非 VHDX) 的 Windows 或 Linux 作業系統虛擬硬碟映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-110">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="fe7f6-111">針對 Windows 映像，hello 文章[上傳資源管理員部署的 Windows VM 映像 tooAzure](../virtual-machines/windows/upload-generalized-managed.md)包含映像準備指示在 hello**準備 hello VHD 上傳**> 一節。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-111">For Windows images, hello article [Upload a Windows VM image tooAzure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in hello **Prepare hello VHD for upload** section.</span></span>
   * <span data-ttu-id="fe7f6-112">針對 Linux 映像，請遵循 hello 步驟來準備 hello 映像，或使用現有 Azure 堆疊 Linux 映像，如 hello 文章所述[Azure 堆疊上部署的 Linux 虛擬機器](azure-stack-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-112">For Linux images, follow hello steps to prepare hello image or use an existing Azure Stack Linux image as described in hello article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="fe7f6-113">現在，執行下列步驟 tooadd hello 映像 toohello 堆疊 Azure marketplace 的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe7f6-113">Now run hello following steps tooadd hello image toohello Azure Stack marketplace:</span></span>

1. <span data-ttu-id="fe7f6-114">匯入 hello 連接和 ComputeAdmin 模組：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-114">Import hello Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="fe7f6-115">登入 tooyour Azure 堆疊環境。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-115">Sign in tooyour Azure Stack environment.</span></span> <span data-ttu-id="fe7f6-116">如果您的 Azure 堆疊環境部署使用 AAD 或 AD FS （請確定 tooreplace hello AAD 租用戶名稱），取決於指令碼執行的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-116">Run hello following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure tooreplace hello AAD tenant name):</span></span> 

   <span data-ttu-id="fe7f6-117">a.</span><span class="sxs-lookup"><span data-stu-id="fe7f6-117">a.</span></span> <span data-ttu-id="fe7f6-118">**Azure Active Directory**，使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe7f6-118">**Azure Active Directory**, use hello following cmdlet:</span></span>

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="fe7f6-119">b.</span><span class="sxs-lookup"><span data-stu-id="fe7f6-119">b.</span></span> <span data-ttu-id="fe7f6-120">**Active Directory Federation Services**，使用下列 cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="fe7f6-120">**Active Directory Federation Services**, use hello following cmdlet:</span></span>
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. <span data-ttu-id="fe7f6-121">藉由叫用 hello 新增 hello VM 映像`Add-AzsVMImage`cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-121">Add hello VM image by invoking hello `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="fe7f6-122">在 hello 新增 AzsVMImage cmdlet 中，指定 hello osType 為 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-122">In hello Add-AzsVMImage cmdlet, specify hello osType as Windows or Linux.</span></span> <span data-ttu-id="fe7f6-123">包含 hello 發行者、 方案、 SKU 和 hello VM 映像的版本。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-123">Include hello publisher, offer, SKU, and version for hello VM image.</span></span> <span data-ttu-id="fe7f6-124">請參閱 hello[參數](#parameters)hello 允許參數的相關資訊的區段。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-124">See hello [Parameters](#parameters) section for information about hello allowed parameters.</span></span> <span data-ttu-id="fe7f6-125">這些參數會使用 Azure Resource Manager 範本 tooreference hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-125">These parameters are used by Azure Resource Manager templates tooreference hello VM image.</span></span> <span data-ttu-id="fe7f6-126">以下是 hello 指令碼的範例引動過程：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-126">Following is an example invocation of hello script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="fe7f6-127">hello 命令沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-127">hello command does hello following:</span></span>

* <span data-ttu-id="fe7f6-128">驗證 toohello Azure 堆疊環境</span><span class="sxs-lookup"><span data-stu-id="fe7f6-128">Authenticates toohello Azure Stack environment</span></span>
* <span data-ttu-id="fe7f6-129">上傳 hello 新建立的暫存儲存體帳戶本機 VHD tooa</span><span class="sxs-lookup"><span data-stu-id="fe7f6-129">Uploads hello local VHD tooa newly created temporary storage account</span></span>
* <span data-ttu-id="fe7f6-130">新增 hello VM 映像 toohello VM 映像儲存機制和</span><span class="sxs-lookup"><span data-stu-id="fe7f6-130">Adds hello VM image toohello VM image repository and</span></span>
* <span data-ttu-id="fe7f6-131">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="fe7f6-131">Creates a Marketplace item</span></span>

<span data-ttu-id="fe7f6-132">hello 命令執行成功的 tooverify 移 tooMarketplace 在 hello 入口網站，然後確認 hello VM 映像位於 hello**虛擬機器**類別目錄。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-132">tooverify that hello command ran successfully, go tooMarketplace in hello portal, and then verify that hello VM image is available in hello **Virtual Machines** category.</span></span>

![已成功新增 VM 映像](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="fe7f6-134">使用 PowerShell 來移除 VM 映像</span><span class="sxs-lookup"><span data-stu-id="fe7f6-134">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="fe7f6-135">當您不再需要 hello 您先前已上傳的虛擬機器映像時，則您可以使用下列 cmdlet 的 hello hello 商場刪除它：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-135">When you no longer need hello virtual machine image that you have uploaded earlier, you can delete it from hello marketplace by using hello following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="fe7f6-136">參數</span><span class="sxs-lookup"><span data-stu-id="fe7f6-136">Parameters</span></span>

| <span data-ttu-id="fe7f6-137">參數</span><span class="sxs-lookup"><span data-stu-id="fe7f6-137">Parameter</span></span> | <span data-ttu-id="fe7f6-138">說明</span><span class="sxs-lookup"><span data-stu-id="fe7f6-138">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe7f6-139">**publisher**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-139">**publisher**</span></span> |<span data-ttu-id="fe7f6-140">hello 發行者名稱的使用者部署 hello 映像時所使用的 hello VM 映像的區段。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-140">hello publisher name segment of hello VM image that users use when deploying hello image.</span></span> <span data-ttu-id="fe7f6-141">例如 ‘Microsoft’。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-141">An example is ‘Microsoft’.</span></span> <span data-ttu-id="fe7f6-142">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-142">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="fe7f6-143">**offer**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-143">**offer**</span></span> |<span data-ttu-id="fe7f6-144">hello 供應項目名稱 hello 使用者部署 hello VM 映像時所使用的 VM 映像的區段。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-144">hello offer name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="fe7f6-145">例如 ‘WindowsServer’。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-145">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="fe7f6-146">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-146">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="fe7f6-147">**sku**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-147">**sku**</span></span> |<span data-ttu-id="fe7f6-148">hello SKU 名稱 hello 使用者部署 hello VM 映像時所使用的 VM 映像的區段。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-148">hello SKU name segment of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="fe7f6-149">例如 ‘Datacenter2016’。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-149">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="fe7f6-150">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-150">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="fe7f6-151">**version**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-151">**version**</span></span> |<span data-ttu-id="fe7f6-152">hello 版的 hello 使用者部署 hello VM 映像時所使用的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-152">hello version of hello VM Image that users use when deploying hello VM image.</span></span> <span data-ttu-id="fe7f6-153">這一版的 hello 格式 *\#。\#。\#*.</span><span class="sxs-lookup"><span data-stu-id="fe7f6-153">This version is in hello format *\#.\#.\#*.</span></span> <span data-ttu-id="fe7f6-154">例如 ‘1.0.0’。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-154">An example is ‘1.0.0’.</span></span> <span data-ttu-id="fe7f6-155">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-155">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="fe7f6-156">**osType**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-156">**osType**</span></span> |<span data-ttu-id="fe7f6-157">hello osType hello 映像必須是 'Windows' 或 'Linux'。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-157">hello osType of hello image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="fe7f6-158">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-158">**osDiskLocalPath**</span></span> |<span data-ttu-id="fe7f6-159">hello 本機路徑 toohello OS 磁碟的 VM 映像 tooAzure 堆疊為您上傳的 VHD。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-159">hello local path toohello OS disk VHD that you are uploading as a VM image tooAzure Stack.</span></span> |
| <span data-ttu-id="fe7f6-160">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-160">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="fe7f6-161">選擇性的 hello 可以 hello VM 映像的過程中上傳的資料磁碟的本機路徑陣列。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-161">An optional array of hello local paths for data disks that can be uploaded as part of hello VM image.</span></span> |
| <span data-ttu-id="fe7f6-162">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-162">**CreateGalleryItem**</span></span> |<span data-ttu-id="fe7f6-163">布林旗標來判斷是否 toocreate Marketplace 中的項目。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-163">A Boolean flag that determines whether toocreate an item in Marketplace.</span></span> <span data-ttu-id="fe7f6-164">根據預設，此屬性設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-164">By default, it is set tootrue.</span></span> |
| <span data-ttu-id="fe7f6-165">**title**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-165">**title**</span></span> |<span data-ttu-id="fe7f6-166">hello 的顯示名稱 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-166">hello display name of Marketplace item.</span></span> <span data-ttu-id="fe7f6-167">根據預設，此屬性設定 toohello 發行者-優惠-Sku hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-167">By default, it is set toohello Publisher-Offer-Sku of hello VM image.</span></span> |
| <span data-ttu-id="fe7f6-168">**description**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-168">**description**</span></span> |<span data-ttu-id="fe7f6-169">hello 描述 hello Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-169">hello description of hello Marketplace item.</span></span> |
| <span data-ttu-id="fe7f6-170">**位置**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-170">**location**</span></span> |<span data-ttu-id="fe7f6-171">應經過發佈 hello 位置 toowhich hello VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-171">hello location toowhich hello VM image should be published.</span></span> <span data-ttu-id="fe7f6-172">根據預設，這個值會設定 toolocal。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-172">By default, this value is set toolocal.</span></span>|
| <span data-ttu-id="fe7f6-173">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-173">**osDiskBlobURI**</span></span> |<span data-ttu-id="fe7f6-174">此指令碼也可視需要接受 osDisk 的 Blob 儲存體 URI。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-174">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="fe7f6-175">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-175">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="fe7f6-176">（選擇性） 此指令碼也會接受 Blob 儲存體 Uri 的陣列新增資料磁碟 toohello 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-176">Optionally, this script also accepts an array of Blob storage URIs for adding data disks toohello image.</span></span> |

## <a name="add-a-vm-image-through-hello-portal"></a><span data-ttu-id="fe7f6-177">新增 VM 映像透過 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="fe7f6-177">Add a VM image through hello portal</span></span>

> [!NOTE]
> <span data-ttu-id="fe7f6-178">此方法需要個別建立 hello Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-178">This method requires creating hello Marketplace item separately.</span></span>

<span data-ttu-id="fe7f6-179">對映像的其中一個需求就是必須可藉由 Blob 儲存體 URI 參考它們。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-179">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="fe7f6-180">準備 Windows 或 Linux 作業系統映像 VHD 格式 (不 VHDX)，然後再上傳 hello 映像 tooa Azure 或 Azure 堆疊中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-180">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload hello image tooa storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="fe7f6-181">如果您的映像已經上傳的 toohello Azure 或 Azure 堆疊中的 Blob 儲存體，您可以略過步驟 1。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-181">If your image is already uploaded toohello Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="fe7f6-182">[上傳資源管理員部署的 Windows VM 映像 tooAzure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)或 Linux 映像，請遵循 hello 中所述的 hello 指示[Azure 堆疊上部署的 Linux 虛擬機器](azure-stack-linux.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-182">[Upload a Windows VM image tooAzure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow hello instructions described in hello [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="fe7f6-183">您應該了解 hello 您上傳 hello 映像之前，下列考量：</span><span class="sxs-lookup"><span data-stu-id="fe7f6-183">You should understand hello following considerations before you upload hello image:</span></span>

   * <span data-ttu-id="fe7f6-184">因為它會接受較少時間 toopush hello 映像 toohello Azure 堆疊映像儲存機制，很效率 tooupload 映像 tooAzure 堆疊 Blob 儲存體比 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-184">It's more efficient tooupload an image tooAzure Stack Blob storage than tooAzure Blob storage because it takes less time toopush hello image toohello Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="fe7f6-185">上傳 hello 時[Windows VM 映像](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)，請確定 toosubstitute hello**登入 tooAzure**步驟以 hello[設定 hello Azure 堆疊操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)步驟。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-185">When uploading hello [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure toosubstitute hello **Login tooAzure** step with hello [Configure hello Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="fe7f6-186">請記下 hello Blob 儲存體您上傳 hello 映像，也就是在 hello 遵循格式的 URI:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="fe7f6-186">Make a note of hello Blob storage URI where you upload hello image, which is in hello following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="fe7f6-187">toomake hello blob 可匿名存取，請移 toohello 儲存體帳戶 blob 容器其中 hello VM 映像 VHD 上傳太**Blob，** ，然後選取 **存取原則**。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-187">toomake hello blob anonymously accessible, go toohello storage account blob container where hello VM image VHD was uploaded too**Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="fe7f6-188">如果您想，您就可以改為產生 hello 容器的共用的存取簽章，並將它包含在 hello blob URI。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-188">If you want, you can instead generate a shared access signature for hello container and include it as part of hello blob URI.</span></span>

   ![瀏覽 toostorage 帳戶的 blob](./media/azure-stack-add-vm-image/image1.png)

   ![設定 blob 存取 toopublic](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="fe7f6-191">登入 tooAzure 雲端系統管理員身分的堆疊 > hello 功能表中按一下**更多服務** > **資源提供者**> 選取**計算** >  **VM 映像** > **新增**</span><span class="sxs-lookup"><span data-stu-id="fe7f6-191">Sign in tooAzure Stack as a cloud administrator > From hello menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="fe7f6-192">在 hello**新增 VM 映像**刀鋒視窗中，輸入 hello 發行者、 方案、 SKU 和 hello 虛擬機器映像的版本。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-192">On hello **Add a VM Image** blade, enter hello publisher, offer, SKU, and version of hello virtual machine image.</span></span> <span data-ttu-id="fe7f6-193">這些名稱區段，請參閱 toohello 資源管理員範本中的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-193">These name segments refer toohello VM image in Resource Manager templates.</span></span> <span data-ttu-id="fe7f6-194">請確定 tooselect **osType**正確。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-194">Make sure tooselect the **osType** correctly.</span></span> <span data-ttu-id="fe7f6-195">如**OD 磁碟 Blob URI**、 輸入 hello 已在上傳映像的 Blob URI，然後按一下**建立**toobegin 建立 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-195">For **OD Disk Blob URI**, enter hello Blob URI where the image was uploaded and click **Create** toobegin creating the VM Image.</span></span>
   
   ![開始 toocreate hello 映像](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="fe7f6-197">當成功建立 hello 映像時，hello VM 映像的狀態會變更 too'Succeeded'。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-197">When hello image is successfully created, hello VM image status changes too‘Succeeded’.</span></span>

4. <span data-ttu-id="fe7f6-198">toomake hello 虛擬機器映像更輕易地可供使用者使用 hello UI 中，建議您最好太[建立 Marketplace 項目](azure-stack-create-and-publish-marketplace-item.md)。</span><span class="sxs-lookup"><span data-stu-id="fe7f6-198">toomake hello virtual machine image more readily available for user consumption in hello UI, it is best too[create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe7f6-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe7f6-199">Next steps</span></span>

[<span data-ttu-id="fe7f6-200">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe7f6-200">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)