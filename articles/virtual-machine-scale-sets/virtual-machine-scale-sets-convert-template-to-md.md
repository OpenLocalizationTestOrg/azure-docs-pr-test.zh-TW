---
title: "Azure Resource Manager 標尺 aaaConvert 設定範本 toouse 受管理的磁碟 |Microsoft 文件"
description: "小數位數組範本 tooa 受管理的磁碟小數位數組將範本轉換。"
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
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a><span data-ttu-id="7fbff-104">小數位數組範本 tooa 受管理的磁碟小數位數組將範本轉換</span><span class="sxs-lookup"><span data-stu-id="7fbff-104">Convert a scale set template tooa managed disk scale set template</span></span>

<span data-ttu-id="7fbff-105">使用資源管理員範本來建立不使用受管理的磁碟設定的標尺的客戶可能會想 toomodify 它 toouse 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish toomodify it toouse managed disk.</span></span> <span data-ttu-id="7fbff-106">本文將說明如何 toodo，使用做為範例提取要求從 hello [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)，範例資源管理員範本的社群導向的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="7fbff-106">This article shows how toodo this, using as an example a pull request from hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="7fbff-107">這裡可以看到 hello 完整提取要求： [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998)，和 hello 相關部分 hello 差異如下，以及說明：</span><span class="sxs-lookup"><span data-stu-id="7fbff-107">hello full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and hello relevant parts of hello diff are below, along with explanations:</span></span>

## <a name="making-hello-os-disks-managed"></a><span data-ttu-id="7fbff-108">讓受管理的 hello OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="7fbff-108">Making hello OS disks managed</span></span>

