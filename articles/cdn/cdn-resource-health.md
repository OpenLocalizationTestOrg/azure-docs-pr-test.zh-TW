---
title: "aaaMonitor hello 健全狀況的 Azure CDN 資源 |Microsoft 文件"
description: "了解如何 toomonitor hello Azure CDN 資源使用 Azure 資源健全狀況的健全狀況。"
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
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a><span data-ttu-id="c5a48-103">監視 Azure CDN 資源 hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="c5a48-103">Monitor hello health of Azure CDN resources</span></span>
  
<span data-ttu-id="c5a48-104">Azure CDN 資源健康狀態是 [Azure 資源健康狀態](../resource-health/resource-health-overview.md)的子集。</span><span class="sxs-lookup"><span data-stu-id="c5a48-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="c5a48-105">您可以使用 Azure 資源健全狀況 toomonitor hello 健全狀況的 CDN 資源，並接收可採取動作的指導方針 tootroubleshoot 問題。</span><span class="sxs-lookup"><span data-stu-id="c5a48-105">You can use Azure resource health toomonitor hello health of CDN resources and receive actionable guidance tootroubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c5a48-106">Azure CDN 資源健全狀況只有目前帳戶 hello 全域 CDN 傳遞和 API 功能的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="c5a48-106">Azure CDN resource health only currently accounts for hello health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="c5a48-107">Azure CDN 資源健康情況不會驗證個別的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="c5a48-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="c5a48-108">摘要 Azure CDN 資源健全狀況的 hello 訊號可能是 up too15 分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="c5a48-108">hello signals that feed Azure CDN resource health may be up too15 minutes delayed.</span></span>

## <a name="how-toofind-azure-cdn-resource-health"></a><span data-ttu-id="c5a48-109">如何 toofind Azure CDN 資源健全狀況</span><span class="sxs-lookup"><span data-stu-id="c5a48-109">How toofind Azure CDN resource health</span></span>

1. <span data-ttu-id="c5a48-110">在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="c5a48-110">In hello [Azure portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>

2. <span data-ttu-id="c5a48-111">按一下 hello**設定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c5a48-111">Click hello **Settings** button.</span></span>

    ![設定按鈕](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="c5a48-113">在 [支援與疑難排解] 下方，按一下 [資源健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="c5a48-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN 資源健康狀態](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="c5a48-115">您也可以尋找 hello 中列出的 CDN 資源*資源健全狀況*磚中 hello*說明 + 支援*刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c5a48-115">You can also find CDN resources listed in hello *Resource health* tile in hello *Help + support* blade.</span></span>  <span data-ttu-id="c5a48-116">您可以快速取得太*說明 + 支援*按一下 hello 圈選起來**嗎？**</span><span class="sxs-lookup"><span data-stu-id="c5a48-116">You can quickly get too*Help + support* by clicking hello circled **?**</span></span> <span data-ttu-id="c5a48-117">hello 右上角的 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c5a48-117">in hello upper right corner of hello portal.</span></span>
>
> ![說明 + 支援](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="c5a48-119">Azure CDN 特定的訊息</span><span class="sxs-lookup"><span data-stu-id="c5a48-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="c5a48-120">下面，您可以找到相關的 tooAzure CDN 資源健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="c5a48-120">Statuses related tooAzure CDN resource health can be found below.</span></span>

|<span data-ttu-id="c5a48-121">訊息</span><span class="sxs-lookup"><span data-stu-id="c5a48-121">Message</span></span> | <span data-ttu-id="c5a48-122">建議的動作</span><span class="sxs-lookup"><span data-stu-id="c5a48-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="c5a48-123">您可能已停止、移除或錯誤設定一或多個 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="c5a48-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="c5a48-124">您可能已停止、移除或錯誤設定一或多個 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="c5a48-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="c5a48-125">很抱歉，目前無法使用 hello CDN 管理服務</span><span class="sxs-lookup"><span data-stu-id="c5a48-125">We are sorry, hello CDN management service is currently unavailable</span></span> | <span data-ttu-id="c5a48-126">回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。</span><span class="sxs-lookup"><span data-stu-id="c5a48-126">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
|<span data-ttu-id="c5a48-127">很抱歉，您的 CDN 端點可能受到我們的部分 CDN 提供者持續出現之問題所影響</span><span class="sxs-lookup"><span data-stu-id="c5a48-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="c5a48-128">回到這裡查看狀態更新。如何使用 hello 疑難排解工具 toolearn tootest 您的原點和 CDN 端點。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。</span><span class="sxs-lookup"><span data-stu-id="c5a48-128">Check back here for status updates; Use hello Troubleshoot tool toolearn how tootest your origin and CDN endpoint; If your problem persists after hello expected resolution time, contact support.</span></span> |
|<span data-ttu-id="c5a48-129">很抱歉，CDN 端點設定變更發生了傳播延遲</span><span class="sxs-lookup"><span data-stu-id="c5a48-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="c5a48-130">回到這裡查看狀態更新。如果您的組態變更不會完全傳播 hello 預期時間，請連絡支援。</span><span class="sxs-lookup"><span data-stu-id="c5a48-130">Check back here for status updates; If your configuration changes are not fully propagated in hello expected time, contact support.</span></span>|
|<span data-ttu-id="c5a48-131">很抱歉，我們遇到問題載入 hello 補充入口網站</span><span class="sxs-lookup"><span data-stu-id="c5a48-131">We're sorry, we are experiencing issues loading hello supplemental portal</span></span> | <span data-ttu-id="c5a48-132">回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。</span><span class="sxs-lookup"><span data-stu-id="c5a48-132">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span>|
<span data-ttu-id="c5a48-133">很抱歉，我們的部分 CDN 提供者發生了問題</span><span class="sxs-lookup"><span data-stu-id="c5a48-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="c5a48-134">回到這裡查看狀態更新。如果問題持續發生 hello 預期的解決時間之後，請連絡支援服務。</span><span class="sxs-lookup"><span data-stu-id="c5a48-134">Check back here for status updates; If your problem persists after hello expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c5a48-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5a48-135">Next steps</span></span>

- [<span data-ttu-id="c5a48-136">閱讀 Azure 資源健康狀態的概觀</span><span class="sxs-lookup"><span data-stu-id="c5a48-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="c5a48-137">針對 CDN 壓縮的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c5a48-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="c5a48-138">針對 404 錯誤的問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="c5a48-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)