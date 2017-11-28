---
title: "自動調整與虛擬機器擴展集 | Microsoft Docs"
description: "深入了解使用診斷和自動調整資源，以自動調整擴展集中的虛擬機器。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06ff9d9ae1dd8256f0d22c1a60ed6a85554f1f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="3c2f3-103">如何使用自動調整與虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="3c2f3-103">How to use automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="3c2f3-104">擴展集內的虛擬機器自動調整是依需求建立或刪除集合中的機器以符合效能需求。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-104">Automatic scaling of virtual machines in a scale set is the creation or deletion of machines in the set as needed to match performance requirements.</span></span> <span data-ttu-id="3c2f3-105">當工作量增長時，應用程式可能需要額外的資源，才能有效執行工作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-105">As the volume of work grows, an application may require additional resources to enable it to effectively perform tasks.</span></span>

<span data-ttu-id="3c2f3-106">自動調整是自動化程序，可協助減輕管理額外負荷。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="3c2f3-107">透過減少額外負荷，您便不需要持續監視系統效能或決定資源的管理方式。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-107">By reducing overhead, you don't need to continually monitor system performance or decide how to manage resources.</span></span> <span data-ttu-id="3c2f3-108">調整是一項彈性的程序。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-108">Scaling is an elastic process.</span></span> <span data-ttu-id="3c2f3-109">當負載增加時，可以新增更多資源。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-109">More resources can be added as the load increases.</span></span> <span data-ttu-id="3c2f3-110">此外，可隨著需求的降低來移除資源，以將成本降至最低並維持效能層級。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-110">And as demand decreases, resources can be removed to minimize costs and maintain performance levels.</span></span>

<span data-ttu-id="3c2f3-111">使用 Azure Resource Manager 範本、Azure PowerShell、Azure CLI 或 Azure 入口網站，在擴展集上設定自動調整。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or the Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="3c2f3-112">使用 Resource Manager 範本，設定調整</span><span class="sxs-lookup"><span data-stu-id="3c2f3-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="3c2f3-113">您不是分開部署與管理應用程式的每個資源，而是使用範本，藉此經由協調的單一作業來部署所有資源。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="3c2f3-114">在範本中，會定義應用程式資源，且會針對不同的環境指定部署參數。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-114">In the template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="3c2f3-115">範本由 JSON 與運算式所組成，可讓您用來為部署建構值。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-115">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="3c2f3-116">若要深入了解，請參閱 [編寫 Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-116">To learn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3c2f3-117">在範本中，您可以指定容量元素︰</span><span class="sxs-lookup"><span data-stu-id="3c2f3-117">In the template, you specify the capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="3c2f3-118">容量會識別集合中的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-118">Capacity identifies the number of virtual machines in the set.</span></span> <span data-ttu-id="3c2f3-119">您可以使用不同值部署範本，手動變更容量。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-119">You can manually change the capacity by deploying a template with a different value.</span></span> <span data-ttu-id="3c2f3-120">如果您部署範本只是要變更容量，您可以僅包含具有更新容量的 SKU 元素。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-120">If you are deploying a template to only change the capacity, you can include only the SKU element with the updated capacity.</span></span>

<span data-ttu-id="3c2f3-121">透過使用 **autoscaleSettings** 資源和診斷擴充功能，可自動調整擴展集的容量。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-121">The capacity of your scale set can be automatically adjusted by using a combination of the **autoscaleSettings** resource and the diagnostics extension.</span></span>

### <a name="configure-the-azure-diagnostics-extension"></a><span data-ttu-id="3c2f3-122">設定 Azure 診斷擴充</span><span class="sxs-lookup"><span data-stu-id="3c2f3-122">Configure the Azure Diagnostics extension</span></span>
<span data-ttu-id="3c2f3-123">自動調整只能夠在擴展集中的每個虛擬機器上的度量集合成功時完成。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in the scale set.</span></span> <span data-ttu-id="3c2f3-124">Azure 診斷擴充提供監視和診斷功能，符合自動調整資源的度量集合需求。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-124">The Azure Diagnostics Extension provides the monitoring and diagnostics capabilities that meets the metrics collection needs of the autoscale resource.</span></span> <span data-ttu-id="3c2f3-125">您可以安裝擴充做為 Resource Manager 範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-125">You can install the extension as part of the Resource Manager template.</span></span>

