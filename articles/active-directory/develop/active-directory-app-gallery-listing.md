---
title: "在 Azure Active Directory 應用程式庫中列出您的應用程式"
description: "如何列出 Azure Active Directory 組件庫中支援單一登入的應用程式 | Microsoft Azure"
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
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="64184-103">在 Azure Active Directory 應用程式庫中列出您的應用程式</span><span class="sxs-lookup"><span data-stu-id="64184-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="64184-104">若要在 [Azure AD 資源庫](https://azure.microsoft.com/marketplace/active-directory/all/)中列出某個支援單一登入搭配 Azure Active Directory 的應用程式 ，該應用程式首先必須實作下列其中一項整合模式：</span><span class="sxs-lookup"><span data-stu-id="64184-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="64184-105">**OpenID Connect** - 直接整合 Azure AD，使用 OpenID Connect 進行驗證，使用 Azure AD 同意 API 進行設定。</span><span class="sxs-lookup"><span data-stu-id="64184-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="64184-106">如果您是剛開始整合，而您的應用程式不支援 SAML，這是建議的模式。</span><span class="sxs-lookup"><span data-stu-id="64184-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="64184-107">**SAML** – 您的應用程式已能夠使用 SAML 通訊協定設定協力廠商識別提供者。</span><span class="sxs-lookup"><span data-stu-id="64184-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="64184-108">每個模式的列出需求如下。</span><span class="sxs-lookup"><span data-stu-id="64184-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="64184-109">OpenID Connect 整合</span><span class="sxs-lookup"><span data-stu-id="64184-109">OpenID Connect Integration</span></span>
<span data-ttu-id="64184-110">若要整合您的應用程式與 Azure AD，請遵循 [開發人員指示](active-directory-authentication-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="64184-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="64184-111">接著完成下面問題，並傳送至 waadpartners@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="64184-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="64184-112">提供可由 Azure AD 小組搭配您的應用程式來測試整合的測試租用戶或帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="64184-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="64184-113">提供有關 Azure AD 小組如何使用 [Azure AD 同意架構](active-directory-integrating-applications.md#overview-of-the-consent-framework)登入並連接 Azure AD 執行個體到您的應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="64184-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="64184-114">提供 Azure AD 小組搭配您的應用程式測試單一登入所需的任何進一步指示。</span><span class="sxs-lookup"><span data-stu-id="64184-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="64184-115">提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="64184-115">Provide the info below:</span></span>

> <span data-ttu-id="64184-116">公司名稱：</span><span class="sxs-lookup"><span data-stu-id="64184-116">Company Name:</span></span>
> 
> <span data-ttu-id="64184-117">公司網站：</span><span class="sxs-lookup"><span data-stu-id="64184-117">Company Website:</span></span>
> 
> <span data-ttu-id="64184-118">應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="64184-118">Application Name:</span></span>
> 
> <span data-ttu-id="64184-119">應用程式描述 (200 個字元的限制)：</span><span class="sxs-lookup"><span data-stu-id="64184-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="64184-120">應用程式網站 (資訊)：</span><span class="sxs-lookup"><span data-stu-id="64184-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="64184-121">應用程式技術支援網站或連絡資訊：</span><span class="sxs-lookup"><span data-stu-id="64184-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="64184-122">應用程式的應用程式識別碼 (如 https://portal.azure.com 中的應用程式詳細資料所示)：</span><span class="sxs-lookup"><span data-stu-id="64184-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="64184-123">客戶前往註冊和 (或) 購買應用程式的應用程式註冊 URL：</span><span class="sxs-lookup"><span data-stu-id="64184-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="64184-124">選擇要為您的應用程式列出的最多三個類別 (如需可用的類別，請參閱 Azure Active Directory Marketplace)：</span><span class="sxs-lookup"><span data-stu-id="64184-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="64184-125">附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="64184-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="64184-126">附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="64184-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="64184-127">附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：</span><span class="sxs-lookup"><span data-stu-id="64184-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="64184-128">SAML 整合</span><span class="sxs-lookup"><span data-stu-id="64184-128">SAML Integration</span></span>
<span data-ttu-id="64184-129">使用 [這些指示來新增自訂應用程式](../active-directory-saas-custom-apps.md)，支援 SAML 2.0 的任何應用程式都可直接與 Azure AD 租用戶整合。</span><span class="sxs-lookup"><span data-stu-id="64184-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="64184-130">一旦您測試過應用程式可與 Azure AD 整合後，請將下列資訊傳送至 <mailto:waadpartners@microsoft.com>。</span><span class="sxs-lookup"><span data-stu-id="64184-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="64184-131">提供可由 Azure AD 小組搭配您的應用程式來測試整合的測試租用戶或帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="64184-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="64184-132">提供您的應用程式的 SAML 登入 URL、簽發者 URL (實體 ID) 和回覆 URL (判斷提示取用者服務) 的值，如 [此處](../active-directory-saas-custom-apps.md)所述。</span><span class="sxs-lookup"><span data-stu-id="64184-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="64184-133">如果您通常會提供這些值做為一個 SAML 中繼資料檔的一部分，也請一併傳送該檔案。</span><span class="sxs-lookup"><span data-stu-id="64184-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="64184-134">提供如何在使用 SAML 2.0 的應用程式中設定 Azure AD 做為身分識別提供者的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="64184-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="64184-135">如果您的應用程式支援透過自助系統管理入口網站來設定 Azure AD 做為身分識別提供者，請確認以上提供的認證包含執行這項設定所需的能力。</span><span class="sxs-lookup"><span data-stu-id="64184-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="64184-136">提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="64184-136">Provide the info below:</span></span>

> <span data-ttu-id="64184-137">公司名稱：</span><span class="sxs-lookup"><span data-stu-id="64184-137">Company Name:</span></span>
> 
> <span data-ttu-id="64184-138">公司網站：</span><span class="sxs-lookup"><span data-stu-id="64184-138">Company Website:</span></span>
> 
> <span data-ttu-id="64184-139">應用程式名稱：</span><span class="sxs-lookup"><span data-stu-id="64184-139">Application Name:</span></span>
> 
> <span data-ttu-id="64184-140">應用程式描述 (200 個字元的限制)：</span><span class="sxs-lookup"><span data-stu-id="64184-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="64184-141">應用程式網站 (資訊)：</span><span class="sxs-lookup"><span data-stu-id="64184-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="64184-142">應用程式技術支援網站或連絡資訊：</span><span class="sxs-lookup"><span data-stu-id="64184-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="64184-143">客戶前往註冊和 (或) 購買應用程式的應用程式註冊 URL：</span><span class="sxs-lookup"><span data-stu-id="64184-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="64184-144">選擇要為您的應用程式列出的最多三個類別 (如需可用的類別，請參閱 [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))：</span><span class="sxs-lookup"><span data-stu-id="64184-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="64184-145">附加應用程式小型圖示 (PNG 檔案、45px x 45px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="64184-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="64184-146">附加應用程式大型圖示 (PNG 檔案、215px x 215px、背景純色)：</span><span class="sxs-lookup"><span data-stu-id="64184-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="64184-147">附加應用程式標誌 (PNG 檔案、150px x 122px、透明背景色彩)：</span><span class="sxs-lookup"><span data-stu-id="64184-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

