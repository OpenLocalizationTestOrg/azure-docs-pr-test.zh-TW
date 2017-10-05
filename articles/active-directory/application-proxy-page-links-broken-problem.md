---
title: "頁面上的連結對 Application Proxy 應用程式沒有作用 | Microsoft Docs"
description: "如何為已與 Azure AD 整合之 Application Proxy 應用程式上的中斷連結問題疑難排解"
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
ms.openlocfilehash: 83c4261fab0498541591c01f9bb692b396c7b751
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="links-on-the-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="cf301-103">頁面上的連結對 Application Proxy 應用程式沒有作用</span><span class="sxs-lookup"><span data-stu-id="cf301-103">Links on the page don't work for an Application Proxy application</span></span>

<span data-ttu-id="cf301-104">這篇文章可協助您為 Azure Active Directory Application Proxy 應用程式上的連結無法正常運作疑難排解。</span><span class="sxs-lookup"><span data-stu-id="cf301-104">This article help you to troubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="cf301-105">概觀</span><span class="sxs-lookup"><span data-stu-id="cf301-105">Overview</span></span> 
<span data-ttu-id="cf301-106">發佈 Application Proxy 應用程式後，只有預設在該應用程式中運作的連結才是已發佈根目錄 URL 內所包含目的地的連結。</span><span class="sxs-lookup"><span data-stu-id="cf301-106">After publishing an Application Proxy app, the only links that work by default in the application are links to destinations contained within the published root URL.</span></span> <span data-ttu-id="cf301-107">該應用程式內的連結未運作，應用程式的內部 URL 或許未包含應用程式內連結的所有目的地。</span><span class="sxs-lookup"><span data-stu-id="cf301-107">The links within the applications aren’t working, the internal URL for the application probably does not include all the destinations of links within the application.</span></span>

<span data-ttu-id="cf301-108">**為何這有關係？**</span><span class="sxs-lookup"><span data-stu-id="cf301-108">**Why does this happen?**</span></span> <span data-ttu-id="cf301-109">當按一下應用程式中的連結時，Application Proxy 會嘗試將 URL 解析為相同應用程式內的內部 URL，或解析為外部可用的 URL。</span><span class="sxs-lookup"><span data-stu-id="cf301-109">When clicking a link in an application, Application Proxy tries to resolve the URL as either an internal URL within the same application, or as an externally available URL.</span></span> <span data-ttu-id="cf301-110">如果連結指向的內部 URL 不在相同應用程式內，則該連結不屬於這些貯體，並會造成此找不到錯誤。</span><span class="sxs-lookup"><span data-stu-id="cf301-110">If the link points to an internal URL that is not within the same application, it does not belong to either of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="cf301-111">中斷連結的解決方式</span><span class="sxs-lookup"><span data-stu-id="cf301-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="cf301-112">有三種方法可以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="cf301-112">There are three ways to resolve this issue.</span></span> <span data-ttu-id="cf301-113">以下依複雜度遞增方式列出解決方法。</span><span class="sxs-lookup"><span data-stu-id="cf301-113">The choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="cf301-114">請確定內部 URL 是包含該應用程式所有相關連結的根目錄。</span><span class="sxs-lookup"><span data-stu-id="cf301-114">Make sure the internal URL is a root that contains all the relevant links for the application.</span></span> <span data-ttu-id="cf301-115">這可讓所有的連結解析為在相同應用程式內發佈的內容。</span><span class="sxs-lookup"><span data-stu-id="cf301-115">This allows all links to be resolved as content published within the same application.</span></span>

    <span data-ttu-id="cf301-116">如果您變更內部 URL，但不想要變更使用者的登陸頁面，請將首頁 URL 變更為先前發佈的內部 URL。</span><span class="sxs-lookup"><span data-stu-id="cf301-116">If you change the internal URL but don’t want to change the landing page for users, change the Home page URL to the previously published internal URL.</span></span> <span data-ttu-id="cf301-117">這可透過執行 [Azure Active Directory] -&gt; [應用程式登錄] -&gt; 選取該應用程式 -&gt; [屬性] 完成。</span><span class="sxs-lookup"><span data-stu-id="cf301-117">This can be done by going to “Azure Active Directory” -&gt; App Registrations -&gt; select the application -&gt; Properties.</span></span> <span data-ttu-id="cf301-118">在此屬性索引標籤中會看到 [首頁 URL] 欄位，您可將此欄位調整至所需的登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="cf301-118">In this properties tab, you see the field “Home Page URL” which you can adjust to be the desired landing page.</span></span>

2.  <span data-ttu-id="cf301-119">如果您的應用程式使用完整的網域名稱 (FQDN)，請使用[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)發佈您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf301-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) to publish your applications.</span></span> <span data-ttu-id="cf301-120">這項功能可讓內部與外部使用相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="cf301-120">This feature allows the same URL to be used both internally and externally.</span></span>

    <span data-ttu-id="cf301-121">此選項可確保外部可透過 Application Proxy 存取您應用程式中的連結，因為外部也能辨識應用程式內對內部 URL 的連結。</span><span class="sxs-lookup"><span data-stu-id="cf301-121">This option ensures that the links in your application are externally accessible through Application Proxy since the links within the application to internal URLs are also recognized externally.</span></span> <span data-ttu-id="cf301-122">請注意，所有的連結仍然必須屬於已發佈的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf301-122">Note that all links still need to belong to a published application.</span></span> <span data-ttu-id="cf301-123">不過有了此選項，連結不必屬於相同應用程式，而且可以屬於多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf301-123">However, with this option the links do not need to belong to the same application and can belong to multiple applications.</span></span>

3.  <span data-ttu-id="cf301-124">如果這些選項皆不可行，您可以加入執行轉譯/重新撰寫 URL 的新功能預覽。</span><span class="sxs-lookup"><span data-stu-id="cf301-124">If neither of these options are feasible, you join the preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="cf301-125">透過此選項，存在於您應用程式 HTML 內文中的內部 URL 或連結會被轉譯或「對應」至已發佈的外部 App Proxy URL。</span><span class="sxs-lookup"><span data-stu-id="cf301-125">With this option, internal URLs or links that exist in the HTML body of your applications be translated, or “mapped”, to the published external App Proxy URLs.</span></span> <span data-ttu-id="cf301-126">此選項僅適用於 HTML 語法或 CSS 中的連結，如果您的連結是透過 JS 產生，則沒有幫助。</span><span class="sxs-lookup"><span data-stu-id="cf301-126">This only works for links in the HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="cf301-127">因此，我們強烈建議使用[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)解決方案 (若適用的話)。</span><span class="sxs-lookup"><span data-stu-id="cf301-127">As a result, we strongly recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="cf301-128">如果您想要加入預覽，請將含 applicationId 的電子郵件傳送至 <aadapfeedback@microsoft.com>。</span><span class="sxs-lookup"><span data-stu-id="cf301-128">If you do want to join the preview, email <aadapfeedback@microsoft.com> with the applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf301-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf301-129">Next steps</span></span>
[<span data-ttu-id="cf301-130">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="cf301-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

