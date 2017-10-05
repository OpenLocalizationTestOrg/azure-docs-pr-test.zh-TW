---
title: "Azure AD Connect：傳遞驗證 - 常見問題集 | Microsoft Docs"
description: "Azure Active Directory 傳遞驗證常見問題的解答。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: ded80330ad323a0019ad59ac54d076a78b70f521
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a><span data-ttu-id="c3ea4-104">Azure Active Directory 傳遞驗證：常見問題集</span><span class="sxs-lookup"><span data-stu-id="c3ea4-104">Azure Active Directory Pass-through Authentication: Frequently asked questions</span></span>

<span data-ttu-id="c3ea4-105">本文將會解決 Azure Active Directory (Azure AD) 傳遞驗證的常見問題。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-105">In this article, we address frequently asked questions about Azure Active Directory (Azure AD) Pass-through Authentication.</span></span> <span data-ttu-id="c3ea4-106">請隨時回來查看新內容。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-106">Keep checking back for new content.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3ea4-107">傳遞驗證功能目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-107">The Pass-through Authentication feature is currently in preview.</span></span>

## <a name="which-of-the-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a><span data-ttu-id="c3ea4-108">我應該選擇哪一種 Azure AD 登入方法，傳遞驗證、密碼雜湊同步處理還是 Active Directory 同盟服務 (AD FS)？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-108">Which of the Azure AD sign-in methods - Pass-through Authentication, Password Hash Synchronization and Active Directory Federation Services (AD FS) - should I choose?</span></span>

<span data-ttu-id="c3ea4-109">這取決於您的內部部署環境和組織需求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-109">It depends on your on-premises environment and organizational requirements.</span></span> <span data-ttu-id="c3ea4-110">請檢閱此文章以[比較各種 Azure AD 登入方法](active-directory-aadconnect-user-signin.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-110">Review this article for a [comparison of the various Azure AD sign-in methods](active-directory-aadconnect-user-signin.md).</span></span>

## <a name="is-pass-through-authentication-a-free-feature"></a><span data-ttu-id="c3ea4-111">傳遞驗證是否為免費功能？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-111">Is Pass-through Authentication a free feature?</span></span>

