---
title: "Azure Active Directory 報告延遲 | Microsoft Docs"
description: "深入了解在您的 Azure 入口網站中針對顯示報告事件所花費的時間長度"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="89b92-103">Azure Active Directory 報告延遲</span><span class="sxs-lookup"><span data-stu-id="89b92-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="89b92-104">透過 Azure Active Directory 中的[報告](active-directory-preview-explainer.md)，您可取得判斷您的環境執行狀況所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="89b92-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="89b92-105">Azure 入口網站中針對顯示報告資料所花費的時間長度也稱為延遲。</span><span class="sxs-lookup"><span data-stu-id="89b92-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="89b92-106">本主題列出 Azure 入口網站中所有報告類別的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="89b92-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="89b92-107">活動報告</span><span class="sxs-lookup"><span data-stu-id="89b92-107">Activity reports</span></span>

<span data-ttu-id="89b92-108">有兩個活動報告的區域︰</span><span class="sxs-lookup"><span data-stu-id="89b92-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="89b92-109">**登入活動** – 受管理應用程式和使用者登入活動的使用情況相關資訊</span><span class="sxs-lookup"><span data-stu-id="89b92-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="89b92-110">**稽核記錄檔** - 使用者和群組管理、受管理應用程式和目錄活動的相關系統活動資訊</span><span class="sxs-lookup"><span data-stu-id="89b92-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="89b92-111">下表列出活動報告的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="89b92-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="89b92-112">報告</span><span class="sxs-lookup"><span data-stu-id="89b92-112">Report</span></span> | <span data-ttu-id="89b92-113">最小值</span><span class="sxs-lookup"><span data-stu-id="89b92-113">Minimum</span></span> | <span data-ttu-id="89b92-114">平均值</span><span class="sxs-lookup"><span data-stu-id="89b92-114">Average</span></span> | <span data-ttu-id="89b92-115">最大值</span><span class="sxs-lookup"><span data-stu-id="89b92-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="89b92-116">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="89b92-116">Audit logs</span></span>             | <span data-ttu-id="89b92-117">30 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-117">30 minutes</span></span>  | <span data-ttu-id="89b92-118">45 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-118">45 Minutes</span></span> | <span data-ttu-id="89b92-119">1 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-119">1 hour</span></span>     |
| <span data-ttu-id="89b92-120">登入</span><span class="sxs-lookup"><span data-stu-id="89b92-120">Sign-ins</span></span>               | <span data-ttu-id="89b92-121">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="89b92-121">15 minutes</span></span>  | <span data-ttu-id="89b92-122">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="89b92-122">15 minutes</span></span> | <span data-ttu-id="89b92-123">2 小時*</span><span class="sxs-lookup"><span data-stu-id="89b92-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="89b92-124">對於某些來自舊版 Office 應用程式的登入活動資料，可能需要 8 小時才會顯示報告資料。</span><span class="sxs-lookup"><span data-stu-id="89b92-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="89b92-125">安全性報告</span><span class="sxs-lookup"><span data-stu-id="89b92-125">Security reports</span></span>

<span data-ttu-id="89b92-126">有兩個安全性報告的區域︰</span><span class="sxs-lookup"><span data-stu-id="89b92-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="89b92-127">**有風險的登入** - 有風險的登入表示非使用者帳戶合法擁有者的某人嘗試登入。</span><span class="sxs-lookup"><span data-stu-id="89b92-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="89b92-128">**標幟為有風險的使用者** - 有風險的使用者表示可能被盜用的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="89b92-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="89b92-129">下表列出安全性報告的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="89b92-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="89b92-130">報告</span><span class="sxs-lookup"><span data-stu-id="89b92-130">Report</span></span> | <span data-ttu-id="89b92-131">最小值</span><span class="sxs-lookup"><span data-stu-id="89b92-131">Minimum</span></span> | <span data-ttu-id="89b92-132">平均值</span><span class="sxs-lookup"><span data-stu-id="89b92-132">Average</span></span> | <span data-ttu-id="89b92-133">最大值</span><span class="sxs-lookup"><span data-stu-id="89b92-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="89b92-134">有風險的使用者</span><span class="sxs-lookup"><span data-stu-id="89b92-134">Users at risk</span></span>          | <span data-ttu-id="89b92-135">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-135">5 minutes</span></span>   | <span data-ttu-id="89b92-136">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="89b92-136">15 minutes</span></span>  | <span data-ttu-id="89b92-137">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-137">2 hours</span></span>  |
| <span data-ttu-id="89b92-138">有風險的登入</span><span class="sxs-lookup"><span data-stu-id="89b92-138">Risky sign-ins</span></span>         | <span data-ttu-id="89b92-139">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-139">5 minutes</span></span>   | <span data-ttu-id="89b92-140">15 Minuten</span><span class="sxs-lookup"><span data-stu-id="89b92-140">15 minutes</span></span>  | <span data-ttu-id="89b92-141">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="89b92-142">風險事件</span><span class="sxs-lookup"><span data-stu-id="89b92-142">Risk events</span></span>

