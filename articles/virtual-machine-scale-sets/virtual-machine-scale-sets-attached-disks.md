---
title: "虛擬機器規模集附加資料磁碟 aaaAzure |Microsoft 文件"
description: "了解如何將 toouse 附加資料磁碟與虛擬機器規模集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 77b66f80934c0aaf7bb1ad0de00a738052a878ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a>Azure VM 擴展集與連線資料磁碟
Azure [虛擬機器擴展集](/azure/virtual-machine-scale-sets/)現在支援具有連線資料磁碟的虛擬機器。 資料磁碟可以定義為已建立 Azure 受管理磁碟的小數位數的 hello 存放裝置設定檔中。 Hello 唯一可用的 vm 規模集的直接連結存放裝置選項之前 hello OS 磁碟和暫存磁碟機。

> [!NOTE]
>  當您建立具有已定義連接的資料磁碟的擴展集時，您仍然需要 toomount 和格式 hello 磁碟從內 VM toouse 它們 （與針對獨立 Azure Vm）。 便利的方式 toodo，這是 toouse 自訂指令碼延伸模組會呼叫標準的指令碼 toopartition 和格式在 VM 上的所有 hello 資料磁碟。

## <a name="create-a-scale-set-with-attached-data-disks"></a>建立具有連結資料磁碟的擴展集
小數位數設定連接的磁碟與簡單的方式 toocreate 為 toouse hello [Azure CLI](https://github.com/Azure/azure-cli) _vmss 建立_命令。 下列範例中的 hello 分別建立 Azure 資源群組和 10 Ubuntu Vm，各有 2 連接的資料磁碟，50 GB 和 100 GB 的 VM 規模調整集合。
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
請注意該 hello _vmss 建立_命令預設某些設定值，如果您未指定。 toosee hello 可用的選項，您可以覆寫再試一次：
```bash
az vmss create --help
```
另一個方式 toocreate 附加的資料磁碟的設定小數位數是的 toodefine 規模調整集合中的 Azure 資源管理員範本，請包含_dataDisks_ > 一節中 hello _storageProfile_，並部署 hello範本。 hello 範本中 hello 50 GB 和 100 GB 磁碟上述範例會定義如下：
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
您可以看到完整的準備 toodeploy 範例的小數位數組範本以此處定義的附加磁碟： [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data)。

## <a name="adding-a-data-disk-tooan-existing-scale-set"></a>加入資料磁碟 tooan 現有縮放設定
> [!NOTE]
>  您只能再附加資料磁碟 tooa 規模集的已建立具有[Azure 受管理磁碟](./virtual-machine-scale-sets-managed-disks.md)。

您可以加入資料磁碟 tooa VM 規模調整設定使用 Azure CLI _az vmss 磁碟附加_命令。 務必指定尚未使用的 lun。 下列範例 CLI hello 新增 50 GB 的磁碟機 toolun 3:
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

下列 PowerShell 範例 hello 將 50 GB 的磁碟機 toolun 3:
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> 不同的 VM 大小 hello 數字，它們支援的附加磁碟機上有不同的限制。 檢查 hello[虛擬機器大小特性](../virtual-machines/windows/sizes.md)然後再加入新的磁碟。

您也可以新增磁碟，藉由新增新的項目 toohello _dataDisks_屬性在 hello _storageProfile_的小數位數設定定義及套用 hello 變更。 tootest，尋找現有的小數位數組定義在 hello [Azure 資源總管](https://resources.azure.com/)。 選取_編輯_並加入新的磁碟 toohello 清單的資料磁碟。 例如 使用上述的 hello 範例：
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

然後選取_放_tooapply hello 變更 tooyour 規模集。 只要您使用的 VM 大小可支援兩個以上的連結資料磁碟，此範例就可行。

> [!NOTE]
> 當您進行變更 tooa 小數位數設定例如加入或移除資料磁碟的定義，它適用於 tooall 新建立的 Vm，但僅適用於 tooexisting Vm hello _upgradePolicy_屬性設定太 「 自動的 」。 如果設定太"Manual 的 」，您需要 toomanually 套用新模型 tooexisting hello Vm。 您可以在 hello 入口網站使用 hello_更新 AzureRmVmssInstance_ PowerShell 命令，或使用 hello _az vmss 更新執行個體_CLI 命令。

## <a name="adding-pre-populated-data-disks-tooan-existent-scale-set"></a>加入預先填入的資料磁碟 tooan 存在規模集 
> 當您將磁碟 tooan 存在擴展集所設計的模型，、 hello 磁碟將一定要建立空白。 此案例中也包含 hello 規模集所建立的新執行個體。 此行為，是因為 hello scaleset 定義空的資料磁碟。 在訂單存在的小數位數設定模型的 toocreate 預先填入的資料磁碟機，您可以選擇下面兩個選項之一：

* 將資料複製從 hello 的執行個體 0 VM toohello 資料磁碟在 hello 其他 Vm 執行自訂指令碼。
* 受管理的映像與建立 hello OS 磁碟加上 （與 hello 所需的資料） 的資料磁碟並建立新的 scaleset 與 hello 映像。 如此一來，每個新建立的 VM 將會有資料磁碟是 hello scaleset hello 定義中所提供。 因為此定義會參考 tooan 已自訂資料的資料磁碟的映像，在 hello scaleset 上每個虛擬機器會自動出現這些變更。

> hello 方式 toocreate 自訂映像可以在這裡找到：[在 Azure 中建立受管理的映像一般化 vm](/azure/virtual-machines/windows/capture-image-resource/) 

> hello 使用者需要 toocapture hello 執行個體 0 VM 有 hello 必要的資料，並再將該 vhd 用於 hello 影像定義。

## <a name="removing-a-data-disk-from-a-scale-set"></a>從擴展集中移除資料磁碟
您可以使用 Azure CLI _az vmss disk detach_ 命令，從 VM 擴展集中移除資料磁碟。 例如 hello 下列命令會移除在 lun 2 定義的 hello 磁碟：
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
您也可以從在擴展集 hello，移除項目移除磁碟的同樣_dataDisks_屬性在 hello _storageProfile_及套用 hello 變更。 

## <a name="additional-notes"></a>其他注意事項
支援 Azure 受管理磁碟和小數位數設定連接的資料磁碟的功能在應用程式開發介面版本[ _2016年-04-30-預覽_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json)或更新版本的 hello Microsoft.Compute API。

在 hello 初始實作中的小數位數設定的附加的磁碟支援，您無法附加或卸離從個別 Vm 規模集中的資料磁碟。

Azure 入口網站對於擴展集中連結資料磁碟的支援一開始就有限制。 您可以使用 Azure 範本的需求，根據 CLI、 PowerShell、 Sdk 和 REST API toomanage 連接的磁碟。


