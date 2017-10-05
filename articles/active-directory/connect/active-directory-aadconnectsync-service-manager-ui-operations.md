---
title: "Azure AD Connect Synchronization Service Manager 作業 | Microsoft Docs"
description: "了解 Azure AD Connect 的 Synchronization Service Manager 中的 [作業] 索引標籤。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1475e4fcd11eb008badba49665f4af6029a1697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="be9ba-103">使用 Sync Service Manager 作業索引標籤</span><span class="sxs-lookup"><span data-stu-id="be9ba-103">Using the Sync Service Manager Operations tab</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="be9ba-105">[作業] 索引標籤顯示最新作業的結果。</span><span class="sxs-lookup"><span data-stu-id="be9ba-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="be9ba-106">此索引標籤主要是用來了解及疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="be9ba-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="be9ba-107">了解 [作業] 索引標籤中顯示的資訊</span><span class="sxs-lookup"><span data-stu-id="be9ba-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="be9ba-108">上半部會依時間順序顯示所有執行。</span><span class="sxs-lookup"><span data-stu-id="be9ba-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="be9ba-109">根據預設，作業記錄會保留最後 7 天的相關資訊，但是您可以利用 [排程器](active-directory-aadconnectsync-feature-scheduler.md)來變更此設定。</span><span class="sxs-lookup"><span data-stu-id="be9ba-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="be9ba-110">若您想要尋找任何未顯示成功狀態的執行。</span><span class="sxs-lookup"><span data-stu-id="be9ba-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="be9ba-111">您可以按一下標頭來變更排序。</span><span class="sxs-lookup"><span data-stu-id="be9ba-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="be9ba-112">[狀態]  欄位是最重要的資訊，並顯示最嚴重的執行問題。</span><span class="sxs-lookup"><span data-stu-id="be9ba-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="be9ba-113">以下快速摘要依照優先順序來調查的最常見狀態 (其中 * 表示數個可能的錯誤字串)。</span><span class="sxs-lookup"><span data-stu-id="be9ba-113">Here is a quick summary of the most common statuses in order of priority to investigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="be9ba-114">狀態</span><span class="sxs-lookup"><span data-stu-id="be9ba-114">Status</span></span> | <span data-ttu-id="be9ba-115">註解</span><span class="sxs-lookup"><span data-stu-id="be9ba-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="be9ba-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="be9ba-116">stopped-*</span></span> |<span data-ttu-id="be9ba-117">執行無法完成。</span><span class="sxs-lookup"><span data-stu-id="be9ba-117">The run could not complete.</span></span> <span data-ttu-id="be9ba-118">例如，如果遠端系統已關閉且無法聯繫。</span><span class="sxs-lookup"><span data-stu-id="be9ba-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="be9ba-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="be9ba-119">stopped-error-limit</span></span> |<span data-ttu-id="be9ba-120">有 5,000 個以上的錯誤。</span><span class="sxs-lookup"><span data-stu-id="be9ba-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="be9ba-121">執行因錯誤數量過多而自動停止。</span><span class="sxs-lookup"><span data-stu-id="be9ba-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="be9ba-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="be9ba-122">completed-\*-errors</span></span> |<span data-ttu-id="be9ba-123">執行已完成，但發生應調查的錯誤 (數量少於 5,000 個)。</span><span class="sxs-lookup"><span data-stu-id="be9ba-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="be9ba-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="be9ba-124">completed-\*-warnings</span></span> |<span data-ttu-id="be9ba-125">執行完成，但某些資料並未處於預期的狀態。</span><span class="sxs-lookup"><span data-stu-id="be9ba-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="be9ba-126">如果您遇到錯誤，則此訊息通常只是一個徵狀。</span><span class="sxs-lookup"><span data-stu-id="be9ba-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="be9ba-127">在您解決錯誤之前，不應該調查警告。</span><span class="sxs-lookup"><span data-stu-id="be9ba-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="be9ba-128">成功</span><span class="sxs-lookup"><span data-stu-id="be9ba-128">success</span></span> |<span data-ttu-id="be9ba-129">沒有問題。</span><span class="sxs-lookup"><span data-stu-id="be9ba-129">No issues.</span></span> |

<span data-ttu-id="be9ba-130">當您選取某個資料列時，底部會更新以顯示該執行的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="be9ba-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="be9ba-131">在底部的最左邊，可能會有一份顯示 [步驟 #] 的清單。</span><span class="sxs-lookup"><span data-stu-id="be9ba-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="be9ba-132">如果您的樹系中有多個網域，而每個網域都以一個步驟來代表，則只會顯示此清單。</span><span class="sxs-lookup"><span data-stu-id="be9ba-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="be9ba-133">您可以在 [分割區] 標題下方找到網域名稱。</span><span class="sxs-lookup"><span data-stu-id="be9ba-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="be9ba-134">在 [同步處理統計資料] 下方，您可以找到關於已處理的變更次數詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="be9ba-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="be9ba-135">您可以按一下連結，以取得變更的物件清單。</span><span class="sxs-lookup"><span data-stu-id="be9ba-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="be9ba-136">如果您有物件發生錯誤，這些會顯示於 [同步處理錯誤] 下方。</span><span class="sxs-lookup"><span data-stu-id="be9ba-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="be9ba-137">如需詳細資訊，請參閱[針對未同步的物件進行疑難排解](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="be9ba-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="be9ba-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be9ba-138">Next steps</span></span>
<span data-ttu-id="be9ba-139">深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。</span><span class="sxs-lookup"><span data-stu-id="be9ba-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="be9ba-140">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="be9ba-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
