---
title: "Azure AD Connect：無縫單一登入 - 快速入門 | Microsoft Docs"
description: "本文描述如何開始使用 Azure Active Directory 無縫單一登入。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 977108687734a5eb7f7a30419de2a6bdef184d0e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="cc52b-104">Azure Active Directory 無縫單一登入：快速入門</span><span class="sxs-lookup"><span data-stu-id="cc52b-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-to-deploy-seamless-sso"></a><span data-ttu-id="cc52b-105">如何部署無縫 SSO</span><span class="sxs-lookup"><span data-stu-id="cc52b-105">How to deploy Seamless SSO</span></span>

<span data-ttu-id="cc52b-106">使用者位於連線到公司網路的公司桌上型電腦時，Azure Active Directory 無縫單一登入 (Azure AD 無縫 SSO) 就會自動將他們登入。</span><span class="sxs-lookup"><span data-stu-id="cc52b-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected to your corporate network.</span></span> <span data-ttu-id="cc52b-107">它可讓使用者輕鬆存取雲端式應用程式，而不需要任何額外的內部部署元件。</span><span class="sxs-lookup"><span data-stu-id="cc52b-107">It provides your users easy access to your cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cc52b-108">無縫 SSO 功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="cc52b-108">The Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="cc52b-109">若要部署無縫 SSO，您需要遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cc52b-109">To deploy Seamless SSO, you need to follow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="cc52b-110">步驟 1：檢查必要條件</span><span class="sxs-lookup"><span data-stu-id="cc52b-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="cc52b-111">請確保已具備下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="cc52b-111">Ensure that the following prerequisites are in place:</span></span>

1. <span data-ttu-id="cc52b-112">設定 Azure AD Connect 伺服器：如果您使用[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)作為登入方法，不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="cc52b-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="cc52b-113">如果您使用[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)作為登入方法，而且 Azure AD Connect 與 Azure AD 之間有防火牆，請確定︰</span><span class="sxs-lookup"><span data-stu-id="cc52b-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="cc52b-114">您使用的是 1.1.484.0 版或更新版本的 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="cc52b-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="cc52b-115">Azure AD Connect 可以與 `*.msappproxy.net` URL 通訊，而且是透過連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="cc52b-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="cc52b-116">只有當您啟用此功能，而不是針對實際使用者登入時，此必要條件才適用。</span><span class="sxs-lookup"><span data-stu-id="cc52b-116">This prerequisite is applicable only when you enable the feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="cc52b-117">Azure AD Connect 可以對 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)直接建立 IP 連線。</span><span class="sxs-lookup"><span data-stu-id="cc52b-117">Azure AD Connect can make direct IP connections to the [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="cc52b-118">同樣地，只有啟用此功能時，此必要條件才適用。</span><span class="sxs-lookup"><span data-stu-id="cc52b-118">Again, this prerequisite is applicable only when you enable the feature.</span></span>
2. <span data-ttu-id="cc52b-119">對於您同步處理至 Azure AD (使用 Azure AD Connect) 的每個 AD 樹系，以及您想要為其使用者啟用無縫 SSO 者，您需要有網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="cc52b-119">You need Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span>

## <a name="step-2-enable-the-feature"></a><span data-ttu-id="cc52b-120">步驟 2︰啟用功能</span><span class="sxs-lookup"><span data-stu-id="cc52b-120">Step 2: Enable the feature</span></span>

<span data-ttu-id="cc52b-121">您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 啟用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="cc52b-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="cc52b-122">如果您要執行 Azure AD Connect 的全新安裝，請選擇[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-122">If you are doing a fresh installation of Azure AD Connect, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="cc52b-123">在 [使用者登入] 頁面上，勾選 [啟用單一登入] 選項。</span><span class="sxs-lookup"><span data-stu-id="cc52b-123">At the "User sign-in" page, check the "Enable single sign on" option.</span></span>

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="cc52b-125">如果您已經安裝 Azure AD Connect，請在 Azure AD Connect 上選擇 [變更使用者登入] 頁面，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="cc52b-126">然後勾選 [啟用單一登入] 選項。</span><span class="sxs-lookup"><span data-stu-id="cc52b-126">Then check the "Enable single sign on" option.</span></span>

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="cc52b-128">繼續執行精靈，直到抵達 [啟用單一登入] 頁面。</span><span class="sxs-lookup"><span data-stu-id="cc52b-128">Continue through the wizard until you get to the "Enable single sign on" page.</span></span> <span data-ttu-id="cc52b-129">對於您同步處理至 Azure AD (使用 Azure AD Connect) 的每個 AD 樹系，以及您想要為其使用者啟用無縫 SSO 者，請提供網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="cc52b-129">Provide Domain Administrator credentials for each AD forest that you synchronize to Azure AD (using Azure AD Connect) and for whose users you want to enable Seamless SSO.</span></span> 

<span data-ttu-id="cc52b-130">完成精靈之後，無縫 SSO 就會在您的租用戶上啟用。</span><span class="sxs-lookup"><span data-stu-id="cc52b-130">After completion of the wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="cc52b-131">網域系統管理員認證不會儲存在 Azure AD Connect 或 Azure AD 中，但只用來啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="cc52b-131">The Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used to enable the feature.</span></span>

<span data-ttu-id="cc52b-132">請遵循下列指示來確認您已正確啟用無縫 SSO：</span><span class="sxs-lookup"><span data-stu-id="cc52b-132">Follow these instructions to verify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="cc52b-133">使用租用戶的全域管理員認證來登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-133">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="cc52b-134">按一下左側導覽上的 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-134">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="cc52b-135">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="cc52b-136">確認 [無縫單一登入] 功能顯示為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-136">Verify that the **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure 入口網站 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-the-feature"></a><span data-ttu-id="cc52b-138">步驟 3：推出功能</span><span class="sxs-lookup"><span data-stu-id="cc52b-138">Step 3: Roll out the feature</span></span>

<span data-ttu-id="cc52b-139">若要對使用者推出此功能，您需要透過 Active Directory 中的群組原則，將兩個 Azure AD URL (https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net) 新增至使用者的內部網路區域設定。</span><span class="sxs-lookup"><span data-stu-id="cc52b-139">To roll out the feature to your users, you need to add two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) to users' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="cc52b-140">下列指示僅適用於 Windows 上的 Internet Explorer 和 Google Chrome (如果它與 Internet Explorer 共用一組受信任的網站 URL)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-140">The following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="cc52b-141">如需在 Mac 上設定 Mozilla Firefox 和 Google Chrome 的指示，請閱讀下節。</span><span class="sxs-lookup"><span data-stu-id="cc52b-141">Read the next section for instructions to set up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-to-modify-users-intranet-zone-settings"></a><span data-ttu-id="cc52b-142">為什麼需要修改使用者的內部網路區域設定？</span><span class="sxs-lookup"><span data-stu-id="cc52b-142">Why do you need to modify users' Intranet zone settings?</span></span>

