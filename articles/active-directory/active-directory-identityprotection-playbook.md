---
title: "Azure Active Directory Identity Protection 腳本 | Microsoft Docs"
description: "了解 Azure AD Identity Protection 如何讓您限制攻擊者利用遭入侵的身分識別或裝置的能力，以及保護先前疑似或已知遭到入侵的身分識別或裝置。"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, 管理應用程式, 安全性, 風險, 風險層級, 弱點, 安全性原則"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="5837c-104">Azure Active Directory Identity Protection 腳本</span><span class="sxs-lookup"><span data-stu-id="5837c-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="5837c-105">這個腳本可協助您︰</span><span class="sxs-lookup"><span data-stu-id="5837c-105">This playbook helps you to:</span></span>

* <span data-ttu-id="5837c-106">藉由模擬風險事件和弱點，在 Identity Protection 環境中填入資料</span><span class="sxs-lookup"><span data-stu-id="5837c-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="5837c-107">設定以風險為基礎的條件式存取原則，並測試這些原則的影響</span><span class="sxs-lookup"><span data-stu-id="5837c-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="5837c-108">模擬風險事件</span><span class="sxs-lookup"><span data-stu-id="5837c-108">Simulating Risk Events</span></span>
<span data-ttu-id="5837c-109">本節將為您提供模擬下列風險事件類型的步驟：</span><span class="sxs-lookup"><span data-stu-id="5837c-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="5837c-110">從匿名 IP 位址登入 (容易)</span><span class="sxs-lookup"><span data-stu-id="5837c-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="5837c-111">從不熟悉的位置登入 (適中)</span><span class="sxs-lookup"><span data-stu-id="5837c-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="5837c-112">不可能到達非典型位置的移動 (困難)</span><span class="sxs-lookup"><span data-stu-id="5837c-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="5837c-113">無法以安全的方式模擬其他風險事件。</span><span class="sxs-lookup"><span data-stu-id="5837c-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="5837c-114">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="5837c-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="5837c-115">此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="5837c-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="5837c-116">這些 Proxy 通常由想要隱藏其裝置 IP 位址的人員使用，而且可能用於惡意意圖。</span><span class="sxs-lookup"><span data-stu-id="5837c-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="5837c-117">**若要模擬從匿名 IP 登入，請執行下列步驟**：</span><span class="sxs-lookup"><span data-stu-id="5837c-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="5837c-118">下載 [Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en)。</span><span class="sxs-lookup"><span data-stu-id="5837c-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="5837c-119">使用 Tor 瀏覽器，瀏覽至 [https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5837c-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="5837c-120">輸入您要在 [從匿名 IP 位址登入]  報告中顯示之帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="5837c-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="5837c-121">登入將會在 5 分鐘內顯示於 Identity Protection 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5837c-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="5837c-122">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="5837c-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="5837c-123">不熟悉的位置風險是一種即時登入評估機制，它會考量過去的登入位置 (IP、經緯度和 ASN) 以判斷新的 / 不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="5837c-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="5837c-124">系統會儲存使用者先前的 IP、經緯度和 ASN，並將這些視為熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="5837c-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="5837c-125">如果登入位置不符合任何現有的熟悉位置，此登入位置會被視為不熟悉。</span><span class="sxs-lookup"><span data-stu-id="5837c-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="5837c-126">Azure Active Directory Identity Protection：</span><span class="sxs-lookup"><span data-stu-id="5837c-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="5837c-127">有為期 14 天的初始學習期間，在這段期間內，它不會將任何新位置標示為不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="5837c-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="5837c-128">忽略從熟悉的裝置以及地理上靠近現有熟悉位置的位置進行的登入。</span><span class="sxs-lookup"><span data-stu-id="5837c-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="5837c-129">若要模擬不熟悉的位置，您必須從帳戶未曾用來登入的位置和裝置進行登入。</span><span class="sxs-lookup"><span data-stu-id="5837c-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="5837c-130">**若要模擬從不熟悉的位置登入，請執行下列步驟**：</span><span class="sxs-lookup"><span data-stu-id="5837c-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="5837c-131">選擇至少有 14 天登入歷程記錄的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5837c-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="5837c-132">請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="5837c-132">Do either:</span></span>
   
   <span data-ttu-id="5837c-133">a.</span><span class="sxs-lookup"><span data-stu-id="5837c-133">a.</span></span> <span data-ttu-id="5837c-134">使用 VPN 時，請瀏覽至 [https://myapps.microsoft.com](https://myapps.microsoft.com)，然後輸入您要用於模擬風險事件之帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="5837c-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="5837c-135">b.</span><span class="sxs-lookup"><span data-stu-id="5837c-135">b.</span></span> <span data-ttu-id="5837c-136">要求不同位置的關聯以使用帳戶的認證進行登入 (不建議)。</span><span class="sxs-lookup"><span data-stu-id="5837c-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="5837c-137">登入將會在 5 分鐘內顯示於 Identity Protection 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5837c-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="5837c-138">不可能到達非典型位置的移動</span><span class="sxs-lookup"><span data-stu-id="5837c-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="5837c-139">模擬不可能的移動情況相當困難，因為此演算法會使用機器學習服務來剔除誤判，例如，不可能來自熟悉裝置的移動，或從目錄中其他使用者所用的 VPN 登入。</span><span class="sxs-lookup"><span data-stu-id="5837c-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="5837c-140">此外，此演算法在開始產生風險事件之前，需要使用者 3 到 14 天的登入歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="5837c-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="5837c-141">**若要模擬不可能到達非典型位置的移動，請執行下列步驟**：</span><span class="sxs-lookup"><span data-stu-id="5837c-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="5837c-142">使用標準瀏覽器，瀏覽至 [https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="5837c-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="5837c-143">輸入您想要對其產生不可能移動風險事件之帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="5837c-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="5837c-144">變更您的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="5837c-144">Change your user agent.</span></span> <span data-ttu-id="5837c-145">您可以在 Internet Explorer 中從 [開發人員工具] 變更使用者代理程式，或在 Firefox 或 Chrome 中使用使用者代理程式切換器附加元件來變更您的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="5837c-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="5837c-146">變更您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5837c-146">Change your IP address.</span></span> <span data-ttu-id="5837c-147">使用 VPN、Tor 附加元件，或在不同資料中心於 Azure 中啟動新機器，即可變更您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5837c-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="5837c-148">在前次登入之後的幾分鐘內，使用與之前相同的認證登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="5837c-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="5837c-149">登入將會在 2-4 小時內顯示於 Identity Protection 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5837c-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="5837c-150">因為牽涉到複雜的機器學習服務模型，所以可能達不到。</span><span class="sxs-lookup"><span data-stu-id="5837c-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="5837c-151">您可能想要針對多個 Azure AD 帳戶複製這些步驟。</span><span class="sxs-lookup"><span data-stu-id="5837c-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="5837c-152">模擬弱點</span><span class="sxs-lookup"><span data-stu-id="5837c-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="5837c-153">弱點是 Azure AD 環境中不良執行者可以利用的弱點。</span><span class="sxs-lookup"><span data-stu-id="5837c-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="5837c-154">Azure AD Identity Protection 中目前顯示 3 種會運用其他 Azure AD 功能的弱點。</span><span class="sxs-lookup"><span data-stu-id="5837c-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="5837c-155">一旦設定好這些功能，這些弱點就會自動顯示在 Identity Protection 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="5837c-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="5837c-156">Azure AD [Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="5837c-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="5837c-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5837c-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="5837c-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="5837c-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="5837c-159">使用者入侵風險</span><span class="sxs-lookup"><span data-stu-id="5837c-159">User compromise risk</span></span>
<span data-ttu-id="5837c-160">**若要測試使用者入侵風險，請執行下列步驟**：</span><span class="sxs-lookup"><span data-stu-id="5837c-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="5837c-161">使用租用戶的全域管理員認證來登入 [https://portal.azure.com](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="5837c-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="5837c-162">瀏覽至 [Identity Protection] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="5837c-163">在主要的 [Azure AD Identity Protection] 刀鋒視窗上，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="5837c-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="5837c-164">在 [入口網站設定] 刀鋒視窗的 [安全性規則] 之下，按一下 [使用者入侵風險]。</span><span class="sxs-lookup"><span data-stu-id="5837c-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="5837c-165">在 [登入風險] 刀鋒視窗上，關閉 [啟用規則]，然後按一下 [儲存] 設定。</span><span class="sxs-lookup"><span data-stu-id="5837c-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="5837c-166">對於指定的使用者帳戶，模擬不熟悉位置或匿名 IP 風險事件。</span><span class="sxs-lookup"><span data-stu-id="5837c-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="5837c-167">這會將該使用者的使用者風險層級提升至 [中] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="5837c-168">等候幾分鐘，然後確認使用者的使用者層級為 [中] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="5837c-169">移至 [入口網站設定]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="5837c-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="5837c-170">在 [使用者入侵風險] 刀鋒視窗的 [啟用規則] 之下，選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="5837c-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="5837c-171">選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="5837c-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="5837c-172">a.</span><span class="sxs-lookup"><span data-stu-id="5837c-172">a.</span></span> <span data-ttu-id="5837c-173">若要封鎖，請選取 [封鎖登入] 之下的 [中]。</span><span class="sxs-lookup"><span data-stu-id="5837c-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="5837c-174">b.</span><span class="sxs-lookup"><span data-stu-id="5837c-174">b.</span></span> <span data-ttu-id="5837c-175">若要強制執行安全的密碼變更，請選取 [需要 Multi-Factor Authentication] 之下的 [中]。</span><span class="sxs-lookup"><span data-stu-id="5837c-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="5837c-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-176">Click **Save**.</span></span>
12. <span data-ttu-id="5837c-177">您現在可以使用具有提高風險等級的使用者進行登入，以測試以風險為基礎的條件式存取。</span><span class="sxs-lookup"><span data-stu-id="5837c-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="5837c-178">如果使用者風險為「中」，則視您的原則設定而定，您的登入會被封鎖，或者會強制您變更密碼。</span><span class="sxs-lookup"><span data-stu-id="5837c-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="5837c-179">
    ![腳本](./media/active-directory-identityprotection-playbook/201.png "腳本")
    </span><span class="sxs-lookup"><span data-stu-id="5837c-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="5837c-180">登入風險</span><span class="sxs-lookup"><span data-stu-id="5837c-180">Sign-in risk</span></span>
<span data-ttu-id="5837c-181">**若要測試登入風險，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="5837c-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="5837c-182">使用租用戶的全域管理員認證來登入 [https://portal.azure.com ](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="5837c-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="5837c-183">瀏覽至 [Identity Protection] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="5837c-184">在主要的 [Azure AD Identity Protection] 刀鋒視窗上，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="5837c-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="5837c-185">在 [入口網站設定] 刀鋒視窗的 [安全性規則] 之下，按一下 [登入風險]。</span><span class="sxs-lookup"><span data-stu-id="5837c-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="5837c-186">在 * * 登入風險 * * 刀鋒視窗中，選取**上**下**規則啟用**。</span><span class="sxs-lookup"><span data-stu-id="5837c-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="5837c-187">選取下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="5837c-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="5837c-188">a.</span><span class="sxs-lookup"><span data-stu-id="5837c-188">a.</span></span> <span data-ttu-id="5837c-189">若要封鎖，請選取 [封鎖登入] 之下的 [中]</span><span class="sxs-lookup"><span data-stu-id="5837c-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="5837c-190">b.</span><span class="sxs-lookup"><span data-stu-id="5837c-190">b.</span></span> <span data-ttu-id="5837c-191">若要強制執行安全的密碼變更，請選取 [需要 Multi-Factor Authentication] 之下的 [中]。</span><span class="sxs-lookup"><span data-stu-id="5837c-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="5837c-192">若要封鎖，請選取 [封鎖登入] 之下的 [中]。</span><span class="sxs-lookup"><span data-stu-id="5837c-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="5837c-193">若要強制執行 Multi-Factor Authentication，請選取 [需要 Multi-Factor Authentication] 之下的 [中]。</span><span class="sxs-lookup"><span data-stu-id="5837c-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="5837c-194">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5837c-194">Click on **Save**.</span></span>
10. <span data-ttu-id="5837c-195">您現在可以藉由模擬不熟悉的位置或匿名 IP 風險事件 (因為它們都是 [中]  風險事件)，測試以風險為基礎的條件式存取。</span><span class="sxs-lookup"><span data-stu-id="5837c-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="5837c-196">![腳本](./media/active-directory-identityprotection-playbook/200.png "腳本")</span><span class="sxs-lookup"><span data-stu-id="5837c-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="5837c-197">另請參閱</span><span class="sxs-lookup"><span data-stu-id="5837c-197">See also</span></span>
* [<span data-ttu-id="5837c-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="5837c-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

