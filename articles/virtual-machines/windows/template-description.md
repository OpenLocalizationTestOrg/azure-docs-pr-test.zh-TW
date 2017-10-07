---
title: "在 Azure 資源管理員範本 aaaVirtual 機器 |Microsoft Azure"
description: "深入了解 Azure Resource Manager 範本中定義 hello 虛擬機器資源的方式。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Azure Resource Manager 範本中的虛擬機器

本文說明 Azure Resource Manager 範本套用 toovirtual 機器中的各個的層面。 本文不會說明建立虛擬機器的完整範本；您需要儲存體帳戶、網路介面、公用 IP 位址與虛擬網路的資源定義。 如需有關如何一起定義這些資源的詳細資訊，請參閱 hello[資源管理員範本逐步解說](../../azure-resource-manager/resource-manager-template-walkthrough.md)。

有許多[hello 組件庫中的範本](https://azure.microsoft.com/documentation/templates/?term=VM)包括 hello VM 資源。 此處並未說明可以包含在範本中的所有項目。

此範例顯示用來建立指定數目之 VM 範本的一般資源區段︰

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>此範例仰賴先前建立的儲存體帳戶。 您可以藉由部署從 hello 範本建立 hello 儲存體帳戶。 hello 範例也依賴網路介面和其相依的資源會 hello 範本中定義的。 這些資源不會顯示在 hello 範例。
>
>

## <a name="api-version"></a>API 版本

當您部署使用範本的資源時，您有 toospecify hello API toouse 的版本。 hello 範例顯示 hello 虛擬機器資源使用此 api 版本項目：

```
"apiVersion": "2016-04-30-preview",
```

hello 版的 hello 應用程式開發介面，您在範本中指定會影響您可以在 hello 範本中定義的屬性。 一般情況下，您應該在建立範本時選取 hello 最新的 API 版本。 對於現有的範本，您可以決定是否 toocontinue 使用較舊的應用程式開發介面版本，或是更新 hello 最新版本 tootake 利用新功能的範本。

使用這些機會，以取得最新 API 版本 hello:

- REST API - [列出所有資源提供者](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Azure CLI 2.0 - [az 提供者顯示](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>參數和變數

[參數](../../resource-group-authoring-templates.md)讓您輕鬆為您 hello 範本 toospecify 值時執行它。 Hello 範例中，會使用此參數 > 一節：

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

當您部署的 hello 範例範本時，您輸入值 hello 名稱和密碼 hello 系統管理員帳戶的每個 VM hello 數目及 Vm toocreate 上。 您可以在 hello 範本時，管理的個別檔案中指定參數值，或提供值，當系統提示您 hello 選擇。

[變數](../../resource-group-authoring-templates.md)讓您輕鬆為您 tooset 值在整個重複使用或，可能會隨時間變更的 hello 範本中。 Hello 範例中，會使用此變數區段：

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

當您部署 hello 範例範本時，變數值會用於 hello 名稱和識別碼 hello 先前建立的儲存體帳戶。 變數也會使用的 tooprovide hello hello 診斷延伸模組的設定。 使用 hello[最佳作法來建立 Azure 資源管理員範本](../../resource-manager-template-best-practices.md)toohelp 您決定要如何 toostructure hello 參數和變數在範本中。

## <a name="resource-loops"></a>資源迴圈

您的應用程式需要一部以上的虛擬機器時，您可以在範本中使用複製項目。 此選擇性項目迴圈建立 hello 數目指定為參數的 Vm:

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

此外，請注意，在 hello 迴圈索引的 hello 範例是指定一些 hello hello 資源的值時使用。 例如，如果您輸入的三個 hello 名稱 hello 作業系統磁碟的執行個體計數為 myOSDisk1、 myOSDisk2 和 myOSDisk3:

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>這個範例會使用受管理的磁碟 hello 虛擬機器。
>
>

請記住，在 hello 範本中建立一個資源的迴圈可能會要求您 toouse hello 迴圈時建立或存取其他資源。 例如，多個 Vm 無法使用相同網路介面，因此如果您的範本執行迴圈，建立三個 Vm，它也必須迴圈建立三個網路介面的 hello。 Hello 迴圈索引指派網路介面 tooa VM 時，會使用的 tooidentify 它：

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>相依項目

最多資源依存於其他資源 toowork 正確。 虛擬機器必須與虛擬網路和 toodo 它需要的網路介面相關聯。 hello [dependsOn](../../resource-group-define-dependencies.md)項目，則使用的 toomake 確定該 hello 網路介面已準備好 toobe 之前建立 hello Vm 使用：

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager 會以平行方式部署任何不依存於另一個要部署資源的資源。 設定相依性時請謹慎，因為您可能會指定非必要相依性而不小心降低您的部署。 相依性可以鏈結多個資源。 例如，hello 網路介面取決於 hello 公用 IP 位址及虛擬網路資源。

如何知道是否需要相依性？ 查看您設定 hello 範本中的 hello 值。 如果 hello 虛擬機器的資源定義中的項目點，部署在 hello tooanother 資源相同的範本，您需要的相依性。 例如，範例虛擬機器會定義網路設定檔︰

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset hello 網路介面必須存在這個屬性。 因此，您需要相依性。 其他資源 （父系） 內定義一項資源 （子系） 時，也需要 tooset 相依性。 比方說，hello 診斷設定和自訂指令碼延伸模組是兩者都定義為 hello 虛擬機器的子資源。 它們之後，才能建立 hello 虛擬機器存在。 因此，這兩個資源都會標示成相依於 hello 虛擬機器。

## <a name="profiles"></a>設定檔

定義虛擬機器資源時，會使用數個設定檔項目。 某些是必要的而有些則是選擇性。 例如，hello hardwareProfile、 osProfile、 storageProfile 和 networkProfile 元素皆為必要，但是 hello diagnosticsProfile 為選擇性。 這些設定檔會定義設定，例如︰
   
- [大小](sizes.md)
- [名稱](/architecture/best-practices/naming-conventions)和認證
- 磁碟和[作業系統設定](cli-ps-findimage.md)
- [網路介面](../../virtual-network/virtual-networks-multiple-nics.md) 
- 開機診斷

## <a name="disks-and-images"></a>磁碟和映像
   
在 Azure 中，VHD 檔案可以代表[磁碟或映像](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 特製化的 toobe 特定 VM 的 vhd 檔案中的 hello 作業系統時，它是參考的 tooas 磁碟。 當一般化的 vhd 檔案中的 hello 作業系統 toobe 用 toocreate 許多 Vm，參照的 tooas 映像。   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>從平台映像建立新的虛擬機器和新的磁碟

當您建立 VM 時，您必須決定哪些作業系統 toouse。 hello imageReference 項目是使用的 toodefine hello 作業系統的新 VM。 hello 範例顯示 Windows 伺服器作業系統的定義：

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

如果您想 toocreate Linux 作業系統，您可以使用此定義：

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Hello 作業系統磁碟的組態設定會指派與 hello osDisk 項目。 hello 範例會定義新的受管理的磁碟以 hello 太快取模式組**ReadWrite** ，而且正在從建立該 hello 磁碟[平台映像](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>從現有受控磁碟建立新的虛擬機器

如果您想從現有的磁碟 toocreate 虛擬機器，移除 hello imageReference 和 hello osProfile 項目，並定義這些磁碟設定：

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>從受控映像建立新的虛擬機器

如果您想 toocreate 受管理的映像中的虛擬機器，變更 hello imageReference 項目，並定義這些磁碟設定：

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>連接資料磁碟

您可以選擇性地加入資料磁碟 toohello Vm。 hello[的磁碟數目](sizes.md)hello 您使用的作業系統磁碟大小而定。 以 hello hello Vm 大小會設定 tooStandard_DS1_v2，hello toohello 它們是兩個可加入的資料磁碟數目上限。 在 hello 範例中，一個受管理的資料磁碟新增 tooeach VM:

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>擴充功能

雖然[延伸](extensions-features.md)是不同的資源，而是 tooVMs 緊密繫結。 可以加入擴充功能，為 hello VM 的子資源，或為個別的資源。 hello 範例顯示 hello[診斷延伸模組](extensions-diagnostics-template.md)加入 toohello Vm:

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Hello storageName 變數和 hello 診斷變數 tooprovide 值，則會使用此延伸模組的資源。 如果您想收集此延伸模組的 toochange hello 資料時，您可以加入更多效能計數器 toohello wadperfcounters 變數。 您也可以選擇 tooput hello 診斷資料至不同的儲存體帳戶比 hello VM 磁碟的儲存位置。

您可以安裝在 VM 的許多擴充功能，但是最有用的 hello 可能 hello[自訂指令碼擴充](extensions-customscript.md)。 在 hello 範例中，名為 start.ps1 PowerShell 指令碼執行每個 VM 上第一次啟動時：

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

hello start.ps1 指令碼可以完成多的組態工作。 例如，未初始化 hello 資料磁碟加入 toohello Vm 在 hello 範例;您可以使用自訂指令碼 tooinitialize 它們。 如果您有多個啟動工作 toodo，您可以使用 hello start.ps1 檔案 toocall 其他 PowerShell 指令碼在 Azure 儲存體。 hello 範例會使用 PowerShell，但您可以使用任何指令碼的方法可在您使用的 hello 作業系統上。

您可以看到 hello 的 hello 入口網站中的 hello 延伸模組設定 hello 安裝擴充功能的狀態：

![取得擴充功能狀態](./media/template-description/virtual-machines-show-extensions.png)

您也可以取得延伸模組資訊使用 hello **Get AzureRmVMExtension** PowerShell 命令，hello **vm 延伸模組取得**Azure CLI 2.0 命令或使用 hello**取得延伸模組的資訊** REST API。

## <a name="deployments"></a>部署

當您部署的範本，為群組和自動部署 Azure 曲目 hello 資源時，會指派名稱 toothis 部署群組。 hello 部署的 hello 名稱是 hello 與 hello hello 範本名稱相同。

如果您了解 hello 狀態 hello 部署中的資源，您可以使用 hello 資源群組 刀鋒視窗中 hello Azure 入口網站：

![取得部署資訊](./media/template-description/virtual-machines-deployment-info.png)
    
它不是問題 toouse hello 相同範本 toocreate 資源或 tooupdate 現有資源。 當您使用命令 toodeploy 範本時，您擁有 hello 機會 toosay 其中[模式](../../resource-group-template-deploy.md)想 toouse。 hello 模式可以設定 tooeither**完成**或**Incremental**。 hello 預設值為 toodo 累加式更新。 小心使用 hello**完成**模式因為您可能會不小心刪除資源。 當您將 hello 模式太**完成**，資源管理員就會刪除 hello 資源群組不在 hello 範本中的任何資源。

## <a name="next-steps"></a>後續步驟

- 使用[編寫 Azure Resource Manager 範本](../../resource-group-authoring-templates.md)來建立專屬範本。
- 部署使用所建立的 hello 範本[使用資源管理員範本建立 Windows 虛擬機器](ps-template.md)。
- 了解如何 toomanage hello 您藉由檢視所建立的 Vm[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
