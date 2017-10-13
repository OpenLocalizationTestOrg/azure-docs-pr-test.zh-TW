---
title: "將 VM 映像新增到 Azure Stack | Microsoft Docs"
description: "新增您組織的自訂 Windows 或 Linux VM 映像以供租用戶使用"
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
ms.date: 09/25/2017
ms.author: sngun
ms.openlocfilehash: de8540397b63093457382cf427a65ea0e48b93e0
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a><span data-ttu-id="f89f5-103">在 Azure Stack 中提供自訂虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="f89f5-103">Make a custom virtual machine image available in Azure Stack</span></span>

<span data-ttu-id="f89f5-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="f89f5-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="f89f5-105">Azure Stack 可讓操作員將自訂虛擬機器映像提供給其使用者使用。</span><span class="sxs-lookup"><span data-stu-id="f89f5-105">Azure Stack enables operators to make custom virtual machine images available to their users.</span></span> <span data-ttu-id="f89f5-106">這些映像可供 Azure Resource Manager 範本參考，或藉由建立 Marketplace 項目新增到 Azure Marketplace UI。</span><span class="sxs-lookup"><span data-stu-id="f89f5-106">These images can be referenced by Azure Resource Manager templates or added to the Azure Marketplace UI with the creation of a Marketplace item.</span></span> 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a><span data-ttu-id="f89f5-107">使用 PowerShell 將 VM 映像新增到市集</span><span class="sxs-lookup"><span data-stu-id="f89f5-107">Add a VM image to marketplace with PowerShell</span></span>

<span data-ttu-id="f89f5-108">從[開發套件](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop)，或從 Windows 型外部用戶端 (如果您是[透過 VPN 連線](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn))，執行下列先決條件</span><span class="sxs-lookup"><span data-stu-id="f89f5-108">Run the following prerequisites either from the [development kit](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), or from a Windows-based external client if you are [connected through VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)</span></span>

