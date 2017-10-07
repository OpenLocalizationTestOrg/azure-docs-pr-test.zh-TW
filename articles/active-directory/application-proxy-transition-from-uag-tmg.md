---
title: "aaaUpgrade tooAzure AD 應用程式 Proxy |Microsoft 文件"
description: "如果您是從 Microsoft Forefront 或 Unified Access Gateway 升級，選擇哪一個 Proxy 解決方案最適合。"
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
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a><span data-ttu-id="2449b-103">比較遠端存取解決方案</span><span class="sxs-lookup"><span data-stu-id="2449b-103">Compare remote access solutions</span></span>

<span data-ttu-id="2449b-104">Azure Active Directory 應用程式 Proxy 是 Microsoft 提供的兩個遠端存取解決方案其中之一。</span><span class="sxs-lookup"><span data-stu-id="2449b-104">Azure Active Directory Application Proxy is one of two remote access solutions that Microsoft offers.</span></span> <span data-ttu-id="2449b-105">其他 hello 是 Web 應用程式 Proxy，hello 在內部部署版本。</span><span class="sxs-lookup"><span data-stu-id="2449b-105">hello other is Web Application Proxy, hello on-premises version.</span></span> <span data-ttu-id="2449b-106">這兩種解決方案取代 Microsoft 提供的舊版產品：Microsoft Forefront Threat Management Gateway (TMG) 和 Unified Access Gateway (UAG)。</span><span class="sxs-lookup"><span data-stu-id="2449b-106">These two solutions replace earlier products that Microsoft offered: Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG).</span></span> <span data-ttu-id="2449b-107">使用此發行項 toounderstand 這些四個解決方案比較 tooeach 其他的方式。</span><span class="sxs-lookup"><span data-stu-id="2449b-107">Use this article toounderstand how these four solutions compare tooeach other.</span></span> <span data-ttu-id="2449b-108">您仍在使用 hello 取代 TMG 或 UAG 解決方案，請使用這個發行項 toohelp 計劃您的移轉 tooone 的 hello 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="2449b-108">For those of you still using hello deprecated TMG or UAG solutions, use this article toohelp plan your migration tooone of hello Application Proxy.</span></span> 


## <a name="feature-comparison"></a><span data-ttu-id="2449b-109">功能比較</span><span class="sxs-lookup"><span data-stu-id="2449b-109">Feature comparison</span></span>

<span data-ttu-id="2449b-110">使用此資料表 toounderstand Threat Management Gateway (TMG)、 統一存取閘道 (UAG)、 Web 應用程式 Proxy (WAP) 和 Azure AD 應用程式 Proxy (AP) 比較 tooeach 其他。</span><span class="sxs-lookup"><span data-stu-id="2449b-110">Use this table toounderstand how Threat Management Gateway (TMG), Unified Access Gateway (UAG), Web Application Proxy (WAP), and Azure AD Application Proxy (AP) compare tooeach other.</span></span>

