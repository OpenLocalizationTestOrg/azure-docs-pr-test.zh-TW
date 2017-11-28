---
title: "aaaDeploy Azure 資源的多個執行個體 |Microsoft 文件"
description: "複製作業時使用和陣列中的 Azure Resource Manager 範本 tooiterate 多次部署資源。"
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
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="625ae-103">在 Azure Resource Manager 範本中部署資源或屬性的多個執行個體</span><span class="sxs-lookup"><span data-stu-id="625ae-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="625ae-104">本主題說明如何在您的 Azure Resource Manager 範本 toocreate tooiterate 多個執行個體的資源或多個執行個體的資源上的屬性。</span><span class="sxs-lookup"><span data-stu-id="625ae-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="625ae-105">如果需要可讓您 toospecify tooadd 邏輯 tooyour 範本是否已部署的資源，請參閱[有條件地部署資源](#conditionally-deploy-resource)。</span><span class="sxs-lookup"><span data-stu-id="625ae-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="625ae-106">資源反覆項目</span><span class="sxs-lookup"><span data-stu-id="625ae-106">Resource iteration</span></span>
<span data-ttu-id="625ae-107">toocreate 資源類型的多個執行個體加入`copy`元素 toohello 資源類型。</span><span class="sxs-lookup"><span data-stu-id="625ae-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="625ae-108">在 hello 複製項目，您可以指定 hello 反覆項目與名稱，此迴圈的數目。</span><span class="sxs-lookup"><span data-stu-id="625ae-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="625ae-109">hello 計數值必須是正整數，而且不能超過 800。</span><span class="sxs-lookup"><span data-stu-id="625ae-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="625ae-110">資源管理員會以平行方式建立 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="625ae-111">因此，不保證它們建立所在的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="625ae-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="625ae-112">依序逐一查看 toocreate 資源，請參閱[序列複製](#serial-copy)。</span><span class="sxs-lookup"><span data-stu-id="625ae-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="625ae-113">hello 資源 toocreate 多次採用下列格式的 hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-113">hello resource toocreate multiple times takes hello following format:</span></span>

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

<span data-ttu-id="625ae-114">請注意該 hello 的每個資源名稱包含 hello`copyIndex()`函式，以傳回 hello 迴圈中的 hello 目前反覆項目。</span><span class="sxs-lookup"><span data-stu-id="625ae-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="625ae-115">`copyIndex()`是以零為基礎。</span><span class="sxs-lookup"><span data-stu-id="625ae-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="625ae-116">下列範例是，hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="625ae-117">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="625ae-117">Creates these names:</span></span>

* <span data-ttu-id="625ae-118">storage0</span><span class="sxs-lookup"><span data-stu-id="625ae-118">storage0</span></span>
* <span data-ttu-id="625ae-119">storage1</span><span class="sxs-lookup"><span data-stu-id="625ae-119">storage1</span></span>
* <span data-ttu-id="625ae-120">storage2.</span><span class="sxs-lookup"><span data-stu-id="625ae-120">storage2.</span></span>

<span data-ttu-id="625ae-121">toooffset hello 索引值時，您可以在 hello copyIndex() 函式中傳遞的值。</span><span class="sxs-lookup"><span data-stu-id="625ae-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="625ae-122">hello tooperform 反覆項目數目仍中指定 hello 複製項目，但依指定的 hello copyIndex hello 值位移值。</span><span class="sxs-lookup"><span data-stu-id="625ae-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="625ae-123">下列範例是，hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="625ae-124">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="625ae-124">Creates these names:</span></span>

* <span data-ttu-id="625ae-125">storage1</span><span class="sxs-lookup"><span data-stu-id="625ae-125">storage1</span></span>
* <span data-ttu-id="625ae-126">storage2</span><span class="sxs-lookup"><span data-stu-id="625ae-126">storage2</span></span>
* <span data-ttu-id="625ae-127">storage3</span><span class="sxs-lookup"><span data-stu-id="625ae-127">storage3</span></span>

<span data-ttu-id="625ae-128">使用陣列，因為您可以逐一 hello 陣列中每個項目時，很有幫助 hello 複製作業。</span><span class="sxs-lookup"><span data-stu-id="625ae-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="625ae-129">使用 hello `length` hello 陣列 toospecify hello 計數反覆項目上的函式和`copyIndex`tooretrieve hello 目前陣列中的索引 hello。</span><span class="sxs-lookup"><span data-stu-id="625ae-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="625ae-130">下列範例是，hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-130">So, hello following example:</span></span>

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

<span data-ttu-id="625ae-131">會建立這些名稱︰</span><span class="sxs-lookup"><span data-stu-id="625ae-131">Creates these names:</span></span>

* <span data-ttu-id="625ae-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="625ae-132">storagecontoso</span></span>
* <span data-ttu-id="625ae-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="625ae-133">storagefabrikam</span></span>
* <span data-ttu-id="625ae-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="625ae-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="625ae-135">序列副本</span><span class="sxs-lookup"><span data-stu-id="625ae-135">Serial copy</span></span>

<span data-ttu-id="625ae-136">當您使用 hello 複製項目 toocreate 多個執行個體的資源類型，資源管理員 中，依預設，會將部署這些執行個體，以平行方式。</span><span class="sxs-lookup"><span data-stu-id="625ae-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="625ae-137">不過，您可能想 toospecify 該資源會部署在順序中的 hello。</span><span class="sxs-lookup"><span data-stu-id="625ae-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="625ae-138">例如，在更新生產環境時，您可能想 toostagger hello 更新，只讓特定數目會更新一次。</span><span class="sxs-lookup"><span data-stu-id="625ae-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="625ae-139">資源管理員提供 hello 複製項目上的屬性，讓您 tooserially 部署多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="625ae-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="625ae-140">在 hello 複製項目，設定`mode`太**序列**和`batchSize`toohello 一次的執行個體 toodeploy 數目。</span><span class="sxs-lookup"><span data-stu-id="625ae-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="625ae-141">序列模式中，資源管理員會在 hello 迴圈中，先前的執行個體上建立相依性，讓它不會啟動一個批次，直到 hello 前一個批次完成。</span><span class="sxs-lookup"><span data-stu-id="625ae-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="625ae-142">hello 模式屬性也會接受**平行**，這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="625ae-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="625ae-143">tootest 序列複製而不需要建立實際的資源，使用下列範本，將空的巢狀的範本部署的 hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="625ae-144">在 hello 部署歷程記錄，請注意，hello 巢狀的部署處理順序。</span><span class="sxs-lookup"><span data-stu-id="625ae-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![序列部署](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="625ae-146">比較實際的案例中，hello 下列範例會將兩個執行個體部署 Linux VM 從巢狀樣板一次：</span><span class="sxs-lookup"><span data-stu-id="625ae-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
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
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="625ae-147">屬性反覆運算</span><span class="sxs-lookup"><span data-stu-id="625ae-147">Property iteration</span></span>

<span data-ttu-id="625ae-148">toocreate 屬性的資源上的多個值加入`copy`hello 屬性項目中的陣列。</span><span class="sxs-lookup"><span data-stu-id="625ae-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="625ae-149">這個陣列包含的物件，且每個物件具有下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="625ae-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="625ae-150">名稱-hello 名稱 hello 屬性 toocreate 的多個值</span><span class="sxs-lookup"><span data-stu-id="625ae-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="625ae-151">計數-hello 值 toocreate 數目</span><span class="sxs-lookup"><span data-stu-id="625ae-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="625ae-152">輸入層包含 hello 值 tooassign toohello 屬性的物件</span><span class="sxs-lookup"><span data-stu-id="625ae-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="625ae-153">下列範例會示範如何 hello tooapply `copy` toohello dataDisks 屬性在虛擬機器上：</span><span class="sxs-lookup"><span data-stu-id="625ae-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="625ae-154">請注意，當使用`copyIndex`內屬性的反覆項目，您必須提供 hello hello 反覆項目名稱。</span><span class="sxs-lookup"><span data-stu-id="625ae-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="625ae-155">您沒有 tooprovide hello 名稱與資源的反覆項目搭配使用時。</span><span class="sxs-lookup"><span data-stu-id="625ae-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="625ae-156">資源管理員會展開 hello`copy`在部署期間的陣列。</span><span class="sxs-lookup"><span data-stu-id="625ae-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="625ae-157">hello hello 陣列名稱會變成 hello hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="625ae-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="625ae-158">hello 輸入的值會變成 hello 物件屬性。</span><span class="sxs-lookup"><span data-stu-id="625ae-158">hello input values become hello object properties.</span></span> <span data-ttu-id="625ae-159">部署的 hello 範本會變成：</span><span class="sxs-lookup"><span data-stu-id="625ae-159">hello deployed template becomes:</span></span>

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

<span data-ttu-id="625ae-160">您可以一起使用資源和屬性反覆運算。</span><span class="sxs-lookup"><span data-stu-id="625ae-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="625ae-161">參考 hello 屬性反覆項目名稱。</span><span class="sxs-lookup"><span data-stu-id="625ae-161">Reference hello property iteration by name.</span></span>

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

<span data-ttu-id="625ae-162">您只可包含一個複製項目中的每個資源的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="625ae-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="625ae-163">toospecify 的反覆項目迴圈，針對多個屬性，定義 hello 複製陣列中的多個物件。</span><span class="sxs-lookup"><span data-stu-id="625ae-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="625ae-164">每個物件會分開反覆運算。</span><span class="sxs-lookup"><span data-stu-id="625ae-164">Each object is iterated separately.</span></span> <span data-ttu-id="625ae-165">比方說，toocreate 多個執行個體的兩個 hello`frontendIPConfigurations`屬性和 hello`loadBalancingRules`負載平衡器上的屬性會定義這兩個物件中的單一複本項目：</span><span class="sxs-lookup"><span data-stu-id="625ae-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="625ae-166">依迴圈中的資源而定</span><span class="sxs-lookup"><span data-stu-id="625ae-166">Depend on resources in a loop</span></span>
<span data-ttu-id="625ae-167">您可以指定資源部署另一個資源之後，使用 hello`dependsOn`項目。</span><span class="sxs-lookup"><span data-stu-id="625ae-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="625ae-168">toodeploy 取決於 hello 集合的資源在迴圈中，資源會提供 hello dependsOn 元素中的 hello 複製迴圈 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="625ae-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="625ae-169">hello 下列範例會示範如何在部署之前 toodeploy 三個儲存體帳戶 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="625ae-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="625ae-170">不會顯示 hello 完整的虛擬機器定義。</span><span class="sxs-lookup"><span data-stu-id="625ae-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="625ae-171">請注意該 hello 複製項目沒有名稱設定得`storagecopy`和 hello 虛擬機器的 hello dependsOn 元素也會設定太`storagecopy`。</span><span class="sxs-lookup"><span data-stu-id="625ae-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="625ae-172">為子資源建立多個執行個體</span><span class="sxs-lookup"><span data-stu-id="625ae-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="625ae-173">您無法為子資源使用複製迴圈。</span><span class="sxs-lookup"><span data-stu-id="625ae-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="625ae-174">toocreate 通常定義為資源的多個執行個體巢狀方式置於另一個資源，您必須改為建立該資源為最上層資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="625ae-175">您定義 hello 與 hello 透過 hello 類型和名稱屬性的父資源的關聯性。</span><span class="sxs-lookup"><span data-stu-id="625ae-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="625ae-176">例如，假設您通常將資料集定義為 Data Factory 中的子資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="625ae-177">toocreate 多個執行個體的資料集，將它移之外 hello 資料 factory。</span><span class="sxs-lookup"><span data-stu-id="625ae-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="625ae-178">hello 資料集必須位於相同層級為 hello 的 data factory，hello，但它仍然是 hello data factory 的子資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="625ae-179">您保留 hello 資料集和資料處理站，透過 hello 類型和名稱屬性之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="625ae-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="625ae-180">從其 hello 範本中的位置不再能夠推斷類型，因為您必須提供完整的 hello hello 格式類型： `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`。</span><span class="sxs-lookup"><span data-stu-id="625ae-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="625ae-181">tooestablish 父子式關聯性與 hello 的 data factory，執行個體提供 hello 包含 hello 父資源名稱的資料集的名稱。</span><span class="sxs-lookup"><span data-stu-id="625ae-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="625ae-182">使用 hello 格式： `{parent-resource-name}/{child-resource-name}`。</span><span class="sxs-lookup"><span data-stu-id="625ae-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="625ae-183">hello 下列範例顯示 hello 實作：</span><span class="sxs-lookup"><span data-stu-id="625ae-183">hello following example shows hello implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="625ae-184">有條件地部署資源</span><span class="sxs-lookup"><span data-stu-id="625ae-184">Conditionally deploy resource</span></span>

<span data-ttu-id="625ae-185">toospecify 部署資源時，是否使用 hello`condition`項目。</span><span class="sxs-lookup"><span data-stu-id="625ae-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="625ae-186">此項目的 hello 值解析 tootrue 或 false。</span><span class="sxs-lookup"><span data-stu-id="625ae-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="625ae-187">當 hello 值為 true 時，部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="625ae-188">當 hello 值為 false 時，未部署 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="625ae-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="625ae-189">比方說，toospecify 是否已部署新的儲存體帳戶，或使用現有的儲存體帳戶時，使用：</span><span class="sxs-lookup"><span data-stu-id="625ae-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="625ae-190">如需使用新的或現有資源的範例，請參閱[新的或現有條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)。</span><span class="sxs-lookup"><span data-stu-id="625ae-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="625ae-191">如需使用密碼或 SSH 金鑰 toodeploy 虛擬機器的範例，請參閱[使用者名稱或 SSH 條件範本](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)。</span><span class="sxs-lookup"><span data-stu-id="625ae-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="625ae-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="625ae-192">Next steps</span></span>
* <span data-ttu-id="625ae-193">如果您想 toolearn 關於 hello 區段的範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="625ae-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="625ae-194">toolearn 如何 toodeploy 您的範本，請參閱[部署應用程式使用 Azure Resource Manager 範本](resource-group-template-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="625ae-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

