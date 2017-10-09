---
title: "aaaAutomatic 縮放比例和虛擬機器擴充集 |Microsoft 文件"
description: "了解如何使用診斷和自動調整資源 tooautomatically 標尺虛擬機器規模集中的。"
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
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a><span data-ttu-id="125c2-103">如何 toouse 自動縮放比例和虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="125c2-103">How toouse automatic scaling and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="125c2-104">自動調整的虛擬機器規模集中的 hello 建立或刪除中設定為 hello 的機器所需 toomatch 效能需求。</span><span class="sxs-lookup"><span data-stu-id="125c2-104">Automatic scaling of virtual machines in a scale set is hello creation or deletion of machines in hello set as needed toomatch performance requirements.</span></span> <span data-ttu-id="125c2-105">當工作的 hello 數量增加時，應用程式可能需要額外的資源 tooenable 它 tooeffectively 執行工作。</span><span class="sxs-lookup"><span data-stu-id="125c2-105">As hello volume of work grows, an application may require additional resources tooenable it tooeffectively perform tasks.</span></span>

<span data-ttu-id="125c2-106">自動調整是自動化程序，可協助減輕管理額外負荷。</span><span class="sxs-lookup"><span data-stu-id="125c2-106">Automatic scaling is an automated process that helps ease management overhead.</span></span> <span data-ttu-id="125c2-107">透過減少額外負荷，您不需要 toocontinually 監視系統效能，或決定如何 toomanage 資源。</span><span class="sxs-lookup"><span data-stu-id="125c2-107">By reducing overhead, you don't need toocontinually monitor system performance or decide how toomanage resources.</span></span> <span data-ttu-id="125c2-108">調整是一項彈性的程序。</span><span class="sxs-lookup"><span data-stu-id="125c2-108">Scaling is an elastic process.</span></span> <span data-ttu-id="125c2-109">Hello 負載增加時，可以加入更多資源。</span><span class="sxs-lookup"><span data-stu-id="125c2-109">More resources can be added as hello load increases.</span></span> <span data-ttu-id="125c2-110">還為視需要降低資源可以移除的 toominimize 成本和維護效能層級。</span><span class="sxs-lookup"><span data-stu-id="125c2-110">And as demand decreases, resources can be removed toominimize costs and maintain performance levels.</span></span>

<span data-ttu-id="125c2-111">設定使用 Azure Resource Manager 範本、 Azure PowerShell、 Azure CLI 或 hello Azure 入口網站來設定標尺上的自動調整。</span><span class="sxs-lookup"><span data-stu-id="125c2-111">Set up automatic scaling on a scale set by using an Azure Resource Manager template, Azure PowerShell, Azure CLI, or hello Azure portal.</span></span>

