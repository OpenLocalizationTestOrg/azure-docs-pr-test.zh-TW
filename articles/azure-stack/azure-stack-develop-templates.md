---
title: "Azure 堆疊 aaaDevelop 範本 |Microsoft 文件"
description: "了解 Azure Stack 範本最佳做法"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a>Azure Resource Manager 範本考量
當您開發應用程式時，它是 Azure 和 Azure 堆疊之間的重要 tooensure 範本可攜性。  本主題提供開發 Azure 資源管理員的考量[範本](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf)，因此您應用程式和測試部署，並在 Azure 中的沒有存取 tooan Azure 堆疊環境可以原型。

## <a name="public-namespaces"></a>公用命名空間
因為 Azure 堆疊裝載在您的資料中心，它會有不同的服務端點的命名空間比 hello Azure 公用雲端。 如此一來，資源管理員範本中的硬式編碼公用端點失敗時嘗試 toodeploy 它們 tooAzure 堆疊。 相反地，您可以使用 hello*參考*和*串連*函式 toodynamically 建置在部署期間從 hello 資源提供者擷取的值為基礎的 hello 服務端點。 例如，而不要指定*account>.blob.core.windows.net*在範本中，擷取 hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically 設定 hello *osDisk.URI*端點：

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a>API 版本控制
Azure 服務版本在 Azure 與 Azure Stack 之間可能不同。 每個資源需要 hello api 版本屬性，定義所提供的 hello 能力。 Azure 堆疊，遵循 hello tooensure API 版本相容性是有效的應用程式開發介面版本，每個資源提供者：

| 資源提供者 | apiVersion |
| --- | --- |
| 計算 |`'2015-06-15'` |
| 網路 |`'2015-06-15'`、`'2015-05-01-preview'` |
| 儲存體 |`'2016-01-01'`、`'2015-06-15'`, `'2015-05-01-preview'` |
| KeyVault | `'2015-06-01'` |
| App Service |`'2015-08-01'` |
| MySQL |`'2015-09-01'` |
| SQL |`'2014-04-01-preview'` |

## <a name="template-functions"></a>範本函式
資源管理員[函式](../azure-resource-manager/resource-group-template-functions.md)提供功能的必要的 toobuild 動態範本。 做為範例，您可以針對如下工作使用函式：

* 串連或修剪字串 
* 參考來自其他資源的值
* 逐一查看資源 toodeploy 上多個執行個體 

當您建置範本時，某些函式在 Azure Stack 開發套件中不提供，因此不應該使用這些函式。 這些函式是：

* Skip
* Take

## <a name="resource-location"></a>資源位置
資源管理員範本在部署期間使用的位置屬性 tooplace 資源。 在 Azure 中，位置，請參閱南美洲西部等 tooa 區域。 在 Azure Stack 中，位置則不同，因為 Azure Stack 位於您的資料中心。  tooensure 範本可在 Azure 與 Azure 堆疊之間傳輸，您應該參考 hello 資源群組的位置，在您將部署個別的資源。 您可以使用`[resourceGroup().Location]`tooensure 繼承的所有資源 hello 資源群組的位置。  hello 下列資源管理員範本摘錄是部署的儲存體帳戶時使用此函式的範例：

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a>後續步驟
* [使用 PowerShell 部署範本](azure-stack-deploy-template-powershell.md)
* [使用 Azure CLI 部署範本](azure-stack-deploy-template-command-line.md)
* [使用 Visual Studio 部署範本](azure-stack-deploy-template-visual-studio.md)

