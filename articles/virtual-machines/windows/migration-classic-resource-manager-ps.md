---
title: "aaaMigrate tooResource 管理員使用 PowerShell |Microsoft 文件"
description: "本文逐步 hello 平台支援移轉的 IaaS 資源，例如虛擬機器 (Vm)、 虛擬網路 (Vnet) 和儲存體帳戶從傳統 tooAzure 資源管理員 (ARM) 可以使用 Azure PowerShell 命令"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>使用 Azure PowerShell，從傳統 tooAzure 資源管理員移轉 IaaS 資源
這些步驟顯示如何 toouse Azure PowerShell 命令為從 hello 傳統部署模型 toohello Azure Resource Manager 部署模型的服務 (IaaS) 資源的 toomigrate 基礎結構。

如果您想，您也可以移轉的資源使用 hello [Azure 命令列介面 (Azure CLI)](../linux/migration-classic-resource-manager-cli.md)。

* 如需有關支援的移轉案例的背景，請參閱[平台支援移轉的 IaaS 資源從資源管理員的傳統 tooAzure](migration-classic-resource-manager-overview.md)。
* 如需詳細的指引和移轉的逐步解說，請參閱[技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md)。
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md)

<br>
以下是步驟需要執行移轉程序期間 toobe 流程圖 tooidentify hello 順序

