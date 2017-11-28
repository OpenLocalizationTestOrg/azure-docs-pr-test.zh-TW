---
title: "Azure AD 傳遞驗證 - 快速入門 | Microsoft Docs"
description: "本文說明 tooget 如何開始使用 Azure Active Directory (Azure AD) 的傳遞驗證。"
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a><span data-ttu-id="6e525-104">Azure Active Directory 傳遞驗證：快速入門</span><span class="sxs-lookup"><span data-stu-id="6e525-104">Azure Active Directory Pass-through Authentication: Quick start</span></span>

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a><span data-ttu-id="6e525-105">如何 toodeploy Azure AD 通過驗證</span><span class="sxs-lookup"><span data-stu-id="6e525-105">How toodeploy Azure AD Pass-through Authentication</span></span>

<span data-ttu-id="6e525-106">Azure Active Directory (Azure AD) 通過驗證可讓使用者 toosign tooboth 內部和雲端型應用程式使用 hello 相同密碼。</span><span class="sxs-lookup"><span data-stu-id="6e525-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users toosign in tooboth on-premises and cloud-based applications using hello same passwords.</span></span> <span data-ttu-id="6e525-107">它會直接向內部部署 Active Directory 驗證使用者的密碼，以決定是否讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="6e525-107">It signs users in by validating their passwords directly against your on-premises Active Directory.</span></span>

>[!IMPORTANT]
><span data-ttu-id="6e525-108">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-108">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="6e525-109">如果您已使用預覽透過這項功能，您應該確定您已升級的 hello 驗證代理程式的預覽版本使用所提供的 hello 指示[這裡](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="6e525-109">If you have been using this feature through preview, you should ensure that you upgrade preview versions of hello Authentication Agents using hello instructions provided [here](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).</span></span>

<span data-ttu-id="6e525-110">您需要 toofollow 這些指示 toodeploy 傳遞驗證：</span><span class="sxs-lookup"><span data-stu-id="6e525-110">You need toofollow these instructions toodeploy Pass-through Authentication:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="6e525-111">步驟 1：檢查必要條件</span><span class="sxs-lookup"><span data-stu-id="6e525-111">Step 1: Check prerequisites</span></span>

<span data-ttu-id="6e525-112">請確定該 hello 下列必要條件已就緒：</span><span class="sxs-lookup"><span data-stu-id="6e525-112">Ensure that hello following prerequisites are in place:</span></span>

### <a name="on-hello-azure-active-directory-admin-center"></a><span data-ttu-id="6e525-113">在 hello Azure Active Directory 系統管理中心</span><span class="sxs-lookup"><span data-stu-id="6e525-113">On hello Azure Active Directory admin center</span></span>

1. <span data-ttu-id="6e525-114">在 Azure AD 租用戶上建立僅限雲端的「全域管理員」帳戶。</span><span class="sxs-lookup"><span data-stu-id="6e525-114">Create a cloud-only Global Administrator account on your Azure AD tenant.</span></span> <span data-ttu-id="6e525-115">如此一來，您可以管理租用戶 hello 設定應該在內部部署服務失敗或無法使用。</span><span class="sxs-lookup"><span data-stu-id="6e525-115">This way, you can manage hello configuration of your tenant should your on-premises services fail or become unavailable.</span></span> <span data-ttu-id="6e525-116">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6e525-116">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="6e525-117">這個步驟是您不會遭到鎖定您的租用戶的重要 tooensure。</span><span class="sxs-lookup"><span data-stu-id="6e525-117">Doing this step is critical tooensure that you don't get locked out of your tenant.</span></span>
2. <span data-ttu-id="6e525-118">新增一或多個[自訂網域名稱](../active-directory-add-domain.md)tooyour Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6e525-118">Add one or more [custom domain name(s)](../active-directory-add-domain.md) tooyour Azure AD tenant.</span></span> <span data-ttu-id="6e525-119">您的使用者會使用其中一個網域名稱登入。</span><span class="sxs-lookup"><span data-stu-id="6e525-119">Your users sign in using one of these domain names.</span></span>

### <a name="in-your-on-premises-environment"></a><span data-ttu-id="6e525-120">在內部部署環境中</span><span class="sxs-lookup"><span data-stu-id="6e525-120">In your on-premises environment</span></span>

