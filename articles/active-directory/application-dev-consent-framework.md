---
title: "應用程式同意如何運作 | Microsoft Docs"
description: "深入了解 Azure AD 同意架構的運作方式，以了解如何在開發搭配 Azure AD 執行的應用程式時使用它"
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
ms.openlocfilehash: 5abddf3a8698e3eb39f118f54eeac62ce68fed39
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="6b253-103">應用程式同意如何運作</span><span class="sxs-lookup"><span data-stu-id="6b253-103">How application consent works</span></span>

<span data-ttu-id="6b253-104">此文章旨在協助您深入了解 Azure AD 同意架構的運作方式，以便您可以更有效地開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b253-104">This article is to help you learn more about how the Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="6b253-105">建議的文件</span><span class="sxs-lookup"><span data-stu-id="6b253-105">Recommended documents</span></span>

- <span data-ttu-id="6b253-106">取得有關[同意如何讓資源擁有者控管應用程式對資源的存取權](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent)的基本知識。</span><span class="sxs-lookup"><span data-stu-id="6b253-106">Get a general understanding of [how consent allows a resource owner to govern an application's access to resources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="6b253-107">取得有關 [Azure AD 同意架構如何實作同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework)的逐步概觀。</span><span class="sxs-lookup"><span data-stu-id="6b253-107">Get a step-by-step overview of [how the Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="6b253-108">深入了解[多租用戶應用程式如何使用同意架構](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent)來實作「使用者」與「系統管理員」同意，進而支援更進階的多層應用程式模式。</span><span class="sxs-lookup"><span data-stu-id="6b253-108">For more depth, learn [how a multi-tenant application can use the consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to implement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="6b253-109">深入了解[授權碼授與流程期間 OAuth 2.0 通訊協定層如何支援同意](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)。</span><span class="sxs-lookup"><span data-stu-id="6b253-109">For more depth, learn [how consent is supported at the OAuth 2.0 protocol layer during the authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b253-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6b253-110">Next steps</span></span>
[<span data-ttu-id="6b253-111">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="6b253-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
