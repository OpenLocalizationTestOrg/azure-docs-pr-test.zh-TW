---
title: "Azure AD 傳遞驗證 - 快速入門 | Microsoft Docs"
description: "本文說明如何開始使用 Azure Active Directory (Azure AD) 傳遞驗證。"
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
ms.openlocfilehash: 07063ea53e96c6467e40e8a7ca70e5c03ce53284
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a><span data-ttu-id="92e86-104">Azure Active Directory 傳遞驗證：快速入門</span><span class="sxs-lookup"><span data-stu-id="92e86-104">Azure Active Directory Pass-through Authentication: Quick start</span></span>

## <a name="how-to-deploy-azure-ad-pass-through-authentication"></a><span data-ttu-id="92e86-105">如何部署 Azure AD 傳遞驗證</span><span class="sxs-lookup"><span data-stu-id="92e86-105">How to deploy Azure AD Pass-through Authentication</span></span>

<span data-ttu-id="92e86-106">Azure Active Directory (Azure AD) 傳遞驗證可讓您的使用者以相同密碼登入內部部署和雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="92e86-106">Azure Active Directory (Azure AD) Pass-through Authentication allows your users to sign in to both on-premises and cloud-based applications using the same passwords.</span></span> <span data-ttu-id="92e86-107">它會直接向內部部署 Active Directory 驗證使用者的密碼，以決定是否讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-107">It signs users in by validating their passwords directly against your on-premises Active Directory.</span></span>

>[!IMPORTANT]
><span data-ttu-id="92e86-108">Azure AD 傳遞驗證目前為預覽功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-108">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="92e86-109">如果您已透過預覽版使用這項功能，請務必使用[這裡](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md)提供的指示將驗證代理程式的預覽版本升級。</span><span class="sxs-lookup"><span data-stu-id="92e86-109">If you have been using this feature through preview, you should ensure that you upgrade preview versions of the Authentication Agents using the instructions provided [here](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).</span></span>

<span data-ttu-id="92e86-110">請依照下列指示部署傳遞驗證：</span><span class="sxs-lookup"><span data-stu-id="92e86-110">You need to follow these instructions to deploy Pass-through Authentication:</span></span>

## <a name="step-1-check-prerequisites"></a><span data-ttu-id="92e86-111">步驟 1：檢查必要條件</span><span class="sxs-lookup"><span data-stu-id="92e86-111">Step 1: Check prerequisites</span></span>

<span data-ttu-id="92e86-112">請確保已具備下列必要條件︰</span><span class="sxs-lookup"><span data-stu-id="92e86-112">Ensure that the following prerequisites are in place:</span></span>

### <a name="on-the-azure-active-directory-admin-center"></a><span data-ttu-id="92e86-113">於 Azure Active Directory 管理中心</span><span class="sxs-lookup"><span data-stu-id="92e86-113">On the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="92e86-114">在 Azure AD 租用戶上建立僅限雲端的「全域管理員」帳戶。</span><span class="sxs-lookup"><span data-stu-id="92e86-114">Create a cloud-only Global Administrator account on your Azure AD tenant.</span></span> <span data-ttu-id="92e86-115">如此一來，如果您的內部部署服務失敗或無法使用，您便可以管理租用戶組態。</span><span class="sxs-lookup"><span data-stu-id="92e86-115">This way, you can manage the configuration of your tenant should your on-premises services fail or become unavailable.</span></span> <span data-ttu-id="92e86-116">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="92e86-116">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="92e86-117">這是確保您不會被租用戶封鎖的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="92e86-117">Doing this step is critical to ensure that you don't get locked out of your tenant.</span></span>
2. <span data-ttu-id="92e86-118">將一或多個[自訂網域名稱](../active-directory-add-domain.md)新增至 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92e86-118">Add one or more [custom domain name(s)](../active-directory-add-domain.md) to your Azure AD tenant.</span></span> <span data-ttu-id="92e86-119">您的使用者會使用其中一個網域名稱登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-119">Your users sign in using one of these domain names.</span></span>

### <a name="in-your-on-premises-environment"></a><span data-ttu-id="92e86-120">在內部部署環境中</span><span class="sxs-lookup"><span data-stu-id="92e86-120">In your on-premises environment</span></span>

