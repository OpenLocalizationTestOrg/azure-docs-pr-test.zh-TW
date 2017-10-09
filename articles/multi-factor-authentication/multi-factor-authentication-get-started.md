---
title: "Azure MFA 雲端或伺服器之間的 aaaChoose |Microsoft 文件"
description: "選擇最適合您要求，我嘗試 toosecure 以及所在位置，我的使用者位於哪個 am hello 多重要素驗證安全性解決方案。  然後選擇雲端、MFA Server 或 AD FS。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a><span data-ttu-id="dc963-104">為您選擇 hello Azure 多因素驗證解決方案</span><span class="sxs-lookup"><span data-stu-id="dc963-104">Choose hello Azure Multi-Factor Authentication solution for you</span></span>
<span data-ttu-id="dc963-105">由於有數款的 Azure Multi-factor Authentication (MFA)，我們必須回答幾個問題 toofigure 哪一個版本是 hello 適當一個 toouse。</span><span class="sxs-lookup"><span data-stu-id="dc963-105">Because there are several flavors of Azure Multi-Factor Authentication (MFA), we must answer a few questions toofigure out which version is hello proper one toouse.</span></span>  <span data-ttu-id="dc963-106">這些問題如下：</span><span class="sxs-lookup"><span data-stu-id="dc963-106">Those questions are:</span></span>

