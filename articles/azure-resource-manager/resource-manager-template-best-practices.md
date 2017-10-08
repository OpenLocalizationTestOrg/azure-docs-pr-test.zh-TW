---
title: "建立資源管理員範本 aaaBest 作法 |Microsoft 文件"
description: "簡化 Azure Resource Manager 範本的指導方針。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a>建立 Azure Resource Manager 範本的最佳做法
這些指導方針可協助您建立可靠且容易 toouse Azure Resource Manager 範本。 hello 指導方針是只建議。 除了另有註明外，它們並非必要項目。 您的案例可能需要 hello 其中一種方法或範例。

## <a name="resource-names"></a>資源名稱
通常，您會使用 Resource Manager 中的三種資源名稱︰

* 必須是唯一的資源名稱。
* 資源名稱不需要 toobe 唯一的但您選擇的 tooprovide 的名稱，可協助您找出內容為基礎的資源。
* 可以是一般的資源名稱。

 如需有關資源名稱限制的詳細資訊，請參閱 [Recommended naming conventions for Azure resources (Azure 資源的建議命名慣例)](../guidance/guidance-naming-conventions.md)。

### <a name="unique-resource-names"></a>唯一的資源名稱
您必須為任何有資料存取端點的資源類型，提供唯一的資源名稱。 一些需要唯一名稱的常見資源類型包括︰

* Azure 儲存體<sup>1</sup> 
* Azure App Service 中的 Web Apps 功能
* SQL Server
* Azure 金鑰保存庫
* Azure Redis 快取
* Azure Batch
* Azure 流量管理員
* Azure 搜尋服務
* Azure HDInsight

<sup>1</sup> 儲存體帳戶名稱也必須是小寫、長度不超過 24 個字元，而且沒有任何連字號。

