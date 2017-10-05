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
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="72e3c-103">在 Azure Resource Manager 範本中部署資源或屬性的多個執行個體</span><span class="sxs-lookup"><span data-stu-id="72e3c-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="72e3c-104">此主題說明如何逐一查看您的 Azure Resource Manager 範本，以建立資源的多個執行個體，或資源屬性的多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="72e3c-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="72e3c-105">如果您需要將邏輯新增至您的範本，讓您指定是否已部署資源，請參閱[有條件地部署資源](#conditionally-deploy-resource)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="72e3c-106">資源反覆項目</span><span class="sxs-lookup"><span data-stu-id="72e3c-106">Resource iteration</span></span>
<span data-ttu-id="72e3c-107">若要建立多個資源類型的執行個體，請將 `copy` 元素新增至資源類型。</span><span class="sxs-lookup"><span data-stu-id="72e3c-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="72e3c-108">在複製元素中，您可以指定反覆項目的數目以及此迴圈的名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="72e3c-109">計數值必須為不超過 800 的正整數。</span><span class="sxs-lookup"><span data-stu-id="72e3c-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="72e3c-110">Resource Manager 會以平行方式建立資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="72e3c-111">因此，不保證資源會循序建立。</span><span class="sxs-lookup"><span data-stu-id="72e3c-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="72e3c-112">若要在序列中建立反覆執行的資源，請參閱[序列複製](#serial-copy)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="72e3c-113">建立多個時間的資源需使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="72e3c-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="72e3c-114">請注意，每個資源的名稱均包含 `copyIndex()` 函式，並會傳回目前的反覆項目迴圈。</span><span class="sxs-lookup"><span data-stu-id="72e3c-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="72e3c-115">`copyIndex()`是以零為基礎。</span><span class="sxs-lookup"><span data-stu-id="72e3c-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="72e3c-116">因此，下列範例：</span><span class="sxs-lookup"><span data-stu-id="72e3c-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="72e3c-117">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="72e3c-117">Creates these names:</span></span>

* <span data-ttu-id="72e3c-118">storage0</span><span class="sxs-lookup"><span data-stu-id="72e3c-118">storage0</span></span>
* <span data-ttu-id="72e3c-119">storage1</span><span class="sxs-lookup"><span data-stu-id="72e3c-119">storage1</span></span>
* <span data-ttu-id="72e3c-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="72e3c-120">storage2.</span></span>

<span data-ttu-id="72e3c-121">若要位移索引值，您可以傳遞 copyIndex() 函式中的值。</span><span class="sxs-lookup"><span data-stu-id="72e3c-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="72e3c-122">要執行的反覆項目數仍然在複製項目中指定，但 copyIndex 的值會由指定的值位移。</span><span class="sxs-lookup"><span data-stu-id="72e3c-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="72e3c-123">因此，下列範例：</span><span class="sxs-lookup"><span data-stu-id="72e3c-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="72e3c-124">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="72e3c-124">Creates these names:</span></span>

* <span data-ttu-id="72e3c-125">storage1</span><span class="sxs-lookup"><span data-stu-id="72e3c-125">storage1</span></span>
* <span data-ttu-id="72e3c-126">storage2</span><span class="sxs-lookup"><span data-stu-id="72e3c-126">storage2</span></span>
* <span data-ttu-id="72e3c-127">storage3</span><span class="sxs-lookup"><span data-stu-id="72e3c-127">storage3</span></span>

<span data-ttu-id="72e3c-128">使用陣列時，複製作業會有幫助，因為您可以逐一查看陣列中的每個項目。</span><span class="sxs-lookup"><span data-stu-id="72e3c-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="72e3c-129">使用陣列上的 `length` 函式指定反覆運算的計數，並使用 `copyIndex` 來擷取陣列中目前的索引。</span><span class="sxs-lookup"><span data-stu-id="72e3c-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="72e3c-130">因此，下列範例：</span><span class="sxs-lookup"><span data-stu-id="72e3c-130">So, the following example:</span></span>

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

<span data-ttu-id="72e3c-131">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="72e3c-131">Creates these names:</span></span>

* <span data-ttu-id="72e3c-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="72e3c-132">storagecontoso</span></span>
* <span data-ttu-id="72e3c-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="72e3c-133">storagefabrikam</span></span>
* <span data-ttu-id="72e3c-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="72e3c-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="72e3c-135">序列副本</span><span class="sxs-lookup"><span data-stu-id="72e3c-135">Serial copy</span></span>

<span data-ttu-id="72e3c-136">當您使用複製元素來建立多個資源類型的執行個體時，根據預設，Resource Manager 會平行部署這些執行個體。</span><span class="sxs-lookup"><span data-stu-id="72e3c-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="72e3c-137">不過，建議您指定將資源部署在序列中。</span><span class="sxs-lookup"><span data-stu-id="72e3c-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="72e3c-138">例如，在更新生產環境時，您可以錯開更新，因此任何一次就只會更新特定數目。</span><span class="sxs-lookup"><span data-stu-id="72e3c-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="72e3c-139">Resource Manager 會提供複製元素的屬性，可讓您以序列方式部署多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="72e3c-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="72e3c-140">在複製元素中，將 `mode` 設定至 **序列**以及將 `batchSize` 設定為一次要部署的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="72e3c-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="72e3c-141">透過序列模式，Resource Manager 會在迴圈先前的執行個體上建立相依性，因此前一批次完成之前，它不會啟動一個批次。</span><span class="sxs-lookup"><span data-stu-id="72e3c-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="72e3c-142">mode 屬性也接受**平行**，這是預設值。</span><span class="sxs-lookup"><span data-stu-id="72e3c-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="72e3c-143">若要測試序列副本而不建立實際的資源，請使用下列部署空白巢狀範本的範本︰</span><span class="sxs-lookup"><span data-stu-id="72e3c-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="72e3c-144">在部署歷程記錄中，請注意，會在序列中處理巢狀部署。</span><span class="sxs-lookup"><span data-stu-id="72e3c-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![序列部署](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="72e3c-146">在更真實的案例中，下列範例會從巢狀範本一次部署兩個 Linux VM 的執行個體︰</span><span class="sxs-lookup"><span data-stu-id="72e3c-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="72e3c-147">屬性反覆運算</span><span class="sxs-lookup"><span data-stu-id="72e3c-147">Property iteration</span></span>

<span data-ttu-id="72e3c-148">若要未資源屬性建立多個值，請在 properties 元素中新增 `copy` 陣列。</span><span class="sxs-lookup"><span data-stu-id="72e3c-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="72e3c-149">此陣列包含物件，且每個物件具有下列屬性：</span><span class="sxs-lookup"><span data-stu-id="72e3c-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="72e3c-150">name - 要建立多個值的屬性名稱</span><span class="sxs-lookup"><span data-stu-id="72e3c-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="72e3c-151">count - 要建立的值數目</span><span class="sxs-lookup"><span data-stu-id="72e3c-151">count - the number of values to create</span></span>
* <span data-ttu-id="72e3c-152">input - 包含要指派給屬性之值的物件</span><span class="sxs-lookup"><span data-stu-id="72e3c-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="72e3c-153">下列範例示範如何將 `copy` 套用至虛擬機器的 dataDisks 屬性：</span><span class="sxs-lookup"><span data-stu-id="72e3c-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="72e3c-154">請注意，在屬性反覆運算內使用 `copyIndex` 時，您必須提供反覆運算的名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="72e3c-155">搭配資源反覆運算使用時，您不必提供名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="72e3c-156">Resource Manager 會在部署期間展開 `copy` 陣列。</span><span class="sxs-lookup"><span data-stu-id="72e3c-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="72e3c-157">陣列名稱會變成屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="72e3c-158">輸入值會變成物件屬性。</span><span class="sxs-lookup"><span data-stu-id="72e3c-158">The input values become the object properties.</span></span> <span data-ttu-id="72e3c-159">已部署的範本會變成：</span><span class="sxs-lookup"><span data-stu-id="72e3c-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="72e3c-160">您可以一起使用資源和屬性反覆運算。</span><span class="sxs-lookup"><span data-stu-id="72e3c-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="72e3c-161">依名稱參考屬性反覆運算。</span><span class="sxs-lookup"><span data-stu-id="72e3c-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="72e3c-162">在每個資源的屬性中，您只可以包含一個 copy 元素。</span><span class="sxs-lookup"><span data-stu-id="72e3c-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="72e3c-163">若要指定多個屬性的反覆運算迴圈，請在 copy 陣列中定義多個物件。</span><span class="sxs-lookup"><span data-stu-id="72e3c-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="72e3c-164">每個物件會分開反覆運算。</span><span class="sxs-lookup"><span data-stu-id="72e3c-164">Each object is iterated separately.</span></span> <span data-ttu-id="72e3c-165">例如，若要在負載平衡器上建立 `frontendIPConfigurations` 屬性和 `loadBalancingRules` 屬性的多個執行個體，請在單一 copy 元素中定義這兩個物件：</span><span class="sxs-lookup"><span data-stu-id="72e3c-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="72e3c-166">依迴圈中的資源而定</span><span class="sxs-lookup"><span data-stu-id="72e3c-166">Depend on resources in a loop</span></span>
<span data-ttu-id="72e3c-167">您可以透過使用 `dependsOn` 元素，讓某個資源在另一個資源之後才部署。</span><span class="sxs-lookup"><span data-stu-id="72e3c-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="72e3c-168">若要部署相依於迴圈中資源集合的資源時，請在 dependsOn 元素中提供複製迴圈的名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="72e3c-169">下列範例示範如何在部署虛擬機器之前部署三個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="72e3c-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="72e3c-170">不會顯示完整的虛擬機器定義。</span><span class="sxs-lookup"><span data-stu-id="72e3c-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="72e3c-171">請注意，複製元素將名稱設定為 `storagecopy`，並將虛擬機器的 dependsOn 元素設定為 `storagecopy`。</span><span class="sxs-lookup"><span data-stu-id="72e3c-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="72e3c-172">為子資源建立多個執行個體</span><span class="sxs-lookup"><span data-stu-id="72e3c-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="72e3c-173">您無法為子資源使用複製迴圈。</span><span class="sxs-lookup"><span data-stu-id="72e3c-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="72e3c-174">若要為通常定義為巢狀在另一個資源內的資源建立多個執行個體，您必須改為將該資源建立為最上層資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="72e3c-175">您可以透過類型和名稱屬性，定義和父資源之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="72e3c-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="72e3c-176">例如，假設您通常將資料集定義為 Data Factory 中的子資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="72e3c-177">若要為資料集建立多個執行個體，請在其移至 Data Factory 外。</span><span class="sxs-lookup"><span data-stu-id="72e3c-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="72e3c-178">資料集必須位於和 Data Factory 相同的層級，但它仍是 Data Factory 的子資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="72e3c-179">您可以透過類型和名稱屬性保留資料集與資料處理站之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="72e3c-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="72e3c-180">由於無法再從類型位於範本中的位置來推斷類型，您必須以此格式提供完整的類型︰`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`。</span><span class="sxs-lookup"><span data-stu-id="72e3c-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="72e3c-181">若要建立與 Data Factory 執行個體的父/子關聯性，請提供包含父資源名稱之資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="72e3c-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="72e3c-182">使用格式︰`{parent-resource-name}/{child-resource-name}`。</span><span class="sxs-lookup"><span data-stu-id="72e3c-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="72e3c-183">下列範例顯示實作：</span><span class="sxs-lookup"><span data-stu-id="72e3c-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="72e3c-184">有條件地部署資源</span><span class="sxs-lookup"><span data-stu-id="72e3c-184">Conditionally deploy resource</span></span>

<span data-ttu-id="72e3c-185">若要指定是否已部署資源，請使用 `condition` 元素。</span><span class="sxs-lookup"><span data-stu-id="72e3c-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="72e3c-186">此元素的值會解析為 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="72e3c-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="72e3c-187">若此值為 true，便已部署資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="72e3c-188">若此值為 false，則未部署資源。</span><span class="sxs-lookup"><span data-stu-id="72e3c-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="72e3c-189">例如，若要指定要部署新的儲存體帳戶或使用現有的儲存體帳戶，請使用：</span><span class="sxs-lookup"><span data-stu-id="72e3c-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="72e3c-190">如需使用新的或現有資源的範例，請參閱[新的或現有條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="72e3c-191">如需使用密碼或 SSH 金鑰來部署虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72e3c-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72e3c-192">Next steps</span></span>
* <span data-ttu-id="72e3c-193">若要了解範本區段的相關資訊，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="72e3c-194">若要了解如何部署範本，請參閱 [使用 Azure 資源管理員範本部署應用程式](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="72e3c-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

