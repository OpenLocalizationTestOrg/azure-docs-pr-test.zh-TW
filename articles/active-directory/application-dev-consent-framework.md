---
title: "aaaHow 應用程式同意 works |Microsoft 文件"
description: "深入了解 hello Azure AD 的同意架構的 toosee 的運作方式如何使用它在 Azure AD 上開發應用程式時"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 1b090c0c8d49320a012d8a06b7e9d35134a3ab43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="ca839-103">應用程式同意如何運作</span><span class="sxs-lookup"><span data-stu-id="ca839-103">How application consent works</span></span>

<span data-ttu-id="ca839-104">本文是的 toohelp 您進一步了解，您可以更有效地開發應用程式，hello Azure AD 的同意架構的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ca839-104">This article is toohelp you learn more about how hello Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="ca839-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="ca839-105">Recommended documents</span></span>

- <span data-ttu-id="ca839-106">取得有基本認識的[如何同意可讓資源擁有者 toogovern 應用程式的存取 tooresources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent)。</span><span class="sxs-lookup"><span data-stu-id="ca839-106">Get a general understanding of [how consent allows a resource owner toogovern an application's access tooresources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="ca839-107">概略逐步[hello Azure AD 的同意架構如何實作同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework)。</span><span class="sxs-lookup"><span data-stu-id="ca839-107">Get a step-by-step overview of [how hello Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="ca839-108">更深入，深入了解[多租用戶應用程式如何使用 hello 同意架構](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)tooimplement"user"和"admin"同意，支援更進階的多層式應用程式模式。</span><span class="sxs-lookup"><span data-stu-id="ca839-108">For more depth, learn [how a multi-tenant application can use hello consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) tooimplement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="ca839-109">更深入，深入了解[同意如何在 hello OAuth 2.0 通訊協定層支援 hello 授權碼授與流程期間。](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span><span class="sxs-lookup"><span data-stu-id="ca839-109">For more depth, learn [how consent is supported at hello OAuth 2.0 protocol layer during hello authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca839-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca839-110">Next steps</span></span>
[<span data-ttu-id="ca839-111">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="ca839-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
