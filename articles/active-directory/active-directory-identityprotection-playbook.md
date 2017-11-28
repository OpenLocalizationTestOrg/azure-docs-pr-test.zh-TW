---
title: "aaaAzure Active Directory 識別身分保護腳本 |Microsoft 文件"
description: "了解如何 Azure AD Identity Protection 可讓您 toolimit hello 能力，攻擊者 tooexploit 遭盜用身分識別的裝置或 toosecure 盜用身分識別或先前已 toobe 可疑或已知的裝置。"
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
ms.openlocfilehash: 6252bc133fc0c0f84800ee245a04bbf62d4cd25b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="45e4a-104">Azure Active Directory Identity Protection 腳本</span><span class="sxs-lookup"><span data-stu-id="45e4a-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="45e4a-105">這個腳本可協助您︰</span><span class="sxs-lookup"><span data-stu-id="45e4a-105">This playbook helps you to:</span></span>

* <span data-ttu-id="45e4a-106">Hello 識別身分保護環境中的資料填入模擬的風險事件和弱點</span><span class="sxs-lookup"><span data-stu-id="45e4a-106">Populate data in hello Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="45e4a-107">設定 風險為基礎的條件式存取原則和測試 hello 這些原則的影響</span><span class="sxs-lookup"><span data-stu-id="45e4a-107">Set up risk-based conditional access policies and test hello impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="45e4a-108">模擬風險事件</span><span class="sxs-lookup"><span data-stu-id="45e4a-108">Simulating Risk Events</span></span>
<span data-ttu-id="45e4a-109">此章節提供您的步驟來模擬 hello 下列風險事件類型：</span><span class="sxs-lookup"><span data-stu-id="45e4a-109">This section provides you with steps for simulating hello following risk event types:</span></span>

* <span data-ttu-id="45e4a-110">從匿名 IP 位址登入 (容易)</span><span class="sxs-lookup"><span data-stu-id="45e4a-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="45e4a-111">從不熟悉的位置登入 (適中)</span><span class="sxs-lookup"><span data-stu-id="45e4a-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="45e4a-112">不可能的旅遊 tooatypical 位置 （困難）</span><span class="sxs-lookup"><span data-stu-id="45e4a-112">Impossible travel tooatypical locations (difficult)</span></span>

<span data-ttu-id="45e4a-113">無法以安全的方式模擬其他風險事件。</span><span class="sxs-lookup"><span data-stu-id="45e4a-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="45e4a-114">從匿名 IP 位址登入</span><span class="sxs-lookup"><span data-stu-id="45e4a-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="45e4a-115">此風險事件類型會識別從被視為匿名 Proxy IP 位址的 IP 位址成功登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="45e4a-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="45e4a-116">這些 proxy 是 toohide 的人使用其裝置的 IP 位址，並可用於被用於惡意用途。</span><span class="sxs-lookup"><span data-stu-id="45e4a-116">These proxies are used by people who want toohide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="45e4a-117">**登入的 toosimulate 從匿名 IP，執行下列步驟的 hello**:</span><span class="sxs-lookup"><span data-stu-id="45e4a-117">**toosimulate a sign-in from an anonymous IP, perform hello following steps**:</span></span>

