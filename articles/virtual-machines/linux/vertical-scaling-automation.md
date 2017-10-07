---
title: "aaaVertically 小數位數與 Azure 自動化的 Azure 虛擬機器 |Microsoft 文件"
description: "如何 toovertically 調整回應 toomonitoring 警示與 Azure 自動化中的 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dcee199e-fa25-44d5-9b25-df564cee9b45
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/29/2016
ms.author: singhkay
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee4c1c33a588bd907d107f1828380a8afdaa725e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vertically-scale-azure-linux-virtual-machine-with-azure-automation"></a><span data-ttu-id="5d412-103">使用 Azure 自動化來垂直調整 Azure Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d412-103">Vertically scale Azure Linux virtual machine with Azure Automation</span></span>
<span data-ttu-id="5d412-104">垂直延展是增加或減少回應 toohello 工作負載中電腦的 hello 資源 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5d412-104">Vertical scaling is hello process of increasing or decreasing hello resources of a machine in response toohello workload.</span></span> <span data-ttu-id="5d412-105">在 Azure 中達成這點可以藉由變更 hello hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="5d412-105">In Azure this can be accomplished by changing hello size of hello Virtual Machine.</span></span> <span data-ttu-id="5d412-106">這可協助在下列案例的 hello</span><span class="sxs-lookup"><span data-stu-id="5d412-106">This can help in hello following scenarios</span></span>

* <span data-ttu-id="5d412-107">如果未使用經常 hello 虛擬機器，可以調整 tooa 較小的大小 tooreduce 向您的每月成本</span><span class="sxs-lookup"><span data-stu-id="5d412-107">If hello Virtual Machine is not being used frequently, you can resize it down tooa smaller size tooreduce your monthly costs</span></span>
* <span data-ttu-id="5d412-108">如果 hello 虛擬機器會看見尖峰負載，它可以是調整過大小的 tooa 較大的大小 tooincrease 其容量</span><span class="sxs-lookup"><span data-stu-id="5d412-108">If hello Virtual Machine is seeing a peak load, it can be resized tooa larger size tooincrease its capacity</span></span>

<span data-ttu-id="5d412-109">這是與 hello 步驟 tooaccomplish 的 hello 大綱下方</span><span class="sxs-lookup"><span data-stu-id="5d412-109">hello outline for hello steps tooaccomplish this is as below</span></span>

1. <span data-ttu-id="5d412-110">設定 Azure 自動化 tooaccess 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d412-110">Setup Azure Automation tooaccess your Virtual Machines</span></span>
2. <span data-ttu-id="5d412-111">Hello 垂直延展的 Azure 自動化 runbook 匯入您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d412-111">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
3. <span data-ttu-id="5d412-112">加入 webhook tooyour runbook</span><span class="sxs-lookup"><span data-stu-id="5d412-112">Add a webhook tooyour runbook</span></span>
4. <span data-ttu-id="5d412-113">新增警示 tooyour 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d412-113">Add an alert tooyour Virtual Machine</span></span>

