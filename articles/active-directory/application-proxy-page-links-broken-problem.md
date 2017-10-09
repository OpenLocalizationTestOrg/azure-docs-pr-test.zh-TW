---
title: "在 hello 頁面上的 aaaLinks 不適用於應用程式 Proxy 應用程式 |Microsoft 文件"
description: "如何 tootroubleshoot 問題上您有與 Azure AD 整合的應用程式 Proxy 應用程式中斷連結"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a><span data-ttu-id="13283-103">在 hello 頁面上的連結無法運作的應用程式 Proxy 應用程式</span><span class="sxs-lookup"><span data-stu-id="13283-103">Links on hello page don't work for an Application Proxy application</span></span>

<span data-ttu-id="13283-104">本文將協助您 tootroubleshoot 為什麼您的 Azure Active Directory 應用程式 Proxy 應用程式的連結無法正確運作。</span><span class="sxs-lookup"><span data-stu-id="13283-104">This article help you tootroubleshoot why links on your Azure Active Directory Application Proxy application don't work correctly.</span></span>

## <a name="overview"></a><span data-ttu-id="13283-105">概觀</span><span class="sxs-lookup"><span data-stu-id="13283-105">Overview</span></span> 
<span data-ttu-id="13283-106">之後發行的應用程式 Proxy 應用程式，工作預設會在 hello 應用程式會包含在 hello 連結 toodestinations hello 只將連結發佈根 URL。</span><span class="sxs-lookup"><span data-stu-id="13283-106">After publishing an Application Proxy app, hello only links that work by default in hello application are links toodestinations contained within hello published root URL.</span></span> <span data-ttu-id="13283-107">hello 應用程式中的 hello 連結並非正在運作，hello hello 應用程式內部 URL 可能不包含所有 hello 目的地 hello 應用程式內的連結。</span><span class="sxs-lookup"><span data-stu-id="13283-107">hello links within hello applications aren’t working, hello internal URL for hello application probably does not include all hello destinations of links within hello application.</span></span>

<span data-ttu-id="13283-108">**為何這有關係？**</span><span class="sxs-lookup"><span data-stu-id="13283-108">**Why does this happen?**</span></span> <span data-ttu-id="13283-109">當按下應用程式中的連結，以做為其中一個內部 URL，在應用程式 Proxy 會嘗試 tooresolve hello URL hello 相同應用程式，或以做為外部使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="13283-109">When clicking a link in an application, Application Proxy tries tooresolve hello URL as either an internal URL within hello same application, or as an externally available URL.</span></span> <span data-ttu-id="13283-110">如果 hello 連結指向不在 tooan 內部 URL hello 相同應用程式中，不屬於 tooeither 的這些值區，導致找不到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="13283-110">If hello link points tooan internal URL that is not within hello same application, it does not belong tooeither of these buckets and result in a not found error.</span></span>

## <a name="ways-you-can-resolve-broken-links"></a><span data-ttu-id="13283-111">中斷連結的解決方式</span><span class="sxs-lookup"><span data-stu-id="13283-111">Ways you can resolve broken links</span></span>

<span data-ttu-id="13283-112">有三種方式 tooresolve 此問題。</span><span class="sxs-lookup"><span data-stu-id="13283-112">There are three ways tooresolve this issue.</span></span> <span data-ttu-id="13283-113">hello 以下幾個選擇是列在增加的複雜性。</span><span class="sxs-lookup"><span data-stu-id="13283-113">hello choices below are in listed in increasing complexity.</span></span>

