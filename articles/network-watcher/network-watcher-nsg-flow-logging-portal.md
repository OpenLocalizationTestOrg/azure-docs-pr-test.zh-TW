---
title: "aaaManage 網路安全性群組流程記錄檔與 Azure 網路監看員 |Microsoft 文件"
description: "此頁面說明 toomanage 網路安全性小組流程如何登入 Azure 網路監看員"
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
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a><span data-ttu-id="4ac2d-103">管理網路安全性群組資料流程中的記錄檔 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4ac2d-103">Manage network security group flow logs in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4ac2d-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4ac2d-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="4ac2d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ac2d-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="4ac2d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4ac2d-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="4ac2d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4ac2d-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="4ac2d-108">REST API</span><span class="sxs-lookup"><span data-stu-id="4ac2d-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="4ac2d-109">網路安全性群組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-109">Network security group flow logs are a feature of Network Watcher that enables you tooview information about ingress and egress IP traffic through a network security group.</span></span> <span data-ttu-id="4ac2d-110">這些流量記錄是以 JSON 格式寫入，並提供重要資訊，包括：</span><span class="sxs-lookup"><span data-stu-id="4ac2d-110">These flow logs are written in JSON format and provide important information, including:</span></span> 

- <span data-ttu-id="4ac2d-111">每個規則的輸出和輸入流量。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-111">Outbound and inbound flows on a per-rule basis.</span></span>
- <span data-ttu-id="4ac2d-112">hello NIC hello 流程，適用於。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-112">hello NIC that hello flow applies to.</span></span>
- <span data-ttu-id="4ac2d-113">5 個 tuple hello 資料流程來源/目的地 IP、 來源/目的地連接埠 （通訊協定） 資訊。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-113">5-tuple information about hello flow (source/destination IP, source/destination port, protocol).</span></span>
- <span data-ttu-id="4ac2d-114">流量被允許或拒絕的資訊。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-114">Information about whether traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ac2d-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="4ac2d-115">Before you begin</span></span>

<span data-ttu-id="4ac2d-116">此案例假設您已依照中的 hello 步驟[建立網路監看員執行個體](network-watcher-create.md)。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher instance](network-watcher-create.md).</span></span> <span data-ttu-id="4ac2d-117">hello 案例也會假設您有有效的虛擬機器的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-117">hello scenario also assumes that a you have a resource group with a valid virtual machine.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="4ac2d-118">註冊 Insights 提供者</span><span class="sxs-lookup"><span data-stu-id="4ac2d-118">Register Insights provider</span></span>

<span data-ttu-id="4ac2d-119">流程記錄 toowork 成功，hello **Microsoft.Insights**必須註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-119">For flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="4ac2d-120">tooregister hello 提供者，採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="4ac2d-120">tooregister hello provider, take hello following steps:</span></span> 

1. <span data-ttu-id="4ac2d-121">跳過**訂閱**，然後選取您想要的 tooenable 流程記錄檔的 hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-121">Go too**Subscriptions**, and then select hello subscription for which you want tooenable flow logs.</span></span> 
2. <span data-ttu-id="4ac2d-122">在 hello**訂用帳戶**刀鋒視窗中，選取**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-122">On hello **Subscription** blade, select **Resource Providers**.</span></span> 
3. <span data-ttu-id="4ac2d-123">查看 hello 提供者清單，並確認該 hello **microsoft.insights**註冊提供者。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-123">Look at hello list of providers, and verify that hello **microsoft.insights** provider is registered.</span></span> <span data-ttu-id="4ac2d-124">如果沒有，則選取 [註冊]。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-124">If not, then select **Register**.</span></span>

![檢視提供者][providers]

## <a name="enable-flow-logs"></a><span data-ttu-id="4ac2d-126">啟用流量記錄</span><span class="sxs-lookup"><span data-stu-id="4ac2d-126">Enable flow logs</span></span>

<span data-ttu-id="4ac2d-127">這些步驟會引導您啟用網路安全性群組上的流量記錄檔的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-127">These steps take you through hello process of enabling flow logs on a network security group.</span></span>

