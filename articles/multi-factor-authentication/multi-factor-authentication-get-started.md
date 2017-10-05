---
title: "選擇 Azure MFA 雲端或伺服器 | Microsoft Docs"
description: "藉由提出我要保護什麼和使用者所在位置等問題，選擇最合適的 Multi-Factor Authentication 安全性解決方案。  然後選擇雲端、MFA Server 或 AD FS。"
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
ms.openlocfilehash: 6f8ee3449244b12d2c8b5714e6ad893e2f0b10ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="choose-the-azure-multi-factor-authentication-solution-for-you"></a><span data-ttu-id="5fe5f-104">選擇您的 Azure Multi-Factor Authentication 方案</span><span class="sxs-lookup"><span data-stu-id="5fe5f-104">Choose the Azure Multi-Factor Authentication solution for you</span></span>
<span data-ttu-id="5fe5f-105">因為 Azure Multi-Factor Authentication (MFA) 的種類繁多，我們必須回答幾個問題，以找出最合適的版本。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-105">Because there are several flavors of Azure Multi-Factor Authentication (MFA), we must answer a few questions to figure out which version is the proper one to use.</span></span>  <span data-ttu-id="5fe5f-106">這些問題如下：</span><span class="sxs-lookup"><span data-stu-id="5fe5f-106">Those questions are:</span></span>