如果您提供的資源名稱參數，您必須提供唯一的名稱，當您部署的 hello 資源。 （選擇性） 您可以建立的變數，會使用 hello [uniqueString()](resource-group-template-functions-string.md#uniquestring)函式 toogenerate 名稱。 

您也可能會想 tooadd 前置詞或後置詞 toohello **uniqueString**結果。 修改 hello 唯一名稱可協助您更輕鬆地識別 hello 名稱中的 hello 資源類型。 例如，您可以使用下列變數的 hello 產生儲存體帳戶的唯一名稱：

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a>用於識別的資源名稱
某些資源類型您可能想 tooname，但其名稱不一定唯一 toobe。 對於這些資源類型，您可以提供識別 hello 資源內容和 hello 資源類型的名稱。 提供可協助您識別資源的清單中的 hello 資源的描述性名稱。 如果您需要 toouse 不同部署不同的資源名稱，您可以使用參數名稱 hello:

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

如果您不需要在名稱中的 toopass 在部署期間，您可以使用變數： 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

您也可以使用硬式編碼的值︰

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a>一般資源名稱
您主要是透過不同的資源存取的資源類型，您可以使用硬式編碼 hello 範本中的泛型名稱。 例如，您可以在 SQL Server 上設定防火牆規則的標準、一般名稱︰

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a>參數
hello 下列資訊可能很有幫助您使用的參數：

* 將參數的使用最小化。 可能的話，使用變數或常值。 只針對這些案例使用參數︰
   
   * 您要根據 tooenvironment SKU、 大小 (容量） toouse 變化的設定。
   * 您想 toospecify 為了易於識別資源名稱。
   * 值，您經常使用 toocomplete 其他工作 （例如系統管理員使用者名稱）。
   * 機密資料 (例如密碼)。
   * 當您建立的資源類型的多個執行個體的值 toouse 的陣列或 hello 數目。
* 參數名稱使用駝峰式大小寫。
* 提供在 hello 中繼資料中的每個參數的描述：

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* 定義參數的預設值 (密碼和 SSH 金鑰除外)：
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* 所有密碼和祕密都要使用 **securestring**： 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* 您應該盡可能不使用參數 toospecify 位置。 請改用 hello**位置**hello 資源群組的屬性。 使用 hello **resourceGroup （).location** hello 範本中的資源會部署在運算式中的所有資源，hello 與 hello 資源群組相同的位置：
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   如果資源類型已支援有限數目的位置，您可能想 toospecify 直接在 hello 範本中的有效位置。 如果您必須使用**位置**參數，該參數值盡可能分享可能 toobe hello 中的資源相同的位置。 這會將系統會要求使用者 tooprovide 位置資訊的 hello 次數降到最低。
* 避免使用 hello API 版本的資源類型的參數或變數。 資源屬性和值可能會隨版本號碼而不同。 Hello API 版本設定 tooa 參數或變數時，程式碼編輯器中的 IntelliSense 無法判斷 hello 正確的結構描述。 相反地，硬式編碼 hello hello 範本中的 API 版本。

## <a name="variables"></a>變數
hello 下列資訊可能很有幫助您使用的變數：

* 使用變數，您需要 toouse 超過一次在範本中的值。 值，只有使用一次，如果硬式編碼值可讓您的範本容易 tooread。
* 您無法使用 hello[參考](resource-group-template-functions-resource.md#reference)函式在 hello**變數**hello 範本的區段。 hello**參考**函式衍生其值從 hello 資源的執行階段狀態。 不過，在 hello 初始 hello 範本的剖析期間解析變數。 建構需要 hello 值**參考**函式直接在 hello**資源**或**輸出**hello 範本的區段。
* 如[資源名稱](#resource-names)中所述，包含變數以用於必須是唯一的資源名稱。
* 您可以將變數組成複雜物件。 使用 hello **variable.subentry**格式化 tooreference 複雜物件中的值。 群組變數可協助您追蹤相關的變數。 它還可提升可讀性 hello 範本。 以下是範例：
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > 複雜物件包含的運算式不可以參考來自複雜物件的值。 請針對此目的，定義個別的變數。
   > 
   > 
   
     如需使用複雜物件作為變數的進階範例，請參閱 [Azure Resource Manager 範本中的共用狀態](best-practices-resource-manager-state.md)。

## <a name="resources"></a>資源
hello 下列資訊可能很有幫助您使用的資源：

* toohelp 了解 hello 資源 hello 用途中，指定其他參與者**註解**hello 範本中的每個資源：
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* 您可以使用標記 tooadd 中繼資料 tooresources。 使用資源的相關中繼資料 tooadd 資訊。 例如，您可以加入資源的中繼資料 toorecord 帳單詳細資料。 如需詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。
* 如果您使用*公用端點*（例如 Azure Blob 儲存體公用端點），在範本中*執行硬式編碼*hello 命名空間。 使用 hello**參考**函式 toodynamically 擷取 hello 命名空間。 您可以使用此方法 toodeploy hello 範本 toodifferent 公用命名空間的環境而不需要手動變更 hello 範本中的 hello 端點。 設定 hello API 版本 toohello hello 儲存體帳戶在範本中使用的相同版本：
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   如果 hello 的已部署的 hello 儲存體帳戶所建立的相同範本，您不需要 toospecify hello 提供者命名空間參照 hello 資源時。 這是簡化的 hello 語法：
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   如果您有在範本中設定的 toouse 公用命名空間的其他值，變更這些值 tooreflect hello 相同**參考**函式。 例如，您可以設定 hello **storageUri** hello 虛擬機器的診斷設定檔的屬性：
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   您也可以參考不同資源群組中現有的儲存體帳戶：

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* 應用程式需要時才指派公用 IP 位址 tooa 虛擬機器。 tooconnect tooa 虛擬機器 (VM) 針對偵錯，或管理或達成管理目的，使用輸入的 NAT 規則、 虛擬網路閘道或 jumpbox。
   
     如需連接 toovirtual 機器的詳細資訊，請參閱：
   
   * [在 Azure 中執行多層式架構的 VM](../guidance/guidance-compute-n-tier-vm.md)
   * [在 Azure Resource Manager 中設定 VM 的 WinRM 存取](../virtual-machines/windows/winrm.md)
   * [允許外部存取 tooyour VM 使用 hello Azure 入口網站](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [允許外部存取 tooyour VM 使用 PowerShell](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [使用 Azure CLI 允許外部存取 tooyour Linux VM](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* hello **domainNameLabel**屬性的公用 IP 位址必須是唯一。 hello **domainNameLabel**值必須介於 3 到 63 個字元，並遵循這個規則運算式所指定的 hello 規則： `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`。 因為 hello **uniqueString**函式會產生的字串 13 個字元長，hello **dnsPrefixString**參數是有限的 too50 字元：

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* 當您新增密碼 tooa 自訂指令碼延伸模組時，使用 hello **commandToExecute**屬性在 hello **protectedSettings**屬性：
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > 密碼的 tooensure 加密傳遞為參數 tooVMs 和擴充功能時，使用 hello **protectedSettings** hello 相關的延伸模組屬性。
   > 
   > 

## <a name="outputs"></a>輸出
如果您使用範本 toocreate 公用 IP 位址，包括**輸出**傳回 hello IP 位址和 hello 完整的網域名稱 (FQDN) 的詳細資料 > 一節。 在部署之後，您可以使用輸出值 tooeasily 擷取詳細公用 IP 位址和 Fqdn。 當您參考 hello 資源時，使用您用 toocreate hello API 版本它： 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a>單一範本與巢狀範本
toodeploy 方案時，您可以使用單一範本或主要範本與多個巢狀範本。 巢狀範本常見於更進階的案例。 使用巢狀的樣板可讓您 hello 下列優點：

* 您可以將解決方案分解為多個目標元件。
* 您可以搭配不同的主要範本重複使用巢狀範本。

如果您選擇 toouse 巢狀範本，hello 指導方針可協助您標準化範本設計。 這些指導方針是以 [設計 Azure Resource Manager 範本模式](best-practices-resource-manager-design-templates.md)為基礎。 我們建議您設計具有下列範本的 hello:

* **主要範本** (azuredeploy.json)。 Hello 輸入參數的使用。
* **共用的資源範本**。 使用 toodeploy 共用的所有其他資源正在使用的資源 （例如，虛擬網路和可用性集）。 使用 hello **dependsOn**運算式 tooensure 此範本其他範本之前部署。
* **選擇性資源範本**。 使用 tooconditionally 部署參數 (例如，jumpbox) 為基礎的資源。
* **成員資源範本**。 應用程式層內的每個執行個體類型都有自己的組態。 您可以在一個階層內定義不同的執行個體類型。 （例如，hello 第一個執行個體建立叢集，和 toohello 現有的叢集中加入其他執行個體）。每個執行個體類型有自己的部署範本。
* **指令碼**。 廣泛可重複使用的指令碼適用於各種個執行個體類型 (例如，將其他磁碟初始化和格式化)。 針對特定的自訂用途所建立的自訂指令碼會不同，根據 hello 執行個體類型。

![巢狀範本](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

如需詳細資訊，請參閱 [透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。

## <a name="conditionally-link-toonested-templates"></a>有條件地連結 toonested 範本
您可以使用參數 tooconditionally 連結 toonested 範本。 hello 參數就會變成 hello URI hello 範本的一部分：

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a>範本格式
它是很好的作法 toopass 您透過 JSON 驗證程式的範本。 驗證程式可協助您移除在部署期間可能會造成錯誤的多餘逗號、括號及方括號。 請嘗試在您喜愛的編輯環境 (Visual Studio 程式碼、Atom、Sublime Text、Visual Studio) 中使用 [JSONLint](http://jsonlint.com/) 或 linter 套件。

它也是個不錯的主意 tooformat 您的 JSON，以增加可讀性。 您可以對本機的編輯器使用 JSON 格式器封裝。 在 Visual Studio，tooformat hello 文件中，按**Ctrl + K、 Ctrl + D**。 在 Visual Studio 程式碼中，請按 **Alt+Shift+F**。 如果您的本機編輯器並不會格式化 hello 文件，您可以使用[線上格式器](https://www.bing.com/search?q=json+formatter)。

## <a name="next-steps"></a>後續步驟
* 如需設計虛擬機器解決方案架構的指引，請參閱[在 Azure 中執行 Windows VM](../guidance/guidance-compute-single-vm.md) 和[在 Azure 中執行 Linux VM](../guidance/guidance-compute-single-vm-linux.md)。
* 如需有關設定儲存體帳戶的指引，請參閱 [Azure 儲存體效能與延展性檢查清單](../storage/common/storage-performance-checklist.md)。
* 企業可以如何使用資源管理員 tooeffectively toolearn 管理訂用帳戶，請參閱[Azure 企業版 scaffold： 精準的訂閱控管](resource-manager-subscription-governance.md)。

