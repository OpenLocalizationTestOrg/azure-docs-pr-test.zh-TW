---
title: "登入自訂開發應用程式的問題 | Microsoft Docs"
description: "會造成您無法登入您使用 Azure AD 所開發應用程式的常見錯誤"
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
ms.openlocfilehash: b0df23e040a73d18968f547eef7347f14cc577c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-custom-developed-application"></a><span data-ttu-id="c457c-103">登入自訂開發應用程式的問題</span><span class="sxs-lookup"><span data-stu-id="c457c-103">Problems signing in to an custom-developed application</span></span>

<span data-ttu-id="c457c-104">有數種錯誤會導致您無法登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="c457c-104">There are several errors that could be causing you to not be able to sign into an app.</span></span> <span data-ttu-id="c457c-105">會遇到此問題的最大原因是應用程式設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="c457c-105">The biggest reason people encounter this problem is misconfigured apps.</span></span>

## <a name="errors-related-to--misconfigured-apps"></a><span data-ttu-id="c457c-106">與應用程式設定錯誤相關的錯誤</span><span class="sxs-lookup"><span data-stu-id="c457c-106">Errors related to  misconfigured apps</span></span>

* <span data-ttu-id="c457c-107">確認入口網站中的兩種組態符合您應用程式中的組態。</span><span class="sxs-lookup"><span data-stu-id="c457c-107">Verify both the configurations in the portal match what you have in your app.</span></span> <span data-ttu-id="c457c-108">特別是，比較用戶端/應用程識別碼、回覆 URL、用戶端密碼/金鑰，及應用程式識別碼 URI。</span><span class="sxs-lookup"><span data-stu-id="c457c-108">Specifically, compare Client/Application ID, Reply URLs, Client Secrets/Keys, and App ID URI.</span></span>

* <span data-ttu-id="c457c-109">將您正以程式碼要求存取的資源，與在 [必要的資源] 索引標籤中設定的權限比較，以確定您只要求所設定的資源。</span><span class="sxs-lookup"><span data-stu-id="c457c-109">Compare the resource you’re requesting access to in code with the configured permissions in the **Required Resources** tab to make sure you only request resources you’ve configured.</span></span>

* <span data-ttu-id="c457c-110">請參閱 [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) 中任何類似的錯誤或問題。</span><span class="sxs-lookup"><span data-stu-id="c457c-110">See [Azure AD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory) for any similar errors or problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c457c-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c457c-111">Next steps</span></span>

[<span data-ttu-id="c457c-112">Azure AD 開發人員指南</span><span class="sxs-lookup"><span data-stu-id="c457c-112">Azure AD Developer Guide</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide)<br>

[<span data-ttu-id="c457c-113">整合應用程式與 Azure AD</span><span class="sxs-lookup"><span data-stu-id="c457c-113">Consent and Integrating Apps to Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications>)<br>

[<span data-ttu-id="c457c-114">Azure AD v2.0 交集應用程式中的同意及權限</span><span class="sxs-lookup"><span data-stu-id="c457c-114">Consent and Permissioning for Azure AD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="c457c-115">Azure AD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="c457c-115">Azure AD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory>)