<span data-ttu-id="cc52b-143">瀏覽器預設會自動從 URL 計算正確的區域 (網際網路或內部網路)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-143">By default, the browser automatically calculates the right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="cc52b-144">例如，http://contoso/ 會對應到內部網路區域，而 http://intranet.contoso.com/ 會對應到網際網路區域 (因為 URL 包含句點)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-144">For example, http://contoso/ is mapped to the Intranet zone, whereas http://intranet.contoso.com/ is mapped to the Internet zone (because the URL contains a period).</span></span> <span data-ttu-id="cc52b-145">除非將 URL 明確地新增至瀏覽器的內部網路區域，否則瀏覽器不會將 Kerberos 票證傳送給雲端端點 (例如兩個 Azure AD URL)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-145">Browsers don't send Kerberos tickets to a cloud endpoint - like the two Azure AD URLs - unless its URL is explicitly added to the browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="cc52b-146">詳細步驟</span><span class="sxs-lookup"><span data-stu-id="cc52b-146">Detailed steps</span></span>

1. <span data-ttu-id="cc52b-147">開啟群組原則管理工具。</span><span class="sxs-lookup"><span data-stu-id="cc52b-147">Open the Group Policy Management tool.</span></span>
2. <span data-ttu-id="cc52b-148">編輯套用至某些或所有使用者的群組原則。</span><span class="sxs-lookup"><span data-stu-id="cc52b-148">Edit the Group Policy that is applied to some or all your users.</span></span> <span data-ttu-id="cc52b-149">在此範例中，我們使用**預設網域原則**。</span><span class="sxs-lookup"><span data-stu-id="cc52b-149">In this example, we use the **Default Domain Policy**.</span></span>
3. <span data-ttu-id="cc52b-150">瀏覽至 **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security 頁面**，並選取 [指派網站到區域清單]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-150">Navigate to **User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site to Zone Assignment List**.</span></span>
<span data-ttu-id="cc52b-151">![單一登入](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="cc52b-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="cc52b-152">啟用原則，並在對話方塊中輸入下列值 (轉送 Kerberos 票證的 Azure AD URL) 和資料 (*1* 指出內部網路區域)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-152">Enable the policy, and enter the following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in the dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="cc52b-153">如果您想要禁止部分使用者使用無縫 SSO (例如，如果這些使用者正在登入共用 Kiosk)，請將先前的值設定為 *4*。</span><span class="sxs-lookup"><span data-stu-id="cc52b-153">If you want to disallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set the preceding values to *4*.</span></span> <span data-ttu-id="cc52b-154">此動作會將 Azure AD URL 新增至限制區域，而且隨時讓無縫 SSO 失敗。</span><span class="sxs-lookup"><span data-stu-id="cc52b-154">This action adds the Azure AD URLs to the Restricted Zone, and fails Seamless SSO all the time.</span></span>

5. <span data-ttu-id="cc52b-155">按一下 [確定]，然後再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-155">Click **OK** and **OK** again.</span></span>

![單一登入](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="cc52b-157">瀏覽器考量</span><span class="sxs-lookup"><span data-stu-id="cc52b-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="cc52b-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="cc52b-158">Mozilla Firefox</span></span>

<span data-ttu-id="cc52b-159">Mozilla Firefox 不會自動執行 Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="cc52b-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="cc52b-160">每個使用者都必須使用下列步驟，手動將 Azure AD URL 新增至其 Firefox 設定：</span><span class="sxs-lookup"><span data-stu-id="cc52b-160">Each user has to manually add the Azure AD URLs to their Firefox settings using the following steps:</span></span>
1. <span data-ttu-id="cc52b-161">執行 Firefox，並在網址列中輸入 `about:config`。</span><span class="sxs-lookup"><span data-stu-id="cc52b-161">Run Firefox and enter `about:config` in the address bar.</span></span> <span data-ttu-id="cc52b-162">關閉任何您看到的通知。</span><span class="sxs-lookup"><span data-stu-id="cc52b-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="cc52b-163">搜尋 **network.negotiate-auth.trusted-uris** 喜好設定。</span><span class="sxs-lookup"><span data-stu-id="cc52b-163">Search for the **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="cc52b-164">此喜好設定列出 Firefox 進行 Kerberos 驗證的受信任網站。</span><span class="sxs-lookup"><span data-stu-id="cc52b-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="cc52b-165">按一下滑鼠右鍵，然後選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="cc52b-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="cc52b-166">在欄位中，輸入 "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net"。</span><span class="sxs-lookup"><span data-stu-id="cc52b-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in the field.</span></span>
5. <span data-ttu-id="cc52b-167">按一下 [確定]，然後重新開啟瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="cc52b-167">Click "OK" and reopen the browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="cc52b-168">Mac OS 上的 Safari</span><span class="sxs-lookup"><span data-stu-id="cc52b-168">Safari on Mac OS</span></span>

<span data-ttu-id="cc52b-169">確定執行 Mac OS 的電腦已加入至 AD。</span><span class="sxs-lookup"><span data-stu-id="cc52b-169">Ensure that the machine running Mac OS is joined to AD.</span></span> <span data-ttu-id="cc52b-170">請參閱[這裡](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)的操作指示。</span><span class="sxs-lookup"><span data-stu-id="cc52b-170">See instructions on how to do that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="cc52b-171">Mac OS 上的 Google Chrome</span><span class="sxs-lookup"><span data-stu-id="cc52b-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="cc52b-172">針對 Mac OS 和其他非 Windows 平台上的 Google Chrome，請參閱[本文](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist)以了解如何將 Azure AD URL 設為白名單進行整合式驗證的資訊。</span><span class="sxs-lookup"><span data-stu-id="cc52b-172">For Google Chrome on Mac OS and other non-Windows platforms, refer to [this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how to whitelist the Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="cc52b-173">使用協力廠商 Active Directory 群組原則延伸模組向 Mac 使用者上的 Firefox 和 Google Chrome 推出 Azure AD URL，不在本文的範圍內。</span><span class="sxs-lookup"><span data-stu-id="cc52b-173">Using third-party Active Directory Group Policy extensions to roll out the Azure AD URLs to Firefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="cc52b-174">已知限制</span><span class="sxs-lookup"><span data-stu-id="cc52b-174">Known limitations</span></span>

<span data-ttu-id="cc52b-175">無縫 SSO 無法在 Firefox 和 Edge 瀏覽器的私人瀏覽模式中運作。</span><span class="sxs-lookup"><span data-stu-id="cc52b-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="cc52b-176">如果瀏覽器是在「增強保護」模式中執行，它也無法在 Internet Explorer 上運作。</span><span class="sxs-lookup"><span data-stu-id="cc52b-176">It also doesn't work on Internet Explorer if the browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cc52b-177">我們最近已復原對 Edge 的支援，以調查客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="cc52b-177">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="cc52b-178">步驟 4：測試功能</span><span class="sxs-lookup"><span data-stu-id="cc52b-178">Step 4: Test the feature</span></span>

<span data-ttu-id="cc52b-179">若要測試特定使用者的功能，請確認已具備下列「所有」條件：</span><span class="sxs-lookup"><span data-stu-id="cc52b-179">To test the feature for a specific user, ensure that _all_ the following conditions are in place:</span></span>
  - <span data-ttu-id="cc52b-180">使用者是在公司裝置上登入。</span><span class="sxs-lookup"><span data-stu-id="cc52b-180">The user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="cc52b-181">裝置先前已加入您的 Active Directory (AD) 網域。</span><span class="sxs-lookup"><span data-stu-id="cc52b-181">The device has been previously joined to your Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="cc52b-182">裝置能夠直接連線至網域控制站 (DC)，不論是在公司的有線或無線網路上進行，還是透過遠端存取連線 (例如 VPN 連線) 來進行。</span><span class="sxs-lookup"><span data-stu-id="cc52b-182">The device has a direct connection to your Domain Controller (DC), either on the corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="cc52b-183">您已向使用群組原則的這位使用者[推出功能](##step-3-roll-out-the-feature)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-183">You have [rolled out the feature](##step-3-roll-out-the-feature) to this user using Group Policy.</span></span>

<span data-ttu-id="cc52b-184">測試使用者只輸入使用者名稱而非密碼的案例：</span><span class="sxs-lookup"><span data-stu-id="cc52b-184">To test the scenario where the user enters only the username, but not the password:</span></span>
- <span data-ttu-id="cc52b-185">在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/*。</span><span class="sxs-lookup"><span data-stu-id="cc52b-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="cc52b-186">測試使用者不需要輸入使用者名稱或密碼的案例：</span><span class="sxs-lookup"><span data-stu-id="cc52b-186">To test the scenario where the user doesn't have to enter the username or the password:</span></span> 
- <span data-ttu-id="cc52b-187">在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.onmicrosoft.com*。</span><span class="sxs-lookup"><span data-stu-id="cc52b-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="cc52b-188">將 "*contoso*" 取代為您租用戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="cc52b-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="cc52b-189">或者，在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="cc52b-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="cc52b-190">將 "*contoso.com*" 取代為租用戶中的已驗證網域 (非同盟網域)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="cc52b-191">步驟 5：變換金鑰</span><span class="sxs-lookup"><span data-stu-id="cc52b-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="cc52b-192">在步驟 2 中，Azure AD Connect 會在您已啟用無縫 SSO 的所有 AD 樹系中建立電腦帳戶 (代表 Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="cc52b-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all the AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="cc52b-193">在[這裡](active-directory-aadconnect-sso-how-it-works.md)詳細了解。</span><span class="sxs-lookup"><span data-stu-id="cc52b-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="cc52b-194">為了提升安全性，建議您經常變換這些電腦帳戶的 Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc52b-194">For improved security, it is recommended that  you frequently roll over the Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="cc52b-195">您不需要在啟用此功能後「立即」執行此步驟。</span><span class="sxs-lookup"><span data-stu-id="cc52b-195">You don't need to do this step _immediately_ after you have enabled the feature.</span></span> <span data-ttu-id="cc52b-196">至少每隔 30 天變換一次 Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc52b-196">Roll over the Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc52b-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc52b-197">Next steps</span></span>

- <span data-ttu-id="cc52b-198">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="cc52b-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="cc52b-199">[**常見問題集**](active-directory-aadconnect-sso-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="cc52b-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="cc52b-200">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="cc52b-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="cc52b-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="cc52b-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
