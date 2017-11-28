---
title: "aaaAzure Active Directory 報告延遲 |Microsoft 文件"
description: "深入了解 hello 報告事件 tooshow 在 Azure 入口網站所花費的時間量"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="97251-103">Azure Active Directory 報告延遲</span><span class="sxs-lookup"><span data-stu-id="97251-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="97251-104">與[reporting](active-directory-preview-explainer.md) hello Azure Active Directory，在您取得所有 hello 資訊需要的 toodetermine 您的環境執行的動作。</span><span class="sxs-lookup"><span data-stu-id="97251-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="97251-105">hello reporting hello Azure 入口網站中的資料 tooshow 總就所謂的延遲所花費的時間量。</span><span class="sxs-lookup"><span data-stu-id="97251-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="97251-106">本主題列出 hello Azure 入口網站中的所有報表類別目錄的 hello hello 延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="97251-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="97251-107">活動報告</span><span class="sxs-lookup"><span data-stu-id="97251-107">Activity reports</span></span>

<span data-ttu-id="97251-108">有兩個活動報告的區域︰</span><span class="sxs-lookup"><span data-stu-id="97251-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="97251-109">**登入活動**– hello 使用量資訊的受管理的應用程式和使用者登入活動</span><span class="sxs-lookup"><span data-stu-id="97251-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="97251-110">**稽核記錄檔** - 使用者和群組管理、受管理應用程式和目錄活動的相關系統活動資訊</span><span class="sxs-lookup"><span data-stu-id="97251-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="97251-111">hello 下表列出 hello 活動報告的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="97251-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="97251-112">報告</span><span class="sxs-lookup"><span data-stu-id="97251-112">Report</span></span> | <span data-ttu-id="97251-113">最小值</span><span class="sxs-lookup"><span data-stu-id="97251-113">Minimum</span></span> | <span data-ttu-id="97251-114">平均值</span><span class="sxs-lookup"><span data-stu-id="97251-114">Average</span></span> | <span data-ttu-id="97251-115">最大值</span><span class="sxs-lookup"><span data-stu-id="97251-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="97251-116">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="97251-116">Audit logs</span></span>             | <span data-ttu-id="97251-117">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-117">30 minutes</span></span>  | <span data-ttu-id="97251-118">45 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-118">45 Minutes</span></span> | <span data-ttu-id="97251-119">1 小時</span><span class="sxs-lookup"><span data-stu-id="97251-119">1 hour</span></span>     |
| <span data-ttu-id="97251-120">登入</span><span class="sxs-lookup"><span data-stu-id="97251-120">Sign-ins</span></span>               | <span data-ttu-id="97251-121">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="97251-121">15 minutes</span></span>  | <span data-ttu-id="97251-122">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="97251-122">15 minutes</span></span> | <span data-ttu-id="97251-123">2 小時*</span><span class="sxs-lookup"><span data-stu-id="97251-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="97251-124">對於某些來自舊版 office 應用程式登入活動資料，可能需要報告資料 tooshow hello too8 的小時。</span><span class="sxs-lookup"><span data-stu-id="97251-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="97251-125">安全性報告</span><span class="sxs-lookup"><span data-stu-id="97251-125">Security reports</span></span>

<span data-ttu-id="97251-126">有兩個安全性報告的區域︰</span><span class="sxs-lookup"><span data-stu-id="97251-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="97251-127">**高風險的登入**-有風險的登入是可能執行的人不是合法 hello 的使用者帳戶擁有者的登入嘗試的指標。</span><span class="sxs-lookup"><span data-stu-id="97251-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="97251-128">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="97251-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="97251-129">hello 下表列出 hello 安全性報告的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="97251-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="97251-130">報告</span><span class="sxs-lookup"><span data-stu-id="97251-130">Report</span></span> | <span data-ttu-id="97251-131">最小值</span><span class="sxs-lookup"><span data-stu-id="97251-131">Minimum</span></span> | <span data-ttu-id="97251-132">平均值</span><span class="sxs-lookup"><span data-stu-id="97251-132">Average</span></span> | <span data-ttu-id="97251-133">最大值</span><span class="sxs-lookup"><span data-stu-id="97251-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="97251-134">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="97251-134">Users at risk</span></span>          | <span data-ttu-id="97251-135">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-135">5 minutes</span></span>   | <span data-ttu-id="97251-136">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="97251-136">15 minutes</span></span>  | <span data-ttu-id="97251-137">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-137">2 hours</span></span>  |
| <span data-ttu-id="97251-138">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="97251-138">Risky sign-ins</span></span>         | <span data-ttu-id="97251-139">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-139">5 minutes</span></span>   | <span data-ttu-id="97251-140">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="97251-140">15 minutes</span></span>  | <span data-ttu-id="97251-141">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="97251-142">風險事件</span><span class="sxs-lookup"><span data-stu-id="97251-142">Risk events</span></span>

