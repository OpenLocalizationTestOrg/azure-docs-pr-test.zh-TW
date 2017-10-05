---
title: "在 Azure 應用程式中使用內部部署 Active Directory 進行驗證 | Microsoft Docs"
description: "了解 Azure App Service 中可使用內部部署 Active Directory 來進行驗證的企業營運應用程式的不同選項"
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
ms.openlocfilehash: a68bcd7040498515a6e35a87ee6e6940a84506d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a><span data-ttu-id="80939-103">在 Azure 應用程式中使用內部部署 Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="80939-103">Authenticate with on-premises Active Directory in your Azure app</span></span>
<span data-ttu-id="80939-104">本文說明如何在 [Azure App Service](../app-service/app-service-value-prop-what-is.md)中使用內部部署 Active Directory (AD) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="80939-104">This article shows you how to authenticate with on-premises Active Directory (AD) in [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> <span data-ttu-id="80939-105">雖然 Azure 應用程式裝載於雲端，但仍有方式可安全地驗證內部部署 AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="80939-105">An Azure app is hosted in the cloud, but there are ways to authenticate on-premises AD users securely.</span></span> 

## <a name="authenticate-through-azure-active-directory"></a><span data-ttu-id="80939-106">透過 Azure Active Directory 進行驗證</span><span class="sxs-lookup"><span data-stu-id="80939-106">Authenticate through Azure Active Directory</span></span>
<span data-ttu-id="80939-107">Azure Active Directory 租用戶的目錄可與內部部署 AD 進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="80939-107">An Azure Active Directory tenant can be directory-synced with an on-premises AD.</span></span> <span data-ttu-id="80939-108">這個方法可讓 AD 使用者從網際網路存取應用程式，並使用其內部部署認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="80939-108">This approach enables AD users to access your App from the internet and authenticate using their on-premises credentials.</span></span> <span data-ttu-id="80939-109">此外，Azure App Service 還提供 [適用於此方法的周全解決方案](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="80939-109">Furthermore, Azure App Service provides a [turn-key solution for this method](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="80939-110">只要按幾下按鈕，您就可以使用 Azure 應用程式的目錄同步租用戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="80939-110">With a few clicks of a button, you can enable authentication with a directory-synced tenant for your Azure app.</span></span> <span data-ttu-id="80939-111">此方法具有下列優點：</span><span class="sxs-lookup"><span data-stu-id="80939-111">This approach has the following advantages:</span></span>

* <span data-ttu-id="80939-112">應用程式中不需要任何驗證程式碼。</span><span class="sxs-lookup"><span data-stu-id="80939-112">Does not require any authentication code in your app.</span></span> <span data-ttu-id="80939-113">可讓 App Service 為您進行驗證，把省下的時間花在提供應用程式的功能。</span><span class="sxs-lookup"><span data-stu-id="80939-113">Let App Service do the authentication for you and spend your time on providing functionality in your app.</span></span>
* <span data-ttu-id="80939-114">[Azure AD 圖形 API](http://msdn.microsoft.com/library/azure/hh974476.aspx) 可從 Azure 應用程式存取目錄資料。</span><span class="sxs-lookup"><span data-stu-id="80939-114">[Azure AD Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx) enables access to directory data from your Azure app.</span></span>
* <span data-ttu-id="80939-115">為 [Azure Active Directory 支援的所有應用程式](/marketplace/active-directory/)(包括 Office 365、Dynamics CRM Online、Microsoft InTune 及數千種非 Microsoft 的雲端應用程式) 提供 SSO。</span><span class="sxs-lookup"><span data-stu-id="80939-115">Provides SSO to [all applications supported by Azure Active Directory](/marketplace/active-directory/), including Office 365, Dynamics CRM Online, Microsoft Intune, and thousands of non-Microsoft cloud applications.</span></span> 
* <span data-ttu-id="80939-116">Azure Active Directory 支援角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="80939-116">Azure Active Directory supports role-based access control.</span></span> <span data-ttu-id="80939-117">您可以使用 [Authorize(Roles="X")] 模式，而且只需要對程式碼進行最少量的變更。</span><span class="sxs-lookup"><span data-stu-id="80939-117">You can use the [Authorize(Roles="X")] pattern with minimal changes to your code.</span></span>

<span data-ttu-id="80939-118">若要了解如何撰寫使用 Azure Active Directory 進行驗證的企業營運 Azure 應用程式，請參閱 [使用 Azure Active Directory 驗證建立企業營運 Azure 應用程式](web-sites-dotnet-lob-application-azure-ad.md)。</span><span class="sxs-lookup"><span data-stu-id="80939-118">To see how to write a line-of-business Azure app that authenticates with Azure Active Directory, see [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md).</span></span>

## <a name="authenticate-through-an-on-premises-sts"></a><span data-ttu-id="80939-119">透過內部部署 STS 進行驗證</span><span class="sxs-lookup"><span data-stu-id="80939-119">Authenticate through an on-premises STS</span></span>
<span data-ttu-id="80939-120">如果您有內部部署的安全權杖服務 (STS) (例如 Active Directory Federation Services (AD FS))，您可以使用該服務同盟 Azure 應用程式的驗證。</span><span class="sxs-lookup"><span data-stu-id="80939-120">If you have an on-premises secure token service (STS) like Active Directory Federation Services (AD FS), you can use that to federate authentication for your Azure app.</span></span> <span data-ttu-id="80939-121">當公司原則禁止 AD 資料儲存在 Azure 時，這是最合適的方法。</span><span class="sxs-lookup"><span data-stu-id="80939-121">This approach is best when company policy prohibits AD data from being stored in Azure.</span></span> <span data-ttu-id="80939-122">不過，請注意下列事項︰</span><span class="sxs-lookup"><span data-stu-id="80939-122">However, note the following:</span></span>

* <span data-ttu-id="80939-123">STS 拓撲必須在內部部署，需要成本和管理費用。</span><span class="sxs-lookup"><span data-stu-id="80939-123">STS topology must be deployed on-premises, with cost and management overhead.</span></span>
* <span data-ttu-id="80939-124">只有 AD FS 系統管理員可設定 [信賴憑證者信任和宣告規則](http://technet.microsoft.com/library/dd807108.aspx)，這可能會限制開發人員的選項。</span><span class="sxs-lookup"><span data-stu-id="80939-124">Only AD FS administrators can configure [relying party trusts and claim rules](http://technet.microsoft.com/library/dd807108.aspx), which may limit the developer's options.</span></span> <span data-ttu-id="80939-125">但另一方面，這可以依每一應用程式來管理及自訂 [宣告](http://technet.microsoft.com/library/ee913571.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="80939-125">On the other hand, it is possible to manage and customize [claims](http://technet.microsoft.com/library/ee913571.aspx) on a per-application basis.</span></span>
* <span data-ttu-id="80939-126">想要存取內部部署 AD 資料就必須有可以穿越公司防火牆的個別解決方案。</span><span class="sxs-lookup"><span data-stu-id="80939-126">Access to on-premises AD data requires a separate solution through the corporate firewall.</span></span>

<span data-ttu-id="80939-127">若要了解如何撰寫使用內部部署 STS 進行驗證的企業營運 Azure 應用程式，請參閱 [使用 AD FS 驗證建立企業營運 Azure 應用程式](web-sites-dotnet-lob-application-adfs.md)。</span><span class="sxs-lookup"><span data-stu-id="80939-127">To see how to write a line-of-business Azure app that authenticates with an on-premises STS, see [Create a line-of-business Azure app with AD FS authentication](web-sites-dotnet-lob-application-adfs.md).</span></span>

