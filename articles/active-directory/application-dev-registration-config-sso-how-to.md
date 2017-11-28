---
title: "aaaHow tooconfigure 新的多租用戶應用程式 |Microsoft 文件"
description: "如何 tooconfigure 單一登入功能的自訂應用程式中，您正在開發且登錄至 Azure AD。"
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="8fffe-103">如何 tooconfigure 新的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="8fffe-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="8fffe-104">在您的應用程式中啟用同盟單一登入 (SSO)，會在針對 OpenID Connect、SAML 2.0 或 WS-Fed 透過 Azure AD 進行同盟時自動啟用。</span><span class="sxs-lookup"><span data-stu-id="8fffe-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="8fffe-105">如果您的使用者有 toosign 儘管已有現有的工作階段與 Azure AD，很可能您的應用程式可能設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="8fffe-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="8fffe-106">如果您使用 ADAL/MSAL，請確定您有**PromptBehavior**設定得**自動**而**永遠**。</span><span class="sxs-lookup"><span data-stu-id="8fffe-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="8fffe-107">如果您正在建置行動應用程式，您可能需要其他組態 tooenable 代理或非代理 SSO。</span><span class="sxs-lookup"><span data-stu-id="8fffe-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="8fffe-108">若是 Android，請參閱[在 Android 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)。</span><span class="sxs-lookup"><span data-stu-id="8fffe-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="8fffe-109">若是 iOS，請參閱[在 iOS 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)。</span><span class="sxs-lookup"><span data-stu-id="8fffe-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fffe-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fffe-110">Next steps</span></span>

[<span data-ttu-id="8fffe-111">Azure AD 的 SSO</span><span class="sxs-lookup"><span data-stu-id="8fffe-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="8fffe-112">在 Android 上啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="8fffe-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="8fffe-113">在 iOS 上啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="8fffe-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="8fffe-114">整合應用程式 tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="8fffe-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="8fffe-115">適用於 AzureAD v2.0 交集應用程式的同意與權限</span><span class="sxs-lookup"><span data-stu-id="8fffe-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="8fffe-116">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="8fffe-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
