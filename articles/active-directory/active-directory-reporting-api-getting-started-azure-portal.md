---
title: "開始使用 Azure AD 報告 API | Microsoft Docs"
description: "如何開始使用 Azure Active Directory 報告 API"
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
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="8bd4c-103">開始使用 Azure Active Directory 報告 API</span><span class="sxs-lookup"><span data-stu-id="8bd4c-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="8bd4c-104">Azure Active Directory 提供各種報告給您。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="8bd4c-105">這些報告的資料對您的應用程式 (例如 SIEM 系統、稽核和商業智慧工具) 可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="8bd4c-106">Azure AD 報告 API 透過一組以 REST 為基礎的 API 提供資料的程式設計方式存取。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="8bd4c-107">您可以從各種程式設計語言和工具呼叫這些 API。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="8bd4c-108">本文提供給您開始使用 Azure AD 報告 API 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="8bd4c-109">在下一節中，您可尋找更多有關使用稽核和登入 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="8bd4c-110">關於閱讀常見問題集，請參閱我們的[常見問題集](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq)。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="8bd4c-111">關於問題，請[提出支援票證](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="8bd4c-112">學習圖</span><span class="sxs-lookup"><span data-stu-id="8bd4c-112">Learning map</span></span>
1. <span data-ttu-id="8bd4c-113">**準備** - 您必須先完成 [存取 Azure AD 報告 API 的必要條件](active-directory-reporting-api-prerequisites-azure-portal.md)，才能測試 API 範例。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="8bd4c-114">**瀏覽** - 取得報告 API 的第一印象：</span><span class="sxs-lookup"><span data-stu-id="8bd4c-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="8bd4c-115">使用稽核 API 的範例</span><span class="sxs-lookup"><span data-stu-id="8bd4c-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="8bd4c-116">使用登入活動報告 API 的範例</span><span class="sxs-lookup"><span data-stu-id="8bd4c-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="8bd4c-117">**自訂** - 建立您自己的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="8bd4c-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="8bd4c-118">使用稽核 API 參考</span><span class="sxs-lookup"><span data-stu-id="8bd4c-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="8bd4c-119">使用登入活動報告 API 參考</span><span class="sxs-lookup"><span data-stu-id="8bd4c-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="8bd4c-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8bd4c-120">Next Steps</span></span>
<span data-ttu-id="8bd4c-121">如果您想要查看所有可用的 Azure AD 圖形 API 端點，請使用此連結：[https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta)。</span><span class="sxs-lookup"><span data-stu-id="8bd4c-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