1. <span data-ttu-id="45e4a-118">下載 hello [Tor 瀏覽器](https://www.torproject.org/projects/torbrowser.html.en)。</span><span class="sxs-lookup"><span data-stu-id="45e4a-118">Download hello [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="45e4a-119">太使用 hello Tor 瀏覽器中，瀏覽[https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="45e4a-119">Using hello Tor Browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="45e4a-120">輸入您想要在 hello tooappear hello 帳戶 hello 認證**從匿名 IP 位址的登入**報表。</span><span class="sxs-lookup"><span data-stu-id="45e4a-120">Enter hello credentials of hello account you want tooappear in hello **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="45e4a-121">hello 登入將會出現在 hello Identity Protection 儀表板在 5 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="45e4a-121">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="45e4a-122">從不熟悉的位置登入</span><span class="sxs-lookup"><span data-stu-id="45e4a-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="45e4a-123">hello 不熟悉位置風險是即時的登入的評估機制，會考慮過去的登入位置 (IP、 緯度 / 經度和 ASN) toodetermine 新 / 不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="45e4a-123">hello unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) toodetermine new / unfamiliar locations.</span></span> <span data-ttu-id="45e4a-124">hello 系統會將儲存先前 Ip 時，緯度 / 經度和使用者的 Asn 會視這些 toobe 熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="45e4a-124">hello system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these toobe familiar locations.</span></span> <span data-ttu-id="45e4a-125">登入位置會被視為不熟悉，如果 hello 登入位置不符合任何 hello 現有熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="45e4a-125">A sign-in location is considered unfamiliar if hello sign-in location does not match any of hello existing familiar locations.</span></span>

<span data-ttu-id="45e4a-126">Azure Active Directory Identity Protection：</span><span class="sxs-lookup"><span data-stu-id="45e4a-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="45e4a-127">有為期 14 天的初始學習期間，在這段期間內，它不會將任何新位置標示為不熟悉的位置。</span><span class="sxs-lookup"><span data-stu-id="45e4a-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="45e4a-128">會忽略從熟悉的裝置和位置的地理位置關閉 tooan 現有熟悉位置登入。</span><span class="sxs-lookup"><span data-stu-id="45e4a-128">ignores sign-ins from familiar devices and locations that are geographically close tooan existing familiar location.</span></span>

<span data-ttu-id="45e4a-129">toosimulate 不熟悉位置，您有 toosign 從位置和 hello 帳戶沒有登入從之前的裝置。</span><span class="sxs-lookup"><span data-stu-id="45e4a-129">toosimulate unfamiliar locations, you have toosign in from a location and device that hello account has not signed in from before.</span></span> 

<span data-ttu-id="45e4a-130">**toosimulate 登入，從不熟悉的位置，執行下列步驟的 hello**:</span><span class="sxs-lookup"><span data-stu-id="45e4a-130">**toosimulate a sign-in from an unfamiliar location, perform hello following steps**:</span></span>

1. <span data-ttu-id="45e4a-131">選擇至少有 14 天登入歷程記錄的帳戶。</span><span class="sxs-lookup"><span data-stu-id="45e4a-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="45e4a-132">請執行下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="45e4a-132">Do either:</span></span>
   
   <span data-ttu-id="45e4a-133">a.</span><span class="sxs-lookup"><span data-stu-id="45e4a-133">a.</span></span> <span data-ttu-id="45e4a-134">在使用 VPN 時，瀏覽過[https://myapps.microsoft.com](https://myapps.microsoft.com)並輸入您想 toosimulate hello 風險事件的 hello 帳戶 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="45e4a-134">While using a VPN, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com) and enter hello credentials of hello account you want toosimulate hello risk event for.</span></span>
   
   <span data-ttu-id="45e4a-135">b.</span><span class="sxs-lookup"><span data-stu-id="45e4a-135">b.</span></span> <span data-ttu-id="45e4a-136">要求中使用 hello 帳戶的認證 （不建議使用） 中的不同位置 toosign 關聯。</span><span class="sxs-lookup"><span data-stu-id="45e4a-136">Ask an associate in a different location toosign in using hello account’s credentials (not recommended).</span></span>

<span data-ttu-id="45e4a-137">hello 登入將會出現在 hello Identity Protection 儀表板在 5 分鐘內。</span><span class="sxs-lookup"><span data-stu-id="45e4a-137">hello sign-in will show up on hello Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-tooatypical-location"></a><span data-ttu-id="45e4a-138">不可能的旅遊 tooatypical 位置</span><span class="sxs-lookup"><span data-stu-id="45e4a-138">Impossible travel tooatypical location</span></span>
<span data-ttu-id="45e4a-139">模擬 hello 不可能的旅遊條件是很困難，因為 hello 演算法會使用機器學習 tooweed 出 false-誤判，例如不可能的旅遊從熟悉的裝置或從 Vpn 所使用的 hello 目錄中的其他使用者的登入。</span><span class="sxs-lookup"><span data-stu-id="45e4a-139">Simulating hello impossible travel condition is difficult because hello algorithm uses machine learning tooweed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in hello directory.</span></span> <span data-ttu-id="45e4a-140">此外，hello 演算法需要登入的歷程記錄 3 too14 天 hello 使用者後，才開始產生風險的事件。</span><span class="sxs-lookup"><span data-stu-id="45e4a-140">Additionally, hello algorithm requires a sign-in history of 3 too14 days for hello user before it begins generating risk events.</span></span>

<span data-ttu-id="45e4a-141">**toosimulate 不可能的旅遊 tooatypical 位置中，執行下列步驟的 hello**:</span><span class="sxs-lookup"><span data-stu-id="45e4a-141">**toosimulate an impossible travel tooatypical location, perform hello following steps**:</span></span>

1. <span data-ttu-id="45e4a-142">使用標準的瀏覽器，巡覽太[https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="45e4a-142">Using your standard browser, navigate too[https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="45e4a-143">輸入您想 toogenerate 不可能的旅遊風險事件的 hello 帳戶 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="45e4a-143">Enter hello credentials of hello account you want toogenerate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="45e4a-144">變更您的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="45e4a-144">Change your user agent.</span></span> <span data-ttu-id="45e4a-145">您可以在 Internet Explorer 中從 [開發人員工具] 變更使用者代理程式，或在 Firefox 或 Chrome 中使用使用者代理程式切換器附加元件來變更您的使用者代理程式。</span><span class="sxs-lookup"><span data-stu-id="45e4a-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="45e4a-146">變更您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="45e4a-146">Change your IP address.</span></span> <span data-ttu-id="45e4a-147">使用 VPN、Tor 附加元件，或在不同資料中心於 Azure 中啟動新機器，即可變更您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="45e4a-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="45e4a-148">登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)使用 hello 之前和之後 hello 先前登入在幾分鐘內相同的認證。</span><span class="sxs-lookup"><span data-stu-id="45e4a-148">Sign-in too[https://myapps.microsoft.com](https://myapps.microsoft.com) using hello same credentials as before and within a few minutes after hello previous sign-in.</span></span>

<span data-ttu-id="45e4a-149">hello 登入將會顯示在 hello Identity Protection 儀表板 2-4 小時內。</span><span class="sxs-lookup"><span data-stu-id="45e4a-149">hello sign-in will show up in hello Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="45e4a-150">Hello 複雜機器學習所涉及的模型，因為沒有的機會，它將無法取得挑選。</span><span class="sxs-lookup"><span data-stu-id="45e4a-150">Because of hello complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="45e4a-151">您可能希望 tooreplicate 步驟執行多個 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="45e4a-151">You might want tooreplicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="45e4a-152">模擬弱點</span><span class="sxs-lookup"><span data-stu-id="45e4a-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="45e4a-153">弱點是 Azure AD 環境中不良執行者可以利用的弱點。</span><span class="sxs-lookup"><span data-stu-id="45e4a-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="45e4a-154">Azure AD Identity Protection 中目前顯示 3 種會運用其他 Azure AD 功能的弱點。</span><span class="sxs-lookup"><span data-stu-id="45e4a-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="45e4a-155">這些弱點會自動顯示 hello Identity Protection 儀表板上設定這些功能之後。</span><span class="sxs-lookup"><span data-stu-id="45e4a-155">These Vulnerabilities will be displayed on hello Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="45e4a-156">Azure AD [Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="45e4a-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="45e4a-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="45e4a-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="45e4a-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="45e4a-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="45e4a-159">使用者入侵風險</span><span class="sxs-lookup"><span data-stu-id="45e4a-159">User compromise risk</span></span>
<span data-ttu-id="45e4a-160">**tootest 使用者危害的風險，執行下列步驟的 hello**:</span><span class="sxs-lookup"><span data-stu-id="45e4a-160">**tootest User compromise risk, perform hello following steps**:</span></span>

1. <span data-ttu-id="45e4a-161">登入太[https://portal.azure.com](https://portal.azure.com)與您的租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="45e4a-161">Sign-in too[https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="45e4a-162">瀏覽過**Identity Protection**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-162">Navigate too**Identity Protection**.</span></span> 
3. <span data-ttu-id="45e4a-163">在主要 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-163">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="45e4a-164">在 hello**入口網站設定**刀鋒視窗底下**安全性規則**，按一下**使用者危害的風險**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-164">On hello **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="45e4a-165">在 hello**登入風險**刀鋒視窗中，開啟**啟用規則**登出，然後按一下**儲存**設定。</span><span class="sxs-lookup"><span data-stu-id="45e4a-165">On hello **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="45e4a-166">對於指定的使用者帳戶，模擬不熟悉位置或匿名 IP 風險事件。</span><span class="sxs-lookup"><span data-stu-id="45e4a-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="45e4a-167">這會提升該使用者的 hello 使用者風險層級太**媒體**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-167">This will elevate hello user risk level for that user too**Medium**.</span></span>
7. <span data-ttu-id="45e4a-168">等候幾分鐘，然後確認使用者的使用者層級為 [中] 。</span><span class="sxs-lookup"><span data-stu-id="45e4a-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="45e4a-169">移 toohello**入口網站設定**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="45e4a-169">Go toohello **Portal Settings** blade.</span></span>
9. <span data-ttu-id="45e4a-170">在 hello**使用者危害的風險**刀鋒視窗底下**規則啟用**，選取**上**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-170">On hello **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="45e4a-171">選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="45e4a-171">Select one of hello following options:</span></span>
    
    <span data-ttu-id="45e4a-172">a.</span><span class="sxs-lookup"><span data-stu-id="45e4a-172">a.</span></span> <span data-ttu-id="45e4a-173">選取 tooblock**媒體**下**區塊登入**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-173">tooblock, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="45e4a-174">b.</span><span class="sxs-lookup"><span data-stu-id="45e4a-174">b.</span></span> <span data-ttu-id="45e4a-175">tooenforce 安全的密碼變更時，選取**媒體**下**需要多重要素驗證**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-175">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="45e4a-176">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="45e4a-176">Click **Save**.</span></span>
12. <span data-ttu-id="45e4a-177">您現在可以使用具有提高風險等級的使用者進行登入，以測試以風險為基礎的條件式存取。</span><span class="sxs-lookup"><span data-stu-id="45e4a-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="45e4a-178">如果 hello 使用者風險中，根據原則的 hello 組態，您是登入可能遭到封鎖，或被迫 toochange 您的密碼。</span><span class="sxs-lookup"><span data-stu-id="45e4a-178">If hello user risk is Medium, depending on hello configuration of your policy, your sign-in is be either blocked or you are forced toochange your password.</span></span> 
    <br><br><span data-ttu-id="45e4a-179">
    ![腳本](./media/active-directory-identityprotection-playbook/201.png "腳本")
    </span><span class="sxs-lookup"><span data-stu-id="45e4a-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="45e4a-180">登入風險</span><span class="sxs-lookup"><span data-stu-id="45e4a-180">Sign-in risk</span></span>
<span data-ttu-id="45e4a-181">**tootest 登入的風險，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="45e4a-181">**tootest a sign in risk, perform hello following steps:**</span></span>

1. <span data-ttu-id="45e4a-182">登入太[https://portal.azure.com](https://portal.azure.com)與您的租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="45e4a-182">Sign-in too[https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="45e4a-183">瀏覽過**Identity Protection**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-183">Navigate too**Identity Protection**.</span></span>
3. <span data-ttu-id="45e4a-184">在主要 hello **Azure AD Identity Protection**刀鋒視窗中，按一下 **設定**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-184">On hello main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="45e4a-185">在 hello**入口網站設定**刀鋒視窗下**安全性規則**，按一下**登入風險**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-185">On hello **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="45e4a-186">在 hello * * 登入風險 * * 刀鋒視窗中，選取**上**下**規則啟用**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-186">On hello **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="45e4a-187">選取其中一個 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="45e4a-187">Select one of hello following options:</span></span>
   
   <span data-ttu-id="45e4a-188">a.</span><span class="sxs-lookup"><span data-stu-id="45e4a-188">a.</span></span> <span data-ttu-id="45e4a-189">選取 tooblock**媒體**下**區塊登入**</span><span class="sxs-lookup"><span data-stu-id="45e4a-189">tooblock, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="45e4a-190">b.</span><span class="sxs-lookup"><span data-stu-id="45e4a-190">b.</span></span> <span data-ttu-id="45e4a-191">tooenforce 安全的密碼變更時，選取**媒體**下**需要多重要素驗證**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-191">tooenforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="45e4a-192">tooblock，選取媒體區塊下的登入。</span><span class="sxs-lookup"><span data-stu-id="45e4a-192">tooblock, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="45e4a-193">tooenforce 多因素驗證，請選取**媒體**下**需要多重要素驗證**。</span><span class="sxs-lookup"><span data-stu-id="45e4a-193">tooenforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="45e4a-194">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="45e4a-194">Click on **Save**.</span></span>
10. <span data-ttu-id="45e4a-195">您現在可以藉由模擬 hello 不熟悉位置測試風險型條件式存取或匿名 IP 風險存在事件，因為兩者都**媒體**事件的風險。</span><span class="sxs-lookup"><span data-stu-id="45e4a-195">You can now test risk-based conditional access by simulating hello unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="45e4a-196">![腳本](./media/active-directory-identityprotection-playbook/200.png "腳本")</span><span class="sxs-lookup"><span data-stu-id="45e4a-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="45e4a-197">另請參閱</span><span class="sxs-lookup"><span data-stu-id="45e4a-197">See also</span></span>
* [<span data-ttu-id="45e4a-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="45e4a-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

