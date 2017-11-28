---
title: "存取 Teams 中的 Azure AD App Proxy 應用程式 | Microsoft Docs"
description: "使用 Azure AD Application Proxy 透過 Microsoft Teams 存取內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 24e22d7314de536714a825cd7035d2cec2112278
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="1805e-103">透過 Microsoft Teams 存取內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="1805e-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="1805e-104">Azure Active Directory Application Proxy 可讓您從任何地方單一登入內部部署應用程式，而 Microsoft Teams 會在一個地方簡化您的共同作業工作。</span><span class="sxs-lookup"><span data-stu-id="1805e-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="1805e-105">將兩者整合在一起，表示使用者可以在任何情況下與其小組成員一起合作。</span><span class="sxs-lookup"><span data-stu-id="1805e-105">Integrating the two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="1805e-106">使用者可以[使用所以標籤](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US)將雲端應用程式新增至其 Teams 通道，但如果他們使用的 SharePoint 網站或規劃工具裝載於內部部署環境，會發生什麼情況？</span><span class="sxs-lookup"><span data-stu-id="1805e-106">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="1805e-107">Application Proxy 是解決方案。</span><span class="sxs-lookup"><span data-stu-id="1805e-107">Application Proxy is the solution.</span></span> <span data-ttu-id="1805e-108">他們可以使用其一直用來從遠端存取應用程式的相同外部 URL，將透過 Application Proxy 發佈的應用程式新增到其通道。</span><span class="sxs-lookup"><span data-stu-id="1805e-108">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span></span> <span data-ttu-id="1805e-109">因為 Application Proxy 會透過 Azure Active Directory 進行驗證，所以可實現相同的單一登入經驗。</span><span class="sxs-lookup"><span data-stu-id="1805e-109">And because Application Proxy authenticates through Azure Active Directory, the same single sign-on experience carries through.</span></span>


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="1805e-110">安裝 Application Proxy 連接器並發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="1805e-110">Install the Application Proxy connector and publish your app</span></span>

<span data-ttu-id="1805e-111">如果您尚未這麼做，請[設定租用戶的 Application Proxy 並安裝連接器](active-directory-application-proxy-enable.md)。</span><span class="sxs-lookup"><span data-stu-id="1805e-111">If you haven't already, [configure Application Proxy for your tenant and install the connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="1805e-112">然後，[發佈內部部署應用程式](application-proxy-publish-azure-portal.md)以供遠端存取。</span><span class="sxs-lookup"><span data-stu-id="1805e-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="1805e-113">當您要發佈應用程式時，請記下外部 URL，因為終端使用者將應用程式新增至 Teams 時需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="1805e-113">When you're publishing the app, make note of the external URL because your end users need that information when they add the app to Teams.</span></span>

<span data-ttu-id="1805e-114">如果您已經發佈應用程式，但不記得其外部 URL，請在 [Azure 入口網站](https://portal.azure.com)中查閱。</span><span class="sxs-lookup"><span data-stu-id="1805e-114">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1805e-115">登入，然後瀏覽至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] > 選取您的應用程式 > [Application Proxy]。</span><span class="sxs-lookup"><span data-stu-id="1805e-115">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-to-teams"></a><span data-ttu-id="1805e-116">將應用程式新增至 Teams</span><span class="sxs-lookup"><span data-stu-id="1805e-116">Add your app to Teams</span></span>

<span data-ttu-id="1805e-117">一旦透過 Application Proxy 發佈應用程式，請讓使用者知道，他們可以在其 Teams 通道中直接將該應用程式新增為一個索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1805e-117">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="1805e-118">請他們遵循下列三個步驟：</span><span class="sxs-lookup"><span data-stu-id="1805e-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="1805e-119">瀏覽至您要新增此應用程式的 Teams 通道，，然後選取 **+** 來新增索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1805e-119">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span></span>

   ![選取 [新增索引標籤]](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="1805e-121">從索引標籤選項中選取 [網站]。</span><span class="sxs-lookup"><span data-stu-id="1805e-121">Select **Website** from the tab options.</span></span>

   ![新增網站](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="1805e-123">指定索引標籤的名稱，並將 URL 設定為 Application Proxy 外部 URL。</span><span class="sxs-lookup"><span data-stu-id="1805e-123">Give the tab a name and set the URL to the Application Proxy external URL.</span></span> 

   ![設定索引標籤名稱和 URL](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="1805e-125">一旦有小組成員新增索引標籤，該索引標籤就會對通道中的每個人顯示。</span><span class="sxs-lookup"><span data-stu-id="1805e-125">Once one member of a team adds the tab, it shows up for everyone in the channel.</span></span> <span data-ttu-id="1805e-126">任何具有此應用程式存取權的使用者均可透過其用於 Microsoft Teams 的認證來取得單一登入存取。</span><span class="sxs-lookup"><span data-stu-id="1805e-126">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="1805e-127">任何不具此應用程式存取權的使用者會在 Teams 中看到此索引標籤，但是在您提供內部部署應用程式和應用程式之 Azure 入口網站發佈版本的權限以前，都會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="1805e-127">Any users who don't have access to the app will see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1805e-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1805e-128">Next steps</span></span>

- <span data-ttu-id="1805e-129">了解如何透過 Application Proxy [發佈內部部署 SharePoint 網站](application-proxy-enable-remote-access-sharepoint.md)。</span><span class="sxs-lookup"><span data-stu-id="1805e-129">Learn how to [publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="1805e-130">將您的應用程式設定為將[自訂網域](active-directory-application-proxy-custom-domains.md)用於其外部 URL。</span><span class="sxs-lookup"><span data-stu-id="1805e-130">Configure your apps to use [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
