---
title: "包含 VM 擴充功能的 Azure 資源群組 aaaExporting |Microsoft 文件"
description: "匯出包含虛擬機器擴充功能的 Resource Manager 範本。"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>匯出包含 VM 擴充功能的資源群組

Azure 資源群組可以匯出到之後會重新部署的新 Resource Manager 範本中。 hello 匯出程序會解譯現有的資源，並建立 Resource Manager 範本的部署時導致類似的資源群組。 使用 hello 資源群組匯出選項，針對包含虛擬機器擴充功能的資源群組時，數個項目需要 toobe 視為例如擴充功能的相容性，而且保護設定。

關於虛擬機器擴充功能，包括一份 hello 資源群組匯出程序的運作方式本文件詳述支援的延伸模組，並以處理的詳細資訊保護的資料。

## <a name="supported-virtual-machine-extensions"></a>支援的虛擬機器擴充功能

有許多虛擬機器擴充功能可以使用。 並非所有擴充功能可以匯出成資源管理員範本使用 hello"自動化指令碼 」 功能。 如果不支援虛擬機器擴充功能，它會需要 toobe 手動放回 hello 匯出的範本。

hello 下列延伸項目可以匯出與 hello 自動化指令碼功能。

| 分機 ||||
|---|---|---|---|
| Acronis Backup | Datadog Windows Agent | OS Patching For Linux | VM Snapshot Linux
| Acronis Backup Linux | Docker 延伸模組 | Puppet Agent |
| Bg Info | DSC 延伸模組 | Site 24x7 Apm Insight |
| BMC CTM Agent Linux | Dynatrace Linux | Site 24x7 Linux Server |
| BMC CTM Agent Windows | Dynatrace Windows | Site 24x7 Windows Server |
| Chef Client | HPE Security Application Defender | Trend Micro DSA |
| Custom Script | IaaS Antimalware | Trend Micro DSA Linux |
| 自訂指令碼延伸模組 | IaaS Diagnostics | VM Access For Linux |
| Custom Script for Linux | Linux Chef Client | VM Access For Linux |
| Datadog Linux Agent | Linux Diagnostic | VM Snapshot |

## <a name="export-hello-resource-group"></a>匯出 hello 資源群組

tooexport 成可重複使用範本，請完成下列步驟的 hello 資源群組：

1. 登入 toohello Azure 入口網站
2. 在 hello 中樞功能表中，按一下 資源群組
3. 從 hello 清單中選取 hello 目標資源群組
4. 在 hello 資源群組刀鋒視窗中，按一下 自動化指令碼

![匯出範本](./media/extensions-export-templates/template-export.png)

hello Azure Resource Manager 不僅指令碼會產生資源管理員範本、 參數檔案，以及數個範例部署指令碼，例如 PowerShell 和 Azure CLI。 此時，hello 匯出的範本可以使用下載 hello 下載 按鈕，為新範本 toohello 範本程式庫，加入或重新部署使用 hello 部署按鈕。

## <a name="configure-protected-settings"></a>設定受保護的設定

許多 Azure 虛擬機器擴充功能都包含受保護的設定組態，以加密敏感性資料，例如認證及組態字串。 受保護的設定不會匯出與 hello 自動化指令碼。 如果需要，受保護的設定需要重新插入 hello toobe 匯出樣板化。

### <a name="step-1---remove-template-parameter"></a>步驟 1 - 移除範本參數

Hello 匯出資源群組時，單一的樣板參數建立 tooprovide 時值 toohello 匯出受保護的設定。 您可移除此參數。 tooremove hello 參數，查看 hello 參數清單，並刪除 hello 參數，看起來類似 toothis JSON 範例。

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>步驟 2 - 取得受保護的設定屬性

因為每個受保護的設定有一組必要的屬性，這些屬性的清單需要 toobe 蒐集。 Hello 受保護的設定組態的每個參數可以在 hello [GitHub 上的 Azure 資源管理員結構描述](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json)。 這個結構描述僅包含 hello hello 延伸模組這份文件 hello 概觀 > 中列出的參數集。 

從內 hello 結構描述儲存機制中，搜尋所需的 hello 延伸模組，此範例中`IaaSDiagnostics`。 一次 hello 延伸`protectedSettings`已找到物件，請注意，每個參數。 在 hello 範例中的 hello`IaasDiagnostic`延伸模組，hello 需要參數`storageAccountName`， `storageAccountKey`，和`storageAccountEndPoint`。

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>步驟 3-重新建立受保護的 hello 組態

Hello 匯出的範本，搜尋`protectedSettings`並取代，其中包含所需的 hello 延伸模組參數和值，針對每個新的 hello 匯出受保護的設定物件。

在 hello 範例中的 hello`IaasDiagnostic`延伸模組，hello 新的受保護的設定組態看起來會像下列範例中的 hello:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

hello 最終的擴充資源看起來類似 toohello 下列 JSON 範例：

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

如果使用範本參數 tooprovide 屬性值，這些會需要建立 toobe。 當受保護的設定值，請建立範本參數，請確定 toouse hello`SecureString`參數型別，以便保護機密值。 如需使用參數的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)。

在 hello 範例中的 hello`IaasDiagnostic`延伸模組，會在 hello Resource Manager 範本 hello 參數 區段中建立 hello 下列參數。

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

此時，您可以使用範本部署的任何方法來部署 hello 範本。
