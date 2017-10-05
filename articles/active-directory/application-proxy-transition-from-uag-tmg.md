---
title: "升級到 Azure AD 應用程式 Proxy | Microsoft Docs"
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
ms.openlocfilehash: 6c9f70493155de6989b26fd4e8bcf1dff01c835c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="compare-remote-access-solutions"></a><span data-ttu-id="3641c-103">比較遠端存取解決方案</span><span class="sxs-lookup"><span data-stu-id="3641c-103">Compare remote access solutions</span></span>

<span data-ttu-id="3641c-104">Azure Active Directory 應用程式 Proxy 是 Microsoft 提供的兩個遠端存取解決方案其中之一。</span><span class="sxs-lookup"><span data-stu-id="3641c-104">Azure Active Directory Application Proxy is one of two remote access solutions that Microsoft offers.</span></span> <span data-ttu-id="3641c-105">另一個是 Web 應用程式 Proxy，內部部署版本。</span><span class="sxs-lookup"><span data-stu-id="3641c-105">The other is Web Application Proxy, the on-premises version.</span></span> <span data-ttu-id="3641c-106">這兩種解決方案取代 Microsoft 提供的舊版產品：Microsoft Forefront Threat Management Gateway (TMG) 和 Unified Access Gateway (UAG)。</span><span class="sxs-lookup"><span data-stu-id="3641c-106">These two solutions replace earlier products that Microsoft offered: Microsoft Forefront Threat Management Gateway (TMG) and Unified Access Gateway (UAG).</span></span> <span data-ttu-id="3641c-107">若要了解這四個解決方案之間的比較，可使用這份文件。</span><span class="sxs-lookup"><span data-stu-id="3641c-107">Use this article to understand how these four solutions compare to each other.</span></span> <span data-ttu-id="3641c-108">若您仍在使用已取代的 TMG 或 UAG 解決方案，使用本文章可協助您規劃移轉至其中一個應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="3641c-108">For those of you still using the deprecated TMG or UAG solutions, use this article to help plan your migration to one of the Application Proxy.</span></span> 


## <a name="feature-comparison"></a><span data-ttu-id="3641c-109">功能比較</span><span class="sxs-lookup"><span data-stu-id="3641c-109">Feature comparison</span></span>

<span data-ttu-id="3641c-110">您可以使用此表格來了解 Threat Management Gateway (TMG)、Unified Access Gateway (UAG)、Web 應用程式 Proxy (WAP) 和 Azure AD 應用程式 Proxy (AP) 之間的比較。</span><span class="sxs-lookup"><span data-stu-id="3641c-110">Use this table to understand how Threat Management Gateway (TMG), Unified Access Gateway (UAG), Web Application Proxy (WAP), and Azure AD Application Proxy (AP) compare to each other.</span></span>