### <a name="step-1"></a><span data-ttu-id="4ac2d-128">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4ac2d-128">Step 1</span></span>

<span data-ttu-id="4ac2d-129">移 tooa 網路監看員執行個體，然後再選取**NSG 流程記錄**。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-129">Go tooa Network Watcher instance, and then select **NSG Flow logs**.</span></span>

![流量記錄概觀][1]

### <a name="step-2"></a><span data-ttu-id="4ac2d-131">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4ac2d-131">Step 2</span></span>

<span data-ttu-id="4ac2d-132">從 hello 清單中選取網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-132">Select a network security group from hello list.</span></span>

![流量記錄概觀][2]

### <a name="step-3"></a><span data-ttu-id="4ac2d-134">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4ac2d-134">Step 3</span></span> 

<span data-ttu-id="4ac2d-135">在 hello**流程記錄設定**刀鋒視窗中，設定 hello 狀態太**上**，然後設定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-135">On hello **Flow logs settings** blade, set hello status too**On**, and then configure a storage account.</span></span>  <span data-ttu-id="4ac2d-136">完成後，選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-136">When you're done, select **OK**.</span></span> <span data-ttu-id="4ac2d-137">然後選取 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-137">Then select **Save**.</span></span>

![流量記錄概觀][3]

## <a name="download-flow-logs"></a><span data-ttu-id="4ac2d-139">下載流量記錄</span><span class="sxs-lookup"><span data-stu-id="4ac2d-139">Download flow logs</span></span>

<span data-ttu-id="4ac2d-140">流量記錄會儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-140">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="4ac2d-141">下載您的流程記錄 tooview 它們。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-141">Download your flow logs tooview them.</span></span>

### <a name="step-1"></a><span data-ttu-id="4ac2d-142">步驟 1</span><span class="sxs-lookup"><span data-stu-id="4ac2d-142">Step 1</span></span>

<span data-ttu-id="4ac2d-143">toodownload 流程記錄檔中，選取**您可以從設定的儲存體帳戶下載流程記錄**。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-143">toodownload flow logs, select **You can download flow logs from configured storage accounts**.</span></span> <span data-ttu-id="4ac2d-144">此步驟會帶您 tooa 儲存體帳戶檢視，您可以選擇哪些記錄檔 toodownload。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-144">This step takes you tooa storage account view where you can choose which logs toodownload.</span></span>

![流量記錄設定][4]

### <a name="step-2"></a><span data-ttu-id="4ac2d-146">步驟 2</span><span class="sxs-lookup"><span data-stu-id="4ac2d-146">Step 2</span></span>

<span data-ttu-id="4ac2d-147">移 toohello 正確的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-147">Go toohello correct storage account.</span></span> <span data-ttu-id="4ac2d-148">然後選取 [容器] > [insights-log-networksecuritygroupflowevent]。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-148">Then select **Containers** > **insights-log-networksecuritygroupflowevent**.</span></span>

![流量記錄設定][5]

### <a name="step-3"></a><span data-ttu-id="4ac2d-150">步驟 3</span><span class="sxs-lookup"><span data-stu-id="4ac2d-150">Step 3</span></span>

<span data-ttu-id="4ac2d-151">移 toohello hello 流程記錄檔位置，選取它，並選取**下載**。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-151">Go toohello location of hello flow log, select it, and then select **Download**.</span></span>

![流量記錄設定][6]

<span data-ttu-id="4ac2d-153">Hello 結構 hello 記錄檔的相關資訊，請造訪[網路安全性群組流程記錄概觀](network-watcher-nsg-flow-logging-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-153">For information about hello structure of hello log, visit [Network security group flow log overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ac2d-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ac2d-154">Next steps</span></span>

<span data-ttu-id="4ac2d-155">了解如何太[視覺化 NSG 流程記錄與 PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)。</span><span class="sxs-lookup"><span data-stu-id="4ac2d-155">Learn how too[visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
