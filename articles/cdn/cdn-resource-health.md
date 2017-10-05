---
title: "監視 Azure CDN 資源的健康狀態 | Microsoft Docs"
description: "了解如何使用 Azure 資源健康狀態監視 Azure CDN 資源的健康狀態。"
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="4836c-103">監視 Azure CDN 資源的健康狀態</span><span class="sxs-lookup"><span data-stu-id="4836c-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="4836c-104">Azure CDN 資源健康狀態是 [Azure 資源健康狀態](../resource-health/resource-health-overview.md)的子集。</span><span class="sxs-lookup"><span data-stu-id="4836c-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="4836c-105">您可以使用 Azure 資源健康狀態來監視 CDN 資源的健康狀態，以及接收可行的指引來進行問題的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="4836c-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="4836c-106">Azure CDN 資源健康狀態目前只負責全域 CDN 傳遞和 API 功能的健康狀態。</span><span class="sxs-lookup"><span data-stu-id="4836c-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="4836c-107">Azure CDN 資源健康情況不會驗證個別的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="4836c-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="4836c-108">摘要 Azure CDN 資源健康狀態的訊號最多可能延遲 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="4836c-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="4836c-109">如何尋找 Azure CDN 資源健康狀態</span><span class="sxs-lookup"><span data-stu-id="4836c-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="4836c-110">在 [Azure 入口網站](https://portal.azure.com)中，瀏覽到您的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="4836c-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="4836c-111">按一下 [設定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4836c-111">Click the **Settings** button.</span></span>

    ![設定按鈕](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="4836c-113">在 [支援與疑難排解] 下方，按一下 [資源健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="4836c-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN 資源健康狀態](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="4836c-115">您也可以尋找 [說明 + 支援] 刀鋒視窗的 [資源健康狀態] 圖格中所列出的 CDN 資源。</span><span class="sxs-lookup"><span data-stu-id="4836c-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="4836c-116">您可以在入口網站的右上角，按一下圓框 **？** 快速取得 [說明 + 支援]</span><span class="sxs-lookup"><span data-stu-id="4836c-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="4836c-117">。</span><span class="sxs-lookup"><span data-stu-id="4836c-117">in the upper right corner of the portal.</span></span>
>
> ![說明 + 支援](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="4836c-119">Azure CDN 特定的訊息</span><span class="sxs-lookup"><span data-stu-id="4836c-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="4836c-120">以下提供與 Azure CDN 資源健康狀態相關的狀態。</span><span class="sxs-lookup"><span data-stu-id="4836c-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="4836c-121">訊息</span><span class="sxs-lookup"><span data-stu-id="4836c-121">Message</span></span> | <span data-ttu-id="4836c-122">建議的動作</span><span class="sxs-lookup"><span data-stu-id="4836c-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="4836c-123">您可能已停止、移除或錯誤設定一或多個 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="4836c-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="4836c-124">您可能已停止、移除或錯誤設定一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="4836c-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="4836c-125">很抱歉，目前無法使用 CDN 管理服務</span><span class="sxs-lookup"><span data-stu-id="4836c-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="4836c-126">請返回這裡以查看狀態更新。如果您的問題在預期解決時間之後持續發生，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4836c-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="4836c-127">很抱歉，您的 CDN 端點可能受到我們的部分 CDN 提供者持續出現之問題所影響</span><span class="sxs-lookup"><span data-stu-id="4836c-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="4836c-128">請返回這裡以查看狀態更新。使用疑難排解工具來了解如何測試您的原始和 CDN 端點。如果您的問題在預期解決時間之後持續發生，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4836c-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="4836c-129">很抱歉，CDN 端點設定變更發生了傳播延遲</span><span class="sxs-lookup"><span data-stu-id="4836c-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="4836c-130">請返回這裡以查看狀態更新。如果您的組態變更在預期時間內並未完全傳播，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4836c-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="4836c-131">很抱歉，我們遇到了載入補充入口網站的問題</span><span class="sxs-lookup"><span data-stu-id="4836c-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="4836c-132">請返回這裡以查看狀態更新。如果您的問題在預期解決時間之後持續發生，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4836c-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="4836c-133">很抱歉，我們的部分 CDN 提供者發生了問題</span><span class="sxs-lookup"><span data-stu-id="4836c-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="4836c-134">請返回這裡以查看狀態更新。如果您的問題在預期解決時間之後持續發生，請連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="4836c-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4836c-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4836c-135">Next steps</span></span>

- [<span data-ttu-id="4836c-136">閱讀 Azure 資源健康狀態的概觀</span><span class="sxs-lookup"><span data-stu-id="4836c-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="4836c-137">針對 CDN 壓縮的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4836c-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="4836c-138">針對 404 錯誤的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="4836c-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)