1. <span data-ttu-id="92e86-121">識別一部執行 Windows Server 2012 R2 或更新版本的伺服器來執行 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="92e86-121">Identify a server running Windows Server 2012 R2 or later on which to run Azure AD Connect.</span></span> <span data-ttu-id="92e86-122">在需要驗證密碼的使用者所在的同一個 AD 樹系中，新增此伺服器。</span><span class="sxs-lookup"><span data-stu-id="92e86-122">Add the server to the same AD forest as the users whose passwords need to be validated.</span></span>
2. <span data-ttu-id="92e86-123">在上一個步驟中識別的伺服器上安裝[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594)。</span><span class="sxs-lookup"><span data-stu-id="92e86-123">Install the [latest version of Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) on the server identified in preceding step.</span></span> <span data-ttu-id="92e86-124">如果您已執行 Azure AD Connect，請確定版本是 1.1.557.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92e86-124">If you already have Azure AD Connect running, ensure that the version is 1.1.557.0 or later.</span></span>
3. <span data-ttu-id="92e86-125">識別額外一部執行 Windows Server 2012 R2 或更新版本的伺服器來執行獨立驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="92e86-125">Identify an additional server running Windows Server 2012 R2 or later on which to run a standalone Authentication Agent.</span></span> <span data-ttu-id="92e86-126">驗證代理程式版本必須是 1.5.193.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="92e86-126">The Authentication Agent version needs to be 1.5.193.0 or later.</span></span> <span data-ttu-id="92e86-127">這是確保有高可用性可滿足登入要求的伺服器。</span><span class="sxs-lookup"><span data-stu-id="92e86-127">This server is needed to ensure high availability of sign-in requests.</span></span> <span data-ttu-id="92e86-128">在需要驗證密碼的使用者所在的同一個 AD 樹系中，新增此伺服器。</span><span class="sxs-lookup"><span data-stu-id="92e86-128">Add the server to the same AD forest as the users whose passwords need to be validated.</span></span>
4. <span data-ttu-id="92e86-129">如果您的伺服器和 Azure AD 之間有防火牆，則您需要設定下列項目：</span><span class="sxs-lookup"><span data-stu-id="92e86-129">If there is a firewall between your servers and Azure AD, you need to configure the following items:</span></span>
   - <span data-ttu-id="92e86-130">確定驗證代理程式會透過以下連接埠對 Azure AD 提出**輸出**要求：</span><span class="sxs-lookup"><span data-stu-id="92e86-130">Ensure that Authentication Agents can make **outbound** requests to Azure AD over the following ports:</span></span>
   
   | <span data-ttu-id="92e86-131">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="92e86-131">Port number</span></span> | <span data-ttu-id="92e86-132">使用方式</span><span class="sxs-lookup"><span data-stu-id="92e86-132">How it's used</span></span> |
   | --- | --- |
   | <span data-ttu-id="92e86-133">**80**</span><span class="sxs-lookup"><span data-stu-id="92e86-133">**80**</span></span> | <span data-ttu-id="92e86-134">下載憑證撤銷清單 (CRL) 時驗證 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="92e86-134">Downloading certificate revocation lists (CRLs) while validating the SSL certificate</span></span> |
   | <span data-ttu-id="92e86-135">**443**</span><span class="sxs-lookup"><span data-stu-id="92e86-135">**443**</span></span> | <span data-ttu-id="92e86-136">所有與我們服務之間的輸出通訊</span><span class="sxs-lookup"><span data-stu-id="92e86-136">All outbound communication with our service</span></span> |
   
   <span data-ttu-id="92e86-137">如果您的防火牆根據原始使用者強制執行規則，請針對來自當作網路服務執行之 Windows 服務的流量，開放這些連接埠。</span><span class="sxs-lookup"><span data-stu-id="92e86-137">If your firewall enforces rules according to originating users, open these ports for traffic from Windows services that run as  Network Service.</span></span>
   - <span data-ttu-id="92e86-138">如果您的防火牆或 Proxy 允許建立 DNS 白名單，便可將對 **\*.msappproxy.net** 與 **\*.servicebus.windows.net** 的連線加入白名單。</span><span class="sxs-lookup"><span data-stu-id="92e86-138">If your firewall or proxy allows DNS whitelisting, whitelist connections to **\*.msappproxy.net** and **\*.servicebus.windows.net**.</span></span> <span data-ttu-id="92e86-139">如果不允許建立，請允許存取每週更新的 [Azure DataCenter IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="92e86-139">If not, allow access to [Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), which are updated weekly.</span></span>
   - <span data-ttu-id="92e86-140">您的驗證代理程式必須存取 **login.windows.net** 與 **login.microsoftonline.com**才能進行初始註冊，因此也請對這些 URL 開啟您的防火牆。</span><span class="sxs-lookup"><span data-stu-id="92e86-140">Your Authentication Agents need access to **login.windows.net** and **login.microsoftonline.com** for initial registration, so open your firewall for those URLs as well.</span></span>
   - <span data-ttu-id="92e86-141">為了驗證憑證，請解除封鎖以下 URL：**mscrl.microsoft.com:80**, **crl.microsoft.com:80**、**ocsp.msocsp.com:80** 與 **www.microsoft.com:80**。</span><span class="sxs-lookup"><span data-stu-id="92e86-141">For certificate validation, unblock the following URLs: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** and **www.microsoft.com:80**.</span></span> <span data-ttu-id="92e86-142">這些 URL 會用於其他 Microsoft 產品的憑證驗證，因此您可能已將這些 URL 解除封鎖。</span><span class="sxs-lookup"><span data-stu-id="92e86-142">These URLs are used for certificate validation with other Microsoft products, so you may already have these URLs unblocked.</span></span>

## <a name="step-2-enable-exchange-activesync-support-optional"></a><span data-ttu-id="92e86-143">步驟 2：啟用 Exchange ActiveSync 支援 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="92e86-143">Step 2: Enable Exchange ActiveSync support (optional)</span></span>

<span data-ttu-id="92e86-144">遵循以下指示啟用 Exchange ActiveSync 支援：</span><span class="sxs-lookup"><span data-stu-id="92e86-144">Follow these instructions to enable Exchange ActiveSync support:</span></span>

1. <span data-ttu-id="92e86-145">使用 [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) 執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="92e86-145">Use [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) to run the following command:</span></span>
```
Get-OrganizationConfig | fl per*
```

2. <span data-ttu-id="92e86-146">檢查 `PerTenantSwitchToESTSEnabled` 設定的值。</span><span class="sxs-lookup"><span data-stu-id="92e86-146">Check the value of the `PerTenantSwitchToESTSEnabled` setting.</span></span> <span data-ttu-id="92e86-147">如果值為 **true**，則您的租用戶已正確設定，大部分客戶通常均是如此。</span><span class="sxs-lookup"><span data-stu-id="92e86-147">If the value is **true**, your tenant is properly configured - this is generally the case for most customers.</span></span> <span data-ttu-id="92e86-148">如果值為**false**，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="92e86-148">If the value is **false**, run the following command:</span></span>
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. <span data-ttu-id="92e86-149">驗證 `PerTenantSwitchToESTSEnabled` 設定的值現在設為 **true**。</span><span class="sxs-lookup"><span data-stu-id="92e86-149">Verify that the value of the `PerTenantSwitchToESTSEnabled` setting is now set to **true**.</span></span> <span data-ttu-id="92e86-150">等候一小時，再開始下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="92e86-150">Wait an hour before moving to the next step.</span></span>

<span data-ttu-id="92e86-151">如果進行此步驟時碰到任何問題，請查閱我們的[疑難排解指南](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues)以取得更多資訊。</span><span class="sxs-lookup"><span data-stu-id="92e86-151">If you face any issues during this step, check our [troubleshooting guide](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) for more information.</span></span>

## <a name="step-3-enable-the-feature"></a><span data-ttu-id="92e86-152">步驟 3︰啟用功能</span><span class="sxs-lookup"><span data-stu-id="92e86-152">Step 3: Enable the feature</span></span>

<span data-ttu-id="92e86-153">您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 來啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="92e86-153">Pass-through Authentication can be enabled using [Azure AD Connect](active-directory-aadconnect.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="92e86-154">您可以在 Azure AD Connect 主要或暫存伺服器上啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="92e86-154">Pass-through Authentication can be enabled on the Azure AD Connect primary or staging server.</span></span> <span data-ttu-id="92e86-155">強烈建議您從主要伺服器啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-155">It is highly recommended that you enable it from the primary server.</span></span>

<span data-ttu-id="92e86-156">如果您是第一次安裝 Azure AD Connect，請選擇[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="92e86-156">If you are installing Azure AD Connect for the first time, choose the [custom installation path](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="92e86-157">在 [使用者登入] 頁面上，選擇 [傳遞驗證] 作為登入方法。</span><span class="sxs-lookup"><span data-stu-id="92e86-157">At the **User sign-in** page, choose **Pass-through Authentication** as the Sign on method.</span></span> <span data-ttu-id="92e86-158">成功完成時，傳遞驗證代理程式會安裝在 Azure AD Connect 所在的同一部伺服器上。</span><span class="sxs-lookup"><span data-stu-id="92e86-158">On successful completion, a Pass-through Authentication agent is installed on the same server as Azure AD Connect.</span></span> <span data-ttu-id="92e86-159">此外，您的租用戶上也會啟用傳遞驗證功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-159">In addition, the Pass-through Authentication feature is enabled on your tenant.</span></span>

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso3.png)

<span data-ttu-id="92e86-161">如果您已安裝 Azure AD Connect (使用[快速安裝](active-directory-aadconnect-get-started-express.md)或[自訂安裝](active-directory-aadconnect-get-started-custom.md)路徑)，請在 Azure AD Connect 上選取 [變更使用者登入] 頁面，並按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="92e86-161">If you have already installed Azure AD Connect (using the [express installation](active-directory-aadconnect-get-started-express.md) or the [custom installation](active-directory-aadconnect-get-started-custom.md) path), select **Change user sign-in page** on Azure AD Connect, and click **Next**.</span></span> <span data-ttu-id="92e86-162">然後選取 [傳遞驗證] 作為登入方法。</span><span class="sxs-lookup"><span data-stu-id="92e86-162">Then select **Pass-through Authentication** as the Sign on method.</span></span> <span data-ttu-id="92e86-163">成功完成時，傳遞驗證代理程式會安裝在 Azure AD Connect 所在的同一部伺服器上，且您的租用戶上會啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-163">On successful completion, a Pass-through Authentication agent is installed on the same server as Azure AD Connect and the feature is enabled on your tenant.</span></span>

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
><span data-ttu-id="92e86-165">傳遞驗證是租用戶層級的功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-165">Pass-through Authentication is a tenant-level feature.</span></span> <span data-ttu-id="92e86-166">開啟此功能會影響租用戶中「所有」受管理網域的使用者登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-166">Turning it on impacts sign-in for users across _all_ the managed domains in your tenant.</span></span> <span data-ttu-id="92e86-167">如果您正從 AD FS 切換到傳遞驗證，建議您先等待至少 12 個小時，再關閉您的 AD FS 基礎結構，需要等待時間是為了確保在轉換期間內，使用者可以繼續登入 Exchange ActiveSync。</span><span class="sxs-lookup"><span data-stu-id="92e86-167">If you are switching from AD FS to Pass-through Authentication, we recommend that you wait at least 12 hours before shutting down your AD FS infrastructure - this wait time is to ensure that users can keep signing in to Exchange ActiveSync during transition.</span></span>

## <a name="step-4-test-the-feature"></a><span data-ttu-id="92e86-168">步驟 4：測試功能</span><span class="sxs-lookup"><span data-stu-id="92e86-168">Step 4: Test the feature</span></span>

<span data-ttu-id="92e86-169">請遵循下列指示來確認您已正確啟用傳遞驗證：</span><span class="sxs-lookup"><span data-stu-id="92e86-169">Follow these instructions to verify that you have enabled Pass-through Authentication correctly:</span></span>

1. <span data-ttu-id="92e86-170">使用租用戶的全域管理員認證來登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="92e86-170">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with the Global Administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="92e86-171">按一下左側導覽上的 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="92e86-171">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="92e86-172">選取 [Azure AD Connect]。</span><span class="sxs-lookup"><span data-stu-id="92e86-172">Select **Azure AD Connect**.</span></span>
4. <span data-ttu-id="92e86-173">確認 [傳遞驗證] 功能顯示為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="92e86-173">Verify that the **Pass-through Authentication** feature shows as **Enabled**.</span></span>
5. <span data-ttu-id="92e86-174">選取 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="92e86-174">Select **Pass-through Authentication**.</span></span> <span data-ttu-id="92e86-175">此刀鋒視窗會列出驗證代理程式的安裝位置。</span><span class="sxs-lookup"><span data-stu-id="92e86-175">This blade lists the servers where your Authentication Agents are installed.</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

<span data-ttu-id="92e86-178">在此階段，租用戶中所有受管理網域的使用者都可以使用傳遞驗證來登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-178">At this stage, users from all managed domains in your tenant can sign in using Pass-through Authentication.</span></span> <span data-ttu-id="92e86-179">不過，同盟網域的使用者會繼續使用 Active Directory Federation Services (ADFS) 或您先前設定的其他同盟提供者來登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-179">However, users from federated domains continue to sign in using Active Directory Federation Services (AD FS) or another federation provider that you have previously configured.</span></span> <span data-ttu-id="92e86-180">如果您將同盟網域轉換成受管理網域，該網域中的所有使用者都會自動開始使用傳遞驗證來登入。</span><span class="sxs-lookup"><span data-stu-id="92e86-180">If you convert a domain from federated to managed, all users from that domain automatically start signing in using Pass-through Authentication.</span></span> <span data-ttu-id="92e86-181">傳遞驗證功能不會影響僅限雲端的使用者。</span><span class="sxs-lookup"><span data-stu-id="92e86-181">Cloud-only users are not impacted by the Pass-through Authentication feature.</span></span>

## <a name="step-5-ensure-high-availability"></a><span data-ttu-id="92e86-182">步驟 5：確保高可用性</span><span class="sxs-lookup"><span data-stu-id="92e86-182">Step 5: Ensure high availability</span></span>

<span data-ttu-id="92e86-183">如果您打算在生產環境中部署傳遞驗證，您應該安裝獨立驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="92e86-183">If you plan to deploy Pass-through Authentication in a production environment, you should install a standalone Authentication Agent.</span></span> <span data-ttu-id="92e86-184">在執行 Azure AD Connect 和第一個驗證代理程式「以外」的伺服器上，安裝這第二個驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="92e86-184">Install this second Authentication Agent on a server _other_ than the one running Azure AD Connect and the first Authentication Agent.</span></span> <span data-ttu-id="92e86-185">此設定可提供高可用性來滿足登入要求。</span><span class="sxs-lookup"><span data-stu-id="92e86-185">This setup provides you high availability of sign-in requests.</span></span> <span data-ttu-id="92e86-186">請依照下列指示來部署獨立驗證代理程式：</span><span class="sxs-lookup"><span data-stu-id="92e86-186">Follow these instructions to deploy a standalone Authentication Agent:</span></span>

1. <span data-ttu-id="92e86-187">**下載最新版的驗證代理程式 (1.5.193.0 版或更新版本)**：使用您租用戶的全域管理員認證登入 [Azure Active Directory 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="92e86-187">**Download the latest version of the Authentication Agent (versions 1.5.193.0 or later)**: Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with your tenant's Global Administrator credentials.</span></span>
2. <span data-ttu-id="92e86-188">按一下左側導覽上的 [Azure Active Directory]。</span><span class="sxs-lookup"><span data-stu-id="92e86-188">Select **Azure Active Directory** on the left-hand navigation.</span></span>
3. <span data-ttu-id="92e86-189">依序選取 [Azure AD Connect] 和 [傳遞驗證]。</span><span class="sxs-lookup"><span data-stu-id="92e86-189">Select **Azure AD Connect** and then **Pass-through Authentication**.</span></span> <span data-ttu-id="92e86-190">然後選取 [下載代理程式]。</span><span class="sxs-lookup"><span data-stu-id="92e86-190">And select **Download agent**.</span></span>
4. <span data-ttu-id="92e86-191">按一下 [接受條款並下載] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92e86-191">Click the **Accept terms & download** button.</span></span>
5. <span data-ttu-id="92e86-192">**安裝最新版的驗證代理程式**：執行在上個步驟中下載的可執行檔。</span><span class="sxs-lookup"><span data-stu-id="92e86-192">**Install the latest version of the Authentication Agent**: Run the executable downloaded in the preceding step.</span></span> <span data-ttu-id="92e86-193">出現提示時，提供您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="92e86-193">Provide your tenant's Global Administrator credentials when prompted.</span></span>

![Azure Active Directory 管理中心 - 下載驗證代理程式按鈕](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory 管理中心 - 下載代理程式刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
><span data-ttu-id="92e86-196">您也可以從[這裡](https://aka.ms/getauthagent)下載驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="92e86-196">You can also download the Authentication Agent from [here](https://aka.ms/getauthagent).</span></span> <span data-ttu-id="92e86-197">請確定在安裝_之前_，檢閱並接受驗證代理程式的[服務條款](https://aka.ms/authagenteula)。</span><span class="sxs-lookup"><span data-stu-id="92e86-197">Ensure that you review and accept the Authentication Agent's [Terms of Service](https://aka.ms/authagenteula) _before_ installing it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92e86-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92e86-198">Next steps</span></span>
- <span data-ttu-id="92e86-199">[**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="92e86-199">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="92e86-200">了解支援的情節和不支援的情節。</span><span class="sxs-lookup"><span data-stu-id="92e86-200">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="92e86-201">[**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="92e86-201">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="92e86-202">[**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) - 常見問題集的答案。</span><span class="sxs-lookup"><span data-stu-id="92e86-202">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="92e86-203">[**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="92e86-203">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="92e86-204">[**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。</span><span class="sxs-lookup"><span data-stu-id="92e86-204">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="92e86-205">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="92e86-205">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