| <span data-ttu-id="2449b-111">功能</span><span class="sxs-lookup"><span data-stu-id="2449b-111">Feature</span></span> | <span data-ttu-id="2449b-112">TMG</span><span class="sxs-lookup"><span data-stu-id="2449b-112">TMG</span></span> | <span data-ttu-id="2449b-113">UAG</span><span class="sxs-lookup"><span data-stu-id="2449b-113">UAG</span></span> | <span data-ttu-id="2449b-114">WAP</span><span class="sxs-lookup"><span data-stu-id="2449b-114">WAP</span></span> | <span data-ttu-id="2449b-115">AP</span><span class="sxs-lookup"><span data-stu-id="2449b-115">AP</span></span> |
| ------- | --- | --- | --- | --- |
| <span data-ttu-id="2449b-116">憑證驗證</span><span class="sxs-lookup"><span data-stu-id="2449b-116">Certificate authentication</span></span> | <span data-ttu-id="2449b-117">是</span><span class="sxs-lookup"><span data-stu-id="2449b-117">Yes</span></span> | <span data-ttu-id="2449b-118">是</span><span class="sxs-lookup"><span data-stu-id="2449b-118">Yes</span></span> | - | - |
| <span data-ttu-id="2449b-119">選擇性地發佈瀏覽器應用程式</span><span class="sxs-lookup"><span data-stu-id="2449b-119">Selectively publish browser apps</span></span> | <span data-ttu-id="2449b-120">是</span><span class="sxs-lookup"><span data-stu-id="2449b-120">Yes</span></span> | <span data-ttu-id="2449b-121">是</span><span class="sxs-lookup"><span data-stu-id="2449b-121">Yes</span></span> | <span data-ttu-id="2449b-122">是</span><span class="sxs-lookup"><span data-stu-id="2449b-122">Yes</span></span> | <span data-ttu-id="2449b-123">是</span><span class="sxs-lookup"><span data-stu-id="2449b-123">Yes</span></span> |
| <span data-ttu-id="2449b-124">預先驗證和單一登入</span><span class="sxs-lookup"><span data-stu-id="2449b-124">Preauthentication and single sign-on</span></span> | <span data-ttu-id="2449b-125">是</span><span class="sxs-lookup"><span data-stu-id="2449b-125">Yes</span></span> | <span data-ttu-id="2449b-126">是</span><span class="sxs-lookup"><span data-stu-id="2449b-126">Yes</span></span> | <span data-ttu-id="2449b-127">是</span><span class="sxs-lookup"><span data-stu-id="2449b-127">Yes</span></span> | <span data-ttu-id="2449b-128">是</span><span class="sxs-lookup"><span data-stu-id="2449b-128">Yes</span></span> | 
| <span data-ttu-id="2449b-129">第 2 層/第 3 層防火牆</span><span class="sxs-lookup"><span data-stu-id="2449b-129">Layer 2/3 firewall</span></span> | <span data-ttu-id="2449b-130">是</span><span class="sxs-lookup"><span data-stu-id="2449b-130">Yes</span></span> | <span data-ttu-id="2449b-131">是</span><span class="sxs-lookup"><span data-stu-id="2449b-131">Yes</span></span> | - | - |
| <span data-ttu-id="2449b-132">轉接 Proxy 功能</span><span class="sxs-lookup"><span data-stu-id="2449b-132">Forward proxy capabilities</span></span> | <span data-ttu-id="2449b-133">是</span><span class="sxs-lookup"><span data-stu-id="2449b-133">Yes</span></span> | - | - | - |
| <span data-ttu-id="2449b-134">VPN 功能</span><span class="sxs-lookup"><span data-stu-id="2449b-134">VPN capabilities</span></span> | <span data-ttu-id="2449b-135">是</span><span class="sxs-lookup"><span data-stu-id="2449b-135">Yes</span></span> | <span data-ttu-id="2449b-136">是</span><span class="sxs-lookup"><span data-stu-id="2449b-136">Yes</span></span> | - | - |
| <span data-ttu-id="2449b-137">豐富通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="2449b-137">Rich protocol support</span></span> | - | <span data-ttu-id="2449b-138">是</span><span class="sxs-lookup"><span data-stu-id="2449b-138">Yes</span></span> | <span data-ttu-id="2449b-139">是，如果是透過 HTTP 執行</span><span class="sxs-lookup"><span data-stu-id="2449b-139">Yes, if running over HTTP</span></span> | <span data-ttu-id="2449b-140">是，如果是透過 HTTP 或透過遠端桌面閘道執行</span><span class="sxs-lookup"><span data-stu-id="2449b-140">Yes, if running over HTTP or through Remote Desktop Gateway</span></span> |
| <span data-ttu-id="2449b-141">作為 ADFS Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="2449b-141">Serves as ADFS proxy server</span></span> | - | <span data-ttu-id="2449b-142">是</span><span class="sxs-lookup"><span data-stu-id="2449b-142">Yes</span></span> | <span data-ttu-id="2449b-143">是</span><span class="sxs-lookup"><span data-stu-id="2449b-143">Yes</span></span> | - |
| <span data-ttu-id="2449b-144">應用程式存取的單一入口網站</span><span class="sxs-lookup"><span data-stu-id="2449b-144">One portal for application access</span></span> | - | <span data-ttu-id="2449b-145">是</span><span class="sxs-lookup"><span data-stu-id="2449b-145">Yes</span></span> | - | <span data-ttu-id="2449b-146">是</span><span class="sxs-lookup"><span data-stu-id="2449b-146">Yes</span></span> |
| <span data-ttu-id="2449b-147">回應內文連結轉譯</span><span class="sxs-lookup"><span data-stu-id="2449b-147">Response body link translation</span></span> | <span data-ttu-id="2449b-148">是</span><span class="sxs-lookup"><span data-stu-id="2449b-148">Yes</span></span> | <span data-ttu-id="2449b-149">是</span><span class="sxs-lookup"><span data-stu-id="2449b-149">Yes</span></span> | - | <span data-ttu-id="2449b-150">是</span><span class="sxs-lookup"><span data-stu-id="2449b-150">Yes</span></span> | 
| <span data-ttu-id="2449b-151">使用標頭進行驗證</span><span class="sxs-lookup"><span data-stu-id="2449b-151">Authentication with headers</span></span> | - | <span data-ttu-id="2449b-152">是</span><span class="sxs-lookup"><span data-stu-id="2449b-152">Yes</span></span> | - | <span data-ttu-id="2449b-153">是，使用 PingAccess</span><span class="sxs-lookup"><span data-stu-id="2449b-153">Yes, with PingAccess</span></span> | 
| <span data-ttu-id="2449b-154">雲端級別安全性</span><span class="sxs-lookup"><span data-stu-id="2449b-154">Cloud-scale security</span></span> | - | - | - | <span data-ttu-id="2449b-155">是</span><span class="sxs-lookup"><span data-stu-id="2449b-155">Yes</span></span> | 
| <span data-ttu-id="2449b-156">條件式存取</span><span class="sxs-lookup"><span data-stu-id="2449b-156">Conditional access</span></span> | - | <span data-ttu-id="2449b-157">是</span><span class="sxs-lookup"><span data-stu-id="2449b-157">Yes</span></span> | - | <span data-ttu-id="2449b-158">是</span><span class="sxs-lookup"><span data-stu-id="2449b-158">Yes</span></span> |
| <span data-ttu-id="2449b-159">Hello 非軍事區域 (DMZ) 中沒有任何元件</span><span class="sxs-lookup"><span data-stu-id="2449b-159">No components in hello demilitarized zone (DMZ)</span></span> | - | - | - | <span data-ttu-id="2449b-160">是</span><span class="sxs-lookup"><span data-stu-id="2449b-160">Yes</span></span> |
| <span data-ttu-id="2449b-161">沒有輸入連線</span><span class="sxs-lookup"><span data-stu-id="2449b-161">No inbound connections</span></span> | - | - | - | <span data-ttu-id="2449b-162">是</span><span class="sxs-lookup"><span data-stu-id="2449b-162">Yes</span></span> |

