---
title: "Azure 受管理備份磁碟上的 aaaCopy |Microsoft 文件"
description: "了解如何 toocreate 回最新或疑難排解磁碟 Azure 受管理磁碟 toouse 一份問題。"
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>使用受控快照集建立 VHD 的複本並儲存為 Azure 受控磁碟
取得備份的受管理磁碟的快照或從 hello 快照集建立受管理磁碟並將它附加 tooa 測試虛擬機器 tootroubleshoot。 受控快照集是 VM 受控磁碟的完整時間點複本。 它會建立 VHD 的唯讀複本，而且根據預設儲存為標準受控磁碟。 

如需價格的詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/managed-disks/)。 <!--Add link tootopic or blog post that explains managed disks. -->

使用 Azure 入口網站或 hello Azure CLI 2.0 tootake 任一 hello hello 受管理磁碟的快照集。

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>使用 Azure CLI 2.0 tootake 快照集

> [!NOTE] 
> hello 下列範例要求 hello Azure CLI 2.0 安裝並登入您的 Azure 帳戶。

hello 下列步驟顯示如何 tooobtain 並採取快照集的受管理的作業系統磁碟使用 hello`az snapshot create`命令與 hello`--source-disk`參數。 hello 下列範例假設有呼叫 VM`myVM`建立的受管理的作業系統磁碟在 hello`myResourceGroup`資源群組。

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

hello 輸出應該看起來像這樣：

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>使用 Azure 入口網站 tootake 快照集 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從開始 hello 左上方，按一下**新增**並搜尋**快照**。
3. 在 hello 快照刀鋒視窗中，按一下 **建立**。
4. 輸入**名稱**hello 快照集。
5. 選取現有[資源群組](../../azure-resource-manager/resource-group-overview.md#resource-groups)或新的型別 hello 名稱。 
6. 選取 Azure 資料中心的 [位置]。  
7. 如**來源磁碟**，選取 hello toosnapshot 管理的磁碟。
8. 選取 hello**帳戶類型**toouse toostore hello 快照集。 除非需要儲存在高效能磁碟上，否則建議選取 **Standard_LRS**。
9. 按一下 [建立] 。

如果您規劃 toouse hello 快照 toocreate 受管理的磁碟，並將它附加 toobe 高執行所需的 VM，使用 hello 參數`--sku Premium_LRS`以 hello`az snapshot create`命令。 這會建立 hello 快照集，使它儲存為 Premium 管理磁碟。 進階受控磁碟的效能比較好，因為它們是固態硬碟 (SSD)，但成本高於標準磁碟 (HDD)。