> [!NOTE]
> <span data-ttu-id="5d412-114">因為 hello hello 大小而第一個虛擬機器，它可以調整，以 hello 大小可能會有所限制到期的 hello toohello 可用性 hello 叢集中其他大小目前部署虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="5d412-114">Because of hello size of hello first Virtual Machine, hello sizes it can be scaled to, may be limited due toohello availability of hello other sizes in hello cluster current Virtual Machine is deployed in.</span></span> <span data-ttu-id="5d412-115">在 hello 發行我們處理此情況下，只調整 VM 大小組下方 hello 內這篇文章中使用自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="5d412-115">In hello published automation runbooks used in this article we take care of this case and only scale within hello below VM size pairs.</span></span> <span data-ttu-id="5d412-116">這表示不突然將 tooStandard_G5 來擴充或縮小 tooBasic_A0 Standard_D1v2 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d412-116">This means that a Standard_D1v2 Virtual Machine will not suddenly be scaled up tooStandard_G5 or scaled down tooBasic_A0.</span></span>
> 
> | <span data-ttu-id="5d412-117">成對的調整 VM 大小</span><span class="sxs-lookup"><span data-stu-id="5d412-117">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="5d412-118">Basic_A0</span><span class="sxs-lookup"><span data-stu-id="5d412-118">Basic_A0</span></span> |<span data-ttu-id="5d412-119">Basic_A4</span><span class="sxs-lookup"><span data-stu-id="5d412-119">Basic_A4</span></span> |
> | <span data-ttu-id="5d412-120">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="5d412-120">Standard_A0</span></span> |<span data-ttu-id="5d412-121">Standard_A4</span><span class="sxs-lookup"><span data-stu-id="5d412-121">Standard_A4</span></span> |
> | <span data-ttu-id="5d412-122">Standard_A5</span><span class="sxs-lookup"><span data-stu-id="5d412-122">Standard_A5</span></span> |<span data-ttu-id="5d412-123">Standard_A7</span><span class="sxs-lookup"><span data-stu-id="5d412-123">Standard_A7</span></span> |
> | <span data-ttu-id="5d412-124">Standard_A8</span><span class="sxs-lookup"><span data-stu-id="5d412-124">Standard_A8</span></span> |<span data-ttu-id="5d412-125">Standard_A9</span><span class="sxs-lookup"><span data-stu-id="5d412-125">Standard_A9</span></span> |
> | <span data-ttu-id="5d412-126">Standard_A10</span><span class="sxs-lookup"><span data-stu-id="5d412-126">Standard_A10</span></span> |<span data-ttu-id="5d412-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="5d412-127">Standard_A11</span></span> |
> | <span data-ttu-id="5d412-128">標準_D1</span><span class="sxs-lookup"><span data-stu-id="5d412-128">Standard_D1</span></span> |<span data-ttu-id="5d412-129">標準_D4</span><span class="sxs-lookup"><span data-stu-id="5d412-129">Standard_D4</span></span> |
> | <span data-ttu-id="5d412-130">標準_D11</span><span class="sxs-lookup"><span data-stu-id="5d412-130">Standard_D11</span></span> |<span data-ttu-id="5d412-131">標準_D14</span><span class="sxs-lookup"><span data-stu-id="5d412-131">Standard_D14</span></span> |
> | <span data-ttu-id="5d412-132">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="5d412-132">Standard_DS1</span></span> |<span data-ttu-id="5d412-133">Standard_DS4</span><span class="sxs-lookup"><span data-stu-id="5d412-133">Standard_DS4</span></span> |
> | <span data-ttu-id="5d412-134">Standard_DS11</span><span class="sxs-lookup"><span data-stu-id="5d412-134">Standard_DS11</span></span> |<span data-ttu-id="5d412-135">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="5d412-135">Standard_DS14</span></span> |
> | <span data-ttu-id="5d412-136">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="5d412-136">Standard_D1v2</span></span> |<span data-ttu-id="5d412-137">Standard_D5v2</span><span class="sxs-lookup"><span data-stu-id="5d412-137">Standard_D5v2</span></span> |
> | <span data-ttu-id="5d412-138">Standard_D11v2</span><span class="sxs-lookup"><span data-stu-id="5d412-138">Standard_D11v2</span></span> |<span data-ttu-id="5d412-139">Standard_D14v2</span><span class="sxs-lookup"><span data-stu-id="5d412-139">Standard_D14v2</span></span> |
> | <span data-ttu-id="5d412-140">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="5d412-140">Standard_G1</span></span> |<span data-ttu-id="5d412-141">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="5d412-141">Standard_G5</span></span> |
> | <span data-ttu-id="5d412-142">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="5d412-142">Standard_GS1</span></span> |<span data-ttu-id="5d412-143">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="5d412-143">Standard_GS5</span></span> |
> 
> 

## <a name="setup-azure-automation-tooaccess-your-virtual-machines"></a><span data-ttu-id="5d412-144">設定 Azure 自動化 tooaccess 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d412-144">Setup Azure Automation tooaccess your Virtual Machines</span></span>
<span data-ttu-id="5d412-145">您需要 toodo hello 第一件事是建立 Azure 自動化帳戶將裝載 hello runbook 使用 tooscale hello VM 規模調整集合執行個體。</span><span class="sxs-lookup"><span data-stu-id="5d412-145">hello first thing you need toodo is create an Azure Automation account that will host hello runbooks used tooscale hello VM Scale Set instances.</span></span> <span data-ttu-id="5d412-146">最近 hello 自動化服務導入了 hello 「 執行身分帳戶 」 功能會自動執行 hello runbook 代表 hello 使用者很容易讓 hello 服務主體的設定。</span><span class="sxs-lookup"><span data-stu-id="5d412-146">Recently hello Automation service introduced hello "Run As account" feature which makes setting up hello Service Principal for automatically running hello runbooks on hello user's behalf very easy.</span></span> <span data-ttu-id="5d412-147">閱讀更多關於此 hello 的下列文件中：</span><span class="sxs-lookup"><span data-stu-id="5d412-147">You can read more about this in hello article below:</span></span>

