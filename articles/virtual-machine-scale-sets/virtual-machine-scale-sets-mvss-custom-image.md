---
title: "在 Azure 擴展集範本中參照自訂映像 | Microsoft Docs"
description: "了解如何 tooadd 自訂映像 tooan 現有 Azure 虛擬機器規模集的範本"
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
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>新增自訂映像 tooan Azure 的小數位數設定的範本

本文將說明如何 toomodify hello[可行的最小小數位數設定範本](./virtual-machine-scale-sets-mvss-start.md)toodeploy 從自訂映像。

## <a name="change-hello-template-definition"></a>變更 hello 樣板定義

可以看到我們可行的最小小數位數的設定範本[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)，而且可以看到我們的範本部署設定從自訂映像的 hello 比例[這裡](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json)。 讓我們來檢查此範本 hello 差異比對使用 toocreate (`git diff minimum-viable-scale-set custom-image`) 逐一：

### <a name="creating-a-managed-disk-image"></a>建立受控磁碟映像

如果您已有自訂的受控磁碟映像 (類型為 `Microsoft.Compute/images` 的資源)，則可略過此節。

首先，我們將加入`sourceImageVhdUri`參數，也就是包含 hello 自訂映像 toodeploy 從 Azure 儲存體中的 hello URI toohello 一般化 blob。


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

接下來，我們將類型的資源`Microsoft.Compute/images`、 哪些 hello 受管理的磁碟映像為基礎 hello 一般化 blob 位於 URI `sourceImageVhdUri`。 此映像必須在 hello 與使用它的 hello 小數位數組相同的區域。 在 hello hello 映像內容中，我們指定 hello OS 型別，hello hello blob 位置 (從 hello`sourceImageVhdUri`參數)，和 hello 儲存體帳戶類型：

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

在 hello 小數位數設定的資源，我們將新增`dependsOn`子句參考 toohello 自訂映像 toomake 確定 hello 規模調整集合會嘗試從該映像 toodeploy 之前，取得建立 hello 映像：

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>變更縮放比例設定屬性 toouse hello 受管理的磁碟映像

在 hello `imageReference` hello 小數位數的設定`storageProfile`，而不是指定 hello 發行者、 方案、 sku 和版本的平台映像，我們在此指定 hello`id`的 hello`Microsoft.Compute/images`資源：

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

在此範例中，我們使用 hello`resourceId`函式 tooget hello 影像資源識別碼 hello 中建立 hello 相同範本。 如果您事先建立 hello 受管理的磁碟映像，您應該改為提供該映像識別碼 hello。 此識別碼 hello 格式必須是： `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`。


## <a name="next-steps"></a>後續步驟

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