<span data-ttu-id="97251-143">Azure Active Directory 使用彈性的機器學習演算法和啟發學習法 toodetect 可疑動作相關的 tooyour 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="97251-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="97251-144">偵測到的每個可疑動作都會儲存在名為風險事件的記錄中。</span><span class="sxs-lookup"><span data-stu-id="97251-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="97251-145">hello 下表列出 hello 風險事件的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="97251-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="97251-146">報告</span><span class="sxs-lookup"><span data-stu-id="97251-146">Report</span></span> | <span data-ttu-id="97251-147">最小值</span><span class="sxs-lookup"><span data-stu-id="97251-147">Minimum</span></span> | <span data-ttu-id="97251-148">平均值</span><span class="sxs-lookup"><span data-stu-id="97251-148">Average</span></span> | <span data-ttu-id="97251-149">最大值</span><span class="sxs-lookup"><span data-stu-id="97251-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="97251-150">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="97251-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="97251-151">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-151">5 minutes</span></span> |<span data-ttu-id="97251-152">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-152">15 Minutes</span></span> |<span data-ttu-id="97251-153">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-153">2 hours</span></span> |
| <span data-ttu-id="97251-154">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="97251-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="97251-155">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-155">5 minutes</span></span> |<span data-ttu-id="97251-156">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-156">15 Minutes</span></span> |<span data-ttu-id="97251-157">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-157">2 hours</span></span> |
| <span data-ttu-id="97251-158">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="97251-158">Users with leaked credentials</span></span> |<span data-ttu-id="97251-159">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-159">2 hours</span></span> |<span data-ttu-id="97251-160">4 小時</span><span class="sxs-lookup"><span data-stu-id="97251-160">4 hours</span></span> |<span data-ttu-id="97251-161">8 小時</span><span class="sxs-lookup"><span data-stu-id="97251-161">8 hours</span></span> |
| <span data-ttu-id="97251-162">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="97251-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="97251-163">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="97251-163">5 minutes</span></span> |<span data-ttu-id="97251-164">1 小時</span><span class="sxs-lookup"><span data-stu-id="97251-164">1 hour</span></span> |<span data-ttu-id="97251-165">8 小時</span><span class="sxs-lookup"><span data-stu-id="97251-165">8 hours</span></span>  |
| <span data-ttu-id="97251-166">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="97251-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="97251-167">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-167">2 hours</span></span> |<span data-ttu-id="97251-168">4 小時</span><span class="sxs-lookup"><span data-stu-id="97251-168">4 hours</span></span> |<span data-ttu-id="97251-169">8 小時</span><span class="sxs-lookup"><span data-stu-id="97251-169">8 hours</span></span>  |
| <span data-ttu-id="97251-170">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="97251-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="97251-171">2 小時</span><span class="sxs-lookup"><span data-stu-id="97251-171">2 hours</span></span> |<span data-ttu-id="97251-172">4 小時</span><span class="sxs-lookup"><span data-stu-id="97251-172">4 hours</span></span> |<span data-ttu-id="97251-173">8 小時</span><span class="sxs-lookup"><span data-stu-id="97251-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="97251-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97251-174">Next steps</span></span>

<span data-ttu-id="97251-175">如果您想 tooknow 更多關於 hello Azure 入口網站中的 hello 活動報告，請參閱：</span><span class="sxs-lookup"><span data-stu-id="97251-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="97251-176">Hello Azure Active Directory 入口網站中的登入活動報表</span><span class="sxs-lookup"><span data-stu-id="97251-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="97251-177">稽核 hello Azure Active Directory 入口網站中的活動報告</span><span class="sxs-lookup"><span data-stu-id="97251-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="97251-178">如果您想 tooknow 更多關於 hello Azure 入口網站中的 hello 安全性報告，請參閱：</span><span class="sxs-lookup"><span data-stu-id="97251-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="97251-179">使用者在風險中檢視 hello Azure Active Directory 入口網站的安全性報表</span><span class="sxs-lookup"><span data-stu-id="97251-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="97251-180">Hello Azure Active Directory 入口網站中的高風險的登入報表</span><span class="sxs-lookup"><span data-stu-id="97251-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="97251-181">如果您想深入了解風險事件 tooknow，請參閱[Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="97251-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