<span data-ttu-id="7fbff-109">在下面的 hello 差異，我們可以看到我們移除了數個變數相關的 toostorage 帳戶和磁碟內容。</span><span class="sxs-lookup"><span data-stu-id="7fbff-109">In hello diff below, we can see that we have removed several variables related toostorage account and disk properties.</span></span> <span data-ttu-id="7fbff-110">儲存體帳戶類型也不再需要 （Standard_LRS 是 hello 預設值），但我們無法仍指定它我們希望。</span><span class="sxs-lookup"><span data-stu-id="7fbff-110">Storage account type is no longer necessary (Standard_LRS is hello default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="7fbff-111">針對受控磁碟，只支援 Standard_LRS 與 Premium_LRS。</span><span class="sxs-lookup"><span data-stu-id="7fbff-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="7fbff-112">新的儲存體帳戶尾碼，唯一的字串陣列，sa 計數用於 hello 舊範本 toogenerate 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="7fbff-112">New storage account suffix, unique string array, and sa count were used in hello old template toogenerate storage account names.</span></span> <span data-ttu-id="7fbff-113">這些變數就不再需要在 hello 新範本，因為 hello 客戶代表受管理的磁碟會自動建立的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7fbff-113">These variables are no longer necessary in hello new template because managed disk automatically creates storage accounts on hello customer's behalf.</span></span> <span data-ttu-id="7fbff-114">同樣地，vhd 容器名稱和作業系統磁碟名稱就不再需要因為受管理的磁碟會自動命名 hello 基礎儲存體 blob 容器和磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names hello underlying storage blob containers and disks.</span></span>

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


<span data-ttu-id="7fbff-115">在 hello 差異下，我們可以我們已更新 hello，請參閱計算應用程式開發介面版本 too2016-04-30-預覽，這是 hello 最早的必要的版本與小數位數設定的受管理的磁碟支援。</span><span class="sxs-lookup"><span data-stu-id="7fbff-115">In hello diff below, we can see that we updated hello compute api version too2016-04-30-preview, which is hello earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="7fbff-116">請注意，我們可能仍會使用未受管理的磁碟在 hello 舊語法與 hello 新 api 版本視。</span><span class="sxs-lookup"><span data-stu-id="7fbff-116">Note that we could still use unmanaged disks in hello new api version with hello old syntax if desired.</span></span> <span data-ttu-id="7fbff-117">換句話說，如果我們只能更新 hello 計算應用程式開發介面版本，而且不會變更任何其他項目，hello 範本應該繼續執行之前為 toowork。</span><span class="sxs-lookup"><span data-stu-id="7fbff-117">In other words, if we only update hello compute api version and don't change anything else, hello template should continue toowork as before.</span></span>

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

<span data-ttu-id="7fbff-118">在下面的 hello 差異，我們可以看到，我們正在移除 hello 儲存體帳戶資源從 hello 資源陣列完全。</span><span class="sxs-lookup"><span data-stu-id="7fbff-118">In hello diff below, we can see that we are removing hello storage account resource from hello resources array completely.</span></span> <span data-ttu-id="7fbff-119">我們已不再需要它們，因為受控磁碟會代表我們自動建立它們。</span><span class="sxs-lookup"><span data-stu-id="7fbff-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

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

<span data-ttu-id="7fbff-120">在下面我們 hello 差異可以我們會移除 hello，請參閱取決於子句參考 hello 小數位數組 toohello 迴圈已建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7fbff-120">In hello diff below, we can see that we are removing hello depends on clause referring from hello scale set toohello loop that was creating storage accounts.</span></span> <span data-ttu-id="7fbff-121">在 hello 舊範本中，這確保 hello 規模集開始建立，但這個子句已不再需要使用受管理磁碟之前，所建立 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7fbff-121">In hello old template, this was ensuring that hello storage accounts were created before hello scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="7fbff-122">我們也會移除 hello vhd 容器的內容，並 hello 作業系統磁碟名稱 屬性，因為這些屬性會自動由幕後 hello 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-122">We also remove hello vhd containers property, and hello os disk name property as these properties are automatically handled under hello hood by managed disk.</span></span> <span data-ttu-id="7fbff-123">如果我們必須承擔更多，我們可以加入`"managedDisk": { "storageAccountType": "Premium_LRS" }`hello"osDisk 」 組態，如果我們想高階 OS 磁碟中。</span><span class="sxs-lookup"><span data-stu-id="7fbff-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in hello "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="7fbff-124">只有 Vm 使用大寫或小寫的 ' hello VM 在 sku 可以使用高階磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-124">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

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

<span data-ttu-id="7fbff-125">Hello 小數位數組組態是否 toouse managed 或 unmanaged 的磁碟中沒有明確的屬性。</span><span class="sxs-lookup"><span data-stu-id="7fbff-125">There is no explicit property in hello scale set configuration for whether toouse managed or unmanaged disk.</span></span> <span data-ttu-id="7fbff-126">hello 規模集知道哪些 toouse hello 儲存體設定檔中的 hello 屬性為基礎。</span><span class="sxs-lookup"><span data-stu-id="7fbff-126">hello scale set knows which toouse based on hello properties that are present in hello storage profile.</span></span> <span data-ttu-id="7fbff-127">因此，請務必修改 hello 範本 tooensure hello 規模集的 hello 存放裝置設定檔中的 hello 權限的內容時。</span><span class="sxs-lookup"><span data-stu-id="7fbff-127">Thus, it is important when modifying hello template tooensure that hello right properties are in hello storage profile of hello scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="7fbff-128">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7fbff-128">Data disks</span></span>

<span data-ttu-id="7fbff-129">Hello 變更上述，hello 小數位數組會使用受管理的磁碟 hello OS 磁碟，但資料磁碟的情況為何？tooadd 資料磁碟，在相同層級為"osDisk"hello，加入下"storageProfile"hello"dataDisks"屬性。</span><span class="sxs-lookup"><span data-stu-id="7fbff-129">With hello changes above, hello scale set uses managed disks for hello OS disk, but what about data disks? tooadd data disks, add hello "dataDisks" property under "storageProfile" at hello same level as "osDisk".</span></span> <span data-ttu-id="7fbff-130">hello hello 屬性的值是 JSON 物件的清單，每一個都有屬性 （這必須是唯一的每個 VM 上的資料磁碟） 的 「 lun"，"createOption"("empty"是目前 hello 唯一支援的選項)，和 「 diskSizeGB 」 （hello hello 磁碟，以 gb 為單位的大小; 必須是大於 0 且小於 1024年） 在 hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="7fbff-130">hello value of hello property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently hello only supported option), and "diskSizeGB" (hello size of hello disk in gigabytes; must be greater than 0 and less than 1024) as in hello following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="7fbff-131">如果您指定`n`此陣列中的磁碟，在 hello 標尺每個 VM 設定取得`n`資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-131">If you specify `n` disks in this array, each VM in hello scale set gets `n` data disks.</span></span> <span data-ttu-id="7fbff-132">但是請注意，這些資料磁碟是未經處理的裝置。</span><span class="sxs-lookup"><span data-stu-id="7fbff-132">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="7fbff-133">它們並未格式化。</span><span class="sxs-lookup"><span data-stu-id="7fbff-133">They are not formatted.</span></span> <span data-ttu-id="7fbff-134">它是最多 toohello 客戶 tooattach、 磁碟分割，以及一個格式 hello 磁碟才能使用它們。</span><span class="sxs-lookup"><span data-stu-id="7fbff-134">It is up toohello customer tooattach, paritition, and format hello disks before using them.</span></span> <span data-ttu-id="7fbff-135">選擇性地，我們也可以指定`"managedDisk": { "storageAccountType": "Premium_LRS" }`它應該是高階資料磁碟的每個資料磁碟物件 toospecify 中。</span><span class="sxs-lookup"><span data-stu-id="7fbff-135">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object toospecify that it should be a premium data disk.</span></span> <span data-ttu-id="7fbff-136">只有 Vm 使用大寫或小寫的 ' hello VM 在 sku 可以使用高階磁碟。</span><span class="sxs-lookup"><span data-stu-id="7fbff-136">Only VMs with an uppercase or lowercase 's' in hello VM sku can use premium disks.</span></span>

<span data-ttu-id="7fbff-137">toolearn 進一步了解使用資料磁碟的小數位數的集合，請參閱[本文](./virtual-machine-scale-sets-attached-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="7fbff-137">toolearn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7fbff-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fbff-138">Next steps</span></span>
<span data-ttu-id="7fbff-139">例如資源管理員範本使用規模集 」 vmss 」 中搜尋 hello [Azure 快速入門範本 github 儲存機制](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="7fbff-139">For example Resource Manager templates using scale sets, search for "vmss" in hello [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="7fbff-140">如需一般資訊，請參閱 hello[規模集的主要登陸頁面](https://azure.microsoft.com/services/virtual-machine-scale-sets/)。</span><span class="sxs-lookup"><span data-stu-id="7fbff-140">For general information, check out hello [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