* <span data-ttu-id="f89f5-109">[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="f89f5-109">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>  

* <span data-ttu-id="f89f5-110">下載[與 Azure Stack 搭配運作所需的工具](azure-stack-powershell-download.md)。</span><span class="sxs-lookup"><span data-stu-id="f89f5-110">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span>  

* <span data-ttu-id="f89f5-111">準備 VHD 格式 (非 VHDX) 的 Windows 或 Linux 作業系統虛擬硬碟映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-111">Prepare a Windows or Linux operating system virtual hard disk image in VHD format (not VHDX).</span></span>
   
   * <span data-ttu-id="f89f5-112">針對 Windows 映像，[將 Windows VM 映像上傳至 Azure 供 Resource Manager 部署使用](../virtual-machines/windows/upload-generalized-managed.md)一文的**準備 VHD 以供上傳**一節中包含了映像準備指示。</span><span class="sxs-lookup"><span data-stu-id="f89f5-112">For Windows images, the article [Upload a Windows VM image to Azure for Resource Manager deployments](../virtual-machines/windows/upload-generalized-managed.md) contains image preparation instructions in the **Prepare the VHD for upload** section.</span></span>
   * <span data-ttu-id="f89f5-113">針對 Linux 映像，請依照[在 Azure Stack 上部署 Linux 虛擬機器](azure-stack-linux.md)一文所述的步驟，準備映像或使用現有的 Azure Stack Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-113">For Linux images, follow the steps to prepare the image or use an existing Azure Stack Linux image as described in the article [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md).</span></span>  

<span data-ttu-id="f89f5-114">現在，執行下列步驟以將映像新增到 Azure Stack 市集：</span><span class="sxs-lookup"><span data-stu-id="f89f5-114">Now run the following steps to add the image to the Azure Stack marketplace:</span></span>

1. <span data-ttu-id="f89f5-115">匯入 Connect 和 ComputeAdmin 模組：</span><span class="sxs-lookup"><span data-stu-id="f89f5-115">Import the Connect and ComputeAdmin modules:</span></span>
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. <span data-ttu-id="f89f5-116">登入您的 Azure Stack 環境。</span><span class="sxs-lookup"><span data-stu-id="f89f5-116">Sign in to your Azure Stack environment.</span></span> <span data-ttu-id="f89f5-117">根據您的 Azure Stack 環境是使用 AAD 還是 AD FS 部署而定，執行下列指令碼 (務必按照您的環境設定來取代 AAD tenantName、GraphAudience 端點和 ArmEndpoint 值)：</span><span class="sxs-lookup"><span data-stu-id="f89f5-117">Run the following script depending on if your Azure Stack environment is deployed by using AAD or AD FS (Make sure to replace the AAD tenantName, GraphAudience endpoint and ArmEndpoint values as per your environment configuration):</span></span> 

   <span data-ttu-id="f89f5-118">a.</span><span class="sxs-lookup"><span data-stu-id="f89f5-118">a.</span></span> <span data-ttu-id="f89f5-119">**Azure Active Directory** - 使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="f89f5-119">**Azure Active Directory**, use the following cmdlet:</span></span>

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   #Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   <span data-ttu-id="f89f5-120">b.</span><span class="sxs-lookup"><span data-stu-id="f89f5-120">b.</span></span> <span data-ttu-id="f89f5-121">**Active Directory 同盟服務** - 使用下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="f89f5-121">**Active Directory Federation Services**, use the following cmdlet:</span></span>
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. <span data-ttu-id="f89f5-122">叫用 `Add-AzsVMImage` Cmdlet 來新增 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-122">Add the VM image by invoking the `Add-AzsVMImage` cmdlet.</span></span> <span data-ttu-id="f89f5-123">在 Add-AzsVMImage Cmdlet 中，將 osType 指定為 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="f89f5-123">In the Add-AzsVMImage cmdlet, specify the osType as Windows or Linux.</span></span> <span data-ttu-id="f89f5-124">請包含 VM 映像的發行者、供應項目、SKU 及版本。</span><span class="sxs-lookup"><span data-stu-id="f89f5-124">Include the publisher, offer, SKU, and version for the VM image.</span></span> <span data-ttu-id="f89f5-125">如需有關所允許參數的資訊，請參閱[參數](#parameters)一節。</span><span class="sxs-lookup"><span data-stu-id="f89f5-125">See the [Parameters](#parameters) section for information about the allowed parameters.</span></span> <span data-ttu-id="f89f5-126">Azure Resource Manager 範本會使用這些參數來參考 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-126">These parameters are used by Azure Resource Manager templates to reference the VM image.</span></span> <span data-ttu-id="f89f5-127">以下是此指令碼的範例引動過程：</span><span class="sxs-lookup"><span data-stu-id="f89f5-127">Following is an example invocation of the script:</span></span>
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

<span data-ttu-id="f89f5-128">命令會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f89f5-128">The command does the following:</span></span>

* <span data-ttu-id="f89f5-129">向 Azure Stack 環境進行驗證</span><span class="sxs-lookup"><span data-stu-id="f89f5-129">Authenticates to the Azure Stack environment</span></span>
* <span data-ttu-id="f89f5-130">將本機 VHD 上傳到新建立的臨時儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f89f5-130">Uploads the local VHD to a newly created temporary storage account</span></span>
* <span data-ttu-id="f89f5-131">將 VM 映像新增到 VM 映像存放庫並</span><span class="sxs-lookup"><span data-stu-id="f89f5-131">Adds the VM image to the VM image repository and</span></span>
* <span data-ttu-id="f89f5-132">建立 Marketplace 項目</span><span class="sxs-lookup"><span data-stu-id="f89f5-132">Creates a Marketplace item</span></span>

<span data-ttu-id="f89f5-133">若要確認命令執行成功，請在入口網站中移至 [Marketplace]，然後確認 [虛擬機器] 類別中有該 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-133">To verify that the command ran successfully, go to Marketplace in the portal, and then verify that the VM image is available in the **Virtual Machines** category.</span></span>

![已成功新增 VM 映像](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a><span data-ttu-id="f89f5-135">使用 PowerShell 來移除 VM 映像</span><span class="sxs-lookup"><span data-stu-id="f89f5-135">Remove a VM image with PowerShell</span></span>

<span data-ttu-id="f89f5-136">當您已不再需要先前上傳的虛擬機器映像時，您可以使用下列 Cmdlet 將它從市集中刪除：</span><span class="sxs-lookup"><span data-stu-id="f89f5-136">When you no longer need the virtual machine image that you have uploaded earlier, you can delete it from the marketplace by using the following cmdlet:</span></span>

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a><span data-ttu-id="f89f5-137">參數</span><span class="sxs-lookup"><span data-stu-id="f89f5-137">Parameters</span></span>

| <span data-ttu-id="f89f5-138">參數</span><span class="sxs-lookup"><span data-stu-id="f89f5-138">Parameter</span></span> | <span data-ttu-id="f89f5-139">說明</span><span class="sxs-lookup"><span data-stu-id="f89f5-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f89f5-140">**publisher**</span><span class="sxs-lookup"><span data-stu-id="f89f5-140">**publisher**</span></span> |<span data-ttu-id="f89f5-141">部署映像時，使用者所使用 VM 映像的發行者名稱區段。</span><span class="sxs-lookup"><span data-stu-id="f89f5-141">The publisher name segment of the VM image that users use when deploying the image.</span></span> <span data-ttu-id="f89f5-142">例如 ‘Microsoft’。</span><span class="sxs-lookup"><span data-stu-id="f89f5-142">An example is ‘Microsoft’.</span></span> <span data-ttu-id="f89f5-143">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f89f5-143">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f89f5-144">**offer**</span><span class="sxs-lookup"><span data-stu-id="f89f5-144">**offer**</span></span> |<span data-ttu-id="f89f5-145">部署 VM 映像時，使用者所使用 VM 映像的供應項目名稱區段。</span><span class="sxs-lookup"><span data-stu-id="f89f5-145">The offer name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="f89f5-146">例如 ‘WindowsServer’。</span><span class="sxs-lookup"><span data-stu-id="f89f5-146">An example is ‘WindowsServer’.</span></span> <span data-ttu-id="f89f5-147">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f89f5-147">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f89f5-148">**sku**</span><span class="sxs-lookup"><span data-stu-id="f89f5-148">**sku**</span></span> |<span data-ttu-id="f89f5-149">部署 VM 映像時，使用者所使用 VM 映像的 SKU 名稱區段。</span><span class="sxs-lookup"><span data-stu-id="f89f5-149">The SKU name segment of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="f89f5-150">例如 ‘Datacenter2016’。</span><span class="sxs-lookup"><span data-stu-id="f89f5-150">An example is ‘Datacenter2016’.</span></span> <span data-ttu-id="f89f5-151">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f89f5-151">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f89f5-152">**version**</span><span class="sxs-lookup"><span data-stu-id="f89f5-152">**version**</span></span> |<span data-ttu-id="f89f5-153">部署 VM 映像時，使用者所使用 VM 映像的版本。</span><span class="sxs-lookup"><span data-stu-id="f89f5-153">The version of the VM Image that users use when deploying the VM image.</span></span> <span data-ttu-id="f89f5-154">版本的格式為 *\#.\#.\#*。</span><span class="sxs-lookup"><span data-stu-id="f89f5-154">This version is in the format *\#.\#.\#*.</span></span> <span data-ttu-id="f89f5-155">例如 ‘1.0.0’。</span><span class="sxs-lookup"><span data-stu-id="f89f5-155">An example is ‘1.0.0’.</span></span> <span data-ttu-id="f89f5-156">請勿在此欄位中包含空格或其他特殊字元。</span><span class="sxs-lookup"><span data-stu-id="f89f5-156">Do not include a space or other special characters in this field.</span></span> |
| <span data-ttu-id="f89f5-157">**osType**</span><span class="sxs-lookup"><span data-stu-id="f89f5-157">**osType**</span></span> |<span data-ttu-id="f89f5-158">映像的 osType 必須是 ‘Windows’ 或 ‘Linux’。</span><span class="sxs-lookup"><span data-stu-id="f89f5-158">The osType of the image must be either ‘Windows’ or ‘Linux’.</span></span> |
| <span data-ttu-id="f89f5-159">**osDiskLocalPath**</span><span class="sxs-lookup"><span data-stu-id="f89f5-159">**osDiskLocalPath**</span></span> |<span data-ttu-id="f89f5-160">您以 VM 映像形式上傳到 Azure Stack 之 OS 磁碟 VHD 的本機路徑。</span><span class="sxs-lookup"><span data-stu-id="f89f5-160">The local path to the OS disk VHD that you are uploading as a VM image to Azure Stack.</span></span> |
| <span data-ttu-id="f89f5-161">**dataDiskLocalPaths**</span><span class="sxs-lookup"><span data-stu-id="f89f5-161">**dataDiskLocalPaths**</span></span> |<span data-ttu-id="f89f5-162">可以與 VM 映像一起上傳之資料磁碟的本機路徑陣列 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="f89f5-162">An optional array of the local paths for data disks that can be uploaded as part of the VM image.</span></span> |
| <span data-ttu-id="f89f5-163">**CreateGalleryItem**</span><span class="sxs-lookup"><span data-stu-id="f89f5-163">**CreateGalleryItem**</span></span> |<span data-ttu-id="f89f5-164">可決定是否要在 Marketplace 中建立項目的布林值旗標。</span><span class="sxs-lookup"><span data-stu-id="f89f5-164">A Boolean flag that determines whether to create an item in Marketplace.</span></span> <span data-ttu-id="f89f5-165">預設會設定為 true。</span><span class="sxs-lookup"><span data-stu-id="f89f5-165">By default, it is set to true.</span></span> |
| <span data-ttu-id="f89f5-166">**title**</span><span class="sxs-lookup"><span data-stu-id="f89f5-166">**title**</span></span> |<span data-ttu-id="f89f5-167">Marketplace 項目的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="f89f5-167">The display name of Marketplace item.</span></span> <span data-ttu-id="f89f5-168">預設會設定為 VM 映像的 Publisher-Offer-Sku。</span><span class="sxs-lookup"><span data-stu-id="f89f5-168">By default, it is set to the Publisher-Offer-Sku of the VM image.</span></span> |
| <span data-ttu-id="f89f5-169">**description**</span><span class="sxs-lookup"><span data-stu-id="f89f5-169">**description**</span></span> |<span data-ttu-id="f89f5-170">Marketplace 項目的描述。</span><span class="sxs-lookup"><span data-stu-id="f89f5-170">The description of the Marketplace item.</span></span> |
| <span data-ttu-id="f89f5-171">**位置**</span><span class="sxs-lookup"><span data-stu-id="f89f5-171">**location**</span></span> |<span data-ttu-id="f89f5-172">應作為 VM 映像發行目的地的位置。</span><span class="sxs-lookup"><span data-stu-id="f89f5-172">The location to which the VM image should be published.</span></span> <span data-ttu-id="f89f5-173">此值預設會設定為 local。</span><span class="sxs-lookup"><span data-stu-id="f89f5-173">By default, this value is set to local.</span></span>|
| <span data-ttu-id="f89f5-174">**osDiskBlobURI**</span><span class="sxs-lookup"><span data-stu-id="f89f5-174">**osDiskBlobURI**</span></span> |<span data-ttu-id="f89f5-175">此指令碼也可視需要接受 osDisk 的 Blob 儲存體 URI。</span><span class="sxs-lookup"><span data-stu-id="f89f5-175">Optionally, this script also accepts a Blob storage URI for osDisk.</span></span> |
| <span data-ttu-id="f89f5-176">**dataDiskBlobURIs**</span><span class="sxs-lookup"><span data-stu-id="f89f5-176">**dataDiskBlobURIs**</span></span> |<span data-ttu-id="f89f5-177">此指令碼也可視需要接受 Blob 儲存體 URI 陣列，以將資料磁碟新增到映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-177">Optionally, this script also accepts an array of Blob storage URIs for adding data disks to the image.</span></span> |

## <a name="add-a-vm-image-through-the-portal"></a><span data-ttu-id="f89f5-178">透過入口網站新增 VM 映像</span><span class="sxs-lookup"><span data-stu-id="f89f5-178">Add a VM image through the portal</span></span>

> [!NOTE]
> <span data-ttu-id="f89f5-179">此方法需要個別建立 Marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="f89f5-179">This method requires creating the Marketplace item separately.</span></span>

<span data-ttu-id="f89f5-180">對映像的其中一個需求就是必須可藉由 Blob 儲存體 URI 參考它們。</span><span class="sxs-lookup"><span data-stu-id="f89f5-180">One requirement of images is that they can be referenced by a Blob storage URI.</span></span> <span data-ttu-id="f89f5-181">準備 VHD 格式 (非 VHDX) 的 Windows 或 Linux 作業系統映像，然後將該映像上傳到 Azure 或 Azure Stack 中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f89f5-181">Prepare a Windows or Linux operating system image in VHD format (not VHDX), and then upload the image to a storage account in Azure or Azure Stack.</span></span> <span data-ttu-id="f89f5-182">如果您的映像已經上傳到 Azure 或 Azure Stack 中的 Blob 儲存體，則您可以略過步驟 1。</span><span class="sxs-lookup"><span data-stu-id="f89f5-182">If your image is already uploaded to the Blob storage in Azure or Azure Stack, you can skip step1.</span></span>

1. <span data-ttu-id="f89f5-183">[將 Windows VM 映像上傳至 Azure 供 Resource Manager 部署使用](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)，或如果是 Linux 映像，則依照[在 Azure Stack 上部署 Linux 虛擬機器](azure-stack-linux.md)一文所述的指示操作。</span><span class="sxs-lookup"><span data-stu-id="f89f5-183">[Upload a Windows VM image to Azure for Resource Manager deployments](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) or for a Linux image, follow the instructions described in the [Deploy Linux virtual machines on Azure Stack](azure-stack-linux.md) article.</span></span> <span data-ttu-id="f89f5-184">上傳映像之前，您應該先了解下列考量：</span><span class="sxs-lookup"><span data-stu-id="f89f5-184">You should understand the following considerations before you upload the image:</span></span>

   * <span data-ttu-id="f89f5-185">將映像上傳到 Azure Stack Blob 儲存體比上傳到 Azure Blob 儲存體有效率，因為將映像推送到 Azure Stack 映像存放庫所需的時間較短。</span><span class="sxs-lookup"><span data-stu-id="f89f5-185">It's more efficient to upload an image to Azure Stack Blob storage than to Azure Blob storage because it takes less time to push the image to the Azure Stack image repository.</span></span> 
   
   * <span data-ttu-id="f89f5-186">上傳 [Windows VM 映像](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/)時，請務必以[設定 Azure Stack 操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md)步驟取代「登入 Azure」步驟。</span><span class="sxs-lookup"><span data-stu-id="f89f5-186">When uploading the [Windows VM image](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), make sure to substitute the **Login to Azure** step with the [Configure the Azure Stack operator's PowerShell environment](azure-stack-powershell-configure-admin.md)  step.</span></span>  

   * <span data-ttu-id="f89f5-187">記下您上傳映像的 Blob 儲存體 URI，其格式如下：*&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span><span class="sxs-lookup"><span data-stu-id="f89f5-187">Make a note of the Blob storage URI where you upload the image, which is in the following format: *&lt;storageAccount&gt;/&lt;blobContainer&gt;/&lt;targetVHDName&gt;*.vhd</span></span>

   * <span data-ttu-id="f89f5-188">若要讓 Blob 可供匿名存取，請移至將 VM 映像 VHD 上傳到 **Blob** 時的儲存體帳戶 Blob 容器，然後選取 [存取原則]。</span><span class="sxs-lookup"><span data-stu-id="f89f5-188">To make the blob anonymously accessible, go to the storage account blob container where the VM image VHD was uploaded to **Blob,** and then select **Access Policy**.</span></span> <span data-ttu-id="f89f5-189">如果您想要的話，也可以改為產生容器的共用存取簽章，然後將它包含在 Blob URI 中。</span><span class="sxs-lookup"><span data-stu-id="f89f5-189">If you want, you can instead generate a shared access signature for the container and include it as part of the blob URI.</span></span>

   ![瀏覽至儲存體帳戶 Blob](./media/azure-stack-add-vm-image/image1.png)

   ![將 Blob 存取權設定為公用](./media/azure-stack-add-vm-image/image2.png)

2. <span data-ttu-id="f89f5-192">以操作員身分登入 Azure Stack，從功能表中按一下 [更多服務] > [資源提供者] > 選取 [計算] > [VM 映像] > [新增]</span><span class="sxs-lookup"><span data-stu-id="f89f5-192">Sign in to Azure Stack as operator > From the menu, click **More services** > **Resource Providers** > select  **Compute** > **VM images** > **Add**</span></span>

3. <span data-ttu-id="f89f5-193">在 [新增 VM 映像] 刀鋒視窗上，輸入虛擬機器映像的發行者、供應項目、SKU 及版本。</span><span class="sxs-lookup"><span data-stu-id="f89f5-193">On the **Add a VM Image** blade, enter the publisher, offer, SKU, and version of the virtual machine image.</span></span> <span data-ttu-id="f89f5-194">這些名稱區段指的是 Resource Manager 範本中的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-194">These name segments refer to the VM image in Resource Manager templates.</span></span> <span data-ttu-id="f89f5-195">請務必正確選取 **osType**。</span><span class="sxs-lookup"><span data-stu-id="f89f5-195">Make sure to select the **osType** correctly.</span></span> <span data-ttu-id="f89f5-196">針對 [OD 磁碟 Blob URI]，請輸入上傳映像的 Blob URI，然後按一下 [建立] 來開始建立 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="f89f5-196">For **OD Disk Blob URI**, enter the Blob URI where the image was uploaded and click **Create** to begin creating the VM Image.</span></span>
   
   ![開始建立映像](./media/azure-stack-add-vm-image/image4.png)

   <span data-ttu-id="f89f5-198">成功建立映像時，VM 映像狀態會變更為「成功」。</span><span class="sxs-lookup"><span data-stu-id="f89f5-198">When the image is successfully created, the VM image status changes to ‘Succeeded’.</span></span>

4. <span data-ttu-id="f89f5-199">若要更容易在 UI 中將虛擬機器映像提供給使用者取用，最好是[建立 Marketplace 項目](azure-stack-create-and-publish-marketplace-item.md)。</span><span class="sxs-lookup"><span data-stu-id="f89f5-199">To make the virtual machine image more readily available for user consumption in the UI, it is best to [create a Marketplace item](azure-stack-create-and-publish-marketplace-item.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f89f5-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f89f5-200">Next steps</span></span>

[<span data-ttu-id="f89f5-201">佈建虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f89f5-201">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)