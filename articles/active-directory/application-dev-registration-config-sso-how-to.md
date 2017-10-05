---
title: "如何設定新的多租用戶應用程式 | Microsoft Docs"
description: "如何為您正在開發並向 Azure AD 註冊的自訂應用程式設定單一登入。"
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="c514e-103">如何設定新的多租用戶應用程式</span><span class="sxs-lookup"><span data-stu-id="c514e-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="c514e-104">在您的應用程式中啟用同盟單一登入 (SSO)，會在針對 OpenID Connect、SAML 2.0 或 WS-Fed 透過 Azure AD 進行同盟時自動啟用。</span><span class="sxs-lookup"><span data-stu-id="c514e-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="c514e-105">如果您的使用者儘管目前已經有含 Azure AD 的工作階段還是必須登入，很可能是您的應用程式設定錯誤。</span><span class="sxs-lookup"><span data-stu-id="c514e-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="c514e-106">如果您使用 ADAL/MSAL，請確定已將 **PromptBehavior** 設為 **Auto**，而不是 **Always**。</span><span class="sxs-lookup"><span data-stu-id="c514e-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="c514e-107">如果您正在建置行動裝置應用程式，您可能需要其他設定來啟用代理或非代理的 SSO。</span><span class="sxs-lookup"><span data-stu-id="c514e-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="c514e-108">若是 Android，請參閱[在 Android 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)。</span><span class="sxs-lookup"><span data-stu-id="c514e-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="c514e-109">若是 iOS，請參閱[在 iOS 上啟用跨應用程式的 SSO](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)。</span><span class="sxs-lookup"><span data-stu-id="c514e-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c514e-110">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c514e-110">Next steps</span></span>

[<span data-ttu-id="c514e-111">Azure AD 的 SSO</span><span class="sxs-lookup"><span data-stu-id="c514e-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="c514e-112">在 Android 上啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="c514e-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="c514e-113">在 iOS 上啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="c514e-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="c514e-114">將應用程式整合到 AzureAD</span><span class="sxs-lookup"><span data-stu-id="c514e-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="c514e-115">適用於 AzureAD v2.0 交集應用程式的同意與權限</span><span class="sxs-lookup"><span data-stu-id="c514e-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="c514e-116">AzureAD StackOverflow (英文)</span><span class="sxs-lookup"><span data-stu-id="c514e-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
