---
title: "使用 Azure 網路監看員管理網路安全性群組流量記錄 | Microsoft Docs"
description: "此頁面說明如何在 Azure 網路監看員中管理網路安全性群組流量記錄"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 41cb5ffab9bd3a3bed75ffdb6a7383ca1690f810
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="322e4-103">在 Azure 入口網站中管理網路安全性群組流量記錄</span><span class="sxs-lookup"><span data-stu-id="322e4-103">Manage network security group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="322e4-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="322e4-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="322e4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="322e4-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="322e4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="322e4-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="322e4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="322e4-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="322e4-108">REST API</span><span class="sxs-lookup"><span data-stu-id="322e4-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="322e4-109">網路安全性群組流量記錄是網路監看員的一項功能，可讓您檢視透過網路安全性群組傳輸的輸入和輸出 IP 流量相關資訊。</span><span class="sxs-lookup"><span data-stu-id="322e4-109">Network security group flow logs are a feature of Network Watcher that enables you to view information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="322e4-110">這些流量記錄是以 JSON 格式寫入，並提供重要資訊，包括：</span><span class="sxs-lookup"><span data-stu-id="322e4-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="322e4-111">每個規則的輸出和輸入流量。</span><span class="sxs-lookup"><span data-stu-id="322e4-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="322e4-112">套用流量的 NIC。</span><span class="sxs-lookup"><span data-stu-id="322e4-112">The NIC that the flow applies to.</span></span>
- <span data-ttu-id="322e4-113">與流量相關的 5-Tuple 資訊 (來源/目的地 IP、來源/目的地連接埠，通訊協定)。</span><span class="sxs-lookup"><span data-stu-id="322e4-113">5-tuple information about the flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="322e4-114">流量被允許或拒絕的資訊。</span><span class="sxs-lookup"><span data-stu-id="322e4-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="322e4-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="322e4-115">Before you begin</span></span>

<span data-ttu-id="322e4-116">此案例假設您已依照[建立網路監看員執行個體](network-watcher-create.md)中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="322e4-116">This scenario assumes you have already followed the steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="322e4-117">此案例也假設您已擁有具備有效虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="322e4-117">The scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="322e4-118">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="322e4-118">Register Insights provider</span></span>

<span data-ttu-id="322e4-119">為了讓流量記錄成功運作，您必須註冊 **Microsoft.Insights** 提供者。</span><span class="sxs-lookup"><span data-stu-id="322e4-119">For flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="322e4-120">若要註冊提供者，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="322e4-120">To register the provider, take the following steps:</span></span> 

1. <span data-ttu-id="322e4-121">移至 [訂用帳戶]，然後選取您要為其啟用流量記錄的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="322e4-121">Go to **Subscriptions**, and then select the subscription for which you want to enable flow logs.</span></span> 
2. <span data-ttu-id="322e4-122">在 [訂用帳戶] 刀鋒視窗中，選取 [資源提供者]。</span><span class="sxs-lookup"><span data-stu-id="322e4-122">On the **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="322e4-123">查看提供者清單，並確認 **microsoft.insights** 提供者已註冊。</span><span class="sxs-lookup"><span data-stu-id="322e4-123">Look at the list of providers, and verify that the **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="322e4-124">如果沒有，則選取 [註冊]。</span><span class="sxs-lookup"><span data-stu-id="322e4-124">If not, then select **Register**.</span></span>

![檢視提供者][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="322e4-126">啟用流量記錄</span><span class="sxs-lookup"><span data-stu-id="322e4-126">Enable flow logs</span></span>

<span data-ttu-id="322e4-127">這些步驟會引導您完成在網路安全性群組上啟用流量記錄的程序。</span><span class="sxs-lookup"><span data-stu-id="322e4-127">These steps take you through the process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="322e4-128">步驟 1</span><span class="sxs-lookup"><span data-stu-id="322e4-128">Step 1</span></span>

<span data-ttu-id="322e4-129">移至網路監看員執行個體，然後選取 [NSG 流量記錄]。</span><span class="sxs-lookup"><span data-stu-id="322e4-129">Go to a Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![流量記錄概觀][1]

### <a name="step-2"></a><span data-ttu-id="322e4-131">步驟 2</span><span class="sxs-lookup"><span data-stu-id="322e4-131">Step 2</span></span>

<span data-ttu-id="322e4-132">從清單中選取網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="322e4-132">Select a network security group from the list.</span></span>

![流量記錄概觀][2]

### <a name="step-3"></a><span data-ttu-id="322e4-134">步驟 3</span><span class="sxs-lookup"><span data-stu-id="322e4-134">Step 3</span></span> 

<span data-ttu-id="322e4-135">在 [流量記錄設定] 刀鋒視窗上，將狀態設為 [開啟] 並設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="322e4-135">On the **Flow logs settings** blade, set the status to **On**, and then configure a storage account.</span></span>  <span data-ttu-id="322e4-136">完成後，選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="322e4-136">When you're done, select **OK**.</span></span> <span data-ttu-id="322e4-137">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="322e4-137">Then select **Save**.</span></span>

![流量記錄概觀][3]

## <a name="download-flow-logs"></a><span data-ttu-id="322e4-139">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="322e4-139">Download flow logs</span></span>

<span data-ttu-id="322e4-140">流量記錄會儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="322e4-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="322e4-141">下載流量記錄以檢視它們。</span><span class="sxs-lookup"><span data-stu-id="322e4-141">Download your flow logs to view them.</span></span>

### <a name="step-1"></a><span data-ttu-id="322e4-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="322e4-142">Step 1</span></span>

<span data-ttu-id="322e4-143">若要下載流量記錄，請選取 [您可從設定的儲存體帳戶下載流量記錄檔]。</span><span class="sxs-lookup"><span data-stu-id="322e4-143">To download flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="322e4-144">此步驟會帶您前往儲存體帳戶檢視，以便在該處選擇要下載的記錄。</span><span class="sxs-lookup"><span data-stu-id="322e4-144">This step takes you to a storage account view where you can choose which logs to download.</span></span>

![流量記錄設定][4]

### <a name="step-2"></a><span data-ttu-id="322e4-146">步驟 2</span><span class="sxs-lookup"><span data-stu-id="322e4-146">Step 2</span></span>

<span data-ttu-id="322e4-147">移至正確的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="322e4-147">Go to the correct storage account.</span></span> <span data-ttu-id="322e4-148">然後選取 [容器] > [insights-log-networksecuritygroupflowevent]。</span><span class="sxs-lookup"><span data-stu-id="322e4-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![流量記錄設定][5]

### <a name="step-3"></a><span data-ttu-id="322e4-150">步驟 3</span><span class="sxs-lookup"><span data-stu-id="322e4-150">Step 3</span></span>

<span data-ttu-id="322e4-151">移至流量記錄的位置並選取它，然後選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="322e4-151">Go to the location of the flow log, select it, and then select **Download**.</span></span>

![流量記錄設定][6]

<span data-ttu-id="322e4-153">如需記錄結構的相關資訊，請造訪[網路安全性群組流量記錄概觀](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="322e4-153">For information about the structure of the log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="322e4-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="322e4-154">Next steps</span></span>

<span data-ttu-id="322e4-155">了解如何[使用 PowerBI 視覺化 NSG 流量記錄](network-watcher-visualize-nsg-flow-logs-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="322e4-155">Learn how to [visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