<span data-ttu-id="c3ea4-112">傳遞驗證是免費功能，您不需要擁有任何 Azure AD 付費版本即可使用此功能。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-112">Pass-through Authentication is a free feature and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="c3ea4-113">此功能正式運作時仍舊會免費提供使用。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-113">It remains free when the feature reaches general availability.</span></span>

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a><span data-ttu-id="c3ea4-114">[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 和 [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/) 是否有提供傳遞驗證功能？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-114">Is Pass-through Authentication available in [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/)?</span></span>

<span data-ttu-id="c3ea4-115">沒有，只有全球版的 Azure AD 執行個體會提供傳遞驗證功能。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-115">No, Pass-through Authentication is only available in the world-wide instance of Azure AD.</span></span>

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a><span data-ttu-id="c3ea4-116">[條件式存取](../active-directory-conditional-access.md)是否能與傳遞驗證搭配運作？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-116">Does [Conditional Access](../active-directory-conditional-access.md) work with Pass-through Authentication?</span></span>

<span data-ttu-id="c3ea4-117">是，所有條件式存取功能 (包括 Azure Multi-Factor Authentication) 都能與傳遞驗證搭配運作。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-117">Yes, all Conditional Access capabilities, including Azure Multi-Factor Authentication, work with Pass-through Authentication.</span></span>

## <a name="does-pass-through-authentication-support-alternate-id-as-the-username-instead-of-userprincipalname"></a><span data-ttu-id="c3ea4-118">傳遞驗證支援以「替代識別碼」而非「userPrincipalName」來作為使用者名稱嗎？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-118">Does Pass-through Authentication support "Alternate ID" as the username, instead of "userPrincipalName"?</span></span>

<span data-ttu-id="c3ea4-119">是。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-119">Yes.</span></span> <span data-ttu-id="c3ea4-120">如[這裡](active-directory-aadconnect-get-started-custom.md)所述，當您在 Azure AD Connect 中設定了傳遞驗證時，傳遞驗證會支援以 `Alternate ID` 來作為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-120">Pass-through Authentication supports `Alternate ID` as the username when configured in Azure AD Connect as shown [here](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="c3ea4-121">並非所有 Office 365 應用程式都支援 `Alternate ID`。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-121">Not all Office 365 applications support `Alternate ID`.</span></span> <span data-ttu-id="c3ea4-122">請參閱支援陳述式的特定應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-122">Refer to the specific application's documentation for the support statement.</span></span>

## <a name="does-password-hash-synchronization-act-as-a-fallback-to-pass-through-authentication"></a><span data-ttu-id="c3ea4-123">密碼雜湊同步處理是否會作為傳遞驗證的遞補？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-123">Does Password Hash Synchronization act as a fallback to Pass-through Authentication?</span></span>

<span data-ttu-id="c3ea4-124">不會，密碼雜湊同步處理不是傳遞驗證的一般遞補。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-124">No, Password Hash Synchronization is not a generic fallback to Pass-through Authentication.</span></span> <span data-ttu-id="c3ea4-125">它只會作為[目前不支援傳遞驗證的情況下](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios)的遞補。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-125">It only acts as a fallback for [scenarios that Pass-through Authentication doesn't support today](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios).</span></span> <span data-ttu-id="c3ea4-126">若要避免使用者登入失敗，您應該為傳遞驗證設定[高可用性](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-126">To avoid user sign-in failures, you should configure Pass-through Authentication for [high availability](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).</span></span>

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-the-same-server-as-a-pass-through-authentication-agent"></a><span data-ttu-id="c3ea4-127">能否在傳遞驗證代理程式所在的同一部伺服器上安裝 [Azure AD 應用程式 Proxy](../active-directory-application-proxy-get-started.md) 連接器？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-127">Can I install an [Azure AD Application Proxy](../active-directory-application-proxy-get-started.md) connector on the same server as a Pass-through Authentication Agent?</span></span>

<span data-ttu-id="c3ea4-128">是，傳遞驗證代理程式的改版版本 (1.5.193.0 版或更新版本) 支援此組態。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-128">Yes, this configuration is supported with the rebranded versions of the Pass-through Authentication Agent (versions 1.5.193.0 or later).</span></span>

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a><span data-ttu-id="c3ea4-129">需要哪些版本的 Azure AD Connect 和傳遞驗證代理程式？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-129">What versions of Azure AD Connect and Pass-through Authentication Agent do you need?</span></span>

<span data-ttu-id="c3ea4-130">您需要 Azure AD Connect 1.1.486.0 版或更新版本以及傳遞驗證代理程式 1.5.58.0 或更新版本，才能讓這項功能運作。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-130">You need version 1.1.486.0 or later for Azure AD Connect and 1.5.58.0 or later for the Pass-through Authentication Agent for this feature to work.</span></span> <span data-ttu-id="c3ea4-131">所有軟體都應該安裝在 Windows Server 2012 R2 或更新版本的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-131">All software should be installed on servers with Windows Server 2012 R2 or later.</span></span>

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-to-sign-in-using-pass-through-authentication"></a><span data-ttu-id="c3ea4-132">如果使用者的密碼過期又嘗試使用傳遞驗證來登入，會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-132">What happens if my user's password has expired and they try to sign in using Pass-through Authentication?</span></span>

<span data-ttu-id="c3ea4-133">如果您已經為特定使用者設定[密碼回寫](../active-directory-passwords-update-your-own-password.md)，而使用者又使用傳遞驗證來登入，則他們將能夠變更或重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-133">If you have configured [password writeback](../active-directory-passwords-update-your-own-password.md) for a specific user, and if the user signs in using Pass-through Authentication, they can change or reset their passwords.</span></span> <span data-ttu-id="c3ea4-134">密碼將會如預期般回寫至內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-134">The passwords are written back to on-premises Active Directory as expected.</span></span>

<span data-ttu-id="c3ea4-135">然而，如果您未為特定使用者設定密碼回寫，或使用者未獲指派有效的 Azure AD 授權，則使用者將無法在雲端中更新其密碼。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-135">However, if password writeback is not configured for a specific user or if the user doesn't have a valid Azure AD license assigned, the user can't update their password in the cloud.</span></span> <span data-ttu-id="c3ea4-136">即使他們的密碼過期，他們也無法加以更新。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-136">They can't update their password even if their password has expired.</span></span> <span data-ttu-id="c3ea4-137">使用者會看到這則訊息：「您的組織不允許您在此網站更新您的密碼。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-137">The user instead sees this message: "Your organization doesn't allow you to update your password on this site.</span></span> <span data-ttu-id="c3ea4-138">請依據您組織所建議的方法更新密碼，或洽詢您的管理員尋求協助。」</span><span class="sxs-lookup"><span data-stu-id="c3ea4-138">Please update it according to the method recommended by your organization, or ask your admin if you need help."</span></span> <span data-ttu-id="c3ea4-139">使用者或系統管理員必須在內部部署 Active Directory 中重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-139">The user or the administrator has to reset their password in your on-premises Active Directory.</span></span>

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a><span data-ttu-id="c3ea4-140">傳遞驗證如何防範暴力密碼破解攻擊？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-140">How does Pass-through Authentication protect you against brute force password attacks?</span></span>

<span data-ttu-id="c3ea4-141">如需詳細資訊，請閱讀[這篇文章](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-141">Read [this article](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) for more information.</span></span>

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a><span data-ttu-id="c3ea4-142">傳遞驗證代理程式會透過連接埠 80 和 443 進行哪些方面的通訊？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-142">What do Pass-through Authentication Agents communicate over ports 80 and 443?</span></span>

- <span data-ttu-id="c3ea4-143">驗證代理程式會透過連接埠 443 對所有功能作業進行 HTTPS 要求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-143">The Authentication Agents make HTTPS requests over port 443 for all feature operations.</span></span>
- <span data-ttu-id="c3ea4-144">驗證代理程式會透過連接埠 80 提出 HTTP 要求，以下載 SSL 憑證撤銷清單。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-144">The Authentication Agents make HTTP requests over port 80 to download SSL certificate revocation lists.</span></span>

     >[!NOTE]
     ><span data-ttu-id="c3ea4-145">在最近的更新中，我們減少了此功能所需的連接埠數目。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-145">In recent updates we reduced the number of ports required by the feature.</span></span> <span data-ttu-id="c3ea4-146">如果您有舊版的 Azure AD Connect 或驗證代理程式，請將下列連接埠保持開放：5671、8080、9090、9091、9350、9352、10100-10120。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-146">If you have older versions of Azure AD Connect or the Authentication Agent, keep these ports also open: 5671, 8080, 9090, 9091, 9350, 9352 and 10100-10120.</span></span>

## <a name="can-the-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a><span data-ttu-id="c3ea4-147">傳遞驗證代理程式是否能透過輸出 Web Proxy 伺服器進行通訊？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-147">Can the Pass-through Authentication Agents communicate over an outbound web proxy server?</span></span>

<span data-ttu-id="c3ea4-148">是。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-148">Yes.</span></span> <span data-ttu-id="c3ea4-149">如果您的內部部署環境啟用了 WPAD (Web Proxy 自動探索)，則驗證代理程式會自動嘗試在網路上找出並使用 Web Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-149">If WPAD (Web Proxy Auto-Discovery) is enabled in your on-premises environment,  Authentication Agents automatically attempt to locate and use a web proxy server on the network.</span></span>

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-the-same-server"></a><span data-ttu-id="c3ea4-150">是否可以在相同的伺服器上安裝兩個以上的傳遞驗證代理程式？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-150">Can I install two or more Pass-through Authentication Agents on the same server?</span></span>

<span data-ttu-id="c3ea4-151">不可以，您只能在單一伺服器上安裝一個傳遞驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-151">No, you can only install one Pass-through Authentication Agent on a single server.</span></span> <span data-ttu-id="c3ea4-152">如果您想要為傳遞驗證設定高可用性，請改為遵循這篇[文章](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)中的指示。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-152">If you want to configure Pass-through Authentication for high availability, follow the instructions in this [article](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) instead.</span></span>

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-to-pass-through-authentication"></a><span data-ttu-id="c3ea4-153">我已經使用 Active Directory 同盟服務 (AD FS) 來進行 Azure AD 登入。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-153">I already use Active Directory Federation Services (AD FS) for Azure AD sign-in.</span></span> <span data-ttu-id="c3ea4-154">要如何改為使用傳遞驗證？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-154">How do I switch it to Pass-through Authentication?</span></span>

<span data-ttu-id="c3ea4-155">如果您已經使用 Azure AD Connect 精靈將 AD FS 設定為您的登入方法，請將使用者的登入方法變更為傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-155">If you have configured AD FS as your sign-in method using the Azure AD Connect wizard, change the user sign-in method to Pass-through Authentication.</span></span> <span data-ttu-id="c3ea4-156">這項變更會讓租用戶啟用傳遞驗證，並將您「所有」的同盟網域轉換為受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-156">This change enables Pass-through Authentication on the tenant and converts _all_ your Federated domains into Managed domains.</span></span> <span data-ttu-id="c3ea4-157">租用戶所有的後續登入要求都會由傳遞驗證來進行處理。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-157">All subsequent sign-in requests in your tenant are handled by Pass-through Authentication.</span></span> <span data-ttu-id="c3ea4-158">Azure AD Connect 內目前沒有任何支援的方法可跨不同網域使用 AD FS 和傳遞驗證的組合。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-158">Currently, there is no supported way within Azure AD Connect to use a combination of AD FS and Pass-through Authentication across different domains.</span></span>

<span data-ttu-id="c3ea4-159">如果 AD FS 已從 Azure AD Connect 精靈「之外」設為登入方法，請將使用者的登入方法變更為傳遞驗證 (從 [不設定] 選項)。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-159">If AD FS was configured as the sign-in method _outside_ of the Azure AD Connect wizard, change the user sign-in method to Pass-through Authentication (from the "Do not configure" option).</span></span> <span data-ttu-id="c3ea4-160">這項變更會讓租用戶啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-160">This change enables Pass-through Authentication on the tenant.</span></span> <span data-ttu-id="c3ea4-161">不過，您所有的同盟網域都會繼續使用 AD FS 來進行登入。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-161">However all your Federated domains continue to use AD FS for sign-in.</span></span> <span data-ttu-id="c3ea4-162">請使用 PowerShell 以手動方式將其中的部分或所有同盟網域轉換為受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-162">Use PowerShell to manually convert some or all these Federated domains to Managed domains.</span></span> <span data-ttu-id="c3ea4-163">完成後，受管理的網域上的所有登入要求便 (只) 會由傳遞驗證來進行處理。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-163">After that all sign-in requests on Managed domains (_only_) are handled by Pass-through Authentication.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3ea4-164">傳遞驗證不會為僅限雲端的 Azure AD 使用者處理登入要求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-164">Pass-through Authentication doesn't handle sign-in for cloud-only Azure AD users.</span></span>

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a><span data-ttu-id="c3ea4-165">是否可以在多樹系 AD 環境中使用傳遞驗證？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-165">Can I use Pass-through Authentication in a multi-forest AD environment?</span></span>

<span data-ttu-id="c3ea4-166">是。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-166">Yes.</span></span> <span data-ttu-id="c3ea4-167">如果 AD 樹系之間有樹系信任且名稱尾碼路由已正確設定，就支援多樹系環境。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-167">Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.</span></span>

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a><span data-ttu-id="c3ea4-168">傳遞驗證代理程式是否提供負載平衡功能？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-168">Do Pass-through Authentication Agents provide load balancing capability?</span></span>

<span data-ttu-id="c3ea4-169">否，安裝多個傳遞驗證代理程式可確保[高可用性](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)，但不會提供負載平衡。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-169">No, installing multiple Pass-through Authentication Agents ensures [high availability](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), but not load balancing.</span></span> <span data-ttu-id="c3ea4-170">最後可能會由其中的一個或兩個驗證代理程式處理大量的登入要求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-170">One or two of the Authentication Agents may end up handling the bulk of the sign-in requests.</span></span>

<span data-ttu-id="c3ea4-171">驗證代理程式所需要處理的密碼驗證要求並不多。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-171">Password validation requests that the Authentication Agents need to handle are lightweight.</span></span> <span data-ttu-id="c3ea4-172">因此對大多數客戶來說，總共只要兩到三個驗證代理程式就能輕鬆應付尖峰負載和平均負載。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-172">Therefore peak and average load for most customers is easily handled by two or three Authentication Agents in total.</span></span>

<span data-ttu-id="c3ea4-173">我們的建議是，您可以在靠近網域控制站的地方安裝驗證代理程式，以改善登入的延遲情形。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-173">We recommend that you install Authentication Agents close to your Domain Controllers to improve sign-in latency.</span></span>

## <a name="can-i-install-the-first-pass-through-authentication-agent-on-a-server-other-than-the-one-that-runs-azure-ad-connect"></a><span data-ttu-id="c3ea4-174">是否可以在不同於 Azure AD Connect 執行所在伺服器的某個伺服器上安裝第一個傳遞驗證代理程式？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-174">Can I install the first Pass-through Authentication Agent on a server other than the one that runs Azure AD Connect?</span></span>

<span data-ttu-id="c3ea4-175">不行，「不」支援這種情況。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-175">No, this scenario is _not_ supported.</span></span>

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a><span data-ttu-id="c3ea4-176">應該安裝幾個傳遞驗證代理程式？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-176">How many Pass-through Authentication Agents should I install?</span></span>

<span data-ttu-id="c3ea4-177">我們的建議如下：</span><span class="sxs-lookup"><span data-stu-id="c3ea4-177">We recommend that:</span></span>

- <span data-ttu-id="c3ea4-178">總共安裝兩到三個驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-178">You install two or three Authentication Agents in total.</span></span> <span data-ttu-id="c3ea4-179">此設定足以應付大部分客戶的需求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-179">This configuration is sufficient for most customers.</span></span>
- <span data-ttu-id="c3ea4-180">您可以在網域控制站上 (或盡可能靠近地) 安裝驗證代理程式，以改善登入延遲情形。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-180">You install Authentication Agents on your Domain Controllers (or as close to them as possible) to improve sign-in latency.</span></span>
- <span data-ttu-id="c3ea4-181">您應該確保用來新增伺服器 (驗證代理程式安裝所在地) 的 AD 樹系，就是需要驗證密碼之使用者所在的相同樹系。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-181">You ensure that servers (where Authentication Agents are installed) are added to the same AD forest as the users whose passwords need to be validated.</span></span>

>[!NOTE]
><span data-ttu-id="c3ea4-182">系統限制每個租用戶只能有 12 個驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-182">There is a system limit of 12 Authentication Agents per tenant.</span></span>

## <a name="how-can-i-disable-pass-through-authentication"></a><span data-ttu-id="c3ea4-183">如何停用傳遞驗證？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-183">How can I disable Pass-through Authentication?</span></span>

<span data-ttu-id="c3ea4-184">重新執行 Azure AD Connect 精靈，並將使用者的登入方法從傳遞驗證變更為其他方法。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-184">Rerun the Azure AD Connect wizard and change the user sign-in method from Pass-through Authentication to another method.</span></span> <span data-ttu-id="c3ea4-185">這項變更會讓租用戶停用傳遞驗證，並從該伺服器解除安裝驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-185">This change disables Pass-through Authentication on the tenant and uninstalls the Authentication Agent from the server.</span></span> <span data-ttu-id="c3ea4-186">至於其他伺服器的驗證代理程式，則必須手動解除安裝。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-186">You have to manually uninstall the Authentication Agents from other servers.</span></span>

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a><span data-ttu-id="c3ea4-187">解除安裝傳遞驗證代理程式會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c3ea4-187">What happens when I uninstall a Pass-through Authentication Agent?</span></span>

<span data-ttu-id="c3ea4-188">從伺服器解除安裝傳遞驗證代理程式，會讓該伺服器不再接受登入要求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-188">Uninstalling a Pass-through Authentication Agent from a server causes it to stop accepting sign-in requests.</span></span> <span data-ttu-id="c3ea4-189">在執行這項操作之前，請先確定您有其他執行中的驗證代理程式，以免使用者無法登入您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-189">Ensure that you have another Authentication Agent running before doing this operation, to avoid breaking user sign-in on your tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ea4-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3ea4-190">Next steps</span></span>
- <span data-ttu-id="c3ea4-191">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-191">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="c3ea4-192">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-192">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="c3ea4-193">[**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-193">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="c3ea4-194">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-194">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="c3ea4-195">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-195">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="c3ea4-196">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-196">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="c3ea4-197">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="c3ea4-197">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
