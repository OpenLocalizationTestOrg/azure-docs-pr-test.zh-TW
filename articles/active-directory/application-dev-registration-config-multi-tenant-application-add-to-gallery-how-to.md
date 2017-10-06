---
title: "aaaHow tooadd 多租用戶應用程式 toohello Azure AD 應用程式庫 |Microsoft 文件"
description: "說明如何您也可以列出自訂開發多租用戶應用程式在 hello Azure AD 應用程式庫"
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
ms.openlocfilehash: 2dc6e0d783835d2639a7e6dda172110ee860a977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-multi-tenant-application-toohello-azure-ad-application-gallery"></a><span data-ttu-id="2a403-103">如何 tooadd 多租用戶應用程式 toohello Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="2a403-103">How tooadd a multi-tenant application toohello Azure AD application gallery</span></span>

## <a name="what-is-hello-azure-ad-application-gallery"></a><span data-ttu-id="2a403-104">什麼是 Azure AD 應用程式庫 hello？</span><span class="sxs-lookup"><span data-stu-id="2a403-104">What is hello Azure AD Application Gallery?</span></span>

<span data-ttu-id="2a403-105">hello Azure AD 應用程式庫是很好的方法 tooget 前面所有 hello 數以百萬計的 Azure Active Directory 客戶 toobroaden hello 影響您應用程式，而抵達 hello marketplace 中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a403-105">hello Azure AD Application Gallery is a great way tooget your application in front of all hello millions of Azure Active Directory customers toobroaden hello impact and reach of your application in hello marketplace.</span></span> <span data-ttu-id="2a403-106">hello 下列步驟說明如何您也可以列出 hello Azure AD 應用程式庫中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="2a403-106">hello below steps explain how you can list your application in hello Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="2a403-107">如果您的應用程式支援 SAML 或 OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="2a403-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="2a403-108">如果您有您想要 toolist hello Azure AD 應用程式庫中的多租用戶應用程式，您必須先確定您的應用程式支援 hello 遵循單一登入技術的其中一個：</span><span class="sxs-lookup"><span data-stu-id="2a403-108">If you have a multi-tenant application you'd like toolist in hello Azure AD Application Gallery, you must first make sure that your application supports one of hello following single sign-on technologies:</span></span>

1. <span data-ttu-id="2a403-109">**OpenID Connect** -直接整合與 Azure AD 使用 OpenID Connect 來進行驗證並 hello 組態的 Azure AD 同意應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="2a403-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="2a403-110">如果您剛開始整合您的應用程式不支援 SAML，這是 hello 建議模式。</span><span class="sxs-lookup"><span data-stu-id="2a403-110">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
2. <span data-ttu-id="2a403-111">**SAML** – 您的應用程式已擁有 hello 能力 tooconfigure 協力廠商身分識別提供者使用 hello SAML 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2a403-111">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="2a403-112">如果您的應用程式支援其中一個單一登入模式，而且您想要 toolist hello Azure AD 應用程式庫中的多租用戶應用程式，您可以依照以下的 hello 文件中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="2a403-112">If your application supports one of these single sign-on modes and you'd like toolist your multi-tenant application in hello Azure AD Application Gallery, you can follow hello steps in hello document below.</span></span> <span data-ttu-id="2a403-113">快速入門 tooget 傳送電子郵件太**waadpartners@microsoft.com**。</span><span class="sxs-lookup"><span data-stu-id="2a403-113">tooget started quickly send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="2a403-114">如果您的應用程式不支援 SAML 或 OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="2a403-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="2a403-115">即使您的應用程式不支援這其中一種模式，我們仍然可以使用密碼單一登入技術，將它整合到我們的資源庫。</span><span class="sxs-lookup"><span data-stu-id="2a403-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="2a403-116">如果您想要 tooexplore 這個選項時，可以傳送電子郵件太**waadpartners@microsoft.com**。</span><span class="sxs-lookup"><span data-stu-id="2a403-116">If you'd like tooexplore this option, you can send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a403-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a403-117">Next steps</span></span>
[<span data-ttu-id="2a403-118">如何 toolist hello Azure Active Directory 應用程式庫中的應用程式</span><span class="sxs-lookup"><span data-stu-id="2a403-118">How toolist your application in hello Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
