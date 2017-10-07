---
title: "aaaGetting 入門 hello Azure AD 傳統入口網站上的 hello Azure AD 報告 API |Microsoft 文件"
description: "如何開始使用 tooget hello Azure Active Directory 報告 API"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="3e000-103">開始使用 hello Azure Active Directory 報告 hello Azure AD 傳統入口網站應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="3e000-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="3e000-104">*本主題是一部分的 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。*</span><span class="sxs-lookup"><span data-stu-id="3e000-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="3e000-105">Azure Active Directory 提供各種報告給您。</span><span class="sxs-lookup"><span data-stu-id="3e000-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="3e000-106">這些報告的 hello 資料可以是很有幫助 tooyour 應用程式，例如 SIEM 系統、 稽核和商業智慧工具。</span><span class="sxs-lookup"><span data-stu-id="3e000-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="3e000-107">hello Azure AD 報告 Api 提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="3e000-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="3e000-108">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="3e000-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="3e000-109">這篇文章提供您 hello 資訊需要 tooget 入門 hello Azure AD 報告 Api。</span><span class="sxs-lookup"><span data-stu-id="3e000-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="3e000-110">在 hello 下一步 區段中，您會發現使用 hello 的更多詳細稽核和登入應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="3e000-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="3e000-111">所有其他應用程式開發介面，請參閱 hello [Azure AD 報告和 events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview)發行項。</span><span class="sxs-lookup"><span data-stu-id="3e000-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="3e000-112">如有相關疑問、問題或意見，請連絡 [AAD 報告協助](mailto:aadreportinghelp@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="3e000-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="3e000-113">學習圖</span><span class="sxs-lookup"><span data-stu-id="3e000-113">Learning map</span></span>
1. <span data-ttu-id="3e000-114">**準備**-您可以測試您應用程式開發介面的範例之前，您需要 toocomplete hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="3e000-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="3e000-115">**瀏覽**-取得的 hello reporting Api 的第一印象：</span><span class="sxs-lookup"><span data-stu-id="3e000-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="3e000-116">Hello 稽核應用程式開發介面使用 hello 範例</span><span class="sxs-lookup"><span data-stu-id="3e000-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="3e000-117">Hello 登入活動報表 api 使用 hello 範例</span><span class="sxs-lookup"><span data-stu-id="3e000-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="3e000-118">**自訂** - 建立您自己的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="3e000-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="3e000-119">使用 hello 稽核應用程式開發介面參考</span><span class="sxs-lookup"><span data-stu-id="3e000-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="3e000-120">使用 hello 登入活動報表應用程式開發介面參考</span><span class="sxs-lookup"><span data-stu-id="3e000-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="3e000-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e000-121">Next Steps</span></span>
<span data-ttu-id="3e000-122">如果您好奇 toosee 的所有瀏覽過 hello 可用的 Azure AD Graph API 端點[https://graph.windows.net/tenant-name/reports/$ metadata？ api 版本 = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta)。</span><span class="sxs-lookup"><span data-stu-id="3e000-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

