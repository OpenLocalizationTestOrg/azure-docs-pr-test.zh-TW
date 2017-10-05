---
title: "垂直調整 Azure 虛擬機器擴展集 | Microsoft Docs"
description: "如何垂直調整虛擬機器大小以回應 Azure 自動化的監視警示"
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
ms.openlocfilehash: 9159a5a9041864fe06785829121233379c46bb03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="fc68a-103">使用虛擬機器擴展集垂直自動調整</span><span class="sxs-lookup"><span data-stu-id="fc68a-103">Vertical autoscale with Virtual Machine Scale sets</span></span>
<span data-ttu-id="fc68a-104">這篇文章描述如何使用或不使用重新佈建以垂直調整 Azure [虛擬機器擴充集](https://azure.microsoft.com/services/virtual-machine-scale-sets/) 。</span><span class="sxs-lookup"><span data-stu-id="fc68a-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="fc68a-105">若為垂直調整不在擴展集中的 VM，請參閱 [使用 Azure 自動化垂直調整 Azure 虛擬機器](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fc68a-105">For vertical scaling of VMs which are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fc68a-106">垂直調整也稱為向相應增加和相應減少，意味增加或減少虛擬機器 (VM) 大小以回應工作負載。</span><span class="sxs-lookup"><span data-stu-id="fc68a-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="fc68a-107">將其與[水平調整](virtual-machine-scale-sets-autoscale-overview.md) (也稱為相應放大和相應縮小) 做比較，會根據工作負載改變 VM 數目。</span><span class="sxs-lookup"><span data-stu-id="fc68a-107">Compare this with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="fc68a-108">重新佈建表示移除現有的 VM，並以新的 VM 取代它。</span><span class="sxs-lookup"><span data-stu-id="fc68a-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="fc68a-109">當您增加或減少 VM 擴展集中的 VM 大小時，在某些情況下您想要調整現有 VM 的大小並保留資料，而在其他情況下您需要部署具有新大小的新 VM。</span><span class="sxs-lookup"><span data-stu-id="fc68a-109">When you increase or decrease the size of VMs in a VM Scale Set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="fc68a-110">本文件涵蓋這兩種情況。</span><span class="sxs-lookup"><span data-stu-id="fc68a-110">This document covers both cases.</span></span>

<span data-ttu-id="fc68a-111">在下列情況下，垂直調整可能十分有用︰</span><span class="sxs-lookup"><span data-stu-id="fc68a-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="fc68a-112">內建在虛擬機器上的服務使用量過低 (例如在週末)。</span><span class="sxs-lookup"><span data-stu-id="fc68a-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="fc68a-113">減少 VM 大小可以降低每月成本。</span><span class="sxs-lookup"><span data-stu-id="fc68a-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="fc68a-114">增加 VM 大小以應付更大的需求，而不需要建立額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="fc68a-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="fc68a-115">您可以根據 VM 擴展集的度量型警示來設定要觸發的垂直調整。</span><span class="sxs-lookup"><span data-stu-id="fc68a-115">You can set up vertical scaling to be triggered based on metric based alerts from your VM Scale Set.</span></span> <span data-ttu-id="fc68a-116">啟動警示時它就會引發 Webhook 來觸發 Runbook，可讓您調整相應增加和相應減少設定。</span><span class="sxs-lookup"><span data-stu-id="fc68a-116">When the alert is activated it fires a webhook that triggers a runbook which can scale your scale set up or down.</span></span> <span data-ttu-id="fc68a-117">您可以依照下列步驟來設定垂直調整︰</span><span class="sxs-lookup"><span data-stu-id="fc68a-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="fc68a-118">使用執行身分功能來建立 Azure 自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc68a-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="fc68a-119">將 VM 擴展集的 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fc68a-119">Import Azure Automation Vertical Scale runbooks for VM Scale Sets into your subscription.</span></span>
3. <span data-ttu-id="fc68a-120">將 Webhook 加入您的 Runbook 中。</span><span class="sxs-lookup"><span data-stu-id="fc68a-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="fc68a-121">使用 Webhook 通知將警示加入至您的 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="fc68a-121">Add an alert to your VM Scale Set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="fc68a-122">垂直自動調整只能在特定範圍的 VM 大小內進行。</span><span class="sxs-lookup"><span data-stu-id="fc68a-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="fc68a-123">先比較各種大小的規格，然後再決定從一種大小調整成另一種大小 (數字較大並不一定代表 VM 大小較大)。</span><span class="sxs-lookup"><span data-stu-id="fc68a-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="fc68a-124">您可以在以下大小配對之間選擇調整︰</span><span class="sxs-lookup"><span data-stu-id="fc68a-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="fc68a-125">成對的調整 VM 大小</span><span class="sxs-lookup"><span data-stu-id="fc68a-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="fc68a-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="fc68a-126">Standard_A0</span></span> |<span data-ttu-id="fc68a-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="fc68a-127">Standard_A11</span></span> |
> | <span data-ttu-id="fc68a-128">標準_D1</span><span class="sxs-lookup"><span data-stu-id="fc68a-128">Standard_D1</span></span> |<span data-ttu-id="fc68a-129">標準_D14</span><span class="sxs-lookup"><span data-stu-id="fc68a-129">Standard_D14</span></span> |
> | <span data-ttu-id="fc68a-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="fc68a-130">Standard_DS1</span></span> |<span data-ttu-id="fc68a-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="fc68a-131">Standard_DS14</span></span> |
> | <span data-ttu-id="fc68a-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="fc68a-132">Standard_D1v2</span></span> |<span data-ttu-id="fc68a-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="fc68a-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="fc68a-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="fc68a-134">Standard_G1</span></span> |<span data-ttu-id="fc68a-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="fc68a-135">Standard_G5</span></span> |
> | <span data-ttu-id="fc68a-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="fc68a-136">Standard_GS1</span></span> |<span data-ttu-id="fc68a-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="fc68a-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="fc68a-138">使用執行身分功能來建立 Azure 自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="fc68a-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="fc68a-139">您需要做的第一件事是建立將裝載 Runbook 的 Azure 自動化帳戶，而 Runbook 用來調整 VM 調整集執行個體。</span><span class="sxs-lookup"><span data-stu-id="fc68a-139">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale the VM Scale Set instances.</span></span> <span data-ttu-id="fc68a-140">最近， [Azure 自動化](https://azure.microsoft.com/services/automation/) 引進「執行身分帳戶」功能，極輕鬆即可代表使用者設定服務主體自動執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fc68a-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on a user's behalf very easy.</span></span> <span data-ttu-id="fc68a-141">您可以在下文中閱讀更多相關資訊：</span><span class="sxs-lookup"><span data-stu-id="fc68a-141">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="fc68a-142">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="fc68a-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="fc68a-143">將 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fc68a-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="fc68a-144">Azure 自動化 Runbook 資源庫已發佈垂直調整 VM 擴展集所需之 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fc68a-144">The runbooks needed to vertically scale your VM Scale Sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="fc68a-145">若要將其匯入到您的訂用帳戶，請依照這篇文章的步驟︰</span><span class="sxs-lookup"><span data-stu-id="fc68a-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="fc68a-146">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="fc68a-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="fc68a-147">從 [Runbooks] 功能表選擇 [瀏覽資源庫] 選項︰</span><span class="sxs-lookup"><span data-stu-id="fc68a-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![要匯入的 Runbook][runbooks]

<span data-ttu-id="fc68a-149">需要如下所示匯入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="fc68a-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="fc68a-150">根據您要使用重新佈建來垂直調整，以選取 Runbook：</span><span class="sxs-lookup"><span data-stu-id="fc68a-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbook 資源庫][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="fc68a-152">將 Webhook 加入您的 Runbook 中</span><span class="sxs-lookup"><span data-stu-id="fc68a-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="fc68a-153">匯入 Runbook 之後，需要將 Webhook 加入 Runbook 中，如此即可從 VM 擴展集發出的警示加以觸發。</span><span class="sxs-lookup"><span data-stu-id="fc68a-153">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a VM Scale Set.</span></span> <span data-ttu-id="fc68a-154">本文說明如何為 Runbook 建立 Webhook 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="fc68a-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="fc68a-155">Azure 自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="fc68a-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="fc68a-156">關閉 Webhook 對話方塊之前，請務必複製 Webhook URI，因為在下一節中將需要此 Webhook。</span><span class="sxs-lookup"><span data-stu-id="fc68a-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-vm-scale-set"></a><span data-ttu-id="fc68a-157">將警示加入至 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="fc68a-157">Add an alert to your VM Scale Set</span></span>
<span data-ttu-id="fc68a-158">下面是顯示如何將警示新增至 VM 擴展集的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="fc68a-158">Below is a PowerShell script which shows how to add an alert to a VM Scale Set.</span></span> <span data-ttu-id="fc68a-159">請參閱下列文章，取得度量名稱以引發警示︰[Azure 監視器自動調整的常用度量](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="fc68a-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

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
> <span data-ttu-id="fc68a-160">建議您設定合理的警示時間範圍以避免頻繁觸發垂直調整，及任何相關聯的服務中斷。</span><span class="sxs-lookup"><span data-stu-id="fc68a-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="fc68a-161">請考慮至少 20-30 分鐘以上的時段。</span><span class="sxs-lookup"><span data-stu-id="fc68a-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="fc68a-162">如果需要避免任何中斷，請考慮水平調整。</span><span class="sxs-lookup"><span data-stu-id="fc68a-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="fc68a-163">如需如何建立警示的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="fc68a-163">For more information on how to create alerts refer to the following articles:</span></span>

* [<span data-ttu-id="fc68a-164">Azure 監視器 PowerShell 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="fc68a-164">Azure Monitor PowerShell quick start samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="fc68a-165">Azure 監視器跨平台 CLI 快速入門範例</span><span class="sxs-lookup"><span data-stu-id="fc68a-165">Azure Monitor Cross-platform CLI quick start samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="fc68a-166">摘要</span><span class="sxs-lookup"><span data-stu-id="fc68a-166">Summary</span></span>
<span data-ttu-id="fc68a-167">這篇文章示範簡單的垂直調整範例。</span><span class="sxs-lookup"><span data-stu-id="fc68a-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="fc68a-168">藉助這些建置組塊 (自動化帳戶、Runbook、Webhook、警示)，您可以連接各式各樣的事件與一組自訂的動作。</span><span class="sxs-lookup"><span data-stu-id="fc68a-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
