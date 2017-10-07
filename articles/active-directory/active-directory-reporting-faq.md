---
title: "aaaAzure Active Directory Reporting 常見問題集 |Microsoft 文件"
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
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="47f14-103">Azure Active Directory 報告常見問題集</span><span class="sxs-lookup"><span data-stu-id="47f14-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="47f14-104">這篇文章包含有關在 Azure Active Directory 報告集 (faq) 解答 toofrequently。</span><span class="sxs-lookup"><span data-stu-id="47f14-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="47f14-105">如需更多詳細資料，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="47f14-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="47f14-106">**問： 什麼是 hello 的活動記錄 （稽核和登入） 的資料保留在 hello Azure 入口網站？**</span><span class="sxs-lookup"><span data-stu-id="47f14-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="47f14-107">**答：**我們免費的客戶，並藉由切換 tooan Azure AD Premium 1 或 Premium 2 授權，我們會提供 7 天的資料存取，您可以向上 too30 天的資料。</span><span class="sxs-lookup"><span data-stu-id="47f14-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="47f14-108">如需有關保留期的更多詳細資料，請參閱 [Azure Active Directory 報告保留原則](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="47f14-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="47f14-109">**問： 如何花費時間直到完成工作之後，我可以看見 hello 活動資料？**</span><span class="sxs-lookup"><span data-stu-id="47f14-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="47f14-110">**答：**稽核活動記錄檔具有介於 15 分鐘 tooan 小時的延遲。</span><span class="sxs-lookup"><span data-stu-id="47f14-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="47f14-111">登入活動記錄檔有延遲，範圍介於 15 分鐘的大部分記錄和 too2 幾個記錄的時數。</span><span class="sxs-lookup"><span data-stu-id="47f14-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="47f14-112">**問： 我需要的 toobe 全域管理員 toosee hello 活動記錄在 hello Azure 入口網站或透過 hello API tooget 資料？**</span><span class="sxs-lookup"><span data-stu-id="47f14-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="47f14-113">**答：**否。</span><span class="sxs-lookup"><span data-stu-id="47f14-113">**A:** No.</span></span> <span data-ttu-id="47f14-114">您可以**安全性讀取器**、**安全性管理員**或**全域管理員**toosee 報告資料在 Azure 入口網站或透過 hello API 存取它。</span><span class="sxs-lookup"><span data-stu-id="47f14-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="47f14-115">**問： 是否可以取得 hello Azure 入口網站透過 Office 365 活動記錄檔資訊？**</span><span class="sxs-lookup"><span data-stu-id="47f14-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="47f14-116">**答：**即使 Office 365 活動和 Azure AD 的活動記錄檔共用大量的 hello 目錄資源，如果您想要的完整檢視 hello Office 365 活動記錄檔，您應該移 toohello Office 365 系統管理中心 tooget Office 365 活動記錄檔資訊。</span><span class="sxs-lookup"><span data-stu-id="47f14-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="47f14-117">**問： 與應用程式開發介面使用 Office 365 活動記錄檔的 tooget 資訊嗎？**</span><span class="sxs-lookup"><span data-stu-id="47f14-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="47f14-118">**答：**使用 hello Office 365 管理 Api tooaccess hello [Office 365 活動記錄應用程式開發介面透過](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview)。</span><span class="sxs-lookup"><span data-stu-id="47f14-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="47f14-119">**問：我可以從 Azure 入口網站下載多少記錄？**</span><span class="sxs-lookup"><span data-stu-id="47f14-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="47f14-120">**答：** too120K 記錄從 hello Azure 入口網站，您可以下載。</span><span class="sxs-lookup"><span data-stu-id="47f14-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="47f14-121">hello 記錄會依照*最近*，而根據預設，您會收到 hello 最近 120 K 記錄。</span><span class="sxs-lookup"><span data-stu-id="47f14-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="47f14-122">**問： 透過 hello 活動 API 可以查詢如何許多記錄？**</span><span class="sxs-lookup"><span data-stu-id="47f14-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="47f14-123">**答：** too1 數百萬筆記錄，您可以查詢 (如果您不使用 hello top 運算子，hello 記錄依最新)。</span><span class="sxs-lookup"><span data-stu-id="47f14-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="47f14-124">如果您使用 hello"top"運算子，您可以查詢 too500K 記錄。</span><span class="sxs-lookup"><span data-stu-id="47f14-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="47f14-125">您可以找到上如何 toouse hello API 此處的範例查詢[這裡](active-directory-reporting-api-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="47f14-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="47f14-126">**問：我要如何取得進階授權？**</span><span class="sxs-lookup"><span data-stu-id="47f14-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="47f14-127">**答：**看到[開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)回應 toothis 問題。</span><span class="sxs-lookup"><span data-stu-id="47f14-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="47f14-128">**問：在取得進階授權之後，我應該多快能看見活動資料？**</span><span class="sxs-lookup"><span data-stu-id="47f14-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="47f14-129">**答：**若您已經有免費的授權，活動資料，則您可以看見 hello 相同的資料。</span><span class="sxs-lookup"><span data-stu-id="47f14-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="47f14-130">如果您沒有任何資料，則必須花一或兩天的時間。</span><span class="sxs-lookup"><span data-stu-id="47f14-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="47f14-131">**問：在取得 Azure AD 進階授權之後，我是否會看見上個月的資料？**</span><span class="sxs-lookup"><span data-stu-id="47f14-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="47f14-132">**答：**您最近切換 tooa Premium 版本 （包括試用版），您可以一開始查看資料 too7 天。</span><span class="sxs-lookup"><span data-stu-id="47f14-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="47f14-133">當資料會累積時，您會看到向上 too30 天。</span><span class="sxs-lookup"><span data-stu-id="47f14-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="47f14-134">**問： 有處於風險事件的識別身分保護，但我我看不到對應登入 hello 中所有的登入。這是預期行為嗎？**</span><span class="sxs-lookup"><span data-stu-id="47f14-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="47f14-135">**答：**是，Identity Protection 會評估所有驗證流程的風險，無論是互動式或非互動式。</span><span class="sxs-lookup"><span data-stu-id="47f14-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="47f14-136">不過，所有登入的唯一報表會都顯示只有 hello 互動式登入。</span><span class="sxs-lookup"><span data-stu-id="47f14-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="47f14-137">**問： 如何可以下載 Azure 入口網站中的 hello 」 使用者標示為進行風險 」 報表？**</span><span class="sxs-lookup"><span data-stu-id="47f14-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="47f14-138">**答：** hello 選項 toodownload*使用者加上旗標的風險*報表很快就會加入。</span><span class="sxs-lookup"><span data-stu-id="47f14-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="47f14-139">**問： 如何知道為什麼登入或使用者已加上旗標 hello Azure 入口網站中有風險？**</span><span class="sxs-lookup"><span data-stu-id="47f14-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="47f14-140">**答：** Premium edition 客戶可以進一步了解 hello 基礎 hello 使用者 」 使用者標示為進行風險 」 中按一下，或按一下 hello"風險登入 」 的風險事件。</span><span class="sxs-lookup"><span data-stu-id="47f14-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="47f14-141">Free 和 Basic 版客戶會取得 toosee hello 高風險使用者和登入沒有 hello 基礎風險事件資訊。</span><span class="sxs-lookup"><span data-stu-id="47f14-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="47f14-142">**問： 如何 IP 位址是以 hello 登入和風險的登入報表計算？**</span><span class="sxs-lookup"><span data-stu-id="47f14-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="47f14-143">**答：** IP 位址所發出的方式沒有任何明確的連接，IP 位址和該位址為 hello 電腦所在實體之間。</span><span class="sxs-lookup"><span data-stu-id="47f14-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="47f14-144">這是比較複雜的因素，例如行動提供者和 Vpn 通常很遠低於 hello 用戶端裝置使用位置為何實際發行從中央集區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="47f14-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="47f14-145">由於上述 hello，轉換 IP 位址 tooa 實體位置是根據追蹤、 登錄資料、 反向查詢 ups 和其他資訊的最大努力。</span><span class="sxs-lookup"><span data-stu-id="47f14-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
