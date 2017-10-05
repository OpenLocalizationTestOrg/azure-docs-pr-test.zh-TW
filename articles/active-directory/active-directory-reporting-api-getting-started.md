---
title: "在 Azure AD 傳統入口網站上開始使用 Azure AD 報告 API | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="40ad3-103">在 Azure AD 傳統入口網站上開始使用 Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="40ad3-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="40ad3-104">*本主題是 [Azure Active Directory 報告指南](active-directory-reporting-guide.md)的一部分。*</span><span class="sxs-lookup"><span data-stu-id="40ad3-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="40ad3-105">Azure Active Directory 提供各種報告給您。</span><span class="sxs-lookup"><span data-stu-id="40ad3-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="40ad3-106">這些報告的資料對您的應用程式 (例如 SIEM 系統、稽核和商業智慧工具) 可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="40ad3-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="40ad3-107">Azure AD 報告 API 透過一組以 REST 為基礎的 API 提供資料的程式設計方式存取。</span><span class="sxs-lookup"><span data-stu-id="40ad3-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="40ad3-108">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="40ad3-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="40ad3-109">本文提供給您開始使用 Azure AD 報告 API 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="40ad3-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="40ad3-110">在下一節中，您可尋找更多有關使用稽核和登入 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="40ad3-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="40ad3-111">對於其他所有 API，請參閱 [Azure AD 報告和事件 (預覽)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) 一文。</span><span class="sxs-lookup"><span data-stu-id="40ad3-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="40ad3-112">如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="40ad3-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="40ad3-113">學習圖</span><span class="sxs-lookup"><span data-stu-id="40ad3-113">Learning map</span></span>
1. <span data-ttu-id="40ad3-114">**準備** - 您必須先完成 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites.md)，才能測試 API 範例。</span><span class="sxs-lookup"><span data-stu-id="40ad3-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="40ad3-115">**瀏覽** - 取得報告 API 的第一印象：</span><span class="sxs-lookup"><span data-stu-id="40ad3-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="40ad3-116">使用稽核 API 的範例</span><span class="sxs-lookup"><span data-stu-id="40ad3-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="40ad3-117">使用登入活動報告 API 的範例</span><span class="sxs-lookup"><span data-stu-id="40ad3-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="40ad3-118">**自訂** - 建立您自己的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="40ad3-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="40ad3-119">使用稽核 API 參考</span><span class="sxs-lookup"><span data-stu-id="40ad3-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="40ad3-120">使用登入活動報告 API 參考</span><span class="sxs-lookup"><span data-stu-id="40ad3-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="40ad3-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="40ad3-121">Next Steps</span></span>
<span data-ttu-id="40ad3-122">如果您想要查看所有可用的 Azure AD 圖形 API 端點，請瀏覽至 [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta)。</span><span class="sxs-lookup"><span data-stu-id="40ad3-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

