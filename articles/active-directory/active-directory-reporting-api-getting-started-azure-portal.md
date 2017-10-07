---
title: "aaaGetting 入門 hello Azure AD 報告 API |Microsoft 文件"
description: "如何開始使用 tooget hello Azure Active Directory 報告 API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="b7e5f-103">開始使用 hello Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="b7e5f-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="b7e5f-104">Azure Active Directory 提供各種報告給您。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="b7e5f-105">這些報告的 hello 資料可以是很有幫助 tooyour 應用程式，例如 SIEM 系統、 稽核和商業智慧工具。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="b7e5f-106">hello Azure AD 報告 Api 提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="b7e5f-107">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="b7e5f-108">這篇文章提供您 hello 資訊需要 tooget 入門 hello Azure AD 報告 Api。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="b7e5f-109">在 hello 下一步 區段中，您會發現使用 hello 的更多詳細稽核和登入應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="b7e5f-110">關於閱讀常見問題集，請參閱我們的[常見問題集](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq)。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="b7e5f-111">關於問題，請[提出支援票證](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="b7e5f-112">學習圖</span><span class="sxs-lookup"><span data-stu-id="b7e5f-112">Learning map</span></span>
1. <span data-ttu-id="b7e5f-113">**準備**-您可以測試您應用程式開發介面的範例之前，您需要 toocomplete hello[必要條件 tooaccess hello Azure AD 報告 API](active-directory-reporting-api-prerequisites-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="b7e5f-114">**瀏覽**-取得的 hello reporting Api 的第一印象：</span><span class="sxs-lookup"><span data-stu-id="b7e5f-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="b7e5f-115">Hello 稽核應用程式開發介面使用 hello 範例</span><span class="sxs-lookup"><span data-stu-id="b7e5f-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="b7e5f-116">Hello 登入活動報表 api 使用 hello 範例</span><span class="sxs-lookup"><span data-stu-id="b7e5f-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="b7e5f-117">**自訂** - 建立您自己的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="b7e5f-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="b7e5f-118">使用 hello 稽核應用程式開發介面參考</span><span class="sxs-lookup"><span data-stu-id="b7e5f-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="b7e5f-119">使用 hello 登入活動報表應用程式開發介面參考</span><span class="sxs-lookup"><span data-stu-id="b7e5f-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="b7e5f-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7e5f-120">Next Steps</span></span>
<span data-ttu-id="b7e5f-121">如果您好奇 toosee 所有可用的 Azure AD Graph API 端點，請使用此連結： [https://graph.windows.net/tenant-name/activities/$ metadata？ api 版本 = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta)。</span><span class="sxs-lookup"><span data-stu-id="b7e5f-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

