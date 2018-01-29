---
title: "部署 Azure 資源的多個執行個體 | Microsoft Docs"
description: "使用「Azure 資源管理員」範本中的複製作業和陣列，並在部署資源時多次逐一執行。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2017
ms.author: tomfitz
ms.openlocfilehash: e19833cb58f37f5f8b83d5558d74255583137684
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/16/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>在 Azure Resource Manager 範本中部署資源或屬性的多個執行個體
本文將說明如何將有條件地部署資源，以及如何逐一查看您的 Azure Resource Manager 範本建立多個資源執行個體中。

## <a name="conditionally-deploy-resource"></a>有條件地部署資源

若要建立一個執行個體或資源的任何執行個體，您必須決定在部署期間，當使用`condition`項目。 此元素的值會解析為 true 或 false。 若此值為 true，便已部署資源。 若此值為 false，則未部署資源。 例如，若要指定要部署新的儲存體帳戶或使用現有的儲存體帳戶，請使用：

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

## <a name="resource-iteration"></a>資源反覆項目
當您必須決定在部署期間建立的資源的一個或多個執行個體時，加入`copy`到資源類型的項目。 在複製元素中，您可以指定反覆項目的數目以及此迴圈的名稱。 計數值必須為不超過 800 的正整數。 

建立多個時間的資源需使用下列格式：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

請注意，每個資源的名稱均包含 `copyIndex()` 函式，並會傳回目前的反覆項目迴圈。 `copyIndex()`是以零為基礎。 因此，下列範例：

```json
"name": "[concat('storage', copyIndex())]",
```

會建立這些名稱︰

* storage0
* storage1
* storage2.

若要位移索引值，您可以傳遞 copyIndex() 函式中的值。 要執行的反覆項目數仍然在複製項目中指定，但 copyIndex 的值會由指定的值位移。 因此，下列範例：

```json
"name": "[concat('storage', copyIndex(1))]",
```

會建立這些名稱︰

* storage1
* storage2
* storage3

使用陣列時，複製作業會有幫助，因為您可以逐一查看陣列中的每個項目。 使用陣列上的 `length` 函式指定反覆運算的計數，並使用 `copyIndex` 來擷取陣列中目前的索引。 因此，下列範例：

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

會建立這些名稱︰

* storagecontoso
* storagefabrikam
* storagecoho

根據預設，資源管理員會以平行方式來建立資源。 因此，不保證資源會循序建立。 不過，建議您指定將資源部署在序列中。 例如，在更新生產環境時，您可以錯開更新，因此任何一次就只會更新特定數目。

若要以序列方式部署資源的多個執行個體，設定`mode`至**序列**和`batchSize`部署一次的執行個體數目。 透過序列模式，Resource Manager 會在迴圈先前的執行個體上建立相依性，因此前一批次完成之前，它不會啟動一個批次。

例如，若要以序列方式每次部署兩個儲存體帳戶，請使用：

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            }
        }
    ],
    "outputs": {}
}
``` 

mode 屬性也接受**平行**，這是預設值。

## <a name="property-iteration"></a>屬性反覆運算

若要未資源屬性建立多個值，請在 properties 元素中新增 `copy` 陣列。 此陣列包含物件，且每個物件具有下列屬性：

* name - 要建立多個值的屬性名稱
* count - 要建立的值數目
* input - 包含要指派給屬性之值的物件  

下列範例示範如何將 `copy` 套用至虛擬機器的 dataDisks 屬性：

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

請注意，在屬性反覆運算內使用 `copyIndex` 時，您必須提供反覆運算的名稱。 搭配資源反覆運算使用時，您不必提供名稱。

Resource Manager 會在部署期間展開 `copy` 陣列。 陣列名稱會變成屬性名稱。 輸入值會變成物件屬性。 已部署的範本會變成：

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

您可以一起使用資源和屬性反覆運算。 依名稱參考屬性反覆運算。

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

## <a name="variable-iteration"></a>變數的反覆項目

若要建立之變數的多個執行個體，請使用`copy`[變數] 區段中的項目。 您可以使用相關的值，建立多個物件執行個體，然後將這些值指派給資源的執行個體。 您可以使用 複製到陣列屬性或陣列中建立的物件。 下列範例中會展示這兩種方法：

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {
    "disk-array-on-object": {
      "copy": [
        {
          "name": "disks",
          "count": 5,
          "input": {
            "name": "[concat('myDataDisk', copyIndex('disks', 1))]",
            "diskSizeGB": "1",
            "diskIndex": "[copyIndex('disks')]"
          }
        }
      ]
    },
    "copy": [
      {
        "name": "disks-top-level-array",
        "count": 5,
        "input": {
          "name": "[concat('myDataDisk', copyIndex('disks-top-level-array', 1))]",
          "diskSizeGB": "1",
          "diskIndex": "[copyIndex('disks-top-level-array')]"
        }
      }
    ]
  },
  "resources": [],
  "outputs": {
    "exampleObject": {
      "value": "[variables('disk-array-on-object')]",
      "type": "object"
    },
    "exampleArrayOnObject": {
      "value": "[variables('disk-array-on-object').disks]",
      "type" : "array"
    },
    "exampleArray": {
      "value": "[variables('disks-top-level-array')]",
      "type" : "array"
    }
  }
}
```