![螢幕擷取畫面顯示 hello 移轉步驟](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>步驟 1︰為移轉做規劃
以下是我們建議您在評估從傳統 tooResource Manager 移轉的 IaaS 資源的一些最佳作法：

* 閱讀 hello[支援和不支援的功能和設定](migration-classic-resource-manager-overview.md)。 如果您有使用不支援的設定或功能的虛擬機器，我們建議您等候 hello 設定/功能支援 toobe 宣布。 或者，如果其符合您的需求時，移除該功能，或移出該設定 tooenable 移轉。
* 如果您有自動化部署基礎結構和應用程式目前的指令碼，請使用這些指令碼移轉嘗試 toocreate 類似的測試設定。 或者，您可以設定範例環境使用 hello Azure 入口網站。

> [!IMPORTANT]
> 從傳統 tooResource Manager 移轉目前不支援應用程式閘道。 toomigrate 傳統虛擬網路與應用程式閘道，執行準備作業 toomove hello 網路之前先移除 hello 閘道。 Hello 移轉完成之後，重新連接 hello 閘道 Azure 資源管理員中。
>
>ExpressRoute 閘道連接 tooExpressRoute 電路，另一個訂用帳戶中的不會自動移轉。 在這種情況下，移除 hello ExpressRoute 閘道、 hello 虛擬網路移轉並重新建立 hello 閘道。 請參閱[移轉 ExpressRoute 電路和相關聯的虛擬網路與 hello 傳統 toohello Resource Manager 部署模型](../../expressroute/expressroute-migration-classic-resource-manager.md)如需詳細資訊。
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>步驟 2： 安裝 Azure PowerShell hello 最新版本
有兩個主要選項 tooinstall Azure PowerShell: [PowerShell 資源庫](https://www.powershellgallery.com/profiles/azure-sdk/)或[Web Platform Installer (WebPI)](http://aka.ms/webpi-azps)。 WebPI 接收每月更新。 PowerShell 資源庫則是持續接收更新。 本文是以 Azure PowerShell 2.1.0 為基礎。

如需安裝指示，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>步驟 3： 確定您在 Azure 入口網站是 hello 訂用帳戶的系統管理員
tooperform 這個移轉中，您必須新增為共同管理員的 hello hello 訂用帳戶[Azure 入口網站](https://portal.azure.com)。

1. 登入 hello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，選取 **訂用帳戶**。 如果您沒有看到，請選取 [更多服務]。
3. 尋找 hello 適當的訂閱項目，然後查看 hello **MY ROLE**欄位。 共同管理員，hello 值應該是_帳戶管理員_。

如果您不能 tooadd 共同管理員，請連絡服務管理員或共同管理員的 hello 訂用帳戶 tooget 自行加入。   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>步驟 4︰設定您的訂用帳戶並註冊以進行移轉
首先，開啟 PowerShell 提示字元。 進行移轉，您需要的這兩種傳統環境 tooset 和資源管理員。

登入 tooyour 帳戶 hello 資源管理員的模型。

```powershell
    Login-AzureRmAccount
```

使用下列命令的 hello 取得 hello 可用的訂用帳戶：

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

設定您的 Azure 訂閱 hello 目前工作階段。 此範例中設定 hello 預設訂用帳戶名稱太**我 Azure 訂用帳戶**。 使用您自己取代 hello 範例訂用帳戶名稱。

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> 註冊是一次性步驟，但您必須在嘗試移轉之前完成。 若未註冊，您會看到下列錯誤訊息的 hello:
>
> *不正確的要求︰訂用帳戶未針對移轉進行註冊。*
>
>

使用下列命令的 hello 註冊與 hello 移轉資源提供者：

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

請等待五分鐘 hello 註冊 toofinish。 您可以使用下列命令的 hello 檢查 hello hello 核准狀態：

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

請先確定 RegistrationState 是 `Registered` ，再繼續進行。

立即登入 tooyour 帳戶 hello 傳統的模型。

```powershell
    Add-AzureAccount
```

使用下列命令的 hello 取得 hello 可用的訂用帳戶：

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

設定您的 Azure 訂閱 hello 目前工作階段。 此範例會設定 hello 預設訂用帳戶太**我 Azure 訂用帳戶**。 使用您自己取代 hello 範例訂用帳戶名稱。

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>步驟 5： 請確定您有足夠的 Azure 資源管理員虛擬機器核心 hello 目前的部署或 VNET 的 Azure 區域中
您可以使用下列 PowerShell 命令 toocheck hello 目前的核心數目有 Azure 資源管理員中的 hello。 toolearn 進一步了解核心配額，請參閱[限制和 hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)。

這個範例會檢查在 hello hello 可用性**美國西部**區域。 使用您自己取代 hello 範例區域名稱。

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>步驟 6： 執行命令 toomigrate IaaS 資源
> [!NOTE]
> 此處所述的所有 hello 作業都是等冪。 如果您有不支援的功能或設定錯誤以外的問題，我們建議您重試 hello 準備、 中止或認可作業。 hello 平台，然後嘗試再次 hello 動作。
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>步驟 6.1：選項 1 - 移轉雲端服務中的虛擬機器 (不在虛擬網路中)
使用下列命令，hello 的雲端服務]，然後按一下 [挑選 hello 雲端服務，而您想 toomigrate 取得 hello 清單。 如果 hello 雲端服務中的 hello Vm 虛擬網路中，或他們有 web 或背景工作角色，hello 命令會傳回錯誤訊息。

```powershell
    Get-AzureService | ft Servicename
```

取得 hello hello 雲端服務的部署名稱。 在此範例中，hello 服務名稱是**我的服務**。 Hello 範例服務名稱取代成您自己的服務名稱。

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

準備移轉的 hello 雲端服務中的 hello 虛擬機器。 您必須從兩個選項 toochoose。

* **選項 1：Hello Vm tooa 平台建立虛擬網路移轉**

    首先，驗證是否可以使用下列命令的 hello hello 雲端服務移轉：

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    hello 上述命令會顯示任何警告及封鎖移轉的錯誤。 如果驗證成功，則可以移 toohello**準備**步驟：

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **選項 2：移轉 tooan 現有的虛擬網路中 hello Resource Manager 部署模型**

    此範例中設定 hello 資源群組名稱太**myResourceGroup**，太 hello 虛擬網路名稱**myVirtualNetwork**太 hello 子網路名稱和**mySubNet**。 取代您自己的資源名稱 hello hello 範例中的 hello 名稱。

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    首先，驗證是否使用下列命令的 hello hello 虛擬網路移轉：

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    hello 上述命令會顯示任何警告及封鎖移轉的錯誤。 如果驗證成功，您可以繼續進行下列準備步驟 hello:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Hello 上述選項的其中一種成功 hello 「 準備 」 作業之後，查詢 hello Vm hello 移轉的狀態。 確保它們處於 hello`Prepared`狀態。

此範例中設定 hello VM 名稱太**myVM**。 Hello 範例名稱取代成您自己的 VM 名稱。

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

檢查 hello hello 準備資源使用 PowerShell 或 hello Azure 入口網站的組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>步驟 6.1：選項 2 - 移轉虛擬網路中的虛擬機器

toomigrate 虛擬機器在虛擬網路中，您可以移轉 hello 虛擬網路。 hello 虛擬機器自動移轉與 hello 虛擬網路。 您想 toomigrate 挑選 hello 虛擬網路。
> [!NOTE]
> [將單一傳統的虛擬機器移轉](migrate-single-classic-to-resource-manager.md)藉由使用受管理的磁碟使用 hello VHD （作業系統和資料） 檔案的 hello 虛擬機器建立新的資源管理員虛擬機器。
<br>

> [!NOTE]
> hello 虛擬網路名稱可能不同於所顯示 hello 中新的入口網站。 hello 新版 Azure 入口網站會顯示 hello 名稱做為`[vnet-name]`但是 hello 實際的虛擬網路名稱必須是型別`Group [resource-group-name] [vnet-name]`。 然後再移轉，查閱 hello 實際的虛擬網路名稱使用 hello 命令`Get-AzureVnetSite | Select -Property Name`檢視在 hello 或舊的 Azure 入口網站。 

此範例中設定 hello 虛擬網路名稱太**myVnet**。 Hello 範例虛擬網路名稱取代您自己。

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> 如果 hello 虛擬網路包含 web 或背景工作角色或 Vm 具有不支援的設定，您會取得驗證錯誤訊息。
>
>

如果您可以使用下列命令的 hello 移轉 hello 虛擬網路，首先，驗證：

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

hello 上述命令會顯示任何警告及封鎖移轉的錯誤。 如果驗證成功，您可以繼續進行下列準備步驟 hello:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

檢查 hello hello 準備使用 Azure PowerShell 或 hello Azure 入口網站的虛擬機器的組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>步驟 6.2：移轉儲存體帳戶
一旦您完成移轉 hello 虛擬機器時，我們建議您移轉 hello 儲存體帳戶。

移轉 hello 儲存體帳戶之前，請執行前的必要條件檢查：

* **將傳統的磁碟儲存 hello 儲存體帳戶中的虛擬機器移轉**

    上述命令傳回 RoleName 和 DiskName 屬性的所有 hello 傳統 VM 磁碟 hello 儲存體帳戶中。 RoleName 是 hello 磁碟連接的虛擬機器 toowhich hello 名稱。 如果上述命令會傳回磁碟，然後確保移轉之前移轉這些磁碟已連接該虛擬機器 toowhich hello 儲存體帳戶。
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **刪除未附加之傳統的 VM 磁碟儲存在 hello 儲存體帳戶**

    找到未附加之傳統 VM 磁碟在 hello 儲存體帳戶使用下列命令：

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    如果上述命令傳回磁碟，則使用下列命令刪除這些磁碟︰

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **刪除 VM 映像儲存在 hello 儲存體帳戶**

    上述命令會傳回所有 hello VM 映像 hello 儲存體帳戶中儲存的作業系統磁碟。
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     上述命令會傳回所有 hello VM 映像 hello 儲存體帳戶中儲存的資料磁碟。
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    刪除所有上述使用上述命令的命令所傳回的 hello VM 映像：
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

使用下列命令的 hello 驗證移轉的每個儲存體帳戶。 此範例中的 hello 儲存體帳戶名稱是**myStorageAccount**。 Hello 範例名稱取代 hello 您自己的儲存體帳戶名稱。

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

下一個步驟是 tooPrepare hello 儲存體帳戶進行移轉

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

檢查 hello hello 準備使用 Azure PowerShell 或 hello Azure 入口網站的儲存體帳戶的組態。 如果您不準備好進行移轉，而且您想要讓 toogo 後 toohello 舊狀態，請使用下列命令的 hello:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

如果 hello 備妥的 configuration 狀況良好，可以向前移動，並使用下列命令的 hello 認可 hello 資源：

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>後續步驟
* [平台支援移轉的 IaaS 資源從傳統 tooAzure 資源管理員概觀](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [規劃移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [使用 CLI toomigrate IaaS 資源從傳統 tooAzure 資源管理員](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [社群工具，用以協助移轉的 IaaS 資源從傳統 tooAzure 資源管理員](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱最常見的移轉錯誤](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [檢閱 hello 最常見問題集從傳統 tooAzure 資源管理員移轉的 IaaS 資源](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