| <span data-ttu-id="3641c-111">功能</span><span class="sxs-lookup"><span data-stu-id="3641c-111">Feature</span></span> | <span data-ttu-id="3641c-112">TMG</span><span class="sxs-lookup"><span data-stu-id="3641c-112">TMG</span></span> | <span data-ttu-id="3641c-113">UAG</span><span class="sxs-lookup"><span data-stu-id="3641c-113">UAG</span></span> | <span data-ttu-id="3641c-114">WAP</span><span class="sxs-lookup"><span data-stu-id="3641c-114">WAP</span></span> | <span data-ttu-id="3641c-115">AP</span><span class="sxs-lookup"><span data-stu-id="3641c-115">AP</span></span> |
| ------- | --- | --- | --- | --- |
| <span data-ttu-id="3641c-116">憑證驗證</span><span class="sxs-lookup"><span data-stu-id="3641c-116">Certificate authentication</span></span> | <span data-ttu-id="3641c-117">是</span><span class="sxs-lookup"><span data-stu-id="3641c-117">Yes</span></span> | <span data-ttu-id="3641c-118">是</span><span class="sxs-lookup"><span data-stu-id="3641c-118">Yes</span></span> | - | - |
| <span data-ttu-id="3641c-119">選擇性地發佈瀏覽器應用程式</span><span class="sxs-lookup"><span data-stu-id="3641c-119">Selectively publish browser apps</span></span> | <span data-ttu-id="3641c-120">是</span><span class="sxs-lookup"><span data-stu-id="3641c-120">Yes</span></span> | <span data-ttu-id="3641c-121">是</span><span class="sxs-lookup"><span data-stu-id="3641c-121">Yes</span></span> | <span data-ttu-id="3641c-122">是</span><span class="sxs-lookup"><span data-stu-id="3641c-122">Yes</span></span> | <span data-ttu-id="3641c-123">是</span><span class="sxs-lookup"><span data-stu-id="3641c-123">Yes</span></span> |
| <span data-ttu-id="3641c-124">預先驗證和單一登入</span><span class="sxs-lookup"><span data-stu-id="3641c-124">Preauthentication and single sign-on</span></span> | <span data-ttu-id="3641c-125">是</span><span class="sxs-lookup"><span data-stu-id="3641c-125">Yes</span></span> | <span data-ttu-id="3641c-126">是</span><span class="sxs-lookup"><span data-stu-id="3641c-126">Yes</span></span> | <span data-ttu-id="3641c-127">是</span><span class="sxs-lookup"><span data-stu-id="3641c-127">Yes</span></span> | <span data-ttu-id="3641c-128">是</span><span class="sxs-lookup"><span data-stu-id="3641c-128">Yes</span></span> | 
| <span data-ttu-id="3641c-129">第 2 層/第 3 層防火牆</span><span class="sxs-lookup"><span data-stu-id="3641c-129">Layer 2/3 firewall</span></span> | <span data-ttu-id="3641c-130">是</span><span class="sxs-lookup"><span data-stu-id="3641c-130">Yes</span></span> | <span data-ttu-id="3641c-131">是</span><span class="sxs-lookup"><span data-stu-id="3641c-131">Yes</span></span> | - | - |
| <span data-ttu-id="3641c-132">轉接 Proxy 功能</span><span class="sxs-lookup"><span data-stu-id="3641c-132">Forward proxy capabilities</span></span> | <span data-ttu-id="3641c-133">是</span><span class="sxs-lookup"><span data-stu-id="3641c-133">Yes</span></span> | - | - | - |
| <span data-ttu-id="3641c-134">VPN 功能</span><span class="sxs-lookup"><span data-stu-id="3641c-134">VPN capabilities</span></span> | <span data-ttu-id="3641c-135">是</span><span class="sxs-lookup"><span data-stu-id="3641c-135">Yes</span></span> | <span data-ttu-id="3641c-136">是</span><span class="sxs-lookup"><span data-stu-id="3641c-136">Yes</span></span> | - | - |
| <span data-ttu-id="3641c-137">豐富通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="3641c-137">Rich protocol support</span></span> | - | <span data-ttu-id="3641c-138">是</span><span class="sxs-lookup"><span data-stu-id="3641c-138">Yes</span></span> | <span data-ttu-id="3641c-139">是，如果是透過 HTTP 執行</span><span class="sxs-lookup"><span data-stu-id="3641c-139">Yes, if running over HTTP</span></span> | <span data-ttu-id="3641c-140">是，如果是透過 HTTP 或透過遠端桌面閘道執行</span><span class="sxs-lookup"><span data-stu-id="3641c-140">Yes, if running over HTTP or through Remote Desktop Gateway</span></span> |
| <span data-ttu-id="3641c-141">作為 ADFS Proxy 伺服器</span><span class="sxs-lookup"><span data-stu-id="3641c-141">Serves as ADFS proxy server</span></span> | - | <span data-ttu-id="3641c-142">是</span><span class="sxs-lookup"><span data-stu-id="3641c-142">Yes</span></span> | <span data-ttu-id="3641c-143">是</span><span class="sxs-lookup"><span data-stu-id="3641c-143">Yes</span></span> | - |
| <span data-ttu-id="3641c-144">應用程式存取的單一入口網站</span><span class="sxs-lookup"><span data-stu-id="3641c-144">One portal for application access</span></span> | - | <span data-ttu-id="3641c-145">是</span><span class="sxs-lookup"><span data-stu-id="3641c-145">Yes</span></span> | - | <span data-ttu-id="3641c-146">是</span><span class="sxs-lookup"><span data-stu-id="3641c-146">Yes</span></span> |
| <span data-ttu-id="3641c-147">回應內文連結轉譯</span><span class="sxs-lookup"><span data-stu-id="3641c-147">Response body link translation</span></span> | <span data-ttu-id="3641c-148">是</span><span class="sxs-lookup"><span data-stu-id="3641c-148">Yes</span></span> | <span data-ttu-id="3641c-149">是</span><span class="sxs-lookup"><span data-stu-id="3641c-149">Yes</span></span> | - | <span data-ttu-id="3641c-150">是</span><span class="sxs-lookup"><span data-stu-id="3641c-150">Yes</span></span> | 
| <span data-ttu-id="3641c-151">使用標頭進行驗證</span><span class="sxs-lookup"><span data-stu-id="3641c-151">Authentication with headers</span></span> | - | <span data-ttu-id="3641c-152">是</span><span class="sxs-lookup"><span data-stu-id="3641c-152">Yes</span></span> | - | <span data-ttu-id="3641c-153">是，使用 PingAccess</span><span class="sxs-lookup"><span data-stu-id="3641c-153">Yes, with PingAccess</span></span> | 
| <span data-ttu-id="3641c-154">雲端級別安全性</span><span class="sxs-lookup"><span data-stu-id="3641c-154">Cloud-scale security</span></span> | - | - | - | <span data-ttu-id="3641c-155">是</span><span class="sxs-lookup"><span data-stu-id="3641c-155">Yes</span></span> | 
| <span data-ttu-id="3641c-156">條件式存取</span><span class="sxs-lookup"><span data-stu-id="3641c-156">Conditional access</span></span> | - | <span data-ttu-id="3641c-157">是</span><span class="sxs-lookup"><span data-stu-id="3641c-157">Yes</span></span> | - | <span data-ttu-id="3641c-158">是</span><span class="sxs-lookup"><span data-stu-id="3641c-158">Yes</span></span> |
| <span data-ttu-id="3641c-159">非軍事區域 (DMZ) 中沒有任何元件</span><span class="sxs-lookup"><span data-stu-id="3641c-159">No components in the demilitarized zone (DMZ)</span></span> | - | - | - | <span data-ttu-id="3641c-160">是</span><span class="sxs-lookup"><span data-stu-id="3641c-160">Yes</span></span> |
| <span data-ttu-id="3641c-161">沒有輸入連線</span><span class="sxs-lookup"><span data-stu-id="3641c-161">No inbound connections</span></span> | - | - | - | <span data-ttu-id="3641c-162">是</span><span class="sxs-lookup"><span data-stu-id="3641c-162">Yes</span></span> |

