---
title: "使用 Azure 自動化來垂直調整 Azure 虛擬機器 | Microsoft Docs"
description: "使用「Azure 自動化」來垂直調整「Windows 虛擬機器」以回應監視警示"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4f964713-fb67-4bcc-8246-3431452ddf7d
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: kasing
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ea5169c1a95f00e78ae3f5f177812466eb7a0deb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="vertically-scale-windows-vms-with-azure-automation"></a><span data-ttu-id="62cf8-103">使用 Azure 自動化來垂直調整 Windows VM</span><span class="sxs-lookup"><span data-stu-id="62cf8-103">Vertically scale Windows VMs with Azure Automation</span></span>

<span data-ttu-id="62cf8-104">垂直調整大小是指為回應工作負載而增加或減少電腦資源的程序。</span><span class="sxs-lookup"><span data-stu-id="62cf8-104">Vertical scaling is the process of increasing or decreasing the resources of a machine in response to the workload.</span></span> <span data-ttu-id="62cf8-105">在 Azure 中，可以透過變更虛擬機器的大小來完成。</span><span class="sxs-lookup"><span data-stu-id="62cf8-105">In Azure this can be accomplished by changing the size of the Virtual Machine.</span></span> <span data-ttu-id="62cf8-106">在下列情況中這種方式很有幫助</span><span class="sxs-lookup"><span data-stu-id="62cf8-106">This can help in the following scenarios</span></span>

* <span data-ttu-id="62cf8-107">如果不常使用虛擬機器，可以將其調整成較小的規模，以降低每月成本</span><span class="sxs-lookup"><span data-stu-id="62cf8-107">If the Virtual Machine is not being used frequently, you can resize it down to a smaller size to reduce your monthly costs</span></span>
* <span data-ttu-id="62cf8-108">如果虛擬機器預期會有尖峰負載，可以將其調整成較大的規模，以增加其容量</span><span class="sxs-lookup"><span data-stu-id="62cf8-108">If the Virtual Machine is seeing a peak load, it can be resized to a larger size to increase its capacity</span></span>

<span data-ttu-id="62cf8-109">完成此作業的步驟大致如下</span><span class="sxs-lookup"><span data-stu-id="62cf8-109">The outline for the steps to accomplish this is as below</span></span>

1. <span data-ttu-id="62cf8-110">將 Azure 自動化設定為可存取您的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="62cf8-110">Setup Azure Automation to access your Virtual Machines</span></span>
2. <span data-ttu-id="62cf8-111">將 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="62cf8-111">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="62cf8-112">將 Webhook 加入您的 Runbook 中</span><span class="sxs-lookup"><span data-stu-id="62cf8-112">Add a webhook to your runbook</span></span>
4. <span data-ttu-id="62cf8-113">將警示加入虛擬機器中</span><span class="sxs-lookup"><span data-stu-id="62cf8-113">Add an alert to your Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="62cf8-114">因為這是第一部虛擬機器大小的緣故，所以它可以調整的大小，會受限於目前虛擬機器部署所在之叢集中是否可使用其他大小。</span><span class="sxs-lookup"><span data-stu-id="62cf8-114">Because of the size of the first Virtual Machine, the sizes it can be scaled to, may be limited due to the availability of the other sizes in the cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="62cf8-115">本文所用的已發佈自動化 Runbook 中，已考量了這個情況，只會於下列成對的 VM 大小內調整大小。</span><span class="sxs-lookup"><span data-stu-id="62cf8-115">In the published automation runbooks used in this article we take care of this case and only scale within the below VM size pairs.</span></span> <span data-ttu-id="62cf8-116">這表示 Standard_D1v2 虛擬機器不會突然相應增加為 Standard_G5 或相應減少為 Basic_A0。</span><span class="sxs-lookup"><span data-stu-id="62cf8-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up to Standard_G5 or scaled down to Basic_A0.</span></span>
> 
> | <span data-ttu-id="62cf8-117">成對的調整 VM 大小</span><span class="sxs-lookup"><span data-stu-id="62cf8-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="62cf8-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="62cf8-118">Basic_A0</span></span> |<span data-ttu-id="62cf8-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="62cf8-119">Basic_A4</span></span> |
> | <span data-ttu-id="62cf8-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="62cf8-120">Standard_A0</span></span> |<span data-ttu-id="62cf8-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="62cf8-121">Standard_A4</span></span> |
> | <span data-ttu-id="62cf8-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="62cf8-122">Standard_A5</span></span> |<span data-ttu-id="62cf8-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="62cf8-123">Standard_A7</span></span> |
> | <span data-ttu-id="62cf8-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="62cf8-124">Standard_A8</span></span> |<span data-ttu-id="62cf8-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="62cf8-125">Standard_A9</span></span> |
> | <span data-ttu-id="62cf8-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="62cf8-126">Standard_A10</span></span> |<span data-ttu-id="62cf8-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="62cf8-127">Standard_A11</span></span> |
> | <span data-ttu-id="62cf8-128">標準_D1</span><span class="sxs-lookup"><span data-stu-id="62cf8-128">Standard_D1</span></span> |<span data-ttu-id="62cf8-129">標準_D4</span><span class="sxs-lookup"><span data-stu-id="62cf8-129">Standard_D4</span></span> |
> | <span data-ttu-id="62cf8-130">標準_D11</span><span class="sxs-lookup"><span data-stu-id="62cf8-130">Standard_D11</span></span> |<span data-ttu-id="62cf8-131">標準_D14</span><span class="sxs-lookup"><span data-stu-id="62cf8-131">Standard_D14</span></span> |
> | <span data-ttu-id="62cf8-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="62cf8-132">Standard_DS1</span></span> |<span data-ttu-id="62cf8-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="62cf8-133">Standard_DS4</span></span> |
> | <span data-ttu-id="62cf8-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="62cf8-134">Standard_DS11</span></span> |<span data-ttu-id="62cf8-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="62cf8-135">Standard_DS14</span></span> |
> | <span data-ttu-id="62cf8-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="62cf8-136">Standard_D1v2</span></span> |<span data-ttu-id="62cf8-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="62cf8-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="62cf8-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="62cf8-138">Standard_D11v2</span></span> |<span data-ttu-id="62cf8-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="62cf8-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="62cf8-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="62cf8-140">Standard_G1</span></span> |<span data-ttu-id="62cf8-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="62cf8-141">Standard_G5</span></span> |
> | <span data-ttu-id="62cf8-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="62cf8-142">Standard_GS1</span></span> |<span data-ttu-id="62cf8-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="62cf8-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-to-access-your-virtual-machines"></a><span data-ttu-id="62cf8-144">將 Azure 自動化設定為可存取您的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="62cf8-144">Setup Azure Automation to access your Virtual Machines</span></span>
<span data-ttu-id="62cf8-145">您首先要做的是建立 Azure 自動化帳戶，其要裝載用來調整虛擬機器的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-145">The first thing you need to do is create an Azure Automation account that will host the runbooks used to scale a Virtual Machine.</span></span> <span data-ttu-id="62cf8-146">最近，自動化服務引進「執行身分帳戶」功能，極輕鬆即可代表使用者設定服務主體來自動執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-146">Recently the Automation service introduced the "Run As account" feature which makes setting up the Service Principal for automatically running the runbooks on the user's behalf very easy.</span></span> <span data-ttu-id="62cf8-147">您可以在下文中閱讀更多相關資訊：</span><span class="sxs-lookup"><span data-stu-id="62cf8-147">You can read more about this in the article below:</span></span>

