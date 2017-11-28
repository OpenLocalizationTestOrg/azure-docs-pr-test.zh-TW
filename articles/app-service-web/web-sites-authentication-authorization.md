---
title: "與 Azure 應用程式中的內部部署 Active Directory aaaAuthenticate |Microsoft 文件"
description: "了解如何在 Azure App Service tooauthenticate 與內部部署 Active Directory 中的特定業務應用程式的 hello 不同方式"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a><span data-ttu-id="df9f0-103">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="df9f0-103">Authenticate with on-premises Active Directory in your Azure app</span></span>
<span data-ttu-id="df9f0-104">本文章將示範如何使用 tooauthenticate 內部部署 Active Directory (AD) 中[Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="df9f0-104">This article shows you how tooauthenticate with on-premises Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> <span data-ttu-id="df9f0-105">Azure 應用程式裝載於 hello 雲端，但有方式 tooauthenticate 內部部署 AD 使用者安全地。</span><span class="sxs-lookup"><span data-stu-id="df9f0-105">An Azure app is hosted in hello cloud, but there are ways tooauthenticate on-premises AD users securely.</span></span> 

## <a name="authenticate-through-azure-active-directory"></a><span data-ttu-id="df9f0-106">透過 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="df9f0-106">Authenticate through Azure Active Directory</span></span>
<span data-ttu-id="df9f0-107">Azure Active Directory 租用戶的目錄可與內部部署 AD 進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="df9f0-107">An Azure Active Directory tenant can be directory-synced with an on-premises AD.</span></span> <span data-ttu-id="df9f0-108">這種方法可讓 AD 使用者要能夠存取您的應用程式從 hello 網際網路，並使用其內部部署認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="df9f0-108">This approach enables AD users to access your App from hello internet and authenticate using their on-premises credentials.</span></span> <span data-ttu-id="df9f0-109">此外，Azure App Service 還提供 [適用於此方法的周全解決方案](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="df9f0-109">Furthermore, Azure App Service provides a [turn-key solution for this method](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="df9f0-110">只要按幾下按鈕，您就可以使用 Azure 應用程式的目錄同步租用戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="df9f0-110">With a few clicks of a button, you can enable authentication with a directory-synced tenant for your Azure app.</span></span> <span data-ttu-id="df9f0-111">這個方法有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="df9f0-111">This approach has hello following advantages:</span></span>

* <span data-ttu-id="df9f0-112">應用程式中不需要任何驗證程式碼。</span><span class="sxs-lookup"><span data-stu-id="df9f0-112">Does not require any authentication code in your app.</span></span> <span data-ttu-id="df9f0-113">可讓應用程式服務，請執行 hello 驗證為您和您的時間花在提供應用程式中的功能。</span><span class="sxs-lookup"><span data-stu-id="df9f0-113">Let App Service do hello authentication for you and spend your time on providing functionality in your app.</span></span>
* <span data-ttu-id="df9f0-114">[Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)啟用存取 toodirectory 資料從 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="df9f0-114">[Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) enables access toodirectory data from your Azure app.</span></span>
* <span data-ttu-id="df9f0-115">提供 SSO 太[所有支援的 Azure Active Directory 的應用程式](/marketplace/active-directory/)，包括 Office 365、 Dynamics CRM Online、 Microsoft Intune 和數千個非 Microsoft 的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="df9f0-115">Provides SSO too[all applications supported by Azure Active Directory](/marketplace/active-directory/), including Office 365, Dynamics CRM Online, Microsoft Intune, and thousands of non-Microsoft cloud applications.</span></span> 
* <span data-ttu-id="df9f0-116">Azure Active Directory 支援角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="df9f0-116">Azure Active Directory supports role-based access control.</span></span> <span data-ttu-id="df9f0-117">您可以使用 hello [Authorize(Roles="X")] 模式幾乎不需要變更 tooyour 程式碼。</span><span class="sxs-lookup"><span data-stu-id="df9f0-117">You can use hello [Authorize(Roles="X")] pattern with minimal changes tooyour code.</span></span>

<span data-ttu-id="df9f0-118">如何 toowrite 業務的 Azure 應用程式，向 Azure Active Directory，請參閱的 toosee[建立業務的 Azure 應用程式與 Azure Active Directory 驗證](web-sites-dotnet-lob-application-azure-ad.md)。</span><span class="sxs-lookup"><span data-stu-id="df9f0-118">toosee how toowrite a line-of-business Azure app that authenticates with Azure Active Directory, see [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md).</span></span>

## <a name="authenticate-through-an-on-premises-sts"></a><span data-ttu-id="df9f0-119">透過內部部署 STS 進行驗證</span><span class="sxs-lookup"><span data-stu-id="df9f0-119">Authenticate through an on-premises STS</span></span>
<span data-ttu-id="df9f0-120">如果您有內部部署安全權杖服務 (STS) 像是 Active Directory Federation Services (AD FS)，您可以使用該 toofederate 驗證 Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="df9f0-120">If you have an on-premises secure token service (STS) like Active Directory Federation Services (AD FS), you can use that toofederate authentication for your Azure app.</span></span> <span data-ttu-id="df9f0-121">當公司原則禁止 AD 資料儲存在 Azure 時，這是最合適的方法。</span><span class="sxs-lookup"><span data-stu-id="df9f0-121">This approach is best when company policy prohibits AD data from being stored in Azure.</span></span> <span data-ttu-id="df9f0-122">不過，請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="df9f0-122">However, note hello following:</span></span>

* <span data-ttu-id="df9f0-123">STS 拓撲必須在內部部署，需要成本和管理費用。</span><span class="sxs-lookup"><span data-stu-id="df9f0-123">STS topology must be deployed on-premises, with cost and management overhead.</span></span>
* <span data-ttu-id="df9f0-124">唯一的 AD FS 系統管理員可以設定[信賴憑證者合作對象信任和宣告規則](http://technet.microsoft.com/library/dd807108.aspx)，這可能會限制 hello 開發人員選項。</span><span class="sxs-lookup"><span data-stu-id="df9f0-124">Only AD FS administrators can configure [relying party trusts and claim rules](http://technet.microsoft.com/library/dd807108.aspx), which may limit hello developer's options.</span></span> <span data-ttu-id="df9f0-125">在上 hello 相反地，它是可能 toomanage 及自訂[宣告](http://technet.microsoft.com/library/ee913571.aspx)每個應用程式為基礎。</span><span class="sxs-lookup"><span data-stu-id="df9f0-125">On hello other hand, it is possible toomanage and customize [claims](http://technet.microsoft.com/library/ee913571.aspx) on a per-application basis.</span></span>
* <span data-ttu-id="df9f0-126">Tooon 內部部署存取 AD 資料需要不同的解決方案，透過 hello 公司防火牆。</span><span class="sxs-lookup"><span data-stu-id="df9f0-126">Access tooon-premises AD data requires a separate solution through hello corporate firewall.</span></span>

<span data-ttu-id="df9f0-127">如何 toowrite 業務的 Azure 應用程式，以便驗證與內部部署 STS，請參閱的 toosee[業務的 Azure 應用程式建立與 AD FS 驗證](web-sites-dotnet-lob-application-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="df9f0-127">toosee how toowrite a line-of-business Azure app that authenticates with an on-premises STS, see [Create a line-of-business Azure app with AD FS authentication](web-sites-dotnet-lob-application-adfs.md).</span></span>