* [<span data-ttu-id="dc963-107">什麼試著 toosecure</span><span class="sxs-lookup"><span data-stu-id="dc963-107">What am I trying toosecure</span></span>](#what-am-i-trying-to-secure)
* [<span data-ttu-id="dc963-108">Hello 使用者位於何處</span><span class="sxs-lookup"><span data-stu-id="dc963-108">Where are hello users located</span></span>](#where-are-the-users-located)
* [<span data-ttu-id="dc963-109">我需要哪些功能？</span><span class="sxs-lookup"><span data-stu-id="dc963-109">What features do I need?</span></span>](#what-featured-do-i-need)

<span data-ttu-id="dc963-110">hello 下列各節提供指引判斷每個答案。</span><span class="sxs-lookup"><span data-stu-id="dc963-110">hello following sections provide guidance on determining each of these answers.</span></span>

## <a name="what-am-i-trying-toosecure"></a><span data-ttu-id="dc963-111">什麼試著 toosecure 嗎？</span><span class="sxs-lookup"><span data-stu-id="dc963-111">What am I trying toosecure?</span></span>
<span data-ttu-id="dc963-112">toodetermine hello 正確的雙步驟驗證解決方案前必須回答什麼是您嘗試 toosecure 與驗證的第二個方法的 hello 問題了。</span><span class="sxs-lookup"><span data-stu-id="dc963-112">toodetermine hello correct two-step verification solution, first we must answer hello question of what are you trying toosecure with a second method of authentication.</span></span>  <span data-ttu-id="dc963-113">它是 Azure 中的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="dc963-113">Is it an application that is in Azure?</span></span>  <span data-ttu-id="dc963-114">或是遠端存取系統？</span><span class="sxs-lookup"><span data-stu-id="dc963-114">Or a remote access system?</span></span>  <span data-ttu-id="dc963-115">藉由判斷我們正在嘗試 toosecure，我們可以回答 hello 的問題必須多因素驗證啟用的 toobe。</span><span class="sxs-lookup"><span data-stu-id="dc963-115">By determining what we are trying toosecure, we can answer hello question of where Multi-Factor Authentication needs toobe enabled.</span></span>  

| <span data-ttu-id="dc963-116">您嘗試 toosecure 有哪些？</span><span class="sxs-lookup"><span data-stu-id="dc963-116">What are you trying toosecure</span></span> | <span data-ttu-id="dc963-117">Hello 雲端中的 MFA</span><span class="sxs-lookup"><span data-stu-id="dc963-117">MFA in hello cloud</span></span> | <span data-ttu-id="dc963-118">MFA Server</span><span class="sxs-lookup"><span data-stu-id="dc963-118">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="dc963-119">第一方 Microsoft 應用程式</span><span class="sxs-lookup"><span data-stu-id="dc963-119">First-party Microsoft apps</span></span> |<span data-ttu-id="dc963-120">●</span><span class="sxs-lookup"><span data-stu-id="dc963-120">●</span></span> |<span data-ttu-id="dc963-121">●</span><span class="sxs-lookup"><span data-stu-id="dc963-121">●</span></span> |
| <span data-ttu-id="dc963-122">在 hello 應用程式庫中的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="dc963-122">SaaS apps in hello app gallery</span></span> |<span data-ttu-id="dc963-123">●</span><span class="sxs-lookup"><span data-stu-id="dc963-123">●</span></span> |  |
| <span data-ttu-id="dc963-124">透過 Azure AD App Proxy 發佈的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="dc963-124">Web applications published through Azure AD App Proxy</span></span> |<span data-ttu-id="dc963-125">●</span><span class="sxs-lookup"><span data-stu-id="dc963-125">●</span></span> |  |
| <span data-ttu-id="dc963-126">非透過 Azure AD App Proxy 發佈的 IIS 應用程式</span><span class="sxs-lookup"><span data-stu-id="dc963-126">IIS applications not published through Azure AD App Proxy</span></span> | |<span data-ttu-id="dc963-127">●</span><span class="sxs-lookup"><span data-stu-id="dc963-127">●</span></span> |
| <span data-ttu-id="dc963-128">VPN、RDG 等遠端存取</span><span class="sxs-lookup"><span data-stu-id="dc963-128">Remote access such as VPN, RDG</span></span> | <span data-ttu-id="dc963-129">●</span><span class="sxs-lookup"><span data-stu-id="dc963-129">●</span></span> | <span data-ttu-id="dc963-130">●</span><span class="sxs-lookup"><span data-stu-id="dc963-130">●</span></span> |

## <a name="where-are-hello-users-located"></a><span data-ttu-id="dc963-131">Hello 使用者位於何處</span><span class="sxs-lookup"><span data-stu-id="dc963-131">Where are hello users located</span></span>
<span data-ttu-id="dc963-132">接下來，查看我們的使用者位於何處 hello 定域機組中是否有助於 toodetermine hello 正確方案 toouse，，或使用內部 hello MFA Server。</span><span class="sxs-lookup"><span data-stu-id="dc963-132">Next, looking at where our users are located helps toodetermine hello correct solution toouse, whether in hello cloud or on-premises using hello MFA Server.</span></span>

| <span data-ttu-id="dc963-133">使用者位置</span><span class="sxs-lookup"><span data-stu-id="dc963-133">User Location</span></span> | <span data-ttu-id="dc963-134">Hello 雲端中的 MFA</span><span class="sxs-lookup"><span data-stu-id="dc963-134">MFA in hello cloud</span></span> | <span data-ttu-id="dc963-135">MFA Server</span><span class="sxs-lookup"><span data-stu-id="dc963-135">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="dc963-136">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc963-136">Azure Active Directory</span></span> |<span data-ttu-id="dc963-137">●</span><span class="sxs-lookup"><span data-stu-id="dc963-137">●</span></span> | |
| <span data-ttu-id="dc963-138">Azure AD 和使用 AD FS 同盟的內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="dc963-138">Azure AD and on-premises AD using federation with AD FS</span></span> |<span data-ttu-id="dc963-139">●</span><span class="sxs-lookup"><span data-stu-id="dc963-139">●</span></span> |<span data-ttu-id="dc963-140">●</span><span class="sxs-lookup"><span data-stu-id="dc963-140">●</span></span> |
| <span data-ttu-id="dc963-141">Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 而沒有密碼同步</span><span class="sxs-lookup"><span data-stu-id="dc963-141">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - no password sync</span></span> |<span data-ttu-id="dc963-142">●</span><span class="sxs-lookup"><span data-stu-id="dc963-142">●</span></span> |<span data-ttu-id="dc963-143">●</span><span class="sxs-lookup"><span data-stu-id="dc963-143">●</span></span> |
| <span data-ttu-id="dc963-144">Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 使用密碼同步</span><span class="sxs-lookup"><span data-stu-id="dc963-144">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - with password sync</span></span> |<span data-ttu-id="dc963-145">●</span><span class="sxs-lookup"><span data-stu-id="dc963-145">●</span></span> | |
| <span data-ttu-id="dc963-146">內部部署 Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc963-146">On-premises Active Directory</span></span> | |<span data-ttu-id="dc963-147">●</span><span class="sxs-lookup"><span data-stu-id="dc963-147">●</span></span> |

## <a name="what-features-do-i-need"></a><span data-ttu-id="dc963-148">我需要哪些功能？</span><span class="sxs-lookup"><span data-stu-id="dc963-148">What features do I need?</span></span>
<span data-ttu-id="dc963-149">hello 下表比較可用 hello 雲端中的多重要素驗證與 hello Multi-factor Authentication Server 的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="dc963-149">hello following table compares hello features that are available with Multi-Factor Authentication in hello cloud and with hello Multi-Factor Authentication Server.</span></span>

| <span data-ttu-id="dc963-150">功能</span><span class="sxs-lookup"><span data-stu-id="dc963-150">Feature</span></span> | <span data-ttu-id="dc963-151">Hello 雲端中的 MFA</span><span class="sxs-lookup"><span data-stu-id="dc963-151">MFA in hello cloud</span></span> | <span data-ttu-id="dc963-152">MFA Server</span><span class="sxs-lookup"><span data-stu-id="dc963-152">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="dc963-153">以行動應用程式通知做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-153">Mobile app notification as a second factor</span></span> | <span data-ttu-id="dc963-154">●</span><span class="sxs-lookup"><span data-stu-id="dc963-154">●</span></span> | <span data-ttu-id="dc963-155">●</span><span class="sxs-lookup"><span data-stu-id="dc963-155">●</span></span> |
| <span data-ttu-id="dc963-156">以行動應用程式驗證碼做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-156">Mobile app verification code as a second factor</span></span> | <span data-ttu-id="dc963-157">●</span><span class="sxs-lookup"><span data-stu-id="dc963-157">●</span></span> | <span data-ttu-id="dc963-158">●</span><span class="sxs-lookup"><span data-stu-id="dc963-158">●</span></span> |
| <span data-ttu-id="dc963-159">以撥打電話做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-159">Phone call as second factor</span></span> | <span data-ttu-id="dc963-160">●</span><span class="sxs-lookup"><span data-stu-id="dc963-160">●</span></span> | <span data-ttu-id="dc963-161">●</span><span class="sxs-lookup"><span data-stu-id="dc963-161">●</span></span> |
| <span data-ttu-id="dc963-162">以單向 SMS 做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-162">One-way SMS as second factor</span></span> | <span data-ttu-id="dc963-163">●</span><span class="sxs-lookup"><span data-stu-id="dc963-163">●</span></span> | <span data-ttu-id="dc963-164">●</span><span class="sxs-lookup"><span data-stu-id="dc963-164">●</span></span> |
| <span data-ttu-id="dc963-165">以雙向 SMS 做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-165">Two-way SMS as second factor</span></span> | | <span data-ttu-id="dc963-166">●</span><span class="sxs-lookup"><span data-stu-id="dc963-166">●</span></span> |
| <span data-ttu-id="dc963-167">以硬體權杖做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="dc963-167">Hardware Tokens as second factor</span></span> | | <span data-ttu-id="dc963-168">●</span><span class="sxs-lookup"><span data-stu-id="dc963-168">●</span></span> |
| <span data-ttu-id="dc963-169">不支援 MFA 之 Office 365 用戶端的應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="dc963-169">App passwords for Office 365 clients that don’t support MFA</span></span> | <span data-ttu-id="dc963-170">●</span><span class="sxs-lookup"><span data-stu-id="dc963-170">●</span></span> | |
| <span data-ttu-id="dc963-171">系統管理員控制驗證方法</span><span class="sxs-lookup"><span data-stu-id="dc963-171">Admin control over authentication methods</span></span> | <span data-ttu-id="dc963-172">●</span><span class="sxs-lookup"><span data-stu-id="dc963-172">●</span></span> | <span data-ttu-id="dc963-173">●</span><span class="sxs-lookup"><span data-stu-id="dc963-173">●</span></span> |
| <span data-ttu-id="dc963-174">PIN 模式</span><span class="sxs-lookup"><span data-stu-id="dc963-174">PIN mode</span></span> | | <span data-ttu-id="dc963-175">●</span><span class="sxs-lookup"><span data-stu-id="dc963-175">●</span></span> |
| <span data-ttu-id="dc963-176">詐騙警示</span><span class="sxs-lookup"><span data-stu-id="dc963-176">Fraud alert</span></span> |<span data-ttu-id="dc963-177">●</span><span class="sxs-lookup"><span data-stu-id="dc963-177">●</span></span> | <span data-ttu-id="dc963-178">●</span><span class="sxs-lookup"><span data-stu-id="dc963-178">●</span></span> |
| <span data-ttu-id="dc963-179">MFA 報告</span><span class="sxs-lookup"><span data-stu-id="dc963-179">MFA Reports</span></span> |<span data-ttu-id="dc963-180">●</span><span class="sxs-lookup"><span data-stu-id="dc963-180">●</span></span> | <span data-ttu-id="dc963-181">●</span><span class="sxs-lookup"><span data-stu-id="dc963-181">●</span></span> |
| <span data-ttu-id="dc963-182">一次性略過</span><span class="sxs-lookup"><span data-stu-id="dc963-182">One-Time Bypass</span></span> | | <span data-ttu-id="dc963-183">●</span><span class="sxs-lookup"><span data-stu-id="dc963-183">●</span></span> |
| <span data-ttu-id="dc963-184">通話的自訂問候語</span><span class="sxs-lookup"><span data-stu-id="dc963-184">Custom greetings for phone calls</span></span> | <span data-ttu-id="dc963-185">●</span><span class="sxs-lookup"><span data-stu-id="dc963-185">●</span></span> | <span data-ttu-id="dc963-186">●</span><span class="sxs-lookup"><span data-stu-id="dc963-186">●</span></span> |
| <span data-ttu-id="dc963-187">可自訂的通話來電者 ID</span><span class="sxs-lookup"><span data-stu-id="dc963-187">Customizable caller ID for phone calls</span></span> | <span data-ttu-id="dc963-188">●</span><span class="sxs-lookup"><span data-stu-id="dc963-188">●</span></span> | <span data-ttu-id="dc963-189">●</span><span class="sxs-lookup"><span data-stu-id="dc963-189">●</span></span> |
| <span data-ttu-id="dc963-190">信任的 IP</span><span class="sxs-lookup"><span data-stu-id="dc963-190">Trusted IPs</span></span> | <span data-ttu-id="dc963-191">●</span><span class="sxs-lookup"><span data-stu-id="dc963-191">●</span></span> | <span data-ttu-id="dc963-192">●</span><span class="sxs-lookup"><span data-stu-id="dc963-192">●</span></span> |
| <span data-ttu-id="dc963-193">記住受信任裝置的 MFA</span><span class="sxs-lookup"><span data-stu-id="dc963-193">Remember MFA for trusted devices</span></span> | <span data-ttu-id="dc963-194">●</span><span class="sxs-lookup"><span data-stu-id="dc963-194">●</span></span> | |
| <span data-ttu-id="dc963-195">條件式存取</span><span class="sxs-lookup"><span data-stu-id="dc963-195">Conditional access</span></span> | <span data-ttu-id="dc963-196">●</span><span class="sxs-lookup"><span data-stu-id="dc963-196">●</span></span> | <span data-ttu-id="dc963-197">●</span><span class="sxs-lookup"><span data-stu-id="dc963-197">●</span></span> |
| <span data-ttu-id="dc963-198">快取</span><span class="sxs-lookup"><span data-stu-id="dc963-198">Cache</span></span> |  | <span data-ttu-id="dc963-199">●</span><span class="sxs-lookup"><span data-stu-id="dc963-199">●</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc963-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc963-200">Next steps</span></span>

<span data-ttu-id="dc963-201">既然我們判定是否 toouse 雲端 multi-factor authentication 或 hello MFA Server 內部部署，我們可以開始設定和使用 Azure Multi-factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="dc963-201">Now that we have determined whether toouse cloud multi-factor authentication or hello MFA Server on-premises, we can get started setting up and using Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="dc963-202">**選取代表您的實例的 hello 圖示**</span><span class="sxs-lookup"><span data-stu-id="dc963-202">**Select hello icon that represents your scenario**</span></span>

<center>




<span data-ttu-id="dc963-203">[![雲端](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![伺服器](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span><span class="sxs-lookup"><span data-stu-id="dc963-203">[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span></span>