* [<span data-ttu-id="5fe5f-107">我要保護什麼</span><span class="sxs-lookup"><span data-stu-id="5fe5f-107">What am I trying to secure</span></span>](#what-am-i-trying-to-secure)
* [<span data-ttu-id="5fe5f-108">使用者位於何處</span><span class="sxs-lookup"><span data-stu-id="5fe5f-108">Where are the users located</span></span>](#where-are-the-users-located)
* [<span data-ttu-id="5fe5f-109">我需要哪些功能？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-109">What features do I need?</span></span>](#what-featured-do-i-need)

<span data-ttu-id="5fe5f-110">下列各節會提供如何確定以上問題之答案的指引。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-110">The following sections provide guidance on determining each of these answers.</span></span>

## <a name="what-am-i-trying-to-secure"></a><span data-ttu-id="5fe5f-111">我要保護什麼？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-111">What am I trying to secure?</span></span>
<span data-ttu-id="5fe5f-112">為了判斷出正確的雙步驟驗證方案，首先我們必須回答一個問題：您試圖使用第二個驗證方法來保護什麼？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-112">To determine the correct two-step verification solution, first we must answer the question of what are you trying to secure with a second method of authentication.</span></span>  <span data-ttu-id="5fe5f-113">它是 Azure 中的應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-113">Is it an application that is in Azure?</span></span>  <span data-ttu-id="5fe5f-114">或是遠端存取系統？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-114">Or a remote access system?</span></span>  <span data-ttu-id="5fe5f-115">藉由判斷我們嘗試保護的東西，我們可以對該在何處啟用 Multi-Factor Authentication 這個問題做出回答。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-115">By determining what we are trying to secure, we can answer the question of where Multi-Factor Authentication needs to be enabled.</span></span>  

| <span data-ttu-id="5fe5f-116">您想要保護什麼</span><span class="sxs-lookup"><span data-stu-id="5fe5f-116">What are you trying to secure</span></span> | <span data-ttu-id="5fe5f-117">雲端 MFA</span><span class="sxs-lookup"><span data-stu-id="5fe5f-117">MFA in the cloud</span></span> | <span data-ttu-id="5fe5f-118">MFA Server</span><span class="sxs-lookup"><span data-stu-id="5fe5f-118">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="5fe5f-119">第一方 Microsoft 應用程式</span><span class="sxs-lookup"><span data-stu-id="5fe5f-119">First-party Microsoft apps</span></span> |<span data-ttu-id="5fe5f-120">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-120">●</span></span> |<span data-ttu-id="5fe5f-121">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-121">●</span></span> |
| <span data-ttu-id="5fe5f-122">應用程式資源庫中的 SaaS 應用程式</span><span class="sxs-lookup"><span data-stu-id="5fe5f-122">SaaS apps in the app gallery</span></span> |<span data-ttu-id="5fe5f-123">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-123">●</span></span> |  |
| <span data-ttu-id="5fe5f-124">透過 Azure AD App Proxy 發佈的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5fe5f-124">Web applications published through Azure AD App Proxy</span></span> |<span data-ttu-id="5fe5f-125">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-125">●</span></span> |  |
| <span data-ttu-id="5fe5f-126">非透過 Azure AD App Proxy 發佈的 IIS 應用程式</span><span class="sxs-lookup"><span data-stu-id="5fe5f-126">IIS applications not published through Azure AD App Proxy</span></span> | |<span data-ttu-id="5fe5f-127">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-127">●</span></span> |
| <span data-ttu-id="5fe5f-128">VPN、RDG 等遠端存取</span><span class="sxs-lookup"><span data-stu-id="5fe5f-128">Remote access such as VPN, RDG</span></span> | <span data-ttu-id="5fe5f-129">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-129">●</span></span> | <span data-ttu-id="5fe5f-130">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-130">●</span></span> |

## <a name="where-are-the-users-located"></a><span data-ttu-id="5fe5f-131">使用者位於何處</span><span class="sxs-lookup"><span data-stu-id="5fe5f-131">Where are the users located</span></span>
<span data-ttu-id="5fe5f-132">接下來，查看使用者的所在位置有助於判斷出合適的解決方案，不論是雲端中或使用 MFA Server 的內部部署。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-132">Next, looking at where our users are located helps to determine the correct solution to use, whether in the cloud or on-premises using the MFA Server.</span></span>

| <span data-ttu-id="5fe5f-133">使用者位置</span><span class="sxs-lookup"><span data-stu-id="5fe5f-133">User Location</span></span> | <span data-ttu-id="5fe5f-134">雲端 MFA</span><span class="sxs-lookup"><span data-stu-id="5fe5f-134">MFA in the cloud</span></span> | <span data-ttu-id="5fe5f-135">MFA Server</span><span class="sxs-lookup"><span data-stu-id="5fe5f-135">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="5fe5f-136">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe5f-136">Azure Active Directory</span></span> |<span data-ttu-id="5fe5f-137">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-137">●</span></span> | |
| <span data-ttu-id="5fe5f-138">Azure AD 和使用 AD FS 同盟的內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="5fe5f-138">Azure AD and on-premises AD using federation with AD FS</span></span> |<span data-ttu-id="5fe5f-139">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-139">●</span></span> |<span data-ttu-id="5fe5f-140">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-140">●</span></span> |
| <span data-ttu-id="5fe5f-141">Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 而沒有密碼同步</span><span class="sxs-lookup"><span data-stu-id="5fe5f-141">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - no password sync</span></span> |<span data-ttu-id="5fe5f-142">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-142">●</span></span> |<span data-ttu-id="5fe5f-143">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-143">●</span></span> |
| <span data-ttu-id="5fe5f-144">Azure AD 和使用 DirSync、Azure AD Sync、Azure AD Connect 的內部部署 AD - 使用密碼同步</span><span class="sxs-lookup"><span data-stu-id="5fe5f-144">Azure AD and on-premises AD using DirSync, Azure AD Sync, Azure AD Connect - with password sync</span></span> |<span data-ttu-id="5fe5f-145">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-145">●</span></span> | |
| <span data-ttu-id="5fe5f-146">內部部署 Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fe5f-146">On-premises Active Directory</span></span> | |<span data-ttu-id="5fe5f-147">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-147">●</span></span> |

## <a name="what-features-do-i-need"></a><span data-ttu-id="5fe5f-148">我需要哪些功能？</span><span class="sxs-lookup"><span data-stu-id="5fe5f-148">What features do I need?</span></span>
<span data-ttu-id="5fe5f-149">下表是雲端中 Multi-Factor Authentication 和 Multi-factor Authentication Server 的可用功能比較。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-149">The following table compares the features that are available with Multi-Factor Authentication in the cloud and with the Multi-Factor Authentication Server.</span></span>

| <span data-ttu-id="5fe5f-150">功能</span><span class="sxs-lookup"><span data-stu-id="5fe5f-150">Feature</span></span> | <span data-ttu-id="5fe5f-151">雲端 MFA</span><span class="sxs-lookup"><span data-stu-id="5fe5f-151">MFA in the cloud</span></span> | <span data-ttu-id="5fe5f-152">MFA Server</span><span class="sxs-lookup"><span data-stu-id="5fe5f-152">MFA Server</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="5fe5f-153">以行動應用程式通知做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-153">Mobile app notification as a second factor</span></span> | <span data-ttu-id="5fe5f-154">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-154">●</span></span> | <span data-ttu-id="5fe5f-155">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-155">●</span></span> |
| <span data-ttu-id="5fe5f-156">以行動應用程式驗證碼做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-156">Mobile app verification code as a second factor</span></span> | <span data-ttu-id="5fe5f-157">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-157">●</span></span> | <span data-ttu-id="5fe5f-158">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-158">●</span></span> |
| <span data-ttu-id="5fe5f-159">以撥打電話做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-159">Phone call as second factor</span></span> | <span data-ttu-id="5fe5f-160">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-160">●</span></span> | <span data-ttu-id="5fe5f-161">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-161">●</span></span> |
| <span data-ttu-id="5fe5f-162">以單向 SMS 做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-162">One-way SMS as second factor</span></span> | <span data-ttu-id="5fe5f-163">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-163">●</span></span> | <span data-ttu-id="5fe5f-164">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-164">●</span></span> |
| <span data-ttu-id="5fe5f-165">以雙向 SMS 做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-165">Two-way SMS as second factor</span></span> | | <span data-ttu-id="5fe5f-166">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-166">●</span></span> |
| <span data-ttu-id="5fe5f-167">以硬體權杖做為第二個因素</span><span class="sxs-lookup"><span data-stu-id="5fe5f-167">Hardware Tokens as second factor</span></span> | | <span data-ttu-id="5fe5f-168">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-168">●</span></span> |
| <span data-ttu-id="5fe5f-169">不支援 MFA 之 Office 365 用戶端的應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="5fe5f-169">App passwords for Office 365 clients that don’t support MFA</span></span> | <span data-ttu-id="5fe5f-170">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-170">●</span></span> | |
| <span data-ttu-id="5fe5f-171">系統管理員控制驗證方法</span><span class="sxs-lookup"><span data-stu-id="5fe5f-171">Admin control over authentication methods</span></span> | <span data-ttu-id="5fe5f-172">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-172">●</span></span> | <span data-ttu-id="5fe5f-173">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-173">●</span></span> |
| <span data-ttu-id="5fe5f-174">PIN 模式</span><span class="sxs-lookup"><span data-stu-id="5fe5f-174">PIN mode</span></span> | | <span data-ttu-id="5fe5f-175">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-175">●</span></span> |
| <span data-ttu-id="5fe5f-176">詐騙警示</span><span class="sxs-lookup"><span data-stu-id="5fe5f-176">Fraud alert</span></span> |<span data-ttu-id="5fe5f-177">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-177">●</span></span> | <span data-ttu-id="5fe5f-178">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-178">●</span></span> |
| <span data-ttu-id="5fe5f-179">MFA 報告</span><span class="sxs-lookup"><span data-stu-id="5fe5f-179">MFA Reports</span></span> |<span data-ttu-id="5fe5f-180">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-180">●</span></span> | <span data-ttu-id="5fe5f-181">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-181">●</span></span> |
| <span data-ttu-id="5fe5f-182">一次性略過</span><span class="sxs-lookup"><span data-stu-id="5fe5f-182">One-Time Bypass</span></span> | | <span data-ttu-id="5fe5f-183">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-183">●</span></span> |
| <span data-ttu-id="5fe5f-184">通話的自訂問候語</span><span class="sxs-lookup"><span data-stu-id="5fe5f-184">Custom greetings for phone calls</span></span> | <span data-ttu-id="5fe5f-185">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-185">●</span></span> | <span data-ttu-id="5fe5f-186">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-186">●</span></span> |
| <span data-ttu-id="5fe5f-187">可自訂的通話來電者 ID</span><span class="sxs-lookup"><span data-stu-id="5fe5f-187">Customizable caller ID for phone calls</span></span> | <span data-ttu-id="5fe5f-188">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-188">●</span></span> | <span data-ttu-id="5fe5f-189">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-189">●</span></span> |
| <span data-ttu-id="5fe5f-190">信任的 IP</span><span class="sxs-lookup"><span data-stu-id="5fe5f-190">Trusted IPs</span></span> | <span data-ttu-id="5fe5f-191">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-191">●</span></span> | <span data-ttu-id="5fe5f-192">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-192">●</span></span> |
| <span data-ttu-id="5fe5f-193">記住受信任裝置的 MFA</span><span class="sxs-lookup"><span data-stu-id="5fe5f-193">Remember MFA for trusted devices</span></span> | <span data-ttu-id="5fe5f-194">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-194">●</span></span> | |
| <span data-ttu-id="5fe5f-195">條件式存取</span><span class="sxs-lookup"><span data-stu-id="5fe5f-195">Conditional access</span></span> | <span data-ttu-id="5fe5f-196">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-196">●</span></span> | <span data-ttu-id="5fe5f-197">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-197">●</span></span> |
| <span data-ttu-id="5fe5f-198">快取</span><span class="sxs-lookup"><span data-stu-id="5fe5f-198">Cache</span></span> |  | <span data-ttu-id="5fe5f-199">●</span><span class="sxs-lookup"><span data-stu-id="5fe5f-199">●</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5fe5f-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5fe5f-200">Next steps</span></span>

<span data-ttu-id="5fe5f-201">既然我們已判斷出要使用雲端 Multi-Factor Authentication 或內部部署 MFA Server，接下來可以開始設定及使用 Azure Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="5fe5f-201">Now that we have determined whether to use cloud multi-factor authentication or the MFA Server on-premises, we can get started setting up and using Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="5fe5f-202">**選取代表您案例的圖示**</span><span class="sxs-lookup"><span data-stu-id="5fe5f-202">**Select the icon that represents your scenario**</span></span>

<center>




<span data-ttu-id="5fe5f-203">[![雲端](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![伺服器](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span><span class="sxs-lookup"><span data-stu-id="5fe5f-203">[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Server](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center></span></span>
