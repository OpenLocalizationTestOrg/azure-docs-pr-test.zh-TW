---
title: "aaaLearn 有關虛擬機器擴展集範本 |Microsoft 文件"
description: "了解 toocreate 最小的可行小數位數設定的虛擬機器擴展集的範本"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>了解虛擬機器擴展集範本
[Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment)是很好的方法 toodeploy 相關資源的群組。 此教學課程 數列會顯示最小的可行刻度 toocreate 設定範本以及如何 toomodify 這個範本 toosuit 各種案例。 所有範例皆來自這個 [GitHub 存放庫](https://github.com/gatneil/mvss)。 

此範本是簡單的預定的 toobe。 如需更完整的範例，小數位數的設定範本，請參閱 hello [Azure 快速入門範本 GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)和搜尋資料夾包含 hello 字串`vmss`。

如果您已經熟悉如何建立範本，您可以如何略過 toohello 「 後續步驟 」 一節 toosee toomodify 此範本。

## <a name="review-hello-template"></a>檢閱 hello 範本

使用 GitHub tooreview 我們最小的可行小數位數設定範本， [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)。

在本教學課程中，我們會檢查 hello 差異比對 (`git diff master minimum-viable-scale-set`) toocreate hello 最小可行規模調整集合範本逐一。

## <a name="define-schema-and-contentversion"></a>定義 $schema 和 contentVersion
首先，我們會定義`$schema`和`contentVersion`hello 範本中。 hello`$schema`元素都會定義 hello hello 範本語言版本和使用 Visual Studio 語法反白顯示和類似的驗證功能。 hello`contentVersion`項目不由 Azure。 相反地，它可協助您追蹤 hello 範本版本。

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>定義參數
接著，我們會定義兩個參數：`adminUsername` 和 `adminPassword`。 參數是您在部署的 hello 階段指定的值。 hello`adminUsername`參數只是`string`型別，但是因為`adminPassword`是密碼，我們提供它的類型`securestring`。 更新版本中，這些參數會傳遞至 hello 小數位數設定的組態。

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>定義變數
資源管理員範本可讓您定義變數 toobe 稍後在 hello 範本中使用。 我們的範例不使用任何變數，因此我們已經空白 hello JSON 物件。

```json
  "variables": {},
```

## <a name="define-resources"></a>定義資源
接下來是 hello hello 範本的資源 > 一節。 在這裡，您會定義您實際想 toodeploy。 與 `parameters` 和 `variables` (這些是 JSON 物件) 不同，`resources` 是一個 JSON 物件的 JSON 清單。

```json
   "resources": [
```

所有資源都必須要有 `type`、`name`、`apiVersion` 及 `location` 屬性。 這個範例的第一個資源具有類型 `Microsft.Network/virtualNetwork`、名稱`myVnet`，和 apiVersion `2016-03-30`。 (toofind hello 最新 API 版本的資源類型，請參閱 hello [Azure REST API 文件](https://docs.microsoft.com/rest/api/)。)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>指定位置
toospecify hello 位置 hello 虛擬網路，我們使用[資源管理員範本函式](../azure-resource-manager/resource-group-template-functions.md)。 此函式必須括在引號和方括號內，如下所示︰`"[<template-function>]"`。 在此情況下，我們使用 hello`resourceGroup`函式。 它會接受任何引數，並傳回 JSON 物件要部署此部署的 hello 資源群組的相關中繼資料。 hello 資源群組部署的 hello 次由 hello 使用者設定。 然後，我們使用此 JSON 物件中的索引`.location`tooget hello hello JSON 物件的位置。

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>指定虛擬網路屬性
每個資源管理員資源都有它自己`properties`設定特定 toohello 資源 > 一節。 我們在此情況下，指定該 hello 虛擬網路應該有一個子網路使用私人 IP 位址範圍 hello `10.0.0.0/16`。 擴展集一律是包含在一個子網路內。 它不能跨子網路。

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>新增 dependsOn 清單
此外 toohello 需要`type`， `name`， `apiVersion`，和`location`屬性，每個資源可以有選擇性`dependsOn`的字串清單。 這份清單會指定此部署中的哪些其他資源必須在部署此資源之前完成。

在此情況下，在 hello 清單中，從上一個範例的 hello hello 虛擬網路沒有只有一個項目。 因為 hello 小數位數組需要 hello 網路 tooexist 建立任何 Vm 之前，我們會指定此相依性。 如此一來，hello 規模集可以讓這些 Vm 私用 IP 位址從 hello 先前 hello 網路內容中指定的 IP 位址範圍。 每個字串 hello dependsOn 清單中的 hello 格式是`<type>/<name>`。 使用 hello 相同`type`和`name`先前 hello 虛擬網路的資源定義中使用。

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>指定擴展集屬性
標尺集具有自訂 hello Vm hello 規模集中的許多屬性。 如需這些屬性的完整清單，請參閱 hello[規模調整集合 REST API 文件](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)。 針對本教學課程，我們只會設定一些常用的屬性。
### <a name="supply-vm-size-and-capacity"></a>提供 VM 大小和容量
hello 小數位數設定需求 tooknow 何種大小的 VM toocreate （「 sku 名稱 」） 及多少這類 Vm toocreate （「 sku 容量 」）。 toosee 的 VM 大小可供使用，請參閱 hello [VM 大小的文件](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)。

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>選擇更新類型
hello 規模集也必須的 tooknow toohandle hello 規模調整集合的更新方式。 目前有兩個選項：`Manual` 和 `Automatic`。 Hello hello 兩個差異的詳細資訊，請參閱 hello 文件，在[如何 tooupgrade 規模調整集合](./virtual-machine-scale-sets-upgrade-scale-set.md)。

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>選擇 VM 作業系統
hello 擴展集需求 tooknow 哪些作業系統 tooput hello Vm 上。 在這裡，我們建立具有完整修補 Ubuntu 16.04 LTS 影像 hello Vm。

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>指定 computerNamePrefix
hello 規模調整集合部署了多個 Vm。 我們會指定 `computerNamePrefix`，而不是指定每個 VM 名稱。 hello 規模集附加索引 toohello 前置詞為每個 VM，所以 VM 名稱有 hello 形式`<computerNamePrefix>_<auto-generated-index>`。

下列程式碼片段的 hello，在中，我們會使用從前面 tooset hello 系統管理員使用者名稱和密碼的 hello 參數 hello 規模集中的所有 vm。 執行此作業，以 hello`parameters`樣板函式。 這個函數接受字串，指定哪些參數 toorefer tooand 輸出 hello 該參數的值。

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>指定 VM 網路組態
最後，我們需要 hello 規模集中的 hello Vm toospecify hello 網路組態。 在此情況下，我們只需要 toospecify hello 識別碼 hello 稍早建立的子網路。 這會告訴 hello 標尺 tooput hello 網路介面中設定此子網路。

您可以取得 hello 識別碼 hello 包含使用 hello hello 子網路的虛擬網路的`resourceId`樣板函式。 此函式會接受 hello 型別和資源的名稱，並傳回 hello 該資源的完整的識別碼。 此識別碼具有 hello 格式：`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

不過，hello 識別碼 hello 虛擬網路是不夠的。 您必須指定 hello 擴展集 Vm 應該位於 hello 特定子網路。 toodo，串連`/subnets/mySubnet`toohello 識別碼 hello 虛擬網路。 hello 結果會是完整的 hello hello 子網路識別碼。 執行以 hello 這個串連`concat`函式，以接受一系列字串並傳回它們的串連。

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>後續步驟

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
