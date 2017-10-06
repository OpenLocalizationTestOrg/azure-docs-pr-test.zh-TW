---
title: "Azure AD Connect：無縫單一登入 - 快速入門 | Microsoft Docs"
description: "本文說明如何 tooget 啟動與 Azure Active Directory 無接縫單一登入。"
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a><span data-ttu-id="88382-104">Azure Active Directory 無縫單一登入：快速入門</span><span class="sxs-lookup"><span data-stu-id="88382-104">Azure Active Directory Seamless Single Sign-On: Quick start</span></span>

## <a name="how-toodeploy-seamless-sso"></a><span data-ttu-id="88382-105">如何 toodeploy 無縫式 SSO</span><span class="sxs-lookup"><span data-stu-id="88382-105">How toodeploy Seamless SSO</span></span>

<span data-ttu-id="88382-106">Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO) 自動簽署時其公司的電腦已連線的 tooyour 公司網路上的使用者。</span><span class="sxs-lookup"><span data-stu-id="88382-106">Azure Active Directory Seamless Single Sign-On (Azure AD Seamless SSO) automatically signs users in when they are on their corporate desktops connected tooyour corporate network.</span></span> <span data-ttu-id="88382-107">它提供您的使用者方便存取 tooyour 雲端型應用程式而不需要任何額外的內部部署元件。</span><span class="sxs-lookup"><span data-stu-id="88382-107">It provides your users easy access tooyour cloud-based applications without needing any additional on-premises components.</span></span>

>[!IMPORTANT]
><span data-ttu-id="88382-108">hello 無縫式 SSO 的功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="88382-108">hello Seamless SSO feature is currently in preview.</span></span>

<span data-ttu-id="88382-109">您需要 toofollow toodeploy 無縫式 SSO，下列步驟：</span><span class="sxs-lookup"><span data-stu-id="88382-109">toodeploy Seamless SSO, you need toofollow these steps:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="88382-110">步驟 1：檢查必要條件</span><span class="sxs-lookup"><span data-stu-id="88382-110">Step 1: Check prerequisites</span></span>

<span data-ttu-id="88382-111">請確定該 hello 下列必要條件已就緒：</span><span class="sxs-lookup"><span data-stu-id="88382-111">Ensure that hello following prerequisites are in place:</span></span>

