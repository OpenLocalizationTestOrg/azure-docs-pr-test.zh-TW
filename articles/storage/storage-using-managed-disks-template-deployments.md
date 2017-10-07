---
title: "aaaUsing 管理的 Azure Resource Manager 範本中的磁碟 |Microsoft 文件"
description: "Toouse misks Azure Resource Manager 範本中的管理方式的詳細資料"
services: storage
documentationcenter: 
author: jboeshart
manager: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/01/2017
ms.author: jaboes
ms.openlocfilehash: ea83f4ed11acfd8f642dbc8331fa8cf077ef577c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>在 Azure Resource Manager 範本中使用受控磁碟

本文件逐步 hello managed 和 unmanaged 磁碟時使用 Azure Resource Manager 範本 tooprovision 虛擬機器之間的差異。 這將協助您使用未受管理的磁碟 toomanaged 磁碟 tooupdate 現有範本。 如需參考，我們使用 hello [101 vm-簡單 windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)範本做為指南。 您可以看到同時使用 hello 範本[管理磁碟](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json)和先前版本使用[unmanaged 磁碟](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json)如果您想要 toodirectly 加以比較。

## <a name="unmanaged-disks-template-formatting"></a>非受控磁碟範本格式

toobegin，我們看看如何 unmanaged 磁碟在部署。 在建立時未受管理的磁碟，您需要儲存體帳戶 toohold hello VHD 檔案。 您可以建立新儲存體帳戶，或使用現有儲存體帳戶。 這篇文章將示範如何 toocreate 新的儲存體帳戶。 tooaccomplish，您需要在 hello 資源區塊中的儲存體帳戶資源，如下所示。

```
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2016-01-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {}
}
```

在 hello 虛擬機器物件中，我們需要 hello hello 的虛擬機器先建立儲存體帳戶 tooensure 的相依性。 在 hello`storageProfile`區段，然後指定 hello hello VHD 的位置，其參考 hello 儲存體帳戶，以及 hello OS 磁碟和任何資料磁碟所需的完整 URI。 

```
{
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "name": "osdisk",
                "vhd": {
                    "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/osdisk.vhd')]"
                },
                "caching": "ReadWrite",
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "name": "datadisk1",
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "vhd": {
                        "uri": "[concat(reference(resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))).primaryEndpoints.blob, 'vhds/datadisk1.vhd')]"
                    },
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

## <a name="managed-disks-template-formatting"></a>受控磁碟範本格式

Azure 受管理磁碟 hello 磁碟會成為最上層資源與 hello 使用者建立的儲存體帳戶 toobe 已不再需要。 受管理的磁碟第一次會暴露在 hello `2016-04-30-preview` API 版本，它們適用於所有後續的 API 版本，而現在 hello 預設磁碟類型。 hello 下列各節逐一查核 hello 預設設定，並詳細說明如何 toofurther 自訂您的磁碟。

> [!NOTE]
> 建議 toouse 應用程式開發介面版本晚於`2016-04-30-preview`之間的重大變更與`2016-04-30-preview`和`2017-03-30`。
>
>

### <a name="default-managed-disk-settings"></a>預設的受控磁碟設定

toocreate VM 使用受管理磁碟時，您不再需要 toocreate hello 儲存體帳戶資源，而且可以更新您的虛擬機器的資源，如下所示。 特別注意該 hello`apiVersion`反映`2017-03-30`和 hello`osDisk`和`dataDisks`不再參考 tooa 特定 hello VHD URI。 當部署但不指定其他屬性，將會使用 hello 磁碟[標準 LRS 儲存體](storage-redundancy.md)。 如果未指定名稱，它可接受的 hello 格式`<VMName>_OsDisk_1_<randomstring>`hello OS 磁碟和`<VMName>_disk<#>_<randomstring>`每個資料磁碟。 根據預設，Azure 磁碟加密已停用;快取是 hello OS 磁碟和任何資料磁碟的讀取/寫入。 您可能會注意到在 hello 面範例中仍有儲存體帳戶的相依性，這只適用於診斷的存放裝置，而且不需要使用磁碟儲存體也一樣。

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "diskSizeGB": 1023,
                    "lun": 0,
                    "createOption": "Empty"
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="using-a-top-level-managed-disk-resource"></a>使用最上層受控磁碟資源