## <a name="depend-on-resources-in-a-loop"></a>依迴圈中的資源而定
您可以透過使用 `dependsOn` 元素，讓某個資源在另一個資源之後才部署。 若要部署相依於迴圈中資源集合的資源時，請在 dependsOn 元素中提供複製迴圈的名稱。 下列範例示範如何在部署虛擬機器之前部署三個儲存體帳戶。 不會顯示完整的虛擬機器定義。 請注意，複製元素將名稱設定為 `storagecopy`，並將虛擬機器的 dependsOn 元素設定為 `storagecopy`。

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="iteration-for-a-child-resource"></a>反覆項目子系資源
您無法為子資源使用複製迴圈。 若要為通常定義為巢狀在另一個資源內的資源建立多個執行個體，您必須改為將該資源建立為最上層資源。 您可以透過類型和名稱屬性，定義和父資源之間的關聯性。

例如，假設您通常將資料集定義為 Data Factory 中的子資源。

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

若要為資料集建立多個執行個體，請在其移至 Data Factory 外。 資料集必須位於和 Data Factory 相同的層級，但它仍是 Data Factory 的子資源。 您可以透過類型和名稱屬性保留資料集與資料處理站之間的關聯性。 由於無法再從類型位於範本中的位置來推斷類型，您必須以此格式提供完整的類型︰`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`。

若要建立與 Data Factory 執行個體的父/子關聯性，請提供包含父資源名稱之資料集的名稱。 使用格式︰`{parent-resource-name}/{child-resource-name}`。  

下列範例顯示實作：

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="example-templates"></a>範本的範例

下列範例顯示建立多個資源或屬性的常見案例。

|範本  |說明  |
|---------|---------|
|[複製儲存空間](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/copystorage.json) |部署多個儲存體帳戶名稱中的索引編號。 |
|[序列的複本儲存體](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/serialcopystorage.json) |部署多個儲存體帳戶一次。 名稱中包含索引編號。 |
|[複製儲存體陣列](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/copystoragewitharray.json) |部署多個儲存體帳戶。 名稱包含陣列中的值。 |
|[新的或現有虛擬網路、 存放裝置，以及公用 IP 的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-new-or-existing-conditions) |有條件地將新的或現有的資源，與虛擬機器的部署。 |
|[VM 部署的資料磁碟數目可變的](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-windows-copy-datadisks) |部署多個資料磁碟與虛擬機器。 |
|[複製變數](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/copyvariables.json) |示範反覆運算變數的不同的方式。 |
|[多個安全性規則](https://github.com/Azure/azure-docs-json-samples/blob/master/azure-resource-manager/multipleinstance/multiplesecurityrules.json) |將多個安全性規則部署到網路安全性群組。 建構自參數的安全性規則。 |

## <a name="next-steps"></a>後續步驟
* 若要了解範本區段的相關資訊，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。
* 若要了解如何部署範本，請參閱 [使用 Azure 資源管理員範本部署應用程式](resource-group-template-deploy.md)。