1. <span data-ttu-id="88382-112">設定 Azure AD Connect 伺服器：如果您使用[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)作為登入方法，不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="88382-112">Set up your Azure AD Connect server: If you use [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) as your sign-in method, no further action is required.</span></span> <span data-ttu-id="88382-113">如果您使用[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)作為登入方法，而且 Azure AD Connect 與 Azure AD 之間有防火牆，請確定︰</span><span class="sxs-lookup"><span data-stu-id="88382-113">If you use [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) as your sign-in method, and if there is a firewall between Azure AD Connect and Azure AD, ensure that:</span></span>
- <span data-ttu-id="88382-114">您使用的是 1.1.484.0 版或更新版本的 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="88382-114">You are using versions 1.1.484.0 or later of Azure AD Connect.</span></span>
- <span data-ttu-id="88382-115">Azure AD Connect 可以與 `*.msappproxy.net` URL 通訊，而且是透過連接埠 443。</span><span class="sxs-lookup"><span data-stu-id="88382-115">Azure AD Connect can communicate with `*.msappproxy.net` URLs and over port 443.</span></span> <span data-ttu-id="88382-116">只有當您啟用 hello 功能，不會針對實際的使用者登入，是適用於此必要條件。</span><span class="sxs-lookup"><span data-stu-id="88382-116">This prerequisite is applicable only when you enable hello feature, not for actual user sign-ins.</span></span>
- <span data-ttu-id="88382-117">Azure AD Connect 可直接 IP 連線 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="88382-117">Azure AD Connect can make direct IP connections toohello [Azure data center IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="88382-118">同樣地，此必要條件時，適用於只啟用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="88382-118">Again, this prerequisite is applicable only when you enable hello feature.</span></span>
2. <span data-ttu-id="88382-119">您需要同步處理 tooAzure AD 每個 AD 樹系的網域系統管理員認證 （使用 Azure AD Connect） 和您要為其使用者 tooenable 無縫式 SSO。</span><span class="sxs-lookup"><span data-stu-id="88382-119">You need Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span>

## <a name="step-2-enable-hello-feature"></a><span data-ttu-id="88382-120">步驟 2： 啟用 hello 功能</span><span class="sxs-lookup"><span data-stu-id="88382-120">Step 2: Enable hello feature</span></span>

<span data-ttu-id="88382-121">您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 啟用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="88382-121">Seamless SSO can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

<span data-ttu-id="88382-122">若您執行全新安裝的 Azure AD Connect，選擇 hello[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="88382-122">If you are doing a fresh installation of Azure AD Connect, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="88382-123">在 hello 「 使用者登入 」 頁面上，核取 hello 」 啟用單一登入 」 選項。</span><span class="sxs-lookup"><span data-stu-id="88382-123">At hello "User sign-in" page, check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso8.png)

<span data-ttu-id="88382-125">如果您已經安裝 Azure AD Connect，請在 Azure AD Connect 上選擇 [變更使用者登入] 頁面，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="88382-125">If you already have an installation of Azure AD Connect, choose "Change user sign-in page" on Azure AD Connect and click "Next".</span></span> <span data-ttu-id="88382-126">然後檢查 hello 」 啟用單一登入 」 選項。</span><span class="sxs-lookup"><span data-stu-id="88382-126">Then check hello "Enable single sign on" option.</span></span>

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

<span data-ttu-id="88382-128">繼續透過 hello 精靈直到到達 toohello 」 啟用單一登入 」 頁面。</span><span class="sxs-lookup"><span data-stu-id="88382-128">Continue through hello wizard until you get toohello "Enable single sign on" page.</span></span> <span data-ttu-id="88382-129">提供每個 AD 樹系同步處理 tooAzure AD 網域系統管理員認證 （使用 Azure AD Connect） 和您要為其使用者 tooenable 無縫式 SSO。</span><span class="sxs-lookup"><span data-stu-id="88382-129">Provide Domain Administrator credentials for each AD forest that you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want tooenable Seamless SSO.</span></span> 

<span data-ttu-id="88382-130">完成之後 hello 精靈，您的租用戶上已啟用無縫式 SSO。</span><span class="sxs-lookup"><span data-stu-id="88382-130">After completion of hello wizard, Seamless SSO is enabled on your tenant.</span></span>

>[!NOTE]
> <span data-ttu-id="88382-131">hello 網域系統管理員認證不會儲存在 Azure AD Connect，或在 Azure AD 中，但使用的 tooenable hello 功能。</span><span class="sxs-lookup"><span data-stu-id="88382-131">hello Domain Administrator credentials are not stored in Azure AD Connect or in Azure AD, but are only used tooenable hello feature.</span></span>

<span data-ttu-id="88382-132">請遵循這些指示 tooverify，您已正確啟用無縫式 SSO:</span><span class="sxs-lookup"><span data-stu-id="88382-132">Follow these instructions tooverify that you have enabled Seamless SSO correctly:</span></span>

1. <span data-ttu-id="88382-133">登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="88382-133">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="88382-134">選取**Azure Active Directory** hello 左側導覽上。</span><span class="sxs-lookup"><span data-stu-id="88382-134">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="88382-135">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="88382-135">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="88382-136">請確認該 hello**無接縫單一登入**功能就會顯示為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="88382-136">Verify that hello **Seamless Single Sign-On** feature shows as **Enabled**.</span></span>

![Azure 入口網站 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a><span data-ttu-id="88382-138">步驟 3： 轉出 hello 功能</span><span class="sxs-lookup"><span data-stu-id="88382-138">Step 3: Roll out hello feature</span></span>

<span data-ttu-id="88382-139">tooroll hello 功能 tooyour 使用者，您必須透過 Active Directory 中的群組原則 tooadd 兩個 Azure AD Url （https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net） toousers' 內部網路區域的設定。</span><span class="sxs-lookup"><span data-stu-id="88382-139">tooroll out hello feature tooyour users, you need tooadd two Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) toousers' Intranet zone settings via Group Policy in Active Directory.</span></span>

>[!NOTE]
> <span data-ttu-id="88382-140">hello 遵循 Windows 上的指示只適用於 Internet Explorer 和 Google Chrome （如果它與 Internet Explorer 共用一組信任的網站 Url）。</span><span class="sxs-lookup"><span data-stu-id="88382-140">hello following instructions only work for Internet Explorer and Google Chrome on Windows  (if it shares set of trusted site URLs with Internet Explorer).</span></span> <span data-ttu-id="88382-141">讀取 Mozilla Firefox 和 Google Chrome mac 上的指示 tooset hello 下一節</span><span class="sxs-lookup"><span data-stu-id="88382-141">Read hello next section for instructions tooset up Mozilla Firefox and Google Chrome on Mac.</span></span>

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a><span data-ttu-id="88382-142">您為什麼需要 toomodify 使用者的內部網路區域的設定？</span><span class="sxs-lookup"><span data-stu-id="88382-142">Why do you need toomodify users' Intranet zone settings?</span></span>

<span data-ttu-id="88382-143">根據預設，hello 瀏覽器會自動從 URL 計算 hello 區域 （網際網路或內部網路）。</span><span class="sxs-lookup"><span data-stu-id="88382-143">By default, hello browser automatically calculates hello right zone (Internet or Intranet) from a URL.</span></span> <span data-ttu-id="88382-144">例如，http://contoso/ 都是對應的 toohello 近端內部網路區域，而 http://intranet.contoso.com/ （因為 hello URL 包含句號） 則是對應的 toohello 網際網路區域。</span><span class="sxs-lookup"><span data-stu-id="88382-144">For example, http://contoso/ is mapped toohello Intranet zone, whereas http://intranet.contoso.com/ is mapped toohello Internet zone (because hello URL contains a period).</span></span> <span data-ttu-id="88382-145">瀏覽器不傳送-像是 hello 兩個 Azure AD Url-Kerberos 票證 tooa 雲端端點，除非其 URL，明確地新增 toohello 瀏覽器的近端內部網路區域。</span><span class="sxs-lookup"><span data-stu-id="88382-145">Browsers don't send Kerberos tickets tooa cloud endpoint - like hello two Azure AD URLs - unless its URL is explicitly added toohello browser's Intranet zone.</span></span>

### <a name="detailed-steps"></a><span data-ttu-id="88382-146">詳細步驟</span><span class="sxs-lookup"><span data-stu-id="88382-146">Detailed steps</span></span>

1. <span data-ttu-id="88382-147">開啟 hello 群組原則管理工具。</span><span class="sxs-lookup"><span data-stu-id="88382-147">Open hello Group Policy Management tool.</span></span>
2. <span data-ttu-id="88382-148">編輯 hello 套用的 toosome 或所有使用者的群組原則。</span><span class="sxs-lookup"><span data-stu-id="88382-148">Edit hello Group Policy that is applied toosome or all your users.</span></span> <span data-ttu-id="88382-149">在此範例中，我們使用 hello**預設網域原則**。</span><span class="sxs-lookup"><span data-stu-id="88382-149">In this example, we use hello **Default Domain Policy**.</span></span>
3. <span data-ttu-id="88382-150">瀏覽過**使用者設定 \ 系統管理範本 \windows 元件 \internet explorer\ 網際網路控制項 Panel\Security 頁面**選取**站台指派清單 tooZone**。</span><span class="sxs-lookup"><span data-stu-id="88382-150">Navigate too**User Configuration\Administrative Templates\Windows Components\Internet Explorer\Internet Control Panel\Security Page** and select **Site tooZone Assignment List**.</span></span>
<span data-ttu-id="88382-151">![單一登入](./media/active-directory-aadconnect-sso/sso6.png)</span><span class="sxs-lookup"><span data-stu-id="88382-151">![Single sign-on](./media/active-directory-aadconnect-sso/sso6.png)</span></span>  
4. <span data-ttu-id="88382-152">啟用 hello 原則，並輸入下列值 (Azure AD Url 會轉送 Kerberos 票證的位置) 的 hello 和資料 (*1*指出近端內部網路區域) hello 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="88382-152">Enable hello policy, and enter hello following values (Azure AD URLs where Kerberos tickets are forwarded) and data (*1* indicates Intranet zone) in hello dialog box.</span></span>

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> <span data-ttu-id="88382-153">如果您想要 toodisallow 比方說，使用無縫式 SSO-有些使用者如果這些使用者內部網路上共用 kiosk-登入設定 hello 太前置值*4*。</span><span class="sxs-lookup"><span data-stu-id="88382-153">If you want toodisallow some users from using Seamless SSO - for instance, if these users are signing in on shared kiosks - set hello preceding values too*4*.</span></span> <span data-ttu-id="88382-154">此動作將 hello Azure AD Url toohello 受限制區域，而且會無縫式 SSO 失敗所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="88382-154">This action adds hello Azure AD URLs toohello Restricted Zone, and fails Seamless SSO all hello time.</span></span>

5. <span data-ttu-id="88382-155">按一下 [確定]，然後再按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="88382-155">Click **OK** and **OK** again.</span></span>

![單一登入](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a><span data-ttu-id="88382-157">瀏覽器考量</span><span class="sxs-lookup"><span data-stu-id="88382-157">Browser considerations</span></span>

#### <a name="mozilla-firefox"></a><span data-ttu-id="88382-158">Mozilla Firefox</span><span class="sxs-lookup"><span data-stu-id="88382-158">Mozilla Firefox</span></span>

<span data-ttu-id="88382-159">Mozilla Firefox 不會自動執行 Kerberos 驗證。</span><span class="sxs-lookup"><span data-stu-id="88382-159">Mozilla Firefox doesn't automatically do Kerberos Authentication.</span></span> <span data-ttu-id="88382-160">每個使用者擁有 toomanually 新增 hello Azure AD Url tootheir Firefox 設定使用 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="88382-160">Each user has toomanually add hello Azure AD URLs tootheir Firefox settings using hello following steps:</span></span>
1. <span data-ttu-id="88382-161">執行 Firefox，並輸入`about:config`hello 網址列中。</span><span class="sxs-lookup"><span data-stu-id="88382-161">Run Firefox and enter `about:config` in hello address bar.</span></span> <span data-ttu-id="88382-162">關閉任何您看到的通知。</span><span class="sxs-lookup"><span data-stu-id="88382-162">Dismiss any notifications that you see.</span></span>
2. <span data-ttu-id="88382-163">搜尋 hello **network.negotiate-auth.trusted-uri**喜好設定。</span><span class="sxs-lookup"><span data-stu-id="88382-163">Search for hello **network.negotiate-auth.trusted-uris** preference.</span></span> <span data-ttu-id="88382-164">此喜好設定列出 Firefox 進行 Kerberos 驗證的受信任網站。</span><span class="sxs-lookup"><span data-stu-id="88382-164">This preference lists Firefox's trusted sites for Kerberos authentication.</span></span>
3. <span data-ttu-id="88382-165">按一下滑鼠右鍵，然後選取 [修改]。</span><span class="sxs-lookup"><span data-stu-id="88382-165">Right-click and select "Modify".</span></span>
4. <span data-ttu-id="88382-166">請輸入"https://autologon.microsoftazuread-sso.com，https://aadg.windows.net.nsatc.net"hello 欄位中。</span><span class="sxs-lookup"><span data-stu-id="88382-166">Enter "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in hello field.</span></span>
5. <span data-ttu-id="88382-167">按一下 [確定]，並重新開啟 hello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="88382-167">Click "OK" and reopen hello browser.</span></span>

#### <a name="safari-on-mac-os"></a><span data-ttu-id="88382-168">Mac OS 上的 Safari</span><span class="sxs-lookup"><span data-stu-id="88382-168">Safari on Mac OS</span></span>

<span data-ttu-id="88382-169">請確認執行 Mac OS 的 hello 機器聯結的 tooAD。</span><span class="sxs-lookup"><span data-stu-id="88382-169">Ensure that hello machine running Mac OS is joined tooAD.</span></span> <span data-ttu-id="88382-170">請參閱指示如何 toodo，[這裡](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)。</span><span class="sxs-lookup"><span data-stu-id="88382-170">See instructions on how toodo that [here](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).</span></span>

#### <a name="google-chrome-on-mac-os"></a><span data-ttu-id="88382-171">Mac OS 上的 Google Chrome</span><span class="sxs-lookup"><span data-stu-id="88382-171">Google Chrome on Mac OS</span></span>

<span data-ttu-id="88382-172">Mac OS 和其他非 Windows 平台上的 Google chrome，請參閱太[本文](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist)如需有關如何 toowhitelist hello 整合式驗證的 Azure AD Url 資訊。</span><span class="sxs-lookup"><span data-stu-id="88382-172">For Google Chrome on Mac OS and other non-Windows platforms, refer too[this article](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) for information on how toowhitelist hello Azure AD URLs for integrated authentication.</span></span>

<span data-ttu-id="88382-173">使用協力廠商架構 Active Directory 群組原則已超出本文的範圍延伸 tooroll 出 hello Azure AD Url tooFirefox 和 Google Chrome Mac 使用者。</span><span class="sxs-lookup"><span data-stu-id="88382-173">Using third-party Active Directory Group Policy extensions tooroll out hello Azure AD URLs tooFirefox and Google Chrome on Mac users is outside of this article's scope.</span></span>

#### <a name="known-limitations"></a><span data-ttu-id="88382-174">已知限制</span><span class="sxs-lookup"><span data-stu-id="88382-174">Known limitations</span></span>

<span data-ttu-id="88382-175">無縫 SSO 無法在 Firefox 和 Edge 瀏覽器的私人瀏覽模式中運作。</span><span class="sxs-lookup"><span data-stu-id="88382-175">Seamless SSO doesn't work in private browsing mode on Firefox and Edge browsers.</span></span> <span data-ttu-id="88382-176">它也不適用於的 Internet Explorer 如果 hello 瀏覽器在增強保護模式中執行。</span><span class="sxs-lookup"><span data-stu-id="88382-176">It also doesn't work on Internet Explorer if hello browser is running in Enhanced Protection mode.</span></span>

>[!IMPORTANT]
><span data-ttu-id="88382-177">我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="88382-177">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="88382-178">步驟 4： 測試 hello 功能</span><span class="sxs-lookup"><span data-stu-id="88382-178">Step 4: Test hello feature</span></span>

<span data-ttu-id="88382-179">tootest hello 功能特定的使用者，確保_所有_已就位 hello 下列條件：</span><span class="sxs-lookup"><span data-stu-id="88382-179">tootest hello feature for a specific user, ensure that _all_ hello following conditions are in place:</span></span>
  - <span data-ttu-id="88382-180">hello 使用者在公司的裝置上登入。</span><span class="sxs-lookup"><span data-stu-id="88382-180">hello user is signing in on a corporate device.</span></span>
  - <span data-ttu-id="88382-181">hello 裝置已進行先前聯結的 tooyour Active Directory (AD) 網域。</span><span class="sxs-lookup"><span data-stu-id="88382-181">hello device has been previously joined tooyour Active Directory (AD) domain.</span></span>
  - <span data-ttu-id="88382-182">hello 裝置有直接連線 tooyour 網域控制站 (DC)，hello 公司有線或無線網路上或是透過遠端存取連線，例如 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="88382-182">hello device has a direct connection tooyour Domain Controller (DC), either on hello corporate wired or wireless network or via a remote access connection, such as a VPN connection.</span></span>
  - <span data-ttu-id="88382-183">您有[推出 hello 功能](##step-3-roll-out-the-feature)toothis 使用群組原則的使用者。</span><span class="sxs-lookup"><span data-stu-id="88382-183">You have [rolled out hello feature](##step-3-roll-out-the-feature) toothis user using Group Policy.</span></span>

<span data-ttu-id="88382-184">tootest hello 案例只 hello 使用者名稱，但不是 hello 密碼 hello 使用者會輸入：</span><span class="sxs-lookup"><span data-stu-id="88382-184">tootest hello scenario where hello user enters only hello username, but not hello password:</span></span>
- <span data-ttu-id="88382-185">在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/*。</span><span class="sxs-lookup"><span data-stu-id="88382-185">Sign into *https://myapps.microsoft.com/* in a new private browser session.</span></span>

<span data-ttu-id="88382-186">其中 hello 使用者沒有 tooenter hello 使用者名稱或 hello 密碼 tootest hello 案例：</span><span class="sxs-lookup"><span data-stu-id="88382-186">tootest hello scenario where hello user doesn't have tooenter hello username or hello password:</span></span> 
- <span data-ttu-id="88382-187">在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.onmicrosoft.com*。</span><span class="sxs-lookup"><span data-stu-id="88382-187">Sign into *https://myapps.microsoft.com/contoso.onmicrosoft.com* in a new private browser session.</span></span> <span data-ttu-id="88382-188">將 "*contoso*" 取代為您租用戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="88382-188">Replace "*contoso*" with your tenant's name.</span></span>
- <span data-ttu-id="88382-189">或者，在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.com*。</span><span class="sxs-lookup"><span data-stu-id="88382-189">Or sign into *https://myapps.microsoft.com/contoso.com* in a new private browser session.</span></span> <span data-ttu-id="88382-190">將 "*contoso.com*" 取代為租用戶中的已驗證網域 (非同盟網域)。</span><span class="sxs-lookup"><span data-stu-id="88382-190">Replace "*contoso.com*" with a verified domain (not a federated domain) in your tenant.</span></span>

## <a name="step-5-roll-over-keys"></a><span data-ttu-id="88382-191">步驟 5：變換金鑰</span><span class="sxs-lookup"><span data-stu-id="88382-191">Step 5: Roll over keys</span></span>

<span data-ttu-id="88382-192">在步驟 2 中，Azure AD Connect 會建立電腦帳戶 （代表 Azure AD） 中所有已啟用無縫式 SSO 的 hello AD 樹系。</span><span class="sxs-lookup"><span data-stu-id="88382-192">In Step 2, Azure AD Connect creates computer accounts (representing Azure AD) in all hello AD forests on which you have enabled Seamless SSO.</span></span> <span data-ttu-id="88382-193">在[這裡](active-directory-aadconnect-sso-how-it-works.md)詳細了解。</span><span class="sxs-lookup"><span data-stu-id="88382-193">Learn more in detail [here](active-directory-aadconnect-sso-how-it-works.md).</span></span> <span data-ttu-id="88382-194">為了提升安全性，建議您經常向前復原透過 hello Kerberos 解密金鑰，這些電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="88382-194">For improved security, it is recommended that  you frequently roll over hello Kerberos decryption keys of these computer accounts.</span></span>

>[!IMPORTANT]
><span data-ttu-id="88382-195">您不需要 toodo 這個步驟_立即_啟用 hello 功能之後。</span><span class="sxs-lookup"><span data-stu-id="88382-195">You don't need toodo this step _immediately_ after you have enabled hello feature.</span></span> <span data-ttu-id="88382-196">至少每隔 30 天變換 hello Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="88382-196">Roll over hello Kerberos decryption keys at least every 30 days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88382-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88382-197">Next steps</span></span>

- <span data-ttu-id="88382-198">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="88382-198">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="88382-199">[**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="88382-199">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="88382-200">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="88382-200">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="88382-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="88382-201">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