當做 hello 虛擬機器物件中的替代 toospecifying hello 磁碟設定，您可以建立最上層的磁碟資源，並附加做為建立 hello 虛擬機器的一部分。 例如，我們可以建立，如下所示 toouse 當做資料磁碟的磁碟資源。

```
{
    "type": "Microsoft.Compute/disks",
    "name": "[concat(variables('vmName'),'-datadisk1')]",
    "apiVersion": "2017-03-30",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "Standard_LRS"
    },
    "properties": {
        "creationData": {
            "createOption": "Empty"
        },
        "diskSizeGB": 1023
    }
}
```

在 hello VM 物件中，我們就可以參考此連接的磁碟物件 toobe。 指定 hello 資源識別碼 hello 管理我們在 hello 建立的磁碟`managedDisk`屬性允許在建立 VM 的 hello hello 磁碟的 hello 附件。 請注意該 hello `apiVersion` hello VM 資源設定太`2017-03-30`。 也請注意我們已在建立 VM 之前已成功建立 hello 磁碟資源 tooensure 建立相依性。 

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[resourceId('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[resourceId('Microsoft.Network/networkInterfaces/', variables('nicName'))]",
        "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
    ],
    "properties": {
        "hardwareProfile": {...},
        "osProfile": {...},
        "storageProfile": {
            "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "[parameters('windowsOSVersion')]",
                "version": "latest"
            },
            "osDisk": {
                "createOption": "FromImage"
            },
            "dataDisks": [
                {
                    "lun": 0,
                    "name": "[concat(variables('vmName'),'-datadisk1')]",
                    "createOption": "attach",
                    "managedDisk": {
                        "id": "[resourceId('Microsoft.Compute/disks/', concat(variables('vmName'),'-datadisk1'))]"
                    }
                }
            ]
        },
        "networkProfile": {...},
        "diagnosticsProfile": {...}
    }
}
```

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>為使用受控磁碟的 VM 建立受控可用性設定組

toocreate 管理可用性集合若具有 Vm 使用受管理的磁碟，新增 hello`sku`物件 toohello 可用性設定資源，並設定 hello`name`屬性太`Aligned`。 這可確保每個 VM 的 hello 磁碟與彼此 tooavoid 單一失敗點完全隔離。 也請注意該 hello `apiVersion` hello 可用性集資源設定得`2017-03-30`。

```
{
    "apiVersion": "2017-03-30",
    "type": "Microsoft.Compute/availabilitySets",
    "location": "[resourceGroup().location]",
    "name": "[variables('avSetName')]",
    "properties": {
        "PlatformUpdateDomainCount": 3,
        "PlatformFaultDomainCount": 2
    },
    "sku": {
        "name": "Aligned"
    }
}
```

### <a name="additional-scenarios-and-customizations"></a>其他案例和自訂

toofind hello 的 REST API 規格的完整資訊，請檢閱 hello[建立受管理的磁碟 REST API 文件](/rest/api/manageddisks/disks/disks-create-or-update)。 您會發現其他案例，以及預設值與可接受的值可以是送出的 toohello API，透過範本部署。 

## <a name="next-steps"></a>後續步驟

* 如需完整的範本使用受管理的磁碟，請造訪 hello 下列 Azure 快速入門儲存機制的連結。
    * [使用受控磁碟的 Windows VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) \(英文\)
    * [使用受控磁碟的 Linux VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux) \(英文\)
    * [受控磁碟範本的完整清單](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md) \(英文\)
* 請瀏覽 hello [Azure 受管理的磁碟概觀](storage-managed-disks-overview.md)深入了解文件 toolearn 管理的磁碟。
* 檢閱虛擬機器資源的 hello 範本參考文件瀏覽 hello [Microsoft.Compute/virtualMachines 範本參考](/templates/microsoft.compute/virtualmachines)文件。
* 檢閱磁碟資源的 hello 範本參考文件瀏覽 hello [Microsoft.Compute/disks 範本參考](/templates/microsoft.compute/disks)文件。
 