<span data-ttu-id="3c2f3-126">此範例會顯示在範本中用來設定診斷擴充的變數︰</span><span class="sxs-lookup"><span data-stu-id="3c2f3-126">This example shows the variables that are used in the template to configure the diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="3c2f3-127">參數將會於範本部署時提供。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-127">Parameters are provided when the template is deployed.</span></span> <span data-ttu-id="3c2f3-128">在這個範例中，會提供儲存體帳戶名稱 (在其中儲存資料) 及擴展集名稱 (在其中收集資料)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-128">In this example, the name of the storage account (where data is stored) and the name of the scale set (where data is collected) are provided.</span></span> <span data-ttu-id="3c2f3-129">此外，在這個 Windows Server 範例中，將只會收集執行緒計數效能計數器。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-129">Also in this Windows Server example, only the Thread Count performance counter is collected.</span></span> <span data-ttu-id="3c2f3-130">Windows 或 Linux 中所有可用的效能計數器都可以用來收集診斷資訊，並且可以包含在擴充組態中。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-130">All the available performance counters in Windows or Linux can be used to collect diagnostics information and can be included in the extension configuration.</span></span>

<span data-ttu-id="3c2f3-131">此範例會顯示範本中擴充的定義︰</span><span class="sxs-lookup"><span data-stu-id="3c2f3-131">This example shows the definition of the extension in the template:</span></span>

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

<span data-ttu-id="3c2f3-132">當診斷擴充功能執行時，會在您指定的儲存體帳戶中，於資料表中儲存和收集資料。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-132">When the diagnostics extension runs, the data is stored and collected in a table, in the storage account that you specify.</span></span> <span data-ttu-id="3c2f3-133">在 **WADPerformanceCounters** 資料表中，您可以找到收集的資料：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-133">In the **WADPerformanceCounters** table, you can find the collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-the-autoscalesettings-resource"></a><span data-ttu-id="3c2f3-134">設定 autoScaleSettings 資源</span><span class="sxs-lookup"><span data-stu-id="3c2f3-134">Configure the autoScaleSettings resource</span></span>
<span data-ttu-id="3c2f3-135">autoscaleSettings 資源會使用來自診斷擴充的資訊，以決定是否要在擴展集中增加或減少虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-135">The autoscaleSettings resource uses the information from the diagnostics extension to decide whether to increase or decrease the number of virtual machines in the scale set.</span></span>

<span data-ttu-id="3c2f3-136">此範例會顯示範本中資源的組態︰</span><span class="sxs-lookup"><span data-stu-id="3c2f3-136">This example shows the configuration of the resource in the template:</span></span>

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
            },
            "scaleAction": {
              "direction": "Increase",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          },
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

<span data-ttu-id="3c2f3-137">在上述範例中，兩個規則用於定義自動調整動作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-137">In the example above, two rules are created for defining the automatic scaling actions.</span></span> <span data-ttu-id="3c2f3-138">第一個規則定義相應放大動作，第二個規則定義相應縮小動作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-138">The first rule defines the scale-out action and the second rule defines the scale-in action.</span></span> <span data-ttu-id="3c2f3-139">在規則中提供這些值︰</span><span class="sxs-lookup"><span data-stu-id="3c2f3-139">These values are provided in the rules:</span></span>

