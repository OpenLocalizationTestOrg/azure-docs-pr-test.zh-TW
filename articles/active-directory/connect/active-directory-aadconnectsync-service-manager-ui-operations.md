---
title: "Azure AD Connect Synchronization Service Manager 作業 | Microsoft Docs"
description: "了解 Azure AD Connect 同步處理服務管理員 hello 的 hello 作業 索引標籤。"
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
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a><span data-ttu-id="d53e3-103">使用 hello 同步處理服務管理員作業 索引標籤</span><span class="sxs-lookup"><span data-stu-id="d53e3-103">Using hello Sync Service Manager Operations tab</span></span>

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="d53e3-105">hello 作業 索引標籤會顯示 hello hello 最新的作業結果。</span><span class="sxs-lookup"><span data-stu-id="d53e3-105">hello operations tab shows hello results from hello most recent operations.</span></span> <span data-ttu-id="d53e3-106">此索引標籤是索引鍵 toounderstand 和疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="d53e3-106">This tab is key toounderstand and troubleshoot issues.</span></span>

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a><span data-ttu-id="d53e3-107">了解 hello hello 作業 索引標籤中顯示的資訊</span><span class="sxs-lookup"><span data-stu-id="d53e3-107">Understand hello information visible in hello operations tab</span></span>
<span data-ttu-id="d53e3-108">hello 上半部會顯示所有執行中依時間先後順序。</span><span class="sxs-lookup"><span data-stu-id="d53e3-108">hello top half shows all runs in chronological order.</span></span> <span data-ttu-id="d53e3-109">根據預設，hello 作業記錄會保留資訊 hello 過去七天，但是可以變更此設定，以 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)。</span><span class="sxs-lookup"><span data-stu-id="d53e3-109">By default, hello operations log keeps information about hello last seven days, but this setting can be changed with hello [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="d53e3-110">您想 toolook 任何不會顯示成功狀態的執行。</span><span class="sxs-lookup"><span data-stu-id="d53e3-110">You want toolook for any run that does not show a success status.</span></span> <span data-ttu-id="d53e3-111">您可以變更 hello hello 標頭，即可排序。</span><span class="sxs-lookup"><span data-stu-id="d53e3-111">You can change hello sorting by clicking hello headers.</span></span>

<span data-ttu-id="d53e3-112">hello**狀態**資料行是 hello 最重要的資訊並顯示 hello 執行最嚴重的問題。</span><span class="sxs-lookup"><span data-stu-id="d53e3-112">hello **Status** column is hello most important information and shows hello most severe problem for a run.</span></span> <span data-ttu-id="d53e3-113">以下是依照優先順序 tooinvestigate hello 最常見狀態的簡短摘要 (其中 * 表示幾個可能的錯誤字串)。</span><span class="sxs-lookup"><span data-stu-id="d53e3-113">Here is a quick summary of hello most common statuses in order of priority tooinvestigate (where * indicate several possible error strings).</span></span>

| <span data-ttu-id="d53e3-114">狀態</span><span class="sxs-lookup"><span data-stu-id="d53e3-114">Status</span></span> | <span data-ttu-id="d53e3-115">註解</span><span class="sxs-lookup"><span data-stu-id="d53e3-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="d53e3-116">stopped-*</span><span class="sxs-lookup"><span data-stu-id="d53e3-116">stopped-*</span></span> |<span data-ttu-id="d53e3-117">執行 hello 無法完成。</span><span class="sxs-lookup"><span data-stu-id="d53e3-117">hello run could not complete.</span></span> <span data-ttu-id="d53e3-118">例如，如果 hello 遠端系統已關閉，且無法聯繫。</span><span class="sxs-lookup"><span data-stu-id="d53e3-118">For example, if hello remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="d53e3-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="d53e3-119">stopped-error-limit</span></span> |<span data-ttu-id="d53e3-120">有 5,000 個以上的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d53e3-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="d53e3-121">hello 執行自動已停止，因為 toohello 大量的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d53e3-121">hello run was automatically stopped due toohello large number of errors.</span></span> |
| <span data-ttu-id="d53e3-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="d53e3-122">completed-\*-errors</span></span> |<span data-ttu-id="d53e3-123">hello 執行已完成，但有錯誤 (少於 5000)，應予調查。</span><span class="sxs-lookup"><span data-stu-id="d53e3-123">hello run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="d53e3-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="d53e3-124">completed-\*-warnings</span></span> |<span data-ttu-id="d53e3-125">hello 執行完成，但某些資料不是處於 hello 預期狀態。</span><span class="sxs-lookup"><span data-stu-id="d53e3-125">hello run completed, but some data is not in hello expected state.</span></span> <span data-ttu-id="d53e3-126">如果您遇到錯誤，則此訊息通常只是一個徵狀。</span><span class="sxs-lookup"><span data-stu-id="d53e3-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="d53e3-127">在您解決錯誤之前，不應該調查警告。</span><span class="sxs-lookup"><span data-stu-id="d53e3-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="d53e3-128">成功</span><span class="sxs-lookup"><span data-stu-id="d53e3-128">success</span></span> |<span data-ttu-id="d53e3-129">沒有問題。</span><span class="sxs-lookup"><span data-stu-id="d53e3-129">No issues.</span></span> |

<span data-ttu-id="d53e3-130">當您選取一個資料列時，hello 底部更新 tooshow hello 詳細資料，執行。</span><span class="sxs-lookup"><span data-stu-id="d53e3-130">When you select a row, hello bottom updates tooshow hello details of that run.</span></span> <span data-ttu-id="d53e3-131">toohello 最左側的 hello 底部，您可能必須清單指出**步驟 #**。</span><span class="sxs-lookup"><span data-stu-id="d53e3-131">toohello far left of hello bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="d53e3-132">如果您的樹系中有多個網域，而每個網域都以一個步驟來代表，則只會顯示此清單。</span><span class="sxs-lookup"><span data-stu-id="d53e3-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="d53e3-133">hello 網域名稱可以找到 hello 標題底下**分割**。</span><span class="sxs-lookup"><span data-stu-id="d53e3-133">hello domain name can be found under hello heading **Partition**.</span></span> <span data-ttu-id="d53e3-134">在下**同步處理統計資料**，您可以找到 hello 數的變更，已處理的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d53e3-134">Under **Synchronization Statistics**, you can find more information about hello number of changes that were processed.</span></span> <span data-ttu-id="d53e3-135">您可以按一下 hello 連結 tooget hello 變更物件的清單。</span><span class="sxs-lookup"><span data-stu-id="d53e3-135">You can click hello links tooget a list of hello changed objects.</span></span> <span data-ttu-id="d53e3-136">如果您有物件發生錯誤，這些會顯示於 [同步處理錯誤] 下方。</span><span class="sxs-lookup"><span data-stu-id="d53e3-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="d53e3-137">如需詳細資訊，請參閱[針對未同步的物件進行疑難排解](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="d53e3-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d53e3-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d53e3-138">Next steps</span></span>
<span data-ttu-id="d53e3-139">深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。</span><span class="sxs-lookup"><span data-stu-id="d53e3-139">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="d53e3-140">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="d53e3-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