<span data-ttu-id="3641c-163">大部分情節中，建議將 Azure AD 應用程式作為現代化解決方案。</span><span class="sxs-lookup"><span data-stu-id="3641c-163">For most scenarios, we recommend Azure AD Application as the modern solution.</span></span> <span data-ttu-id="3641c-164">Web 應用程式 Proxy 只建議用在需要 AD FS Proxy 伺服器的情節中，而且您無法使用 Azure Active Directory 中的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="3641c-164">Web Application Proxy is only preferred in scenarios that require a proxy server for AD FS, and you can't use custom domains in Azure Active Directory.</span></span> 

<span data-ttu-id="3641c-165">相較於類似的產品，Azure AD 應用程式 Proxy 提供獨特的優點，包括：</span><span class="sxs-lookup"><span data-stu-id="3641c-165">Azure AD Application Proxy offers unique benefits when compared to similar products, including:</span></span>

- <span data-ttu-id="3641c-166">將 Azure AD 擴充至內部部署資源</span><span class="sxs-lookup"><span data-stu-id="3641c-166">Extending Azure AD to on-premises resources</span></span>
   - <span data-ttu-id="3641c-167">雲端級別安全性和保護</span><span class="sxs-lookup"><span data-stu-id="3641c-167">Cloud-scale security and protection</span></span>
   - <span data-ttu-id="3641c-168">可輕鬆地啟用諸如條件式存取和 Multi-Factor Authentication 等功能</span><span class="sxs-lookup"><span data-stu-id="3641c-168">Features like conditional access and Multi-Factor Authentication are easy to enable</span></span>
- <span data-ttu-id="3641c-169">非軍事區域中沒有任何元件</span><span class="sxs-lookup"><span data-stu-id="3641c-169">No componenet in the demilitarized zone</span></span>
- <span data-ttu-id="3641c-170">沒有所需的輸入連線</span><span class="sxs-lookup"><span data-stu-id="3641c-170">No inbound connections required</span></span>
- <span data-ttu-id="3641c-171">您的使用者可以使用其所有應用程式的單一存取面板，包括 O365、Azure AD 整合式 SaaS 應用程式，以及您的內部部署 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3641c-171">One access panel that your users can go to for all their applications, including O365, Azure AD integrated SaaS apps, and your on-premises web apps.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="3641c-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3641c-172">Next steps</span></span>

- [<span data-ttu-id="3641c-173">使用 Azure AD 應用程式提供對內部部署應用程式的安全遠端存取</span><span class="sxs-lookup"><span data-stu-id="3641c-173">Use Azure AD Application to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- <span data-ttu-id="3641c-174">[從 Forefront TMG 和 UAG 轉換至應用程式 Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)。</span><span class="sxs-lookup"><span data-stu-id="3641c-174">[Transition from Forefront TMG and UAG to Application Proxy](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/).</span></span>