| <span data-ttu-id="3c2f3-140">規則</span><span class="sxs-lookup"><span data-stu-id="3c2f3-140">Rule</span></span> | <span data-ttu-id="3c2f3-141">說明</span><span class="sxs-lookup"><span data-stu-id="3c2f3-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="3c2f3-142">metricName</span><span class="sxs-lookup"><span data-stu-id="3c2f3-142">metricName</span></span>        | <span data-ttu-id="3c2f3-143">此值與您在診斷擴充功能的 wadperfcounter 變數中定義的效能計數器相同。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-143">This value is the same as the performance counter that you defined in the wadperfcounter variable for the diagnostics extension.</span></span> <span data-ttu-id="3c2f3-144">在上述範例中，會使用「執行緒計數」計數器。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-144">In the example above, the Thread Count counter is used.</span></span>    |
| <span data-ttu-id="3c2f3-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="3c2f3-145">metricResourceUri</span></span> | <span data-ttu-id="3c2f3-146">此值是虛擬機器擴展集的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-146">This value is the resource identifier of the virtual machine scale set.</span></span> <span data-ttu-id="3c2f3-147">這個識別碼包含資源群組的名稱、資源提供者的名稱和要調整的擴展集的名稱。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-147">This identifier contains the name of the resource group, the name of the resource provider, and the name of the scale set to scale.</span></span> |
| <span data-ttu-id="3c2f3-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="3c2f3-148">timeGrain</span></span>         | <span data-ttu-id="3c2f3-149">此值是所收集之計量的精細度。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-149">This value is the granularity of the metrics that are collected.</span></span> <span data-ttu-id="3c2f3-150">在先前的範例中，資料是以一分鐘的間隔進行收集。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-150">In the preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="3c2f3-151">此值是搭配 timeWindow 使用。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="3c2f3-152">statistic</span><span class="sxs-lookup"><span data-stu-id="3c2f3-152">statistic</span></span>         | <span data-ttu-id="3c2f3-153">此值會決定如何結合計量以因應自動調整動作的需要。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-153">This value determines how the metrics are combined to accommodate the automatic scaling action.</span></span> <span data-ttu-id="3c2f3-154">可能的值為：Average、Min、Max。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-154">The possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="3c2f3-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="3c2f3-155">timeWindow</span></span>        | <span data-ttu-id="3c2f3-156">此值是收集執行個體資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-156">This value is the range of time in which instance data is collected.</span></span> <span data-ttu-id="3c2f3-157">其值必須介於 5 分鐘到 12 小時之間。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="3c2f3-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="3c2f3-158">timeAggregation</span></span>   | <span data-ttu-id="3c2f3-159">此值會決定收集的資料應如何隨著時間結合。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-159">This value determines how the data that is collected should be combined over time.</span></span> <span data-ttu-id="3c2f3-160">預設值為 Average。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-160">The default value is Average.</span></span> <span data-ttu-id="3c2f3-161">可能的值為：Average、Minimum、Maximum、Last、Total、Count。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-161">The possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="3c2f3-162">operator</span><span class="sxs-lookup"><span data-stu-id="3c2f3-162">operator</span></span>          | <span data-ttu-id="3c2f3-163">此值是用來比較計量資料和臨界值的運算子。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-163">This value is the operator that is used to compare the metric data and the threshold.</span></span> <span data-ttu-id="3c2f3-164">可能的值為：Equals、NotEquals、GreaterThan、GreaterThanOrEqual、LessThan、LessThanOrEqual。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-164">The possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="3c2f3-165">threshold</span><span class="sxs-lookup"><span data-stu-id="3c2f3-165">threshold</span></span>         | <span data-ttu-id="3c2f3-166">此值是觸發調整動作的值。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-166">This value is the value that triggers the scale action.</span></span> <span data-ttu-id="3c2f3-167">請確定會在**相應放大**及**相應縮小**動作的臨界值之間提供足夠的差異。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-167">Be sure to provide a sufficient difference between the threshold values for the **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="3c2f3-168">如果您為這兩個動作設定相同值，系統會預期持續性變更，這會防止系統實作調整動作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-168">If you set the same values for both actions, the system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="3c2f3-169">例如，在先前的範例中將兩者設定為 600 個執行緒將無法運作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-169">For example, setting both to 600 threads in the preceding example doesn't work.</span></span> |
| <span data-ttu-id="3c2f3-170">direction</span><span class="sxs-lookup"><span data-stu-id="3c2f3-170">direction</span></span>         | <span data-ttu-id="3c2f3-171">此值會決定達到臨界值時所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-171">This value determines the action that is taken when the threshold value is achieved.</span></span> <span data-ttu-id="3c2f3-172">可能的值為 Increase 或 Decrease。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-172">The possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="3c2f3-173">類型</span><span class="sxs-lookup"><span data-stu-id="3c2f3-173">type</span></span>              | <span data-ttu-id="3c2f3-174">此值是所應採取的動作類型，必須設為 ChangeCount。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-174">This value is the type of action that should occur and must be set to ChangeCount.</span></span> |
| <span data-ttu-id="3c2f3-175">value</span><span class="sxs-lookup"><span data-stu-id="3c2f3-175">value</span></span>             | <span data-ttu-id="3c2f3-176">此值是從擴展集內新增或移除的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-176">This value is the number of virtual machines that are added to or removed from the scale set.</span></span> <span data-ttu-id="3c2f3-177">此值必須是 1 或更大。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="3c2f3-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="3c2f3-178">cooldown</span></span>          | <span data-ttu-id="3c2f3-179">此值是在上一個調整動作之後、下一個動作執行之前的等待時間量。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-179">This value is the amount of time to wait since the last scaling action before the next action occurs.</span></span> <span data-ttu-id="3c2f3-180">此值必須介於一分鐘到一週之間。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="3c2f3-181">根據您使用的效能計數器而定，會以不同的方式使用範本設定中的某些元素。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-181">Depending on the performance counter, you are using, some of the elements in the template configuration are used differently.</span></span> <span data-ttu-id="3c2f3-182">在先前的範例中，效能計數器是「執行緒計數」、針對相應放大動作的臨界值為 650，而針對相應縮小動作的臨界值則為 550。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-182">In the preceding example, the performance counter is Thread Count, the threshold value is 650 for a scale-out action, and the threshold value is 550 for the scale-in action.</span></span> <span data-ttu-id="3c2f3-183">如果您使用如 %Processor Time 的計數器，臨界值會設定為能判斷調整動作的 CPU 使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-183">If you use a counter such as %Processor Time, the threshold value is set to the percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="3c2f3-184">觸發調整動作 (例如高負載) 時，集合的容量會根據範本中的值而增加。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-184">When a scaling action is triggered, such as a high load, the capacity of the set is increased based on the value in the template.</span></span> <span data-ttu-id="3c2f3-185">例如，在容量設為 3 且調整動作值設為 1 的擴展集中：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-185">For example, in a scale set where the capacity is set to 3 and the scale action value is set to 1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="3c2f3-186">當目前的負載導致平均執行緒計數超過 650 的臨界值時：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-186">When the current load causes the average thread count to go above the threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="3c2f3-187">會觸發**相應放大**動作，讓集合的容量增加 1：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-187">A **scale-out** action is triggered that causes the capacity of the set to be increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="3c2f3-188">結果會將虛擬機器新增至擴展集：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-188">The result is a virtual machine is added to the scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="3c2f3-189">經過五分鐘的冷卻期間之後，如果機器上的執行緒平均數目仍然超過 600，則會將另一部機器新增至集合。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-189">After a cooldown period of five minutes, if the average number of threads on the machines stays over 600, another machine is added to the set.</span></span> <span data-ttu-id="3c2f3-190">如果平均執行緒計數保持在 550 以下，則擴展集的容量會減少 1，且機器會從集合中移除。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-190">If the average thread count stays below 550, the capacity of the scale set is reduced by one and a machine is removed from the set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="3c2f3-191">使用 Azure PowerShell 設定調整</span><span class="sxs-lookup"><span data-stu-id="3c2f3-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="3c2f3-192">若要查看使用 PowerShell 設定自動調整的範例，請參閱 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-192">To see examples of using PowerShell to set up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="3c2f3-193">使用 Azure CLI 設定調整</span><span class="sxs-lookup"><span data-stu-id="3c2f3-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="3c2f3-194">若要查看使用 Azure CLI 設定自動調整的範例，請參閱 [Azure 監視器跨平台 CLI 快速入門範例](../monitoring-and-diagnostics/insights-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-194">To see examples of using Azure CLI to set up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-the-azure-portal"></a><span data-ttu-id="3c2f3-195">使用 Azure 入口網站設定調整</span><span class="sxs-lookup"><span data-stu-id="3c2f3-195">Set up scaling using the Azure portal</span></span>

<span data-ttu-id="3c2f3-196">若要查看使用 Azure 入口網站來設定自動調整的範例，請參閱[使用 Azure 入口網站建立虛擬機器擴展集](virtual-machine-scale-sets-portal-create.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-196">To see an example of using the Azure portal to set up autoscaling, look at [Create a Virtual Machine Scale Set using the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="3c2f3-197">調查調整動作</span><span class="sxs-lookup"><span data-stu-id="3c2f3-197">Investigate scaling actions</span></span>

* <span data-ttu-id="3c2f3-198">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="3c2f3-198">**Azure portal**</span></span>  
<span data-ttu-id="3c2f3-199">您目前可以使用入口網站來取得有限的資訊。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-199">You can currently get a limited amount of information using the portal.</span></span>

* <span data-ttu-id="3c2f3-200">**Azure 資源總管**</span><span class="sxs-lookup"><span data-stu-id="3c2f3-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="3c2f3-201">此工具是瀏覽擴展集目前狀態的最佳選項。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-201">This tool is the best for exploring the current state of your scale set.</span></span> <span data-ttu-id="3c2f3-202">按照此路徑，您應該會看到您所建立之調整集的執行個體檢視：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-202">Follow this path and you should see the instance view of the scale set that you created:</span></span>  
<span data-ttu-id="3c2f3-203">**訂用帳戶 > {您的訂用帳戶} > resourceGroups > {您的資源群組} > 提供者 > Microsoft.Compute > virtualMachineScaleSets > {您的擴展集} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="3c2f3-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="3c2f3-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3c2f3-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="3c2f3-205">使用下列命令可取得某些資訊：</span><span class="sxs-lookup"><span data-stu-id="3c2f3-205">Use this command to get some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="3c2f3-206">比照任何其他機器連接到 Jumpbox 虛擬機器，您即可從遠端存取調整集內的虛擬機器，以監視個別程序。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-206">Connect to the jumpbox virtual machine just like you would any other machine and then you can remotely access the virtual machines in the scale set to monitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c2f3-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3c2f3-207">Next Steps</span></span>
* <span data-ttu-id="3c2f3-208">請參閱 [在虛擬機器擴展集中自動調整機器](virtual-machine-scale-sets-windows-autoscale.md) ，以查看如何建立已設定自動調整的擴展集。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) to see an example of how to create a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="3c2f3-209">在 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)中找到 Azure 監視器監視功能的範例</span><span class="sxs-lookup"><span data-stu-id="3c2f3-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="3c2f3-210">若要深入了解通知功能，請參閱[使用自動調整動作在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-210">Learn about notification features in [Use autoscale actions to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="3c2f3-211">深入了解如何[使用稽核記錄，在 Azure 監視器中傳送電子郵件和 Webhook 警示通知](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="3c2f3-211">Learn about how to [Use audit logs to send email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="3c2f3-212">深入了解 [進階自動調整案例](virtual-machine-scale-sets-advanced-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="3c2f3-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
