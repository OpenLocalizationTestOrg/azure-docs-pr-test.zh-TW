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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="0e5c7-103">新增自訂映像 tooan Azure 的小數位數設定的範本</span><span class="sxs-lookup"><span data-stu-id="0e5c7-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="0e5c7-104">本文將說明如何 toomodify hello[可行的最小小數位數設定範本](./virtual-machine-scale-sets-mvss-start.md)toodeploy 從自訂映像。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="0e5c7-105">變更 hello 樣板定義</span><span class="sxs-lookup"><span data-stu-id="0e5c7-105">Change hello template definition</span></span>

<span data-ttu-id="0e5c7-106">可以看到我們可行的最小小數位數的設定範本[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)，而且可以看到我們的範本部署設定從自訂映像的 hello 比例[這裡](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json)。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="0e5c7-107">讓我們來檢查此範本 hello 差異比對使用 toocreate (`git diff minimum-viable-scale-set custom-image`) 逐一：</span><span class="sxs-lookup"><span data-stu-id="0e5c7-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="0e5c7-108">建立受控磁碟映像</span><span class="sxs-lookup"><span data-stu-id="0e5c7-108">Creating a managed disk image</span></span>

<span data-ttu-id="0e5c7-109">如果您已有自訂的受控磁碟映像 (類型為 `Microsoft.Compute/images` 的資源)，則可略過此節。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="0e5c7-110">首先，我們將加入`sourceImageVhdUri`參數，也就是包含 hello 自訂映像 toodeploy 從 Azure 儲存體中的 hello URI toohello 一般化 blob。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


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

<span data-ttu-id="0e5c7-111">接下來，我們將類型的資源`Microsoft.Compute/images`、 哪些 hello 受管理的磁碟映像為基礎 hello 一般化 blob 位於 URI `sourceImageVhdUri`。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="0e5c7-112">此映像必須在 hello 與使用它的 hello 小數位數組相同的區域。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="0e5c7-113">在 hello hello 映像內容中，我們指定 hello OS 型別，hello hello blob 位置 (從 hello`sourceImageVhdUri`參數)，和 hello 儲存體帳戶類型：</span><span class="sxs-lookup"><span data-stu-id="0e5c7-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="0e5c7-114">在 hello 小數位數設定的資源，我們將新增`dependsOn`子句參考 toohello 自訂映像 toomake 確定 hello 規模調整集合會嘗試從該映像 toodeploy 之前，取得建立 hello 映像：</span><span class="sxs-lookup"><span data-stu-id="0e5c7-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="0e5c7-115">變更縮放比例設定屬性 toouse hello 受管理的磁碟映像</span><span class="sxs-lookup"><span data-stu-id="0e5c7-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="0e5c7-116">在 hello `imageReference` hello 小數位數的設定`storageProfile`，而不是指定 hello 發行者、 方案、 sku 和版本的平台映像，我們在此指定 hello`id`的 hello`Microsoft.Compute/images`資源：</span><span class="sxs-lookup"><span data-stu-id="0e5c7-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="0e5c7-117">在此範例中，我們使用 hello`resourceId`函式 tooget hello 影像資源識別碼 hello 中建立 hello 相同範本。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="0e5c7-118">如果您事先建立 hello 受管理的磁碟映像，您應該改為提供該映像識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="0e5c7-119">此識別碼 hello 格式必須是： `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`。</span><span class="sxs-lookup"><span data-stu-id="0e5c7-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0e5c7-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0e5c7-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