<span data-ttu-id="2449b-163">大部分情況下，我們建議 Azure AD 應用程式，做為 hello 現代解決方案。</span><span class="sxs-lookup"><span data-stu-id="2449b-163">For most scenarios, we recommend Azure AD Application as hello modern solution.</span></span> <span data-ttu-id="2449b-164">Web 應用程式 Proxy 只建議用在需要 AD FS Proxy 伺服器的情節中，而且您無法使用 Azure Active Directory 中的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="2449b-164">Web Application Proxy is only preferred in scenarios that require a proxy server for AD FS, and you can't use custom domains in Azure Active Directory.</span></span> 

<span data-ttu-id="2449b-165">Azure AD 應用程式 Proxy 提供唯一優勢在於，當比較 toosimilar 產品，包括：</span><span class="sxs-lookup"><span data-stu-id="2449b-165">Azure AD Application Proxy offers unique benefits when compared toosimilar products, including:</span></span>

- <span data-ttu-id="2449b-166">擴充 Azure AD tooon 內部部署資源</span><span class="sxs-lookup"><span data-stu-id="2449b-166">Extending Azure AD tooon-premises resources</span></span>
   - <span data-ttu-id="2449b-167">雲端級別安全性和保護</span><span class="sxs-lookup"><span data-stu-id="2449b-167">Cloud-scale security and protection</span></span>
   - <span data-ttu-id="2449b-168">條件式存取和多因素驗證等功能是簡單 tooenable</span><span class="sxs-lookup"><span data-stu-id="2449b-168">Features like conditional access and Multi-Factor Authentication are easy tooenable</span></span>
- <span data-ttu-id="2449b-169">在 hello 非軍事區域中沒有 componenet</span><span class="sxs-lookup"><span data-stu-id="2449b-169">No componenet in hello demilitarized zone</span></span>
- <span data-ttu-id="2449b-170">沒有所需的輸入連線</span><span class="sxs-lookup"><span data-stu-id="2449b-170">No inbound connections required</span></span>
- <span data-ttu-id="2449b-171">一個存取面板，您的使用者可以前往 toofor 所有其應用程式，包括 O365、 Azure AD 整合的 SaaS 應用程式，而您內部部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2449b-171">One access panel that your users can go toofor all their applications, including O365, Azure AD integrated SaaS apps, and your on-premises web apps.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="2449b-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2449b-172">Next steps</span></span>

- [<span data-ttu-id="2449b-173">使用 Azure AD 應用程式 tooprovide 安全遠端存取 tooon 內部部署應用程式</span><span class="sxs-lookup"><span data-stu-id="2449b-173">Use Azure AD Application tooprovide secure remote access tooon-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- <span data-ttu-id="2449b-174">[從 Forefront TMG 和 UAG tooApplication Proxy 轉換](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)。</span><span class="sxs-lookup"><span data-stu-id="2449b-174">[Transition from Forefront TMG and UAG tooApplication Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).</span></span>