* [<span data-ttu-id="62cf8-148">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="62cf8-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-the-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="62cf8-149">將 Azure 自動化垂直調整大小 Runbook 匯入訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="62cf8-149">Import the Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="62cf8-150">Azure 自動化 Runbook 資源庫中已發佈的垂直調整虛擬機器大小所需之 Runbook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-150">The runbooks that are needed for Vertically Scaling your Virtual Machine are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="62cf8-151">您必須將其匯入您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="62cf8-151">You will need to import them into your subscription.</span></span> <span data-ttu-id="62cf8-152">您可以閱讀下列文章，了解如何匯入 Runbook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-152">You can learn how to import runbooks by reading the following article.</span></span>

* [<span data-ttu-id="62cf8-153">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="62cf8-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="62cf8-154">需要如下圖所示匯入 Runbook</span><span class="sxs-lookup"><span data-stu-id="62cf8-154">The runbooks that need to be imported are shown in the image below</span></span>

![匯入 Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="62cf8-156">將 Webhook 加入您的 Runbook 中</span><span class="sxs-lookup"><span data-stu-id="62cf8-156">Add a webhook to your runbook</span></span>
<span data-ttu-id="62cf8-157">匯入 Runbook 之後，需要將 Webhook 加入 Runbook 中，如此即可從虛擬機器發出的警示加以觸發。</span><span class="sxs-lookup"><span data-stu-id="62cf8-157">Once you've imported the runbooks you'll need to add a webhook to the runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="62cf8-158">如需為 Runbook 建立 Webhook 的詳細資訊，請參閱</span><span class="sxs-lookup"><span data-stu-id="62cf8-158">The details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="62cf8-159">Azure 自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="62cf8-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="62cf8-160">關閉 Webhook 對話方塊之前，請務必複製 Webhook，因為在下一節中將需要此 Webhook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-160">Make sure you copy the webhook before closing the webhook dialog as you will need this in the next section.</span></span>

## <a name="add-an-alert-to-your-virtual-machine"></a><span data-ttu-id="62cf8-161">將警示加入虛擬機器中</span><span class="sxs-lookup"><span data-stu-id="62cf8-161">Add an alert to your Virtual Machine</span></span>
1. <span data-ttu-id="62cf8-162">選取虛擬機器設定</span><span class="sxs-lookup"><span data-stu-id="62cf8-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="62cf8-163">選取 [警示規則]</span><span class="sxs-lookup"><span data-stu-id="62cf8-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="62cf8-164">選取 [加入警示]</span><span class="sxs-lookup"><span data-stu-id="62cf8-164">Select "Add alert"</span></span>
4. <span data-ttu-id="62cf8-165">選取要引發警示的衡量標準</span><span class="sxs-lookup"><span data-stu-id="62cf8-165">Select a metric to fire the alert on</span></span>
5. <span data-ttu-id="62cf8-166">選取要符合才會引發警示的條件</span><span class="sxs-lookup"><span data-stu-id="62cf8-166">Select a condition, which when fulfilled will cause the alert to fire</span></span>
6. <span data-ttu-id="62cf8-167">針對步驟 5 的條件選取臨界值。</span><span class="sxs-lookup"><span data-stu-id="62cf8-167">Select a threshold for the condition in Step 5.</span></span> <span data-ttu-id="62cf8-168">要符合的</span><span class="sxs-lookup"><span data-stu-id="62cf8-168">to be fulfilled</span></span>
7. <span data-ttu-id="62cf8-169">選取監視服務將檢查步驟 5 和 6 之條件和臨界值的期間</span><span class="sxs-lookup"><span data-stu-id="62cf8-169">Select a period over which the monitoring service will check for the condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="62cf8-170">貼上從上一節複製的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="62cf8-170">Paste in the webhook you copied from the previous section.</span></span>

![將警示加入虛擬機器 1 中](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![將警示加入虛擬機器 2 中](./media/vertical-scaling-automation/add-alert-webhook-2.png)

