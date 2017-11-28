---
title: "aaaListing hello Azure Active Directory 應用程式庫中的應用程式"
description: "Toolist 支援單一登入的應用程式如何 hello Azure Active Directory 庫 |Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="f94c5-103">列出在 hello Azure Active Directory 應用程式庫中的應用程式</span><span class="sxs-lookup"><span data-stu-id="f94c5-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="f94c5-104">toolist hello 中支援單一登入與 Azure Active Directory 的應用程式[Azure AD 資源庫](https://azure.microsoft.com/marketplace/active-directory/all/)，hello 應用程式第一次需要 hello 下列整合模式的其中一個 tooimplement:</span><span class="sxs-lookup"><span data-stu-id="f94c5-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="f94c5-105">**OpenID Connect** -直接整合與 Azure AD 使用 OpenID Connect 來進行驗證並 hello 組態的 Azure AD 同意應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="f94c5-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="f94c5-106">如果您剛開始整合您的應用程式不支援 SAML，這是 hello 建議模式。</span><span class="sxs-lookup"><span data-stu-id="f94c5-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="f94c5-107">**SAML** – 您的應用程式已擁有 hello 能力 tooconfigure 協力廠商身分識別提供者使用 hello SAML 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="f94c5-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="f94c5-108">每個模式的列出需求如下。</span><span class="sxs-lookup"><span data-stu-id="f94c5-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="f94c5-109">OpenID Connect 整合</span><span class="sxs-lookup"><span data-stu-id="f94c5-109">OpenID Connect Integration</span></span>
<span data-ttu-id="f94c5-110">toointegrate 應用程式與 Azure AD，下列 hello[開發人員指示](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="f94c5-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="f94c5-111">然後完成 hello 回答以下問題和傳送toowaadpartners@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="f94c5-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="f94c5-112">提供可供 hello Azure AD team tootest hello 整合的應用程式中的測試租用戶或帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="f94c5-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="f94c5-113">提供有關如何 hello Azure AD 的小組可以登入和連接的 Azure AD 使用 hello 的 tooyour 應用程式執行個體的指示[Azure AD 的同意架構](active-directory-integrating-applications.md#overview-of-the-consent-framework)。</span><span class="sxs-lookup"><span data-stu-id="f94c5-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="f94c5-114">提供所需的 hello Azure AD 的任何進一步指示小組 tootest 單一登入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f94c5-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="f94c5-115">提供下列 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="f94c5-115">Provide hello info below:</span></span>

> <span data-ttu-id="f94c5-116">公司名稱：</span><span class="sxs-lookup"><span data-stu-id="f94c5-116">Company Name:</span></span>
> 
> <span data-ttu-id="f94c5-117">公司網站：</span><span class="sxs-lookup"><span data-stu-id="f94c5-117">Company Website:</span></span>
> 
> <span data-ttu-id="f94c5-118">應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="f94c5-118">Application Name:</span></span>
> 
> <span data-ttu-id="f94c5-119">應用程式描述 (200 個字元的限制)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="f94c5-120">應用程式網站 (資訊)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="f94c5-121">應用程式技術支援網站或連絡資訊：</span><span class="sxs-lookup"><span data-stu-id="f94c5-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="f94c5-122">應用程式識別碼 hello 應用程式，在 https://portal.azure.com hello 應用程式詳細資料中所示：</span><span class="sxs-lookup"><span data-stu-id="f94c5-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="f94c5-123">客戶尋求 toosign 註冊應用程式註冊 URL 和/或購買 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f94c5-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="f94c5-124">選擇您的應用程式 toobe （如可用的類別目錄，請參閱 Azure Active Directory Marketplace hello） 底下所列的 toothree 類別：</span><span class="sxs-lookup"><span data-stu-id="f94c5-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="f94c5-125">附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="f94c5-126">附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="f94c5-127">附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="f94c5-128">SAML 整合</span><span class="sxs-lookup"><span data-stu-id="f94c5-128">SAML Integration</span></span>
<span data-ttu-id="f94c5-129">支援 SAML 2.0 的任何應用程式可直接與使用 Azure AD 租用戶整合[這些指示 tooadd 自訂應用程式](../active-directory-saas-custom-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="f94c5-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="f94c5-130">一旦您已經測試過您的應用程式整合搭配 Azure AD，傳送下列資訊太 hello<mailto:waadpartners@microsoft.com>。</span><span class="sxs-lookup"><span data-stu-id="f94c5-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="f94c5-131">提供可供 hello Azure AD team tootest hello 整合的應用程式中的測試租用戶或帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="f94c5-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="f94c5-132">提供 hello SAML 登入 URL，簽發者 URL (實體 ID) 和應用程式的回覆 URL （判斷提示取用者服務） 值，如所述[這裡](../active-directory-saas-custom-apps.md)。</span><span class="sxs-lookup"><span data-stu-id="f94c5-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="f94c5-133">如果您通常會提供這些值做為一個 SAML 中繼資料檔的一部分，也請一併傳送該檔案。</span><span class="sxs-lookup"><span data-stu-id="f94c5-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="f94c5-134">提供如何的簡短描述 tooconfigure Azure AD 作為身分識別提供者使用 SAML 2.0 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="f94c5-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="f94c5-135">如果您的應用程式支援設定的 Azure AD 作為身分識別提供者透過自助系統管理網站，然後請確定 hello 以上所提供的認證包含 hello 能力 tooset 其設定。</span><span class="sxs-lookup"><span data-stu-id="f94c5-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="f94c5-136">提供下列 hello 資訊：</span><span class="sxs-lookup"><span data-stu-id="f94c5-136">Provide hello info below:</span></span>

> <span data-ttu-id="f94c5-137">公司名稱：</span><span class="sxs-lookup"><span data-stu-id="f94c5-137">Company Name:</span></span>
> 
> <span data-ttu-id="f94c5-138">公司網站：</span><span class="sxs-lookup"><span data-stu-id="f94c5-138">Company Website:</span></span>
> 
> <span data-ttu-id="f94c5-139">應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="f94c5-139">Application Name:</span></span>
> 
> <span data-ttu-id="f94c5-140">應用程式描述 (200 個字元的限制)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="f94c5-141">應用程式網站 (資訊)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="f94c5-142">應用程式技術支援網站或連絡資訊：</span><span class="sxs-lookup"><span data-stu-id="f94c5-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="f94c5-143">客戶尋求 toosign 註冊應用程式註冊 URL 和/或購買 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f94c5-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="f94c5-144">選擇您的應用程式 toobe 底下所列的 toothree 類別 (如可用的類別目錄，請參閱 hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="f94c5-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="f94c5-145">附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="f94c5-146">附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="f94c5-147">附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：</span><span class="sxs-lookup"><span data-stu-id="f94c5-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

