---
title: "aaaVertically 向 Azure 虛擬機器規模集 |Microsoft 文件"
description: "Toovertically 如何回應 toomonitoring 警示與 Azure 自動化中調整虛擬機器"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: madhana
editor: 
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: guybo
ms.openlocfilehash: 1cc35a805b6a5742252a89c21588ca451ff547a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="bbef0-103">使用虛擬機器擴展集垂直自動調整</span><span class="sxs-lookup"><span data-stu-id="bbef0-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="bbef0-104">本文說明如何 toovertically 調整 Azure[虛擬機器擴展集](https://azure.microsoft.com/services/virtual-machine-scale-sets/)不論是否重新佈建。</span><span class="sxs-lookup"><span data-stu-id="bbef0-104">This article describes how toovertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="bbef0-105">不在擴展集 Vm 的垂直調整，請參閱太[垂直調整 Azure 虛擬機器與 Azure 自動化](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bbef0-105">For vertical scaling of VMs which are not in scale sets, refer too[Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bbef0-106">垂直縮放比例，也稱為*向上延展*和*向下調整*，增加或減少回應 tooa 工作負載中的虛擬機器 (VM) 大小的方式。</span><span class="sxs-lookup"><span data-stu-id="bbef0-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response tooa workload.</span></span> <span data-ttu-id="bbef0-107">比較此[水平延展](virtual-machine-scale-sets-autoscale-overview.md)，也稱為 tooas*向外延展*和*縮放*其中更改 hello Vm 數目視 hello 工作負載而定。</span><span class="sxs-lookup"><span data-stu-id="bbef0-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred tooas *scale out* and *scale in*, where hello number of VMs is altered depending on hello workload.</span></span>

<span data-ttu-id="bbef0-108">重新佈建表示移除現有的 VM，並以新的 VM 取代它。</span><span class="sxs-lookup"><span data-stu-id="bbef0-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="bbef0-109">當您增加或減少中虛擬機器擴展集 Vm 的 hello 大小時，在某些情況下您想 tooresize 現有的 Vm 並保留您的資料，而在其他情況下，您需要 toodeploy hello 新大小的新 Vm。</span><span class="sxs-lookup"><span data-stu-id="bbef0-109">When you increase or decrease hello size of VMs in a VM Scale Set, in some cases you want tooresize existing VMs and retain your data, while in other cases you need toodeploy new VMs of hello new size.</span></span> <span data-ttu-id="bbef0-110">本文件涵蓋這兩種情況。</span><span class="sxs-lookup"><span data-stu-id="bbef0-110">This document covers both cases.</span></span>

<span data-ttu-id="bbef0-111">在下列情況下，垂直調整可能十分有用︰</span><span class="sxs-lookup"><span data-stu-id="bbef0-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="bbef0-112">內建在虛擬機器上的服務使用量過低 (例如在週末)。</span><span class="sxs-lookup"><span data-stu-id="bbef0-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="bbef0-113">減少 hello VM 大小可以降低每月成本。</span><span class="sxs-lookup"><span data-stu-id="bbef0-113">Reducing hello VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="bbef0-114">增加而不需要建立其他 Vm 的 VM 大小 toocope 以較大的要求。</span><span class="sxs-lookup"><span data-stu-id="bbef0-114">Increasing VM size toocope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="bbef0-115">您可以設定垂直縮放比例 toobe 觸發根據從您的 虛擬機器擴展集的度量根據警示。</span><span class="sxs-lookup"><span data-stu-id="bbef0-115">You can set up vertical scaling toobe triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="bbef0-116">Hello 警示啟動時引發的 webhook runbook 可以調整您的標尺以便設定向上或向下該觸發程序。</span><span class="sxs-lookup"><span data-stu-id="bbef0-116">When hello alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="bbef0-117">您可以依照下列步驟來設定垂直調整︰</span><span class="sxs-lookup"><span data-stu-id="bbef0-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="bbef0-118">使用執行身分功能來建立 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="bbef0-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="bbef0-119">將 VM 擴展集的 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bbef0-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="bbef0-120">加入 webhook tooyour runbook。</span><span class="sxs-lookup"><span data-stu-id="bbef0-120">Add a webhook tooyour runbook.</span></span>
4. <span data-ttu-id="bbef0-121">新增虛擬機器擴展集使用 webhook 通知警示 tooyour。</span><span class="sxs-lookup"><span data-stu-id="bbef0-121">Add an alert tooyour VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="bbef0-122">垂直自動調整只能在特定範圍的 VM 大小內進行。</span><span class="sxs-lookup"><span data-stu-id="bbef0-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="bbef0-123">然後再決定從一個 tooanother tooscale 比較 hello 規格的每個的大小 （高的數字並不一定代表較大的 VM 大小）。</span><span class="sxs-lookup"><span data-stu-id="bbef0-123">Compare hello specifications of each size before deciding tooscale from one tooanother (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="bbef0-124">您可以選擇 tooscale 之間 hello 遵循組的大小：</span><span class="sxs-lookup"><span data-stu-id="bbef0-124">You can choose tooscale between hello following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="bbef0-125">成對的調整 VM 大小</span><span class="sxs-lookup"><span data-stu-id="bbef0-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="bbef0-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="bbef0-126">Standard_A0</span></span> |<span data-ttu-id="bbef0-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="bbef0-127">Standard_A11</span></span> |
> | <span data-ttu-id="bbef0-128">標準_D1</span><span class="sxs-lookup"><span data-stu-id="bbef0-128">Standard_D1</span></span> |<span data-ttu-id="bbef0-129">標準_D14</span><span class="sxs-lookup"><span data-stu-id="bbef0-129">Standard_D14</span></span> |
> | <span data-ttu-id="bbef0-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="bbef0-130">Standard_DS1</span></span> |<span data-ttu-id="bbef0-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="bbef0-131">Standard_DS14</span></span> |
> | <span data-ttu-id="bbef0-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="bbef0-132">Standard_D1v2</span></span> |<span data-ttu-id="bbef0-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="bbef0-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="bbef0-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="bbef0-134">Standard_G1</span></span> |<span data-ttu-id="bbef0-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="bbef0-135">Standard_G5</span></span> |
> | <span data-ttu-id="bbef0-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="bbef0-136">Standard_GS1</span></span> |<span data-ttu-id="bbef0-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="bbef0-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="bbef0-138">使用執行身分功能來建立 Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="bbef0-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="bbef0-139">您需要 toodo hello 第一件事是建立 Azure 自動化帳戶將裝載 hello runbook 使用 tooscale hello VM 規模調整集合執行個體。</span><span class="sxs-lookup"><span data-stu-id="bbef0-139">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="bbef0-140">最近[Azure 自動化](https://azure.microsoft.com/services/automation/)導入了 hello 「 執行身分帳戶 」 功能會自動執行 hello runbook 上代表使用者很容易讓 hello 服務主體的設定。</span><span class="sxs-lookup"><span data-stu-id="bbef0-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="bbef0-141">閱讀更多關於此 hello 的下列文件中：</span><span class="sxs-lookup"><span data-stu-id="bbef0-141">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="bbef0-142">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="bbef0-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="bbef0-143">將 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bbef0-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="bbef0-144">hello runbook 需要 toovertically hello Azure 自動化 Runbook 資源庫中已發行您的 VM 規模集的小數位數。</span><span class="sxs-lookup"><span data-stu-id="bbef0-144">hello runbooks needed toovertically scale your VM Scale Sets are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="bbef0-145">這篇文章中的步驟 tooimport 到您的訂用帳戶遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="bbef0-145">tooimport them into your subscription follow hello steps in this article:</span></span>

* [<span data-ttu-id="bbef0-146">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="bbef0-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="bbef0-147">從 hello Runbook 功能表中選擇 hello 瀏覽圖庫選項：</span><span class="sxs-lookup"><span data-stu-id="bbef0-147">Choose hello Browse Gallery option from hello Runbooks menu:</span></span>

![匯入的 Runbook toobe][runbooks]

<span data-ttu-id="bbef0-149">會顯示 hello 需要 toobe 匯入的 runbook。</span><span class="sxs-lookup"><span data-stu-id="bbef0-149">hello runbooks that need toobe imported are shown.</span></span> <span data-ttu-id="bbef0-150">選取 根據您是否要垂直縮放比例重新佈建含 hello runbook:</span><span class="sxs-lookup"><span data-stu-id="bbef0-150">Select hello runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbook 資源庫][gallery]

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="bbef0-152">加入 webhook tooyour runbook</span><span class="sxs-lookup"><span data-stu-id="bbef0-152">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="bbef0-153">您已匯入 hello runbook 之後您將需要 tooadd webhook toohello runbook，如此可藉由從虛擬機器擴展集警示。</span><span class="sxs-lookup"><span data-stu-id="bbef0-153">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="bbef0-154">這篇文章描述 hello 的 webhook 建立您的 Runbook 的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="bbef0-154">hello details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="bbef0-155">Azure 自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="bbef0-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="bbef0-156">請確定您複製之後才關閉 hello webhook 對話方塊，將會需要這個 hello 下一節中的 hello webhook URI。</span><span class="sxs-lookup"><span data-stu-id="bbef0-156">Make sure you copy hello webhook URI before closing hello webhook dialog as you will need this in hello next section.</span></span>
> 
> 

## <a name="add-an-alert-tooyour-vm-scale-set"></a><span data-ttu-id="bbef0-157">新增虛擬機器擴展集警示 tooyour</span><span class="sxs-lookup"><span data-stu-id="bbef0-157">Add an alert tooyour VM Scale Set</span></span>
<span data-ttu-id="bbef0-158">以下是 PowerShell 指令碼會顯示如何 tooadd 警示 tooa VM 規模調整集合。</span><span class="sxs-lookup"><span data-stu-id="bbef0-158">Below is a PowerShell script which shows how tooadd an alert tooa VM Scale Set.</span></span> <span data-ttu-id="bbef0-159">Toohello 遵循 hello 度量 toofire hello 警示文章 tooget hello 名稱上，請參閱： [Azure 監視自動調整常見標準](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="bbef0-159">Refer toohello following article tooget hello name of hello metric toofire hello alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="bbef0-160">它會建議 tooconfigure 合理的時間視窗 hello 警示順序 tooavoid 觸發垂直縮放比例，以及任何相關聯的服務中斷，太過頻繁。</span><span class="sxs-lookup"><span data-stu-id="bbef0-160">It is recommended tooconfigure a reasonable time window for hello alert in order tooavoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="bbef0-161">請考慮至少 20-30 分鐘以上的時段。</span><span class="sxs-lookup"><span data-stu-id="bbef0-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="bbef0-162">請考慮水平縮放比例，如果您需要 tooavoid 中斷任何項目。</span><span class="sxs-lookup"><span data-stu-id="bbef0-162">Consider horizontal scaling if you need tooavoid any interruption.</span></span>
> 
> 

<span data-ttu-id="bbef0-163">如需有關如何 toocreate 警示，請參閱下列文章 toohello 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="bbef0-163">For more information on how toocreate alerts refer toohello following articles:</span></span>

* [<span data-ttu-id="bbef0-164">Azure 監視器 PowerShell 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="bbef0-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="bbef0-165">Azure 監視器跨平台 CLI 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="bbef0-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="bbef0-166">摘要</span><span class="sxs-lookup"><span data-stu-id="bbef0-166">Summary</span></span>
<span data-ttu-id="bbef0-167">這篇文章示範簡單的垂直調整範例。</span><span class="sxs-lookup"><span data-stu-id="bbef0-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="bbef0-168">藉助這些建置組塊 (自動化帳戶、Runbook、Webhook、警示)，您可以連接各式各樣的事件與一組自訂的動作。</span><span class="sxs-lookup"><span data-stu-id="bbef0-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