* [<span data-ttu-id="5d412-148">使用 Azure 執行身分帳戶驗證 Runbook</span><span class="sxs-lookup"><span data-stu-id="5d412-148">Authenticate Runbooks with Azure Run As account</span></span>](../../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-hello-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="5d412-149">Hello 垂直延展的 Azure 自動化 runbook 匯入您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d412-149">Import hello Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="5d412-150">所需的垂直調整您的虛擬機器已經發行 hello Azure 自動化 Runbook 資源庫中的 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="5d412-150">hello runbooks that are needed for Vertically Scaling your Virtual Machine are already published in hello Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="5d412-151">您將需要 tooimport 為您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d412-151">You will need tooimport them into your subscription.</span></span> <span data-ttu-id="5d412-152">您可以了解如何藉由讀取 tooimport runbook hello 下列文章。</span><span class="sxs-lookup"><span data-stu-id="5d412-152">You can learn how tooimport runbooks by reading hello following article.</span></span>

* [<span data-ttu-id="5d412-153">Azure 自動化的 Runbook 和模組資源庫</span><span class="sxs-lookup"><span data-stu-id="5d412-153">Runbook and module galleries for Azure Automation</span></span>](../../automation/automation-runbook-gallery.md)

<span data-ttu-id="5d412-154">需要 toobe 匯入的 hello runbook 所示 hello 圖</span><span class="sxs-lookup"><span data-stu-id="5d412-154">hello runbooks that need toobe imported are shown in hello image below</span></span>

![匯入 Runbook](./media/vertical-scaling-automation/scale-runbooks.png)

## <a name="add-a-webhook-tooyour-runbook"></a><span data-ttu-id="5d412-156">加入 webhook tooyour runbook</span><span class="sxs-lookup"><span data-stu-id="5d412-156">Add a webhook tooyour runbook</span></span>
<span data-ttu-id="5d412-157">您已匯入 hello runbook 之後您將需要 tooadd webhook toohello runbook，如此可藉由從虛擬機器警示。</span><span class="sxs-lookup"><span data-stu-id="5d412-157">Once you've imported hello runbooks you'll need tooadd a webhook toohello runbook so it can be triggered by an alert from a Virtual Machine.</span></span> <span data-ttu-id="5d412-158">為您的 Runbook 建立 webhook hello 詳細資料可以在這裡</span><span class="sxs-lookup"><span data-stu-id="5d412-158">hello details of creating a webhook for your Runbook can be read here</span></span>

* [<span data-ttu-id="5d412-159">Azure 自動化 Webhook</span><span class="sxs-lookup"><span data-stu-id="5d412-159">Azure Automation webhooks</span></span>](../../automation/automation-webhooks.md)

<span data-ttu-id="5d412-160">請確定您複製 hello webhook 之後才關閉 hello webhook 對話方塊，將會需要這個 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="5d412-160">Make sure you copy hello webhook before closing hello webhook dialog as you will need this in hello next section.</span></span>

## <a name="add-an-alert-tooyour-virtual-machine"></a><span data-ttu-id="5d412-161">新增警示 tooyour 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d412-161">Add an alert tooyour Virtual Machine</span></span>
1. <span data-ttu-id="5d412-162">選取虛擬機器設定</span><span class="sxs-lookup"><span data-stu-id="5d412-162">Select Virtual Machine settings</span></span>
2. <span data-ttu-id="5d412-163">選取 [警示規則]</span><span class="sxs-lookup"><span data-stu-id="5d412-163">Select "Alert rules"</span></span>
3. <span data-ttu-id="5d412-164">選取 [加入警示]</span><span class="sxs-lookup"><span data-stu-id="5d412-164">Select "Add alert"</span></span>
4. <span data-ttu-id="5d412-165">在選取度量 toofire hello 警示</span><span class="sxs-lookup"><span data-stu-id="5d412-165">Select a metric toofire hello alert on</span></span>
5. <span data-ttu-id="5d412-166">選取條件，當完成將導致 hello 警示 toofire</span><span class="sxs-lookup"><span data-stu-id="5d412-166">Select a condition, which when fulfilled will cause hello alert toofire</span></span>
6. <span data-ttu-id="5d412-167">選取在步驟 5 中的 hello 條件的臨界值。</span><span class="sxs-lookup"><span data-stu-id="5d412-167">Select a threshold for hello condition in Step 5.</span></span> <span data-ttu-id="5d412-168">toobe 完成</span><span class="sxs-lookup"><span data-stu-id="5d412-168">toobe fulfilled</span></span>
7. <span data-ttu-id="5d412-169">在步驟 5 和 6 選取的期間透過哪一個 hello 監視服務會檢查 hello 條件和臨界值</span><span class="sxs-lookup"><span data-stu-id="5d412-169">Select a period over which hello monitoring service will check for hello condition and threshold in Steps 5 & 6</span></span>
8. <span data-ttu-id="5d412-170">貼上您複製 hello 前一節的 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="5d412-170">Paste in hello webhook you copied from hello previous section.</span></span>

![新增警示 tooVirtual 機器 1](./media/vertical-scaling-automation/add-alert-webhook-1.png)

![新增警示 tooVirtual 機器 2](./media/vertical-scaling-automation/add-alert-webhook-2.png)

