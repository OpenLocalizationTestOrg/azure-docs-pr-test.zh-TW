---
title: "轉換 Azure Resource Manager 擴展集範本以使用受控磁碟 | Microsoft Docs"
description: "轉換擴展集範本至受控磁碟擴展集範本。"
keywords: "虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="565b9-104">轉換擴展集範本至受控磁碟擴展集範本</span><span class="sxs-lookup"><span data-stu-id="565b9-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="565b9-105">使用 Resource Manager 範本來建立不使用受控磁碟之擴展集的客戶可能希望修改它以使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="565b9-106">此文章說明如何使用來自 [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates) (提供範例 Resource Manager 範本的社群導向存放庫) 的提取要求範例執行此動作。</span><span class="sxs-lookup"><span data-stu-id="565b9-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="565b9-107">您可以在 [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998) 找到完整提取要求，並在下面找到主要差異部分以及說明：</span><span class="sxs-lookup"><span data-stu-id="565b9-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="565b9-108">將 OS 磁碟設定為受控磁碟</span><span class="sxs-lookup"><span data-stu-id="565b9-108">Making the OS disks managed</span></span>

<span data-ttu-id="565b9-109">在下面的差異中，我們可以看到我們已移除數個與儲存體帳戶相關的變數和磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="565b9-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="565b9-110">儲存體帳戶類型已不再是必要項目 (Standard_LRS 是預設值)，但我們仍然可以視需要指定。</span><span class="sxs-lookup"><span data-stu-id="565b9-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="565b9-111">針對受控磁碟，只支援 Standard_LRS 與 Premium_LRS。</span><span class="sxs-lookup"><span data-stu-id="565b9-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="565b9-112">我們在舊範本中使用新的儲存體帳戶尾碼、唯一字串陣列與 SA 計數來產生儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="565b9-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="565b9-113">這些變數在新範本中已不再是必要項目，因為受控磁碟會代表客戶自動建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="565b9-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="565b9-114">同樣地，VHD 容器名稱與 OS 磁碟名稱已不再是必要項目，因為受控磁碟會自動命名底層儲存體 Blob 容器與磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="565b9-115">在下面的差異中，我們可以看到我們已將計算 API 版本更新為 2016-04-30-preview，這是針對具有擴展集之受控磁碟支援的最低版本。</span><span class="sxs-lookup"><span data-stu-id="565b9-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="565b9-116">請注意，我們仍然可以視需要在新 API 版本中搭配舊語法使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="565b9-117">換句話說，若我們只更新計算 API 版本但未變更任何其他項目，範本應該可繼續如往常一樣運作。</span><span class="sxs-lookup"><span data-stu-id="565b9-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="565b9-118">在下面的差異中，我們可以看到我們正在將儲存體帳戶資源完全從資源陣列移除。</span><span class="sxs-lookup"><span data-stu-id="565b9-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="565b9-119">我們已不再需要它們，因為受控磁碟會代表我們自動建立它們。</span><span class="sxs-lookup"><span data-stu-id="565b9-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="565b9-120">在下面的差異中，我們可以看到我們正在將從擴展集參考的「相依於」子句移至建立儲存體帳戶的迴圈。</span><span class="sxs-lookup"><span data-stu-id="565b9-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="565b9-121">在舊範本中，這可以確保會在開始建立擴展集之前先建立儲存體帳戶，但搭配受控磁碟使用時，此子句已非必要。</span><span class="sxs-lookup"><span data-stu-id="565b9-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="565b9-122">我們也已經移除 VHD 容器屬性與 OS 磁碟名稱屬性，因為這些屬性會自動由受控磁碟處理。</span><span class="sxs-lookup"><span data-stu-id="565b9-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="565b9-123">如果需要，我們可以在 "osDisk" 設定中新增 `"managedDisk": { "storageAccountType": "Premium_LRS" }`，以建立進階 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="565b9-124">只有 VM SKU 中具有大寫或小寫 's' 的 VM 可以使用進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="565b9-125">擴展集設定中並沒有明確的屬性可決定要使用受控或非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="565b9-126">擴展集會根據儲存體設定檔中的屬性來判斷要使用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="565b9-127">因此，修改範本以確保擴展集的儲存體設定檔中有正確的屬性非常重要。</span><span class="sxs-lookup"><span data-stu-id="565b9-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="565b9-128">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="565b9-128">Data disks</span></span>

<span data-ttu-id="565b9-129">根據上面的變更，擴展集會針對 OS 磁碟使用受控磁碟，但對於資料磁碟呢？</span><span class="sxs-lookup"><span data-stu-id="565b9-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="565b9-130">若要新增資料磁碟，請在與 "osDisk" 相同層級的 "storageProfile" 下新增 "dataDisks" 屬性。</span><span class="sxs-lookup"><span data-stu-id="565b9-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="565b9-131">屬性的值是 JSON 物件清單，其中每個物件都具有屬性 "lun" (對於 VM 上的每個資料磁碟，這必須是唯一的)、"createOption" ("empty" 是目前唯一支援的選項) 與 "diskSizeGB" (以 GB 為單位的磁碟大小，必須大於 0 並小於 1024)，如下列範例中所示：</span><span class="sxs-lookup"><span data-stu-id="565b9-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="565b9-132">若在此陣列中指定 `n` 磁碟，擴展集中的每個 VM 都會取得 `n` 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="565b9-133">但是請注意，這些資料磁碟是未經處理的裝置。</span><span class="sxs-lookup"><span data-stu-id="565b9-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="565b9-134">它們並未格式化。</span><span class="sxs-lookup"><span data-stu-id="565b9-134">They are not formatted.</span></span> <span data-ttu-id="565b9-135">客戶可以決定是否要在使用這些磁碟之前先連結、分割或格式化它們。</span><span class="sxs-lookup"><span data-stu-id="565b9-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="565b9-136">或者，我們也可以在每個資料磁碟物件中指定 `"managedDisk": { "storageAccountType": "Premium_LRS" }`，以指定它應該是進階資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="565b9-137">只有 VM SKU 中具有大寫或小寫 's' 的 VM 可以使用進階磁碟。</span><span class="sxs-lookup"><span data-stu-id="565b9-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="565b9-138">若要深入了解如何搭配擴展集使用資料磁碟，請參閱[此文章](./virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="565b9-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="565b9-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="565b9-139">Next steps</span></span>
<span data-ttu-id="565b9-140">如需使用擴展集的範例 Resource Manager 範本，請在 [Azure 快速入門範本 github 儲存機制](https://github.com/Azure/azure-quickstart-templates)中搜尋 "vmss"。</span><span class="sxs-lookup"><span data-stu-id="565b9-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="565b9-141">如需一般資訊，請參閱 [擴展集的主要登陸頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="565b9-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

