---
title: "在 Azure 中的 Linux Vm 上的 aaaRun 自訂指令碼 |Microsoft 文件"
description: "使用 hello 自訂指令碼擴充自動化 Linux VM 組態工作"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>使用 Azure 自訂指令碼擴充的 hello 與 Linux 虛擬機器
hello 自訂指令碼擴充功能下載並在 Azure 虛擬機器上執行指令碼。 此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。 可以下載自 Azure 儲存體或其他可存取網際網路的位置，或提供 toohello 延伸模組執行階段指令碼。 hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。

如何 toouse hello 自訂指令碼擴充，從本文件詳述 hello Azure CLI 和 Azure 資源管理員範本，以及詳細的疑難排解步驟，在 Linux 系統上。

## <a name="extension-configuration"></a>擴充功能組態
hello 自訂指令碼延伸模組組態會指定指令碼位置和執行 hello 命令 toobe 等。 此組態可以儲存在組態檔中指定 hello 命令列上，或在 Azure Resource Manager 範本。 可以在受保護組態中，其加密，並只能解密 hello 虛擬機器內儲存機密資料。 hello 受保護的組態時，hello 執行命令包含機密資料，例如密碼。

### <a name="public-configuration"></a>公用組態
結構描述：

**注意** - 屬性名稱會區分大小寫。 如下所示 tooavoid 部署問題，請使用 hello 名稱。

* **commandToExecute**: (需要，string) hello 進入點指令碼 tooexecute
* **fileUris**: （選擇性，字串陣列），檔案 toobe hello Url 的下載。
* **時間戳記**（選擇性，整數） 使用此欄位只有 tootrigger hello 指令碼的重新執行，藉由變更這個欄位的值。

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>受保護的組態
結構描述：

**注意** - 屬性名稱會區分大小寫。 如下所示 tooavoid 部署問題，請使用 hello 名稱。

* **commandToExecute**: (選擇性，string) hello 進入點指令碼 tooexecute。 如果您的命令包含機密資料 (例如密碼)，請改用此欄位。
* **storageAccountName**: (選擇性，string) hello 儲存體帳戶名稱。 如果您指定儲存體證明資料，則所有 fileUri 都必須是 Azure Blob 的 URL。
* **storageAccountKey**: (選擇性，string) hello 儲存體帳戶存取金鑰。

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>Azure CLI
當使用 hello Azure CLI toorun hello 自訂指令碼擴充，建立組態檔或檔案，其中包含在最小 hello 檔案 uri，以及 hello 指令碼執行命令。

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

選擇性地 hello 設定可以 hello 命令中指定，以 JSON 格式字串。 這可讓 hello 組態 toobe 指定在執行期間並不使用個別的組態檔案。

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Azure CLI 範例

**範例 1** - 含指令檔的公用組態。

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**範例 2** - 不含指令檔的公用組態。

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**範例 3** -公用組態檔是使用的 toospecify hello 指令碼檔案的 URI，且受保護的組態檔是使用的 toospecify hello 命令 toobe 執行。

公用組態檔：

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

受保護的組態檔：  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Azure CLI 命令：

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Resource Manager 範本
可以在虛擬機器部署時間使用資源管理員範本執行 hello Azure 自訂指令碼擴充。 因此，toodo 中加入格式正確的 JSON toohello 部署範本。

### <a name="resource-manager-examples"></a>Resource Manager 範例
**範例 1** - 公用組態。

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

**範例 2** - 受保護組態中的執行命令。

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

請參閱 hello.Net Core Music Store 示範如需完整的範例-[音樂存放區示範](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db)。

## <a name="troubleshooting"></a>疑難排解
Hello 自訂指令碼延伸執行時，hello 指令碼建立，或下載到目錄類似 toohello，下列範例。 hello 命令輸出也會儲存到此目錄中`stdout`和`stderr`檔案。

```bash
/var/lib/waagent/custom-script/download/0/
```

hello Azure 指令碼延伸模組會產生記錄檔，可以在這裡找到。

```bash
/var/log/azure/custom-script/handler.log
```

hello hello 自訂指令碼延伸執行狀態也可以擷取與 hello Azure CLI。

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

hello 輸出看起來類似下列文字的 hello:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>後續步驟
如需有關其他「VM 指令碼擴充功能」的資訊，請參閱 [適用於 Linux 的 Azure 指令碼擴充功能概觀](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