## <a name="set-up-scaling-by-using-resource-manager-templates"></a><span data-ttu-id="125c2-112">使用 Resource Manager 範本，設定調整</span><span class="sxs-lookup"><span data-stu-id="125c2-112">Set up scaling by using Resource Manager templates</span></span>
<span data-ttu-id="125c2-113">您不是分開部署與管理應用程式的每個資源，而是使用範本，藉此經由協調的單一作業來部署所有資源。</span><span class="sxs-lookup"><span data-stu-id="125c2-113">Rather than deploying and managing each resource of your application separately, use a template that deploys all resources in a single, coordinated operation.</span></span> <span data-ttu-id="125c2-114">在 hello 範本中，應用程式的資源定義時，部署參數指定不同的環境。</span><span class="sxs-lookup"><span data-stu-id="125c2-114">In hello template, application resources are defined and deployment parameters are specified for different environments.</span></span> <span data-ttu-id="125c2-115">hello 範本包含 JSON 和您可以為您的部署使用 tooconstruct 值的運算式。</span><span class="sxs-lookup"><span data-stu-id="125c2-115">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="125c2-116">toolearn 詳細資訊，看看[撰寫 Azure 資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-116">toolearn more, look at [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="125c2-117">在 hello 範本中，您可以指定 hello 容量項目：</span><span class="sxs-lookup"><span data-stu-id="125c2-117">In hello template, you specify hello capacity element:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

<span data-ttu-id="125c2-118">容量識別 hello hello 集合中的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="125c2-118">Capacity identifies hello number of virtual machines in hello set.</span></span> <span data-ttu-id="125c2-119">您可以藉由部署具有不同值的範本手動變更 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="125c2-119">You can manually change hello capacity by deploying a template with a different value.</span></span> <span data-ttu-id="125c2-120">如果您要部署範本 tooonly 變更 hello 容量，您可以包含 hello SKU 元素與 hello 更新容量。</span><span class="sxs-lookup"><span data-stu-id="125c2-120">If you are deploying a template tooonly change hello capacity, you can include only hello SKU element with hello updated capacity.</span></span>

<span data-ttu-id="125c2-121">hello 規模集的容量可以自動調整使用的 hello 組合**autoscaleSettings**資源和 hello 診斷延伸模組。</span><span class="sxs-lookup"><span data-stu-id="125c2-121">hello capacity of your scale set can be automatically adjusted by using a combination of hello **autoscaleSettings** resource and hello diagnostics extension.</span></span>

### <a name="configure-hello-azure-diagnostics-extension"></a><span data-ttu-id="125c2-122">設定 hello Azure 診斷擴充功能</span><span class="sxs-lookup"><span data-stu-id="125c2-122">Configure hello Azure Diagnostics extension</span></span>
<span data-ttu-id="125c2-123">自動縮放只能夠如果度量收集是成功 hello 規模集中的每部虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="125c2-123">Automatic scaling can only be done if metrics collection is successful on each virtual machine in hello scale set.</span></span> <span data-ttu-id="125c2-124">hello Azure 診斷擴充功能提供符合 hello 自動調整資源 hello 度量集合需求的 hello 監視和診斷功能。</span><span class="sxs-lookup"><span data-stu-id="125c2-124">hello Azure Diagnostics Extension provides hello monitoring and diagnostics capabilities that meets hello metrics collection needs of hello autoscale resource.</span></span> <span data-ttu-id="125c2-125">您可以安裝 hello 延伸 hello Resource Manager 範本的一部分。</span><span class="sxs-lookup"><span data-stu-id="125c2-125">You can install hello extension as part of hello Resource Manager template.</span></span>

<span data-ttu-id="125c2-126">此範例會顯示 hello 範本 tooconfigure hello 診斷延伸模組中使用的 hello 變數：</span><span class="sxs-lookup"><span data-stu-id="125c2-126">This example shows hello variables that are used in hello template tooconfigure hello diagnostics extension:</span></span>

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

<span data-ttu-id="125c2-127">部署 hello 範本時，會提供參數。</span><span class="sxs-lookup"><span data-stu-id="125c2-127">Parameters are provided when hello template is deployed.</span></span> <span data-ttu-id="125c2-128">在此範例中，hello （儲存資料） 的 hello 儲存體帳戶名稱和 hello 提供 hello 規模集 （其中收集資料） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="125c2-128">In this example, hello name of hello storage account (where data is stored) and hello name of hello scale set (where data is collected) are provided.</span></span> <span data-ttu-id="125c2-129">也在 Windows Server 本例中，會收集僅 hello 執行緒計數 」 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="125c2-129">Also in this Windows Server example, only hello Thread Count performance counter is collected.</span></span> <span data-ttu-id="125c2-130">所有 hello 可用的效能計數器，在 Windows 或 Linux 可以是使用的 toocollect 診斷資訊，而且可以包含在 hello 延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="125c2-130">All hello available performance counters in Windows or Linux can be used toocollect diagnostics information and can be included in hello extension configuration.</span></span>

<span data-ttu-id="125c2-131">此範例會顯示 hello 範本中的 hello 延伸模組的 hello 定義：</span><span class="sxs-lookup"><span data-stu-id="125c2-131">This example shows hello definition of hello extension in hello template:</span></span>

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

<span data-ttu-id="125c2-132">Hello 診斷延伸模組在執行時，要 hello 資料儲存及收集在資料表中，您指定的 hello 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="125c2-132">When hello diagnostics extension runs, hello data is stored and collected in a table, in hello storage account that you specify.</span></span> <span data-ttu-id="125c2-133">在 hello **WADPerformanceCounters**資料表中，您可以找到 hello 收集資料：</span><span class="sxs-lookup"><span data-stu-id="125c2-133">In hello **WADPerformanceCounters** table, you can find hello collected data:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a><span data-ttu-id="125c2-134">設定 hello autoScaleSettings 資源</span><span class="sxs-lookup"><span data-stu-id="125c2-134">Configure hello autoScaleSettings resource</span></span>
<span data-ttu-id="125c2-135">hello autoscaleSettings 資源使用 hello 診斷延伸模組 toodecide hello 資訊是否 tooincrease 或減少 hello 虛擬機器數目 hello 規模設定。</span><span class="sxs-lookup"><span data-stu-id="125c2-135">hello autoscaleSettings resource uses hello information from hello diagnostics extension toodecide whether tooincrease or decrease hello number of virtual machines in hello scale set.</span></span>

<span data-ttu-id="125c2-136">此範例顯示 hello 範本中的 hello 資源的 hello 設定：</span><span class="sxs-lookup"><span data-stu-id="125c2-136">This example shows hello configuration of hello resource in hello template:</span></span>

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

<span data-ttu-id="125c2-137">在 hello 上述範例中，兩個規則會建立定義 hello 自動調整規模動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-137">In hello example above, two rules are created for defining hello automatic scaling actions.</span></span> <span data-ttu-id="125c2-138">hello 第一項規則會定義 hello 向外延展動作和 hello 第二個規則定義 hello 標尺的動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-138">hello first rule defines hello scale-out action and hello second rule defines hello scale-in action.</span></span> <span data-ttu-id="125c2-139">Hello 規則提供這些值：</span><span class="sxs-lookup"><span data-stu-id="125c2-139">These values are provided in hello rules:</span></span>

| <span data-ttu-id="125c2-140">規則</span><span class="sxs-lookup"><span data-stu-id="125c2-140">Rule</span></span> | <span data-ttu-id="125c2-141">說明</span><span class="sxs-lookup"><span data-stu-id="125c2-141">Description</span></span> |
| ---- | ----------- |
| <span data-ttu-id="125c2-142">metricName</span><span class="sxs-lookup"><span data-stu-id="125c2-142">metricName</span></span>        | <span data-ttu-id="125c2-143">此值為 hello 與 hello 效能計數器，您在 hello 診斷延伸模組的 hello wadperfcounter 變數中定義相同的。</span><span class="sxs-lookup"><span data-stu-id="125c2-143">This value is hello same as hello performance counter that you defined in hello wadperfcounter variable for hello diagnostics extension.</span></span> <span data-ttu-id="125c2-144">在 hello 上述範例中，會使用 hello 執行緒計數計數器。</span><span class="sxs-lookup"><span data-stu-id="125c2-144">In hello example above, hello Thread Count counter is used.</span></span>    |
| <span data-ttu-id="125c2-145">metricResourceUri</span><span class="sxs-lookup"><span data-stu-id="125c2-145">metricResourceUri</span></span> | <span data-ttu-id="125c2-146">此值為 hello 虛擬機器規模集的 hello 資源識別項。</span><span class="sxs-lookup"><span data-stu-id="125c2-146">This value is hello resource identifier of hello virtual machine scale set.</span></span> <span data-ttu-id="125c2-147">此識別碼包含 hello hello 資源群組名稱、 hello hello 資源提供者名稱和 hello 小數位數組 tooscale hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="125c2-147">This identifier contains hello name of hello resource group, hello name of hello resource provider, and hello name of hello scale set tooscale.</span></span> |
| <span data-ttu-id="125c2-148">timeGrain</span><span class="sxs-lookup"><span data-stu-id="125c2-148">timeGrain</span></span>         | <span data-ttu-id="125c2-149">此值為 hello 的 hello 計量所收集的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="125c2-149">This value is hello granularity of hello metrics that are collected.</span></span> <span data-ttu-id="125c2-150">在上述範例中的 hello，一分鐘的間隔收集資料。</span><span class="sxs-lookup"><span data-stu-id="125c2-150">In hello preceding example, data is collected on an interval of one minute.</span></span> <span data-ttu-id="125c2-151">此值是搭配 timeWindow 使用。</span><span class="sxs-lookup"><span data-stu-id="125c2-151">This value is used with timeWindow.</span></span> |
| <span data-ttu-id="125c2-152">statistic</span><span class="sxs-lookup"><span data-stu-id="125c2-152">statistic</span></span>         | <span data-ttu-id="125c2-153">這個值會決定如何 hello 度量資訊會結合的 tooaccommodate hello 自動調整規模動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-153">This value determines how hello metrics are combined tooaccommodate hello automatic scaling action.</span></span> <span data-ttu-id="125c2-154">hello 可能的值為： 平均值、 最小值、 最大值。</span><span class="sxs-lookup"><span data-stu-id="125c2-154">hello possible values are: Average, Min, Max.</span></span> |
| <span data-ttu-id="125c2-155">timeWindow</span><span class="sxs-lookup"><span data-stu-id="125c2-155">timeWindow</span></span>        | <span data-ttu-id="125c2-156">此值為 hello 收集執行個體資料的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="125c2-156">This value is hello range of time in which instance data is collected.</span></span> <span data-ttu-id="125c2-157">其值必須介於 5 分鐘到 12 小時之間。</span><span class="sxs-lookup"><span data-stu-id="125c2-157">It must be between 5 minutes and 12 hours.</span></span> |
| <span data-ttu-id="125c2-158">timeAggregation</span><span class="sxs-lookup"><span data-stu-id="125c2-158">timeAggregation</span></span>   | <span data-ttu-id="125c2-159">這個值會決定如何隨著時間結合收集的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="125c2-159">This value determines how hello data that is collected should be combined over time.</span></span> <span data-ttu-id="125c2-160">hello 預設值是 Average。</span><span class="sxs-lookup"><span data-stu-id="125c2-160">hello default value is Average.</span></span> <span data-ttu-id="125c2-161">hello 可能的值為： 平均、 最小值、 最大值、 最後一個、 總和、 計數。</span><span class="sxs-lookup"><span data-stu-id="125c2-161">hello possible values are: Average, Minimum, Maximum, Last, Total, Count.</span></span> |
| <span data-ttu-id="125c2-162">operator</span><span class="sxs-lookup"><span data-stu-id="125c2-162">operator</span></span>          | <span data-ttu-id="125c2-163">這個值是使用的 toocompare hello 度量資料與 hello 臨界值的 hello 運算子。</span><span class="sxs-lookup"><span data-stu-id="125c2-163">This value is hello operator that is used toocompare hello metric data and hello threshold.</span></span> <span data-ttu-id="125c2-164">hello 可能的值為： NotEquals、 GreaterThan、 GreaterThanOrEqual、 LessThan、 LessThanOrEqual 等於。</span><span class="sxs-lookup"><span data-stu-id="125c2-164">hello possible values are: Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.</span></span> |
| <span data-ttu-id="125c2-165">threshold</span><span class="sxs-lookup"><span data-stu-id="125c2-165">threshold</span></span>         | <span data-ttu-id="125c2-166">此值為 hello 觸發 hello 調整規模動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-166">This value is hello value that triggers hello scale action.</span></span> <span data-ttu-id="125c2-167">會確定 tooprovide hello hello 臨界值之間有足夠的差異**向外延展**和**標尺中**動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-167">Be sure tooprovide a sufficient difference between hello threshold values for hello **scale-out** and **scale-in** actions.</span></span> <span data-ttu-id="125c2-168">如果這兩個動作的相同值，設定 hello，hello 系統將不常變更，而使它無法執行調整動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-168">If you set hello same values for both actions, hello system anticipates constant change, which prevents it from implementing a scaling action.</span></span> <span data-ttu-id="125c2-169">例如，在上述範例中的 hello 中設定兩個 too600 執行緒無法運作。</span><span class="sxs-lookup"><span data-stu-id="125c2-169">For example, setting both too600 threads in hello preceding example doesn't work.</span></span> |
| <span data-ttu-id="125c2-170">direction</span><span class="sxs-lookup"><span data-stu-id="125c2-170">direction</span></span>         | <span data-ttu-id="125c2-171">這個值會決定 hello 為止 hello 臨界值時所執行的動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-171">This value determines hello action that is taken when hello threshold value is achieved.</span></span> <span data-ttu-id="125c2-172">hello 可能的值為增加或減少。</span><span class="sxs-lookup"><span data-stu-id="125c2-172">hello possible values are Increase or Decrease.</span></span> |
| <span data-ttu-id="125c2-173">類型</span><span class="sxs-lookup"><span data-stu-id="125c2-173">type</span></span>              | <span data-ttu-id="125c2-174">此值為 hello 應該會發生，且必須設定 tooChangeCount 的動作類型。</span><span class="sxs-lookup"><span data-stu-id="125c2-174">This value is hello type of action that should occur and must be set tooChangeCount.</span></span> |
| <span data-ttu-id="125c2-175">value</span><span class="sxs-lookup"><span data-stu-id="125c2-175">value</span></span>             | <span data-ttu-id="125c2-176">此值為 hello 加入 tooor 從 hello 規模調整集合中移除的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="125c2-176">This value is hello number of virtual machines that are added tooor removed from hello scale set.</span></span> <span data-ttu-id="125c2-177">此值必須是 1 或更大。</span><span class="sxs-lookup"><span data-stu-id="125c2-177">This value must be 1 or greater.</span></span> |
| <span data-ttu-id="125c2-178">cooldown</span><span class="sxs-lookup"><span data-stu-id="125c2-178">cooldown</span></span>          | <span data-ttu-id="125c2-179">Hello 下一個動作發生之前，這個值會是 hello 數量時間 toowait 自 hello 的最後一個調整動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-179">This value is hello amount of time toowait since hello last scaling action before hello next action occurs.</span></span> <span data-ttu-id="125c2-180">此值必須介於一分鐘到一週之間。</span><span class="sxs-lookup"><span data-stu-id="125c2-180">This value must be between one minute and one week.</span></span> |

<span data-ttu-id="125c2-181">Hello 效能計數器，根據使用的，某些 hello hello 範本組態中的項目會以不同的方式使用。</span><span class="sxs-lookup"><span data-stu-id="125c2-181">Depending on hello performance counter, you are using, some of hello elements in hello template configuration are used differently.</span></span> <span data-ttu-id="125c2-182">在上述範例中的 hello，hello 效能計數器是執行緒計數、 hello 臨界值會是向外延展動作，650 和 hello 臨界值是 550 hello 標尺的動作。</span><span class="sxs-lookup"><span data-stu-id="125c2-182">In hello preceding example, hello performance counter is Thread Count, hello threshold value is 650 for a scale-out action, and hello threshold value is 550 for hello scale-in action.</span></span> <span data-ttu-id="125c2-183">如果您使用如 %Processor Time 計數器，hello 臨界值會設定 toohello 判斷調整動作的 CPU 使用量百分比。</span><span class="sxs-lookup"><span data-stu-id="125c2-183">If you use a counter such as %Processor Time, hello threshold value is set toohello percentage of CPU usage that determines a scaling action.</span></span>

<span data-ttu-id="125c2-184">當觸發調整動作時，高負載，例如 hello 集合的 hello 容量會增加根據 hello hello 範本中的值。</span><span class="sxs-lookup"><span data-stu-id="125c2-184">When a scaling action is triggered, such as a high load, hello capacity of hello set is increased based on hello value in hello template.</span></span> <span data-ttu-id="125c2-185">比方說，在小數位數設定的 hello 容量設定 too3 而設定 too1 hello 的調整動作值：</span><span class="sxs-lookup"><span data-stu-id="125c2-185">For example, in a scale set where hello capacity is set too3 and hello scale action value is set too1:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

<span data-ttu-id="125c2-186">當 hello 目前負載原因 hello 平均執行緒計數 toogo 超過 650 hello 閾值：</span><span class="sxs-lookup"><span data-stu-id="125c2-186">When hello current load causes hello average thread count toogo above hello threshold of 650:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

<span data-ttu-id="125c2-187">A**向外延展**原因 hello hello 組 toobe 以一遞增的容量來觸發動作：</span><span class="sxs-lookup"><span data-stu-id="125c2-187">A **scale-out** action is triggered that causes hello capacity of hello set toobe increased by one:</span></span>

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

<span data-ttu-id="125c2-188">hello 結果會是虛擬機器加入 toohello 規模集：</span><span class="sxs-lookup"><span data-stu-id="125c2-188">hello result is a virtual machine is added toohello scale set:</span></span>

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

<span data-ttu-id="125c2-189">Cooldown 段五分鐘，如果 hello 平均數目的執行緒在 hello 機器上停留超過 600，另一部電腦新增後 toohello 組。</span><span class="sxs-lookup"><span data-stu-id="125c2-189">After a cooldown period of five minutes, if hello average number of threads on hello machines stays over 600, another machine is added toohello set.</span></span> <span data-ttu-id="125c2-190">如果 hello 平均執行緒計數停留下方 550，hello 規模集的 hello 容量會減 1，並從 hello 集就會移除機器。</span><span class="sxs-lookup"><span data-stu-id="125c2-190">If hello average thread count stays below 550, hello capacity of hello scale set is reduced by one and a machine is removed from hello set.</span></span>

## <a name="set-up-scaling-using-azure-powershell"></a><span data-ttu-id="125c2-191">使用 Azure PowerShell 設定調整</span><span class="sxs-lookup"><span data-stu-id="125c2-191">Set up scaling using Azure PowerShell</span></span>

<span data-ttu-id="125c2-192">使用 PowerShell tooset 自動調整，向上的 toosee 範例查看[監視 Azure PowerShell，快速啟動範例](../monitoring-and-diagnostics/insights-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-192">toosee examples of using PowerShell tooset up autoscaling, look at [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md).</span></span>

## <a name="set-up-scaling-using-azure-cli"></a><span data-ttu-id="125c2-193">使用 Azure CLI 設定調整</span><span class="sxs-lookup"><span data-stu-id="125c2-193">Set up scaling using Azure CLI</span></span>

<span data-ttu-id="125c2-194">使用 Azure CLI tooset 自動調整，向上的 toosee 範例查看[Azure 監視跨平台 CLI 快速啟動範例](../monitoring-and-diagnostics/insights-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-194">toosee examples of using Azure CLI tooset up autoscaling, look at [Azure Monitor Cross-platform CLI quick start samples](../monitoring-and-diagnostics/insights-cli-samples.md).</span></span>

## <a name="set-up-scaling-using-hello-azure-portal"></a><span data-ttu-id="125c2-195">設定調整使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="125c2-195">Set up scaling using hello Azure portal</span></span>

<span data-ttu-id="125c2-196">toosee 的使用範例 hello Azure 入口網站的 tooset 設定自動調整，查看在[建立虛擬機器擴展集使用 hello Azure 入口網站](virtual-machine-scale-sets-portal-create.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-196">toosee an example of using hello Azure portal tooset up autoscaling, look at [Create a Virtual Machine Scale Set using hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="investigate-scaling-actions"></a><span data-ttu-id="125c2-197">調查調整動作</span><span class="sxs-lookup"><span data-stu-id="125c2-197">Investigate scaling actions</span></span>

* <span data-ttu-id="125c2-198">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="125c2-198">**Azure portal**</span></span>  
<span data-ttu-id="125c2-199">目前，您可以取得使用 hello 入口網站的資訊數量有限。</span><span class="sxs-lookup"><span data-stu-id="125c2-199">You can currently get a limited amount of information using hello portal.</span></span>

* <span data-ttu-id="125c2-200">**Azure 資源總管**</span><span class="sxs-lookup"><span data-stu-id="125c2-200">**Azure Resource Explorer**</span></span>  
<span data-ttu-id="125c2-201">此工具為 hello 最適合瀏覽 hello 擴展集的目前狀態。</span><span class="sxs-lookup"><span data-stu-id="125c2-201">This tool is hello best for exploring hello current state of your scale set.</span></span> <span data-ttu-id="125c2-202">按照此路徑，您應該會看到您建立 hello hello 標尺的執行個體檢視集：</span><span class="sxs-lookup"><span data-stu-id="125c2-202">Follow this path and you should see hello instance view of hello scale set that you created:</span></span>  
<span data-ttu-id="125c2-203">**訂用帳戶 > {您的訂用帳戶} > resourceGroups > {您的資源群組} > 提供者 > Microsoft.Compute > virtualMachineScaleSets > {您的擴展集} > virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="125c2-203">**Subscriptions > {your subscription} > resourceGroups > {your resource group} > providers > Microsoft.Compute > virtualMachineScaleSets > {your scale set} > virtualMachines**</span></span>

* <span data-ttu-id="125c2-204">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="125c2-204">**Azure PowerShell**</span></span>  
<span data-ttu-id="125c2-205">使用此命令 tooget 一些資訊：</span><span class="sxs-lookup"><span data-stu-id="125c2-205">Use this command tooget some information:</span></span>

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* <span data-ttu-id="125c2-206">Toohello jumpbox 虛擬機器連線，就像任何其他電腦，然後您可以從遠端存取 hello hello 小數位數組 toomonitor 個別處理程序中的虛擬機器時，一樣。</span><span class="sxs-lookup"><span data-stu-id="125c2-206">Connect toohello jumpbox virtual machine just like you would any other machine and then you can remotely access hello virtual machines in hello scale set toomonitor individual processes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="125c2-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="125c2-207">Next Steps</span></span>
* <span data-ttu-id="125c2-208">查看[自動調整虛擬機器規模集中的機器](virtual-machine-scale-sets-windows-autoscale.md)toosee 如何 toocreate 小數位數設定自動調整設定的範例。</span><span class="sxs-lookup"><span data-stu-id="125c2-208">Look at [Automatically scale machines in a Virtual Machine Scale Set](virtual-machine-scale-sets-windows-autoscale.md) toosee an example of how toocreate a scale set with automatic scaling configured.</span></span>

* <span data-ttu-id="125c2-209">在 [Azure 監視器 PowerShell 快速入門範例](../monitoring-and-diagnostics/insights-powershell-samples.md)中找到 Azure 監視器監視功能的範例</span><span class="sxs-lookup"><span data-stu-id="125c2-209">Find examples of Azure Monitor monitoring features in [Azure Monitor PowerShell quick start samples](../monitoring-and-diagnostics/insights-powershell-samples.md)</span></span>

* <span data-ttu-id="125c2-210">了解通知功能[用於 Azure 監視的自動調整規模動作 toosend 電子郵件和 webhook 警示通知](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-210">Learn about notification features in [Use autoscale actions toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).</span></span>

* <span data-ttu-id="125c2-211">深入了解如何太[使用稽核記錄 toosend 電子郵件和 webhook 警示通知，在 Azure 監視器](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span><span class="sxs-lookup"><span data-stu-id="125c2-211">Learn about how too[Use audit logs toosend email and webhook alert notifications in Azure Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)</span></span>

* <span data-ttu-id="125c2-212">深入了解 [進階自動調整案例](virtual-machine-scale-sets-advanced-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="125c2-212">Learn about [advanced autoscale scenarios](virtual-machine-scale-sets-advanced-autoscale.md).</span></span>
