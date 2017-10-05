---
title: "Azure Active Directory 報告常見問題集 | Microsoft Docs"
description: "Azure Active Directory 報告常見問題集。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="e1647-103">Azure Active Directory 報告常見問題集</span><span class="sxs-lookup"><span data-stu-id="e1647-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="e1647-104">本文會回答有關 Azure Active Directory 報告的常見問題 (FAQ)。</span><span class="sxs-lookup"><span data-stu-id="e1647-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="e1647-105">如需更多詳細資料，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="e1647-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="e1647-106">**問：Azure 入口網站中活動記錄 (稽核和登入) 的資料保留期是多長？**</span><span class="sxs-lookup"><span data-stu-id="e1647-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="e1647-107">**答：**針對免費客戶，我們提供 7 天的資料，而只要切換到 Azure AD Premium 1 或 Premium 2 授權，您便可以存取最長達 30 天的資料。</span><span class="sxs-lookup"><span data-stu-id="e1647-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="e1647-108">如需有關保留期的更多詳細資料，請參閱 [Azure Active Directory 報告保留原則](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="e1647-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="e1647-109">**問：在我完成工作之後，要多久的時間才能看見活動資料？**</span><span class="sxs-lookup"><span data-stu-id="e1647-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="e1647-110">**答：**稽核活動記錄的延遲時間為 15 分鐘到 1 小時。</span><span class="sxs-lookup"><span data-stu-id="e1647-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="e1647-111">登入活動記錄中大多數記錄的延遲時間為 15 分鐘，而少數記錄的延遲時間則最長可達 2 小時。</span><span class="sxs-lookup"><span data-stu-id="e1647-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="e1647-112">**問：我是否必須是全域系統管理員，才能在 Azure 入口網站中看到活動記錄，或是透過 API 取得資料？**</span><span class="sxs-lookup"><span data-stu-id="e1647-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="e1647-113">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="e1647-113">**A:** No.</span></span> <span data-ttu-id="e1647-114">您只要是「安全性讀取者」、「安全性系統管理員」或「全域系統管理員」，便能在 Azure 入口網站中看見報告資料，或是透過 API 存取該資料。</span><span class="sxs-lookup"><span data-stu-id="e1647-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="e1647-115">**問：我是否可以透過 Azure 入口網站取得 Office 365 活動記錄資訊？**</span><span class="sxs-lookup"><span data-stu-id="e1647-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="e1647-116">**答：**雖然 Office 365 活動和 Azure AD 活動記錄共用許多目錄資源，但如果您想要完整檢視 Office 365 活動記錄，應該前往「Office 365 系統管理中心」以取得 Office 365 活動記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="e1647-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="e1647-117">**問：我應該使用哪些 API 來取得 Office 365 活動記錄的相關資訊？**</span><span class="sxs-lookup"><span data-stu-id="e1647-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="e1647-118">**答：**請使用「Office 365 管理 API」來存取 [Office 365 活動記錄 (透過 API)](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview)。</span><span class="sxs-lookup"><span data-stu-id="e1647-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="e1647-119">**問：我可以從 Azure 入口網站下載多少記錄？**</span><span class="sxs-lookup"><span data-stu-id="e1647-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="e1647-120">**答：**您可以從 Azure 入口網站最多下載 12 萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="e1647-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="e1647-121">這些記錄會依「時間上最近」方式來排序，而根據預設，您會取得最近的 12 萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="e1647-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="e1647-122">**問：我可以透過活動 API 查詢多少記錄？**</span><span class="sxs-lookup"><span data-stu-id="e1647-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="e1647-123">**答：**如果您未使用 top 運算子 (依時間上最近方式來排序記錄)，您最多可以查詢 100 萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="e1647-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="e1647-124">如果您使用 “top” 運算子，則最多可以查詢 50 萬筆記錄。</span><span class="sxs-lookup"><span data-stu-id="e1647-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="e1647-125">如果有關如何使用 API 的範例查詢，請參閱[這裡](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e1647-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="e1647-126">**問：我要如何取得進階授權？**</span><span class="sxs-lookup"><span data-stu-id="e1647-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="e1647-127">**答：**如需此問題的解答，請參閱[開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)。</span><span class="sxs-lookup"><span data-stu-id="e1647-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="e1647-128">**問：在取得進階授權之後，我應該多快能看見活動資料？**</span><span class="sxs-lookup"><span data-stu-id="e1647-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="e1647-129">**答：**如果您在使用免費授權時即已經有活動資料，您便可以看見相同的資料。</span><span class="sxs-lookup"><span data-stu-id="e1647-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="e1647-130">如果您沒有任何資料，則必須花一或兩天的時間。</span><span class="sxs-lookup"><span data-stu-id="e1647-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="e1647-131">**問：在取得 Azure AD 進階授權之後，我是否會看見上個月的資料？**</span><span class="sxs-lookup"><span data-stu-id="e1647-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="e1647-132">**答：**如果您是最近切換到進階版 (包括試用版)，一開始最多可以看見 7 天的資料。</span><span class="sxs-lookup"><span data-stu-id="e1647-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="e1647-133">當資料累積之後，您將最多可以看見 30 天的資料。</span><span class="sxs-lookup"><span data-stu-id="e1647-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="e1647-134">**問：Identity Protection 有風險事件，但是我在所有登入中看不到對應的登入。這是預期行為嗎？**</span><span class="sxs-lookup"><span data-stu-id="e1647-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="e1647-135">**答：**是，Identity Protection 會評估所有驗證流程的風險，無論是互動式或非互動式。</span><span class="sxs-lookup"><span data-stu-id="e1647-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="e1647-136">不過，所有登入只會報告顯示互動式登入。</span><span class="sxs-lookup"><span data-stu-id="e1647-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="e1647-137">**問：如何下載 Azure 入口網站中的「使用者標示為風險」報告？**</span><span class="sxs-lookup"><span data-stu-id="e1647-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="e1647-138">**答：**：下載「使用者標示為風險」報告的選項即將新增。</span><span class="sxs-lookup"><span data-stu-id="e1647-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="e1647-139">**問：如何知道為何在 Azure 入口網站中登入或使用者會標示為風險？**</span><span class="sxs-lookup"><span data-stu-id="e1647-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="e1647-140">**答**：進階版的客戶可以按一下「使用者標示為風險」中的使用者，或按一下「風險登入」，進一步了解基礎風險事件。</span><span class="sxs-lookup"><span data-stu-id="e1647-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="e1647-141">Free 和 Basic 版本的客戶只能看到不含基礎風險事件資訊的風險使用者和登入。</span><span class="sxs-lookup"><span data-stu-id="e1647-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="e1647-142">**問：如何在登入和有風險的登入報告中計算 IP 位址？**</span><span class="sxs-lookup"><span data-stu-id="e1647-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="e1647-143">**答：**IP 位址的發出方式如下：IP 位址與該位址實際所在的電腦之間沒有任何明確的連線。</span><span class="sxs-lookup"><span data-stu-id="e1647-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="e1647-144">有些因素會使這種情況變復雜，例如行動提供者和從中央集區發出 IP 位址的 VPN 通常距離實際使用用戶端裝置的位置非常遠。</span><span class="sxs-lookup"><span data-stu-id="e1647-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="e1647-145">基於上述的假設，根據追蹤、登錄資料、反向查詢和其他資訊，將 IP 位址轉換為實體位置的效果最佳。</span><span class="sxs-lookup"><span data-stu-id="e1647-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
