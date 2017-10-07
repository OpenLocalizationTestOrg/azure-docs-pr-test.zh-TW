---
title: "在 Azure 擴展集範本中參考現有的虛擬網路 | Microsoft Docs"
description: "了解如何 tooadd 的虛擬網路 tooan 現有 Azure 虛擬機器擴展集的範本"
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
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a>在 Azure 的小數位數組範本中加入參考 tooan 現有的虛擬網路

本文將說明如何 toomodify hello[可行的最小小數位數設定範本](./virtual-machine-scale-sets-mvss-start.md)toodeploy 到現有的虛擬網路，而不是建立一個新。

## <a name="change-hello-template-definition"></a>變更 hello 樣板定義

可以看到我們可行的最小小數位數的設定範本[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)，而且可以看到我們的範本部署到現有的虛擬網路設定的 hello 比例[這裡](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json)。 讓我們來檢查此範本 hello 差異比對使用 toocreate (`git diff minimum-viable-scale-set existing-vnet`) 逐一：

首先，我們會新增 `subnetId` 參數。 這個字串會傳入 hello 小數位數組設定，讓 hello 規模調整集合 tooidentify hello 預先建立的子網路到 toodeploy 虛擬機器。 這個字串格式必須為 hello: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`。 比方說，toodeploy hello 標尺將設定到現有的虛擬網路名稱`myvnet`，子網路`mysubnet`，資源群組`myrg`，和訂用帳戶`00000000-0000-0000-0000-000000000000`，是 hello subnetId: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`。

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

接下來，我們就可以刪除 hello 虛擬網路資源從 hello`resources`陣列，因為我們使用現有的虛擬網路，而且無須 toodeploy 新建一個。

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

hello 虛擬網路已存在 hello 範本部署之前，所以不需要 toospecify hello 標尺的 dependsOn 子句設定 toohello 虛擬網路。 因此，我們會刪除這幾行︰

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

最後，我們傳入 hello `subnetId` hello 使用者所設定的參數 (而不是使用`resourceId`hello 相同部署中，這是什麼 hello 最小可行規模調整集合範本未在 vnet tooget hello 識別碼)。

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a>後續步驟

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
