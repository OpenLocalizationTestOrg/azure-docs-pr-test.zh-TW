---
title: "aaaUpgrade Azure 虛擬機器規模集 |Microsoft 文件"
description: "升級 Azure 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>升級虛擬機器擴展集
本文描述您可以制定 OS 更新 tooan Azure 虛擬機器擴展集完全不需要停機。 在此情況下，作業系統更新包括變更 hello 版本或 SKU 的 hello OS 或變更 hello 的自訂映像的 URI。 在不需停機的情況下進行更新意謂著一次更新一部虛擬機器，或依群組 (例如一次一個容錯網域) 更新虛擬機器，而不是全部一起更新。 透過這種方式，任何非升級中的虛擬機器都可繼續執行。

tooavoid 模稜兩可，讓我們來區別四種類型的作業系統更新，您可能會想 tooperform:

* 變更 hello 版本或平台映像的 SKU。 例如，變更 Ubuntu 14.04.201506100 14.04.2-LTS 版本 too14.04.201507060，或變更 hello Ubuntu 15.10/最新 SKU too16.04.0-LTS/latest。 本文涵蓋此案例。
* 變更 hello 指向 tooa 新版本，您所建立的自訂映像的 URI (**屬性** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **映像** > **uri**)。 本文涵蓋此案例。
* 變更使用 Azure 受管理的磁碟建立規模集的 hello 影像參考。
* 修補程式的虛擬機器內 hello 從作業系統 （這個範例包含安裝的安全性修補程式和執行 Windows Update）。 支援此案例，但本文並未涵蓋此案例。

這裡未涵蓋隨 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) 一起部署的虛擬機器擴展集。 如需修補 Service Fabric 的詳細資訊，請參閱[在 Service Fabric 叢集中修補 Windows OS](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)。

hello 基本順序變更 hello OS 版本/平台映像的 SKU 或 hello URI 自訂影像看起來像這樣：

1. 收到 hello 虛擬機器擴充集模型。
2. 變更 hello 版本、 SKU、 映像參考或 hello 模型中的 URI 值。
3. 更新 hello 模型。
4. 請勿*manualUpgrade*呼叫 hello hello 規模集中的虛擬機器上。 此步驟中，才會相關如果*upgradePolicy*設定得**手動**集中您的標尺。 如果設定太**自動**，hello 的所有虛擬機器都升級，因此會造成停機時間。

請注意這項資訊，我們來看看您無法更新在擴展集在 PowerShell 中，而藉由使用 REST API hello hello 版本的方式。 這些範例中涵蓋的平台映像的 hello 大小寫，但本文章提供足夠的資訊讓您 tooadapt 此程序 tooa 自訂映像。

## <a name="powershell"></a>PowerShell
這個範例會更新 Windows 虛擬機器規模集 （建立 toohello 新版 4.0.20160229。 在更新之後 hello 模型，則它會更新一個虛擬機器執行個體一次。

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

如果您要更新 hello URI，而不是變更平台映像版本的自訂映像，取代 hello 「 組 hello 新的版本 」 將更新的命令列 hello 來源影像 URI。 例如，如果 hello 規模集不使用 Azure 受管理的磁碟建立的 hello 更新看起來會像這樣：

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

如果自訂映像基礎規模調整集合會建立使用 Azure 受管理的磁碟，則會更新 hello 影像參考。 例如：

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>hello REST API
以下是幾個使用 hello Azure REST API tooroll OS 版本更新的 Python 範例。 同時使用 hello 輕量型[azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API 的包裝函式的函式 toodo hello 標尺上 GET 的程式庫設定模型的 PUT 與更新的模型。 它們也查看虛擬機器執行個體檢視 tooidentify hello 虛擬機器的更新網域。

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools)是否 Python 指令碼使用 tooroll 出 OS 升級 tooa 執行虛擬機器擴展集一次一個更新網域。

![選擇虛擬機器或更新網域的 vmssupgrade 指令碼](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

此指令碼可讓您選擇特定虛擬機器 tooupdate 或指定的更新網域。 它支援變更平台映像版本，或變更 hello 的自訂映像的 URI。

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 是虛擬機器擴展集的一般用途編輯器，能夠以熱力圖的形式顯示虛擬機器狀態，其中一個資料列代表一個更新網域。 在其他方面，您可以擴展集 hello 模型使用新的版本、 SKU 或更新自訂映像的 URI，，，然後挑選容錯網域 tooupgrade。 當您這樣做時，所有更新網域中的 hello 虛擬機器將都會升級的 toohello 新模型。 或者，您可以根據您選擇的 hello 批次大小的輪流升級。  

hello 下列螢幕擷取畫面顯示 Ubuntu 14.04 2LTS 14.04.201507060 版本設定標尺的模型。 更多選擇已加入 toothis 工具執行這個螢幕擷取畫面之後。

![Ubuntu 14.04-2LTS 的擴展集 vmsseditor 模型](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

按一下 之後**升級**然後**取得詳細資料**，UD 0 中的虛擬機器啟動 tooupdate。

![顯示更新進行中的 vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