1. <span data-ttu-id="6e525-121">識別執行 Windows Server 2012 R2 或更新版本上的 toorun Azure AD Connect 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6e525-121">Identify a server running Windows Server 2012 R2 or later on which toorun Azure AD Connect.</span></span> <span data-ttu-id="6e525-122">新增 hello 伺服器 toohello 相同 AD 樹系做為其密碼需要驗證的 toobe hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="6e525-122">Add hello server toohello same AD forest as hello users whose passwords need toobe validated.</span></span>
2. <span data-ttu-id="6e525-123">安裝 hello[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) hello 上一個步驟中所識別的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="6e525-123">Install hello [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) on hello server identified in preceding step.</span></span> <span data-ttu-id="6e525-124">如果您已經有 Azure AD Connect 執行，請確定該 hello 版本 1.1.557.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e525-124">If you already have Azure AD Connect running, ensure that hello version is 1.1.557.0 or later.</span></span>
3. <span data-ttu-id="6e525-125">找出額外的伺服器執行 Windows Server 2012 R2 或稍後哪些 toorun 的獨立驗證代理程式 」。</span><span class="sxs-lookup"><span data-stu-id="6e525-125">Identify an additional server running Windows Server 2012 R2 or later on which toorun a standalone Authentication Agent.</span></span> <span data-ttu-id="6e525-126">必須 toobe 1.5.193.0 的 hello 驗證代理程式版本或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6e525-126">hello Authentication Agent version needs toobe 1.5.193.0 or later.</span></span> <span data-ttu-id="6e525-127">此伺服器是需要的 tooensure 的登入要求的高可用性。</span><span class="sxs-lookup"><span data-stu-id="6e525-127">This server is needed tooensure high availability of sign-in requests.</span></span> <span data-ttu-id="6e525-128">新增 hello 伺服器 toohello 相同 AD 樹系做為其密碼需要驗證的 toobe hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="6e525-128">Add hello server toohello same AD forest as hello users whose passwords need toobe validated.</span></span>
4. <span data-ttu-id="6e525-129">如果您的伺服器和 Azure AD 之間的防火牆，您需要下列項目 tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="6e525-129">If there is a firewall between your servers and Azure AD, you need tooconfigure hello following items:</span></span>
   - <span data-ttu-id="6e525-130">請驗證代理程式可以做出**輸出**要求 tooAzure AD 透過下列連接埠的 hello:</span><span class="sxs-lookup"><span data-stu-id="6e525-130">Ensure that Authentication Agents can make **outbound** requests tooAzure AD over hello following ports:</span></span>
   
   | <span data-ttu-id="6e525-131">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="6e525-131">Port number</span></span> | <span data-ttu-id="6e525-132">使用方式</span><span class="sxs-lookup"><span data-stu-id="6e525-132">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="6e525-133">**80**</span><span class="sxs-lookup"><span data-stu-id="6e525-133">**80**</span></span> | <span data-ttu-id="6e525-134">下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6e525-134">Downloading certificate revocation lists (CRLs) while validating hello SSL certificate</span></span> |
   | <span data-ttu-id="6e525-135">**443**</span><span class="sxs-lookup"><span data-stu-id="6e525-135">**443**</span></span> | <span data-ttu-id="6e525-136">所有與我們服務之間的輸出通訊</span><span class="sxs-lookup"><span data-stu-id="6e525-136">All outbound communication with our service</span></span> |
   
   <span data-ttu-id="6e525-137">如果您的防火牆，強制執行規則，根據 toooriginating 使用者，開啟這些連接埠的流量從做為網路服務執行的 Windows 服務。</span><span class="sxs-lookup"><span data-stu-id="6e525-137">If your firewall enforces rules according toooriginating users, open these ports for traffic from Windows services that run as  Network Service.</span></span>
   - <span data-ttu-id="6e525-138">如果您的防火牆或 proxy 可讓 DNS 允許清單，白名單連線太**\*。 msappproxy.net**和 **\*。.servicebus.windows.net**。</span><span class="sxs-lookup"><span data-stu-id="6e525-138">If your firewall or proxy allows DNS whitelisting, whitelist connections too**\*.msappproxy.net** and **\*.servicebus.windows.net**.</span></span> <span data-ttu-id="6e525-139">如果沒有，請允許存取太[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這每週更新。</span><span class="sxs-lookup"><span data-stu-id="6e525-139">If not, allow access too[Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.</span></span>
   - <span data-ttu-id="6e525-140">驗證代理程式需要存取太**login.windows.net**和**login.microsoftonline.com**的初始註冊時，開啟您的防火牆，以及這些 url。</span><span class="sxs-lookup"><span data-stu-id="6e525-140">Your Authentication Agents need access too**login.windows.net** and **login.microsoftonline.com** for initial registration, so open your firewall for those URLs as well.</span></span>
   - <span data-ttu-id="6e525-141">憑證驗證解除封鎖 hello 下列 Url: **mscrl.microsoft.com:80**， **crl.microsoft.com:80**， **ocsp.msocsp.com:80**和**www.microsoft.com:80**。</span><span class="sxs-lookup"><span data-stu-id="6e525-141">For certificate validation, unblock hello following URLs: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** and **www.microsoft.com:80**.</span></span> <span data-ttu-id="6e525-142">這些 URL 會用於其他 Microsoft 產品的憑證驗證，因此您可能已將這些 URL 解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="6e525-142">These URLs are used for certificate validation with other Microsoft products, so you may already have these URLs unblocked.</span></span>

## <a name="step-2-enable-exchange-activesync-support-optional"></a><span data-ttu-id="6e525-143">步驟 2：啟用 Exchange ActiveSync 支援 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="6e525-143">Step 2: Enable Exchange ActiveSync support (optional)</span></span>

<span data-ttu-id="6e525-144">請遵循這些指示 tooenable Exchange ActiveSync 的支援：</span><span class="sxs-lookup"><span data-stu-id="6e525-144">Follow these instructions tooenable Exchange ActiveSync support:</span></span>

1. <span data-ttu-id="6e525-145">使用[Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) toorun hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6e525-145">Use [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) toorun hello following command:</span></span>
```
Get-OrganizationConfig | fl per*
```

2. <span data-ttu-id="6e525-146">檢查 hello hello 值`PerTenantSwitchToESTSEnabled`設定。</span><span class="sxs-lookup"><span data-stu-id="6e525-146">Check hello value of hello `PerTenantSwitchToESTSEnabled` setting.</span></span> <span data-ttu-id="6e525-147">如果 hello 值**true**、 您的租用戶已正確設定-通常是對大多數客戶來說 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="6e525-147">If hello value is **true**, your tenant is properly configured - this is generally hello case for most customers.</span></span> <span data-ttu-id="6e525-148">如果 hello 值**false**，請執行 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="6e525-148">If hello value is **false**, run hello following command:</span></span>
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. <span data-ttu-id="6e525-149">請確認 hello 值的 hello`PerTenantSwitchToESTSEnabled`現在設定為太**true**。</span><span class="sxs-lookup"><span data-stu-id="6e525-149">Verify that hello value of hello `PerTenantSwitchToESTSEnabled` setting is now set too**true**.</span></span> <span data-ttu-id="6e525-150">等候一小時前移動 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="6e525-150">Wait an hour before moving toohello next step.</span></span>

<span data-ttu-id="6e525-151">如果進行此步驟時碰到任何問題，請查閱我們的[疑難排解指南](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues)以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="6e525-151">If you face any issues during this step, check our [troubleshooting guide](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) for more information.</span></span>

## <a name="step-3-enable-hello-feature"></a><span data-ttu-id="6e525-152">步驟 3： 啟用 hello 功能</span><span class="sxs-lookup"><span data-stu-id="6e525-152">Step 3: Enable hello feature</span></span>

<span data-ttu-id="6e525-153">您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 來啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="6e525-153">Pass-through Authentication can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="6e525-154">Hello Azure AD Connect 的主要或暫存伺服器上，可以啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="6e525-154">Pass-through Authentication can be enabled on hello Azure AD Connect primary or staging server.</span></span> <span data-ttu-id="6e525-155">強烈建議您啟用從 hello 主要伺服器。</span><span class="sxs-lookup"><span data-stu-id="6e525-155">It is highly recommended that you enable it from hello primary server.</span></span>

<span data-ttu-id="6e525-156">如果您第一次安裝 Azure AD Connect hello，選擇 hello[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="6e525-156">If you are installing Azure AD Connect for hello first time, choose hello [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="6e525-157">在 hello**使用者登入**頁面上，選擇**傳遞驗證**為 hello 登入方法。</span><span class="sxs-lookup"><span data-stu-id="6e525-157">At hello **User sign-in** page, choose **Pass-through Authentication** as hello Sign on method.</span></span> <span data-ttu-id="6e525-158">成功完成時，傳遞驗證代理程式安裝在 hello 與 Azure AD Connect 相同的伺服器。</span><span class="sxs-lookup"><span data-stu-id="6e525-158">On successful completion, a Pass-through Authentication agent is installed on hello same server as Azure AD Connect.</span></span> <span data-ttu-id="6e525-159">此外，您的租用戶上啟用 hello 傳遞驗證功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-159">In addition, hello Pass-through Authentication feature is enabled on your tenant.</span></span>

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso3.png)

<span data-ttu-id="6e525-161">如果您已安裝 Azure AD Connect (使用 hello[快速安裝](active-directory-aadconnect-get-started-express.md)或 hello[自訂安裝](active-directory-aadconnect-get-started-custom.md)路徑)，請選取**變更使用者的登入頁面**上 Azure AD連接，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="6e525-161">If you have already installed Azure AD Connect (using hello [express installation](active-directory-aadconnect-get-started-express.md) or hello [custom installation](active-directory-aadconnect-get-started-custom.md) path), select **Change user sign-in page** on Azure AD Connect, and click **Next**.</span></span> <span data-ttu-id="6e525-162">然後選取**傳遞驗證**為 hello 登入方法。</span><span class="sxs-lookup"><span data-stu-id="6e525-162">Then select **Pass-through Authentication** as hello Sign on method.</span></span> <span data-ttu-id="6e525-163">成功完成時，傳遞驗證代理程式安裝在 hello 與 Azure AD Connect 和 hello 功能相同的伺服器已啟用您的租用戶上。</span><span class="sxs-lookup"><span data-stu-id="6e525-163">On successful completion, a Pass-through Authentication agent is installed on hello same server as Azure AD Connect and hello feature is enabled on your tenant.</span></span>

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
><span data-ttu-id="6e525-165">傳遞驗證是租用戶層級的功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-165">Pass-through Authentication is a tenant-level feature.</span></span> <span data-ttu-id="6e525-166">開啟此功能會影響的跨使用者登入_所有_hello 管理您的租用戶中的網域。</span><span class="sxs-lookup"><span data-stu-id="6e525-166">Turning it on impacts sign-in for users across _all_ hello managed domains in your tenant.</span></span> <span data-ttu-id="6e525-167">如果您要從 AD FS tooPass 透過驗證切換，我們建議您等待至少 12 小時，關閉您的 AD FS 基礎結構之前，-這個等候時間是使用者可以保持登入 tooExchange ActiveSync 轉換期間的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="6e525-167">If you are switching from AD FS tooPass-through Authentication, we recommend that you wait at least 12 hours before shutting down your AD FS infrastructure - this wait time is tooensure that users can keep signing in tooExchange ActiveSync during transition.</span></span>

## <a name="step-4-test-hello-feature"></a><span data-ttu-id="6e525-168">步驟 4： 測試 hello 功能</span><span class="sxs-lookup"><span data-stu-id="6e525-168">Step 4: Test hello feature</span></span>

<span data-ttu-id="6e525-169">請遵循這些指示 tooverify，您已正確啟用傳遞驗證：</span><span class="sxs-lookup"><span data-stu-id="6e525-169">Follow these instructions tooverify that you have enabled Pass-through Authentication correctly:</span></span>

1. <span data-ttu-id="6e525-170">登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6e525-170">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with hello Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="6e525-171">選取**Azure Active Directory** hello 左側導覽上。</span><span class="sxs-lookup"><span data-stu-id="6e525-171">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="6e525-172">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="6e525-172">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="6e525-173">請確認該 hello**傳遞驗證**功能就會顯示為**啟用**。</span><span class="sxs-lookup"><span data-stu-id="6e525-173">Verify that hello **Pass-through Authentication** feature shows as **Enabled**.</span></span>
5. <span data-ttu-id="6e525-174">選取 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="6e525-174">Select **Pass-through Authentication**.</span></span> <span data-ttu-id="6e525-175">此刀鋒視窗會列出 hello 伺服器驗證代理程式的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="6e525-175">This blade lists hello servers where your Authentication Agents are installed.</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

<span data-ttu-id="6e525-178">在此階段，租用戶中所有受管理網域的使用者都可以使用傳遞驗證來登入。</span><span class="sxs-lookup"><span data-stu-id="6e525-178">At this stage, users from all managed domains in your tenant can sign in using Pass-through Authentication.</span></span> <span data-ttu-id="6e525-179">不過，同盟網域的使用者會繼續 toosign 中使用 Active Directory Federation Services (AD FS) 或您先前設定的另一個同盟提供者。</span><span class="sxs-lookup"><span data-stu-id="6e525-179">However, users from federated domains continue toosign in using Active Directory Federation Services (AD FS) or another federation provider that you have previously configured.</span></span> <span data-ttu-id="6e525-180">如果您從同盟 toomanaged 轉換網域，請從該網域的所有使用者會自動都啟動使用傳遞驗證登入。</span><span class="sxs-lookup"><span data-stu-id="6e525-180">If you convert a domain from federated toomanaged, all users from that domain automatically start signing in using Pass-through Authentication.</span></span> <span data-ttu-id="6e525-181">僅限雲端的使用者不會受到 hello 通過驗證功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-181">Cloud-only users are not impacted by hello Pass-through Authentication feature.</span></span>

## <a name="step-5-ensure-high-availability"></a><span data-ttu-id="6e525-182">步驟 5：確保高可用性</span><span class="sxs-lookup"><span data-stu-id="6e525-182">Step 5: Ensure high availability</span></span>

<span data-ttu-id="6e525-183">如果您計劃 toodeploy 傳遞驗證實際執行環境中的，您應該安裝在獨立驗證代理程式 」。</span><span class="sxs-lookup"><span data-stu-id="6e525-183">If you plan toodeploy Pass-through Authentication in a production environment, you should install a standalone Authentication Agent.</span></span> <span data-ttu-id="6e525-184">在伺服器上安裝此第二個驗證代理程式_其他_比 hello 一個執行 Azure AD Connect 與 hello 第一個驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="6e525-184">Install this second Authentication Agent on a server _other_ than hello one running Azure AD Connect and hello first Authentication Agent.</span></span> <span data-ttu-id="6e525-185">此設定可提供高可用性來滿足登入要求。</span><span class="sxs-lookup"><span data-stu-id="6e525-185">This setup provides you high availability of sign-in requests.</span></span> <span data-ttu-id="6e525-186">請遵循這些指示 toodeploy 獨立驗證代理程式：</span><span class="sxs-lookup"><span data-stu-id="6e525-186">Follow these instructions toodeploy a standalone Authentication Agent:</span></span>

1. <span data-ttu-id="6e525-187">**下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6e525-187">**Download hello latest version of hello Authentication Agent (versions 1.5.193.0 or later)**: Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span>
2. <span data-ttu-id="6e525-188">選取**Azure Active Directory** hello 左側導覽上。</span><span class="sxs-lookup"><span data-stu-id="6e525-188">Select **Azure Active Directory** on hello left-hand navigation.</span></span>
3. <span data-ttu-id="6e525-189">依序選取 [Azure AD Connect] 和 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="6e525-189">Select **Azure AD Connect** and then **Pass-through Authentication**.</span></span> <span data-ttu-id="6e525-190">然後選取 [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="6e525-190">And select **Download agent**.</span></span>
4. <span data-ttu-id="6e525-191">按一下 hello**接受條款 （& s) 下載** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6e525-191">Click hello **Accept terms & download** button.</span></span>
5. <span data-ttu-id="6e525-192">**Hello 最新版本的 hello 驗證代理程式安裝**: hello 前面步驟中所下載的可執行檔執行 hello。</span><span class="sxs-lookup"><span data-stu-id="6e525-192">**Install hello latest version of hello Authentication Agent**: Run hello executable downloaded in hello preceding step.</span></span> <span data-ttu-id="6e525-193">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="6e525-193">Provide your tenant's Global Administrator credentials when prompted.</span></span>

![Azure Active Directory 管理中心 - 下載驗證代理程式按鈕](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory 管理中心 - 下載代理程式刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
><span data-ttu-id="6e525-196">您也可以下載 hello 驗證代理程式 」 從[這裡](https://aka.ms/getauthagent)。</span><span class="sxs-lookup"><span data-stu-id="6e525-196">You can also download hello Authentication Agent from [here](https://aka.ms/getauthagent).</span></span> <span data-ttu-id="6e525-197">請確定您檢閱並接受 hello 驗證代理程式的[服務條款](https://aka.ms/authagenteula)_之前_安裝它。</span><span class="sxs-lookup"><span data-stu-id="6e525-197">Ensure that you review and accept hello Authentication Agent's [Terms of Service](https://aka.ms/authagenteula) _before_ installing it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e525-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e525-198">Next steps</span></span>
- <span data-ttu-id="6e525-199">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="6e525-199">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="6e525-200">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="6e525-200">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="6e525-201">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="6e525-201">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="6e525-202">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="6e525-202">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="6e525-203">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-203">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="6e525-204">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="6e525-204">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="6e525-205">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="6e525-205">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
