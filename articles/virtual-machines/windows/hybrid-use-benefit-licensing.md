---
title: "aaaAzure 混合使用權益，適用於 Windows Server 和 Windows 用戶端 |Microsoft 文件"
description: "了解如何 toomaximize 您的 Windows 軟體保證權益 toobring 內部部署授權 tooAzure"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="af833-103">適用於 Windows Server 和 Windows 用戶端的 Azure Hybrid Use Benefit</span><span class="sxs-lookup"><span data-stu-id="af833-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="af833-104">附有軟體保證客戶，Azure 混合式使用權益可讓您 toouse 在內部部署 Windows Server 和 Windows 用戶端授權和執行的 Windows Azure 中虛擬機器以降低成本。</span><span class="sxs-lookup"><span data-stu-id="af833-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="af833-105">適用於 Windows Server 的 Azure Hybrid Use Benefit 包含 Windows Server 2008R2、Windows Server 2012、Windows Server 2012R2 及 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="af833-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="af833-106">適用於 Windows 用戶端的 Azure Hybrid Use Benefit 包含 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="af833-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="af833-107">如需詳細資訊，請參閱 hello [Azure 混合式使用權益授權頁面](https://azure.microsoft.com/pricing/hybrid-use-benefit/)。</span><span class="sxs-lookup"><span data-stu-id="af833-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="af833-108">Azure 混合式使用優點的 Windows 用戶端目前為預覽狀態使用 hello Azure Marketplace 中 hello Windows 10 映像。</span><span class="sxs-lookup"><span data-stu-id="af833-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="af833-109">只有下列企業版客戶有資格使用：每位使用者都具有 Windows 10 Enterprise E3/E5，或者每位使用者都具有 Windows VDA (使用者訂閱授權或附加元件使用者訂閱授權) (「合格授權」)。</span><span class="sxs-lookup"><span data-stu-id="af833-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="af833-110">方式 toouse Azure 混合式使用權益</span><span class="sxs-lookup"><span data-stu-id="af833-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="af833-111">有幾個不同的方式 toodeploy Windows Vm 以 hello Azure 混合式使用好處：</span><span class="sxs-lookup"><span data-stu-id="af833-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="af833-112">您可以從使用 Azure Hybrid Use Benefit - Windows Server 2016、Windows Server 2012R2、Windows Server 2012 和 Windows Server 2008SP1 預先設定的[特定 Marketplace 映像](#deploy-a-vm-using-the-azure-marketplace)部署 VM。</span><span class="sxs-lookup"><span data-stu-id="af833-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="af833-113">您可以[上傳自訂 VM](#upload-a-windows-vhd)，並使用 [Resource Manager 範本來部署](#deploy-a-vm-via-resource-manager)或使用 [Azure PowerShell](#detailed-powershell-deployment-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="af833-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="af833-114">部署使用 hello Azure Marketplace 的 VM</span><span class="sxs-lookup"><span data-stu-id="af833-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="af833-115">Hello 與 Azure 混合式使用權益預先設定的服務商場中的下列映像可用： Windows Server 2016 中，Windows Server 2012R2、 Windows Server 2012 和 Windows Server 2008SP1。</span><span class="sxs-lookup"><span data-stu-id="af833-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="af833-116">可以部署這些映像，直接從 hello Azure 入口網站中，資源管理員範本或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="af833-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="af833-117">您可以部署這些映像，直接從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="af833-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="af833-118">使用資源管理員範本，並使用 Azure PowerShell，請檢視 hello 的映像的清單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af833-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="af833-119">對於 Windows Server：</span><span class="sxs-lookup"><span data-stu-id="af833-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="af833-120">2016-Datacenter 版本 2016.127.20170406 或更高版本</span><span class="sxs-lookup"><span data-stu-id="af833-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="af833-121">2012-R2-Datacenter 版本 4.127.20170406 或更高版本</span><span class="sxs-lookup"><span data-stu-id="af833-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="af833-122">2012-Datacenter 版本 3.127.20170406 或更高版本</span><span class="sxs-lookup"><span data-stu-id="af833-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="af833-123">2008-R2-SP1 版本 2.127.20170406 或更高版本</span><span class="sxs-lookup"><span data-stu-id="af833-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="af833-124">對於 Windows 用戶端：</span><span class="sxs-lookup"><span data-stu-id="af833-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="af833-125">上傳 Windows Server VHD</span><span class="sxs-lookup"><span data-stu-id="af833-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="af833-126">toodeploy Azure 中的 Windows Server VM，您必須先 toocreate 包含基底的 Windows 組建的 VHD。</span><span class="sxs-lookup"><span data-stu-id="af833-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="af833-127">此 VHD 必須先適當地準備透過 Sysprep tooAzure 上載。</span><span class="sxs-lookup"><span data-stu-id="af833-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="af833-128">您可以[深入了解有關 hello VHD 需求和 Sysprep 程序](upload-generalized-managed.md)和[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。</span><span class="sxs-lookup"><span data-stu-id="af833-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="af833-129">執行 Sysprep 之前先備份 hello VM。</span><span class="sxs-lookup"><span data-stu-id="af833-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="af833-130">請確定您有[安裝和設定的 hello 最新的 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="af833-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="af833-131">一旦您已經備妥您的 VHD 上, 傳 hello VHD tooyour Azure 儲存體帳戶使用 hello `Add-AzureRmVhd` cmdlet，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af833-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="af833-132">Microsoft SQL Server、SharePoint 伺服器、Dynamics 也可以使用您的軟體保證授權。</span><span class="sxs-lookup"><span data-stu-id="af833-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="af833-133">您仍然需要 tooprepare hello Windows Server 映像安裝應用程式元件，並提供授權金鑰，然後上傳 hello 磁碟映像 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="af833-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="af833-134">檢閱 hello 適當文件與您的應用程式中，執行 Sysprep，例如[使用 Sysprep 安裝 SQL Server 的考量](https://msdn.microsoft.com/library/ee210754.aspx)或[建置 SharePoint Server 2016 參照映像 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="af833-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="af833-135">您也可以深入了解[上載 hello VHD tooAzure 程序](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="af833-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="af833-136">透過 Resource Manager 範本部署 VM</span><span class="sxs-lookup"><span data-stu-id="af833-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="af833-137">在 Resource Manager 範本內，可以指定 `licenseType` 的額外參數。</span><span class="sxs-lookup"><span data-stu-id="af833-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="af833-138">您可以進一步了解如何 [製作 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="af833-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="af833-139">一旦上傳的 VHD tooAzure，編輯您資源管理員範本 tooinclude hello 授權類型為 hello 一部分計算提供者，並部署您的範本，像平常一樣：</span><span class="sxs-lookup"><span data-stu-id="af833-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="af833-140">對於 Windows Server：</span><span class="sxs-lookup"><span data-stu-id="af833-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="af833-141">為 Windows 用戶端 toouse 與 Azure Marketplace 映像只：</span><span class="sxs-lookup"><span data-stu-id="af833-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="af833-142">透過 PowerShell 快速入門部署 VM</span><span class="sxs-lookup"><span data-stu-id="af833-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="af833-143">透過 PowerShell 部署 Windows Server VM 時，您會有 `-LicenseType`的額外參數。</span><span class="sxs-lookup"><span data-stu-id="af833-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="af833-144">上傳的 VHD tooAzure 之後，您建立 VM 使用`New-AzureRmVM`並指定 hello 授權類型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af833-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="af833-145">對於 Windows Server：</span><span class="sxs-lookup"><span data-stu-id="af833-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="af833-146">為 Windows 用戶端 toouse 與 Azure Marketplace 映像只：</span><span class="sxs-lookup"><span data-stu-id="af833-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="af833-147">您可以[閱讀更詳細的逐步解說部署在透過 PowerShell 的 Azure VM](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough)上更具描述性的指南，或讀取太 hello 記憶體不同的步驟[建立 Windows VM 使用資源管理員和 PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af833-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="af833-148">請確認您的 VM 利用 hello 授權權益</span><span class="sxs-lookup"><span data-stu-id="af833-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="af833-149">當您部署您的 VM，透過 hello PowerShell 或資源管理員部署方法時，驗證與 hello 授權類型`Get-AzureRmVM`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="af833-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="af833-150">hello 輸出是 toohello 類似下列範例適用於 Windows Server:</span><span class="sxs-lookup"><span data-stu-id="af833-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="af833-151">此輸出會與下列 VM 不授權 Azure 混合式使用權益，例如直接從 hello Azure 組件庫中部署的 VM 部署的 hello 相反：</span><span class="sxs-lookup"><span data-stu-id="af833-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="af833-152">詳細的 PowerShell 部署逐步解說</span><span class="sxs-lookup"><span data-stu-id="af833-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="af833-153">hello 下列詳細的 PowerShell 步驟顯示完整部署 VM。</span><span class="sxs-lookup"><span data-stu-id="af833-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="af833-154">您可以閱讀更多的內容以及 toohello 實際指令程式中建立的不同元件[建立使用資源管理員和 PowerShell 的 Windows VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="af833-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="af833-155">您將逐步進行建立資源群組、儲存體帳戶和虛擬網路，然後定義 VM 並完成建立 VM 的步驟。</span><span class="sxs-lookup"><span data-stu-id="af833-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="af833-156">首先，安全地取得認證，並設定位置和資源群組名稱：</span><span class="sxs-lookup"><span data-stu-id="af833-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="af833-157">建立公用 IP：</span><span class="sxs-lookup"><span data-stu-id="af833-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="af833-158">定義子網路、NIC 和 VNET：</span><span class="sxs-lookup"><span data-stu-id="af833-158">Define your subnet, NIC, and VNET:</span></span>

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

<span data-ttu-id="af833-159">命名 VM，並建立 VM 設定：</span><span class="sxs-lookup"><span data-stu-id="af833-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="af833-160">定義您的 OS：</span><span class="sxs-lookup"><span data-stu-id="af833-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="af833-161">加入您的 NIC toohello VM:</span><span class="sxs-lookup"><span data-stu-id="af833-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="af833-162">定義 hello 儲存體帳戶 toouse:</span><span class="sxs-lookup"><span data-stu-id="af833-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="af833-163">上傳您的 VHD，適當地備妥，並將用於 tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="af833-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="af833-164">最後，建立您的 VM，並定義 hello 授權類型 tooutilize Azure 混合式使用好處：</span><span class="sxs-lookup"><span data-stu-id="af833-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="af833-165">對於 Windows Server：</span><span class="sxs-lookup"><span data-stu-id="af833-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="af833-166">透過 Resource Manager 範本來部署虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="af833-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="af833-167">在 VMSS Resource Manager 範本內，必須指定 `licenseType` 的額外參數。</span><span class="sxs-lookup"><span data-stu-id="af833-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="af833-168">您可以進一步了解如何 [製作 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="af833-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="af833-169">編輯資源管理員範本 tooinclude hello licenseType 屬性 virtualMachineProfile hello 規模集的一部分，並部署您的範本，像平常一樣-請參閱下例使用 2016 Windows Server 映像：</span><span class="sxs-lookup"><span data-stu-id="af833-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> <span data-ttu-id="af833-170">即將推出的部署虛擬機器擴展集支援可透過 PowerShell 和其他 SDK 工具提供 AHUB 權益。</span><span class="sxs-lookup"><span data-stu-id="af833-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="af833-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="af833-171">Next steps</span></span>
<span data-ttu-id="af833-172">深入了解 [Azure Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/)授權。</span><span class="sxs-lookup"><span data-stu-id="af833-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="af833-173">深入了解如何[使用 Resource Manager 範本](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="af833-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="af833-174">深入了解[Azure 混合式使用效益和 Azure Site Recovery 進行移轉的應用程式 tooAzure 更符合成本效益](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/)。</span><span class="sxs-lookup"><span data-stu-id="af833-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
