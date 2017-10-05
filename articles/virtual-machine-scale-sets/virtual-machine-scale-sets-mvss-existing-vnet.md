---
title: "在 Azure 擴展集範本中參考現有的虛擬網路 | Microsoft Docs"
description: "了解如何將虛擬網路新增到現有的「Azure 虛擬機器擴展集」範本"
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
ms.openlocfilehash: 28117d467b491704aed8d45e5eba42530579dfa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-reference-to-an-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="beb3c-103">在 Azure 擴展集範本中新增對現有虛擬網路的參考</span><span class="sxs-lookup"><span data-stu-id="beb3c-103">Add reference to an existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="beb3c-104">本文說明如何修改[最基本的可行擴展集範本](./virtual-machine-scale-sets-mvss-start.md)以便將其部署至現有虛擬網路，而非建立新的範本。</span><span class="sxs-lookup"><span data-stu-id="beb3c-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="beb3c-105">變更範本定義</span><span class="sxs-lookup"><span data-stu-id="beb3c-105">Change the template definition</span></span>

<span data-ttu-id="beb3c-106">您可以在[這裡](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)看到最基本的可行擴展集範本，並在[這裡](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json)看到用於將擴展集部署至現有虛擬網路的範本。</span><span class="sxs-lookup"><span data-stu-id="beb3c-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="beb3c-107">讓我們逐步檢查用來建立此範本 (`git diff minimum-viable-scale-set existing-vnet`) 的差異：</span><span class="sxs-lookup"><span data-stu-id="beb3c-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="beb3c-108">首先，我們會新增 `subnetId` 參數。</span><span class="sxs-lookup"><span data-stu-id="beb3c-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="beb3c-109">這個字串會傳遞至擴展集組態，讓擴展集可識別要將虛擬機器部署到的預建子網路。</span><span class="sxs-lookup"><span data-stu-id="beb3c-109">This string will be passed into the scale set configuration, allowing the scale set to identify the pre-created subnet to deploy virtual machines into.</span></span> <span data-ttu-id="beb3c-110">這個字串的格式必須是︰`/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`。</span><span class="sxs-lookup"><span data-stu-id="beb3c-110">This string must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="beb3c-111">例如，若要將擴展集部署到名稱為 `myvnet`、子網路為 `mysubnet`、資源群組為 `myrg` 和訂用帳戶為 `00000000-0000-0000-0000-000000000000` 的現有虛擬網路，subnetId 會是：`/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`。</span><span class="sxs-lookup"><span data-stu-id="beb3c-111">For instance, to deploy the scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, the subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

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

<span data-ttu-id="beb3c-112">接下來，我們可以從 `resources` 陣列刪除虛擬網路資源，因為我們要使用現有虛擬網路，因此不需要部署新的資源。</span><span class="sxs-lookup"><span data-stu-id="beb3c-112">Next, we can delete the virtual network resource from the `resources` array, since we are using an existing virtual network and don't need to deploy a new one.</span></span>

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

<span data-ttu-id="beb3c-113">虛擬網路在部署範本之前就已存在，因此不需要指定從擴展集到虛擬網路的 dependsOn 子句。</span><span class="sxs-lookup"><span data-stu-id="beb3c-113">The virtual network already exists before the template is deployed, so there is no need to specify a dependsOn clause from the scale set to the virtual network.</span></span> <span data-ttu-id="beb3c-114">因此，我們會刪除這幾行︰</span><span class="sxs-lookup"><span data-stu-id="beb3c-114">Thus, we delete these lines:</span></span>

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

<span data-ttu-id="beb3c-115">最後，我們會傳入使用者所設定的 `subnetId` 參數 (而不是使用 `resourceId` 來取得相同部署中的 vnet 識別碼，這是最基本的可行擴展集範本的作法)。</span><span class="sxs-lookup"><span data-stu-id="beb3c-115">Finally, we pass in the `subnetId` parameter set by the user (instead of using `resourceId` to get the id of a vnet in the same deployment, which is what the minimum viable scale set template does).</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="beb3c-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="beb3c-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