1.  <span data-ttu-id="13283-114">請確定 hello 內部 URL 是包含所有 hello 相關連結 hello 應用程式的根目錄。</span><span class="sxs-lookup"><span data-stu-id="13283-114">Make sure hello internal URL is a root that contains all hello relevant links for hello application.</span></span> <span data-ttu-id="13283-115">這可讓所有連結 toobe 解析為發佈的內容內 hello 相同應用程式。</span><span class="sxs-lookup"><span data-stu-id="13283-115">This allows all links toobe resolved as content published within hello same application.</span></span>

    <span data-ttu-id="13283-116">如果您變更 hello 內部 URL，但不想 toochange hello 登陸頁面的使用者，變更 hello 首頁 URL toohello 先前發行的內部 URL。</span><span class="sxs-lookup"><span data-stu-id="13283-116">If you change hello internal URL but don’t want toochange hello landing page for users, change hello Home page URL toohello previously published internal URL.</span></span> <span data-ttu-id="13283-117">作法是前往太"Azure Active Directory-"&gt;應用程式註冊-&gt;選取 hello 應用程式-&gt;屬性。</span><span class="sxs-lookup"><span data-stu-id="13283-117">This can be done by going too“Azure Active Directory” -&gt; App Registrations -&gt; select hello application -&gt; Properties.</span></span> <span data-ttu-id="13283-118">在這個內容索引標籤中，您會看到 hello 欄位 「 首頁 URL 」，您可以調整 toobe hello 預期登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="13283-118">In this properties tab, you see hello field “Home Page URL” which you can adjust toobe hello desired landing page.</span></span>

2.  <span data-ttu-id="13283-119">如果您的應用程式使用完整的網域名稱 (Fqdn)，使用[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)toopublish 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13283-119">If your applications use fully qualified domain names (FQDNs), use [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish your applications.</span></span> <span data-ttu-id="13283-120">這項功能可讓您同時在內部使用，相同的 URL toobe 和外部的 hello。</span><span class="sxs-lookup"><span data-stu-id="13283-120">This feature allows hello same URL toobe used both internally and externally.</span></span>

    <span data-ttu-id="13283-121">此選項可確保您的應用程式中的 hello 連結是透過應用程式 Proxy 可外部存取，因為 hello 應用程式 toointernal Url 中的 hello 連結也會辨識外部。</span><span class="sxs-lookup"><span data-stu-id="13283-121">This option ensures that hello links in your application are externally accessible through Application Proxy since hello links within hello application toointernal URLs are also recognized externally.</span></span> <span data-ttu-id="13283-122">請注意，所有的連結仍然需要 toobelong tooa 發行應用程式。</span><span class="sxs-lookup"><span data-stu-id="13283-122">Note that all links still need toobelong tooa published application.</span></span> <span data-ttu-id="13283-123">不過，使用此選項 hello 連結不需要 toobelong toohello 相同的應用程式，而且可以隸屬 toomultiple 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13283-123">However, with this option hello links do not need toobelong toohello same application and can belong toomultiple applications.</span></span>

3.  <span data-ttu-id="13283-124">如果這些選項都不可行時，您將執行 URL 轉譯/重寫的新功能的 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="13283-124">If neither of these options are feasible, you join hello preview for a new feature that do URL translation/rewriting.</span></span> <span data-ttu-id="13283-125">使用此選項時，內部 Url 或 hello HTML 主體的應用程式中存在的連結會轉譯，或 「 對應 」，toohello 發佈外部應用程式 Proxy Url。</span><span class="sxs-lookup"><span data-stu-id="13283-125">With this option, internal URLs or links that exist in hello HTML body of your applications be translated, or “mapped”, toohello published external App Proxy URLs.</span></span> <span data-ttu-id="13283-126">這只適用於 hello HTML 或 CSS 中的連結，這無法協助如果透過 JS 產生您的連結。</span><span class="sxs-lookup"><span data-stu-id="13283-126">This only works for links in hello HTML or CSS, and this not help if your link is generated through JS.</span></span> 

<span data-ttu-id="13283-127">如此一來，我們強烈建議使用 hello[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)盡可能方案。</span><span class="sxs-lookup"><span data-stu-id="13283-127">As a result, we strongly recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution if possible.</span></span> <span data-ttu-id="13283-128">如果您想 toojoin hello 預覽，電子郵件傳送< aadapfeedback@microsoft.com >與 hello applicationId(s)。</span><span class="sxs-lookup"><span data-stu-id="13283-128">If you do want toojoin hello preview, email <aadapfeedback@microsoft.com> with hello applicationId(s).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13283-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13283-129">Next steps</span></span>
[<span data-ttu-id="13283-130">使用現有的內部部署 Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="13283-130">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)

