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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>適用於 Windows Server 和 Windows 用戶端的 Azure Hybrid Use Benefit
附有軟體保證客戶，Azure 混合式使用權益可讓您 toouse 在內部部署 Windows Server 和 Windows 用戶端授權和執行的 Windows Azure 中虛擬機器以降低成本。 適用於 Windows Server 的 Azure Hybrid Use Benefit 包含 Windows Server 2008R2、Windows Server 2012、Windows Server 2012R2 及 Windows Server 2016。 適用於 Windows 用戶端的 Azure Hybrid Use Benefit 包含 Windows 10。 如需詳細資訊，請參閱 hello [Azure 混合式使用權益授權頁面](https://azure.microsoft.com/pricing/hybrid-use-benefit/)。

>[!IMPORTANT]
>Azure 混合式使用優點的 Windows 用戶端目前為預覽狀態使用 hello Azure Marketplace 中 hello Windows 10 映像。 只有下列企業版客戶有資格使用：每位使用者都具有 Windows 10 Enterprise E3/E5，或者每位使用者都具有 Windows VDA (使用者訂閱授權或附加元件使用者訂閱授權) (「合格授權」)。
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>方式 toouse Azure 混合式使用權益
有幾個不同的方式 toodeploy Windows Vm 以 hello Azure 混合式使用好處：

1. 您可以從使用 Azure Hybrid Use Benefit - Windows Server 2016、Windows Server 2012R2、Windows Server 2012 和 Windows Server 2008SP1 預先設定的[特定 Marketplace 映像](#deploy-a-vm-using-the-azure-marketplace)部署 VM。
2. 您可以[上傳自訂 VM](#upload-a-windows-vhd)，並使用 [Resource Manager 範本來部署](#deploy-a-vm-via-resource-manager)或使用 [Azure PowerShell](#detailed-powershell-deployment-walkthrough)。

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>部署使用 hello Azure Marketplace 的 VM
Hello 與 Azure 混合式使用權益預先設定的服務商場中的下列映像可用： Windows Server 2016 中，Windows Server 2012R2、 Windows Server 2012 和 Windows Server 2008SP1。 可以部署這些映像，直接從 hello Azure 入口網站中，資源管理員範本或 Azure PowerShell。

您可以部署這些映像，直接從 hello Azure 入口網站。 使用資源管理員範本，並使用 Azure PowerShell，請檢視 hello 的映像的清單，如下所示：

對於 Windows Server：
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter 版本 2016.127.20170406 或更高版本

- 2012-R2-Datacenter 版本 4.127.20170406 或更高版本

- 2012-Datacenter 版本 3.127.20170406 或更高版本

- 2008-R2-SP1 版本 2.127.20170406 或更高版本

對於 Windows 用戶端：
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>上傳 Windows Server VHD
toodeploy Azure 中的 Windows Server VM，您必須先 toocreate 包含基底的 Windows 組建的 VHD。 此 VHD 必須先適當地準備透過 Sysprep tooAzure 上載。 您可以[深入了解有關 hello VHD 需求和 Sysprep 程序](upload-generalized-managed.md)和[伺服器角色的 Sysprep 支援](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)。 執行 Sysprep 之前先備份 hello VM。 

請確定您有[安裝和設定的 hello 最新的 Azure PowerShell](/powershell/azure/overview)。 一旦您已經備妥您的 VHD 上, 傳 hello VHD tooyour Azure 儲存體帳戶使用 hello `Add-AzureRmVhd` cmdlet，如下所示：

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server、SharePoint 伺服器、Dynamics 也可以使用您的軟體保證授權。 您仍然需要 tooprepare hello Windows Server 映像安裝應用程式元件，並提供授權金鑰，然後上傳 hello 磁碟映像 tooAzure。 檢閱 hello 適當文件與您的應用程式中，執行 Sysprep，例如[使用 Sysprep 安裝 SQL Server 的考量](https://msdn.microsoft.com/library/ee210754.aspx)或[建置 SharePoint Server 2016 參照映像 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

您也可以深入了解[上載 hello VHD tooAzure 程序](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>透過 Resource Manager 範本部署 VM
在 Resource Manager 範本內，可以指定 `licenseType` 的額外參數。 您可以進一步了解如何 [製作 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。 一旦上傳的 VHD tooAzure，編輯您資源管理員範本 tooinclude hello 授權類型為 hello 一部分計算提供者，並部署您的範本，像平常一樣：

對於 Windows Server：
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

為 Windows 用戶端 toouse 與 Azure Marketplace 映像只：
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>透過 PowerShell 快速入門部署 VM
透過 PowerShell 部署 Windows Server VM 時，您會有 `-LicenseType`的額外參數。 上傳的 VHD tooAzure 之後，您建立 VM 使用`New-AzureRmVM`並指定 hello 授權類型，如下所示：

對於 Windows Server：
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

為 Windows 用戶端 toouse 與 Azure Marketplace 映像只：
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

您可以[閱讀更詳細的逐步解說部署在透過 PowerShell 的 Azure VM](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough)上更具描述性的指南，或讀取太 hello 記憶體不同的步驟[建立 Windows VM 使用資源管理員和 PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>請確認您的 VM 利用 hello 授權權益
當您部署您的 VM，透過 hello PowerShell 或資源管理員部署方法時，驗證與 hello 授權類型`Get-AzureRmVM`，如下所示：

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

hello 輸出是 toohello 類似下列範例適用於 Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

此輸出會與下列 VM 不授權 Azure 混合式使用權益，例如直接從 hello Azure 組件庫中部署的 VM 部署的 hello 相反：

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>詳細的 PowerShell 部署逐步解說
hello 下列詳細的 PowerShell 步驟顯示完整部署 VM。 您可以閱讀更多的內容以及 toohello 實際指令程式中建立的不同元件[建立使用資源管理員和 PowerShell 的 Windows VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 您將逐步進行建立資源群組、儲存體帳戶和虛擬網路，然後定義 VM 並完成建立 VM 的步驟。

首先，安全地取得認證，並設定位置和資源群組名稱：

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

建立公用 IP：

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

定義子網路、NIC 和 VNET：

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

命名 VM，並建立 VM 設定：

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

定義您的 OS：

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

加入您的 NIC toohello VM:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

定義 hello 儲存體帳戶 toouse:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

上傳您的 VHD，適當地備妥，並將用於 tooyour VM:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

最後，建立您的 VM，並定義 hello 授權類型 tooutilize Azure 混合式使用好處：

對於 Windows Server：
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>透過 Resource Manager 範本來部署虛擬機器擴展集
在 VMSS Resource Manager 範本內，必須指定 `licenseType` 的額外參數。 您可以進一步了解如何 [製作 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。 編輯資源管理員範本 tooinclude hello licenseType 屬性 virtualMachineProfile hello 規模集的一部分，並部署您的範本，像平常一樣-請參閱下例使用 2016 Windows Server 映像：


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
> 即將推出的部署虛擬機器擴展集支援可透過 PowerShell 和其他 SDK 工具提供 AHUB 權益。
>

## <a name="next-steps"></a>後續步驟
深入了解 [Azure Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/)授權。

深入了解如何[使用 Resource Manager 範本](../../azure-resource-manager/resource-group-overview.md)。

深入了解[Azure 混合式使用效益和 Azure Site Recovery 進行移轉的應用程式 tooAzure 更符合成本效益](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/)。