<span data-ttu-id="89b92-143">Azure Active Directory 使用調適性機器學習服務演算法和啟發學習法，來偵測與您使用者帳戶相關的可疑動作。</span><span class="sxs-lookup"><span data-stu-id="89b92-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="89b92-144">偵測到的每個可疑動作都會儲存在名為風險事件的記錄中。</span><span class="sxs-lookup"><span data-stu-id="89b92-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="89b92-145">下表列出風險事件的延遲資訊。</span><span class="sxs-lookup"><span data-stu-id="89b92-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="89b92-146">報告</span><span class="sxs-lookup"><span data-stu-id="89b92-146">Report</span></span> | <span data-ttu-id="89b92-147">最小值</span><span class="sxs-lookup"><span data-stu-id="89b92-147">Minimum</span></span> | <span data-ttu-id="89b92-148">平均值</span><span class="sxs-lookup"><span data-stu-id="89b92-148">Average</span></span> | <span data-ttu-id="89b92-149">最大值</span><span class="sxs-lookup"><span data-stu-id="89b92-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="89b92-150">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="89b92-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="89b92-151">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-151">5 minutes</span></span> |<span data-ttu-id="89b92-152">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-152">15 Minutes</span></span> |<span data-ttu-id="89b92-153">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-153">2 hours</span></span> |
| <span data-ttu-id="89b92-154">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="89b92-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="89b92-155">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-155">5 minutes</span></span> |<span data-ttu-id="89b92-156">15 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-156">15 Minutes</span></span> |<span data-ttu-id="89b92-157">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-157">2 hours</span></span> |
| <span data-ttu-id="89b92-158">認證外洩的使用者</span><span class="sxs-lookup"><span data-stu-id="89b92-158">Users with leaked credentials</span></span> |<span data-ttu-id="89b92-159">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-159">2 hours</span></span> |<span data-ttu-id="89b92-160">4 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-160">4 hours</span></span> |<span data-ttu-id="89b92-161">8 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-161">8 hours</span></span> |
| <span data-ttu-id="89b92-162">不可能到達非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="89b92-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="89b92-163">5 分鐘</span><span class="sxs-lookup"><span data-stu-id="89b92-163">5 minutes</span></span> |<span data-ttu-id="89b92-164">1 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-164">1 hour</span></span> |<span data-ttu-id="89b92-165">8 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-165">8 hours</span></span>  |
| <span data-ttu-id="89b92-166">從受感染的裝置登入</span><span class="sxs-lookup"><span data-stu-id="89b92-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="89b92-167">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-167">2 hours</span></span> |<span data-ttu-id="89b92-168">4 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-168">4 hours</span></span> |<span data-ttu-id="89b92-169">8 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-169">8 hours</span></span>  |
| <span data-ttu-id="89b92-170">從具有可疑活動的 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="89b92-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="89b92-171">2 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-171">2 hours</span></span> |<span data-ttu-id="89b92-172">4 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-172">4 hours</span></span> |<span data-ttu-id="89b92-173">8 小時</span><span class="sxs-lookup"><span data-stu-id="89b92-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="89b92-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89b92-174">Next steps</span></span>

<span data-ttu-id="89b92-175">如果您想要深入了解 Azure 入口網站中的活動報告，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="89b92-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="89b92-176">Azure Active Directory 入口網站中的登入活動報告</span><span class="sxs-lookup"><span data-stu-id="89b92-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="89b92-177">Azure Active Directory 入口網站中的稽核活動報告</span><span class="sxs-lookup"><span data-stu-id="89b92-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="89b92-178">如果您想要深入了解 Azure 入口網站中的安全性報告，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="89b92-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="89b92-179">Azure Active Directory 入口網站中具有風險的使用者安全性報告</span><span class="sxs-lookup"><span data-stu-id="89b92-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="89b92-180">Azure Active Directory 入口網站中的風險登入報告</span><span class="sxs-lookup"><span data-stu-id="89b92-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="89b92-181">如果您想要深入了解風險事件，請參閱 [Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)。</span><span class="sxs-lookup"><span data-stu-id="89b92-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
