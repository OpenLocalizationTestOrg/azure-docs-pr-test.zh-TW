---
title: "如何將多租用戶應用程式新增至 Azure AD 應用程式庫 | Microsoft Docs"
description: "說明如何在 Azure AD 應用程式庫中列出自訂開發的多租用戶應用程式"
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="6f9ad-103">如何將多租用戶應用程式新增至 Azure AD 應用程式庫</span><span class="sxs-lookup"><span data-stu-id="6f9ad-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="6f9ad-104">什麼是 Azure AD 應用程式庫？</span><span class="sxs-lookup"><span data-stu-id="6f9ad-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="6f9ad-105">Azure AD 應用程式庫是在數百萬 Azure Active Directory 客戶面前，讓您的應用程式脫穎而出的絕佳方法，以擴大該應用程式在市集的影響力和曝光率。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="6f9ad-106">下列步驟說明如何在 Azure AD 應用程式庫中列出您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="6f9ad-107">如果您的應用程式支援 SAML 或 OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="6f9ad-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="6f9ad-108">如果您有想要列在 Azure AD 應用程式庫中的多租用戶應用程式，您必須先確定該應用程式支援下列其中一種單一登入技術：</span><span class="sxs-lookup"><span data-stu-id="6f9ad-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="6f9ad-109">**OpenID Connect** - 直接整合 Azure AD，使用 OpenID Connect 進行驗證，使用 Azure AD 同意 API 進行設定。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="6f9ad-110">如果您是剛開始整合，而您的應用程式不支援 SAML，這是建議的模式。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="6f9ad-111">**SAML** – 您的應用程式已能夠使用 SAML 通訊協定設定協力廠商識別提供者。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="6f9ad-112">如果您的應用程式支援這其中一種單一登入模式，而且您想要在 Azure AD 應用程式庫列出您的多租用戶應用程式，即可依照本文件後續內容中的步驟執行。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="6f9ad-113">若要即刻開始使用，請將電子郵件傳送至 **waadpartners@microsoft.com** 。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="6f9ad-114">如果您的應用程式不支援 SAML 或 OpenIDConnect</span><span class="sxs-lookup"><span data-stu-id="6f9ad-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="6f9ad-115">即使您的應用程式不支援這其中一種模式，我們仍然可以使用密碼單一登入技術，將它整合到我們的資源庫。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="6f9ad-116">如果您想要探索此選項，您可以將電子郵件傳送至 **waadpartners@microsoft.com**。</span><span class="sxs-lookup"><span data-stu-id="6f9ad-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f9ad-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6f9ad-117">Next steps</span></span>
[<span data-ttu-id="6f9ad-118">如何在 Azure Active Directory 應用程式庫中列出您的應用程式</span><span class="sxs-lookup"><span data-stu-id="6f9ad-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
