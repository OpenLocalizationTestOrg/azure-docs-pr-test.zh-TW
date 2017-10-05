---
title: "Office 365 和 Azure AD 使用者的憑證更新 | Microsoft Docs"
description: "本文說明 Office 365 使用者如何解決收到電子郵件通知續約憑證的問題。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7f1a3303eff9c413602e745b702baa659343eba6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a><span data-ttu-id="2ffaa-103">更新 Office 365 和 Azure Active Directory 的同盟憑證</span><span class="sxs-lookup"><span data-stu-id="2ffaa-103">Renew federation certificates for Office 365 and Azure Active Directory</span></span>
## <a name="overview"></a><span data-ttu-id="2ffaa-104">Overview</span><span class="sxs-lookup"><span data-stu-id="2ffaa-104">Overview</span></span>
<span data-ttu-id="2ffaa-105">為了讓 Azure Active Directory (Azure AD) 與 Active Directory Federation Services (AD FS) 之間能夠成功地同盟，AD FS 用來向 Azure AD 簽署安全性權杖的憑證應該符合 Azure AD 中所設定的憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-105">For successful federation between Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS), the certificates used by AD FS to sign security tokens to Azure AD should match what is configured in Azure AD.</span></span> <span data-ttu-id="2ffaa-106">任何不相符都可能導致信任受損。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-106">Any mismatch can lead to broken trust.</span></span> <span data-ttu-id="2ffaa-107">Azure AD 會確保這項資訊在您部署 AD FS 和 Web 應用程式 Proxy (適用於外部網路存取) 時保持同步。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-107">Azure AD ensures that this information is kept in sync when you deploy AD FS and Web Application Proxy (for extranet access).</span></span>

<span data-ttu-id="2ffaa-108">本文提供您其他資訊，以便在下列情況時管理權杖簽署憑證，並讓憑證與 Azure AD 保持同步︰</span><span class="sxs-lookup"><span data-stu-id="2ffaa-108">This article provides you additional information to manage your token signing certificates and keep them in sync with Azure AD, in the following cases:</span></span>

* <span data-ttu-id="2ffaa-109">您不會部署 Web 應用程式 Proxy，因此無法在外部網路取得同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-109">You are not deploying the Web Application Proxy, and therefore the federation metadata is not available in the extranet.</span></span>
* <span data-ttu-id="2ffaa-110">您不會對權杖簽署憑證使用預設的 AD FS 設定。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-110">You are not using the default configuration of AD FS for token signing certificates.</span></span>
* <span data-ttu-id="2ffaa-111">您要使用協力廠商的識別提供者。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-111">You are using a third-party identity provider.</span></span>

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a><span data-ttu-id="2ffaa-112">權杖簽署憑證的預設 AD FS 設定</span><span class="sxs-lookup"><span data-stu-id="2ffaa-112">Default configuration of AD FS for token signing certificates</span></span>
<span data-ttu-id="2ffaa-113">權杖簽署和權杖解密憑證通常是自我簽署的憑證，有效期為一年。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-113">The token signing and token decrypting certificates are usually self-signed certificates, and are good for one year.</span></span> <span data-ttu-id="2ffaa-114">根據預設，AD FS 包含名為 **AutoCertificateRollover**的自動更新程序。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-114">By default, AD FS includes an auto-renewal process called **AutoCertificateRollover**.</span></span> <span data-ttu-id="2ffaa-115">如果您使用 AD FS 2.0 或更新版本，Office 365 和 Azure AD 在您的憑證到期之前會自動進行更新。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-115">If you are using AD FS 2.0 or later, Office 365 and Azure AD automatically update your certificate before it expires.</span></span>

### <a name="renewal-notification-from-the-office-365-portal-or-an-email"></a><span data-ttu-id="2ffaa-116">從 Office 365 入口網站或電子郵件更新通知</span><span class="sxs-lookup"><span data-stu-id="2ffaa-116">Renewal notification from the Office 365 portal or an email</span></span>
> [!NOTE]
> <span data-ttu-id="2ffaa-117">如果您收到電子郵件或入口網站通知，要求您更新 Office 憑證，請參閱 [管理權杖簽署憑證的變更](#managecerts) ，檢查您是否需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-117">If you received an email or a portal notification asking you to renew your certificate for Office, see [Managing changes to token signing certificates](#managecerts) to check if you need to take any action.</span></span> <span data-ttu-id="2ffaa-118">Microsoft 已知可能會有在不需要採取任何動作的情況下仍送出憑證更新通知的問題。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-118">Microsoft is aware of a possible issue that can lead to notifications for certificate renewal being sent, even when no action is required.</span></span>
>
>

<span data-ttu-id="2ffaa-119">Azure AD 會嘗試監視同盟中繼資料，並依照此中繼資料的指示更新權杖簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-119">Azure AD attempts to monitor the federation metadata, and update the token signing certificates as indicated by this metadata.</span></span> <span data-ttu-id="2ffaa-120">在權杖簽署憑證到期前 30 天，Azure AD 會藉由輪詢同盟中繼資料，檢查是否已有新的憑證可供使用。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-120">30 days before the expiration of the token signing certificates, Azure AD checks if new certificates are available by polling the federation metadata.</span></span>

* <span data-ttu-id="2ffaa-121">如果它能成功輪詢同盟中繼資料並擷取新的憑證，使用者就不會收到電子郵件通知或 Office 365 入口網站發出的警告。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-121">If it can successfully poll the federation metadata and retrieve the new certificates, no email notification or warning in the Office 365 portal is issued to the user.</span></span>
* <span data-ttu-id="2ffaa-122">如果它無法擷取新的權杖簽署憑證，不論原因是無法取得同盟中繼資料，還是自動憑證變換並未啟用，Azure AD 都會發出電子郵件通知和 O365 入口網站中的警告。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-122">If it cannot retrieve the new token signing certificates, either because the federation metadata is not reachable or automatic certificate rollover is not enabled, Azure AD issues an email notification and a warning in the Office 365 portal.</span></span>

![Office 365 入口網站通知](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> <span data-ttu-id="2ffaa-124">如果您使用 AD FS，為確保商務持續性，請確認您的伺服器具備下列更新，以免發生已知問題驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-124">If you are using AD FS, to ensure business continuity, please verify that your servers have the following updates so that authentication failures for known issues do not occur.</span></span> <span data-ttu-id="2ffaa-125">這可減少在此更新和未來更新期間的已知 AD FS Proxy 伺服器問題︰</span><span class="sxs-lookup"><span data-stu-id="2ffaa-125">This mitigates known AD FS proxy server issues for this renewal and future renewal periods:</span></span>
>
> <span data-ttu-id="2ffaa-126">Server 2012 R2 - [Windows Server 2014 年 5 月彙總套件](http://support.microsoft.com/kb/2955164)</span><span class="sxs-lookup"><span data-stu-id="2ffaa-126">Server 2012 R2 - [Windows Server May 2014 rollup](http://support.microsoft.com/kb/2955164)</span></span>
>
> <span data-ttu-id="2ffaa-127">Server 2008 R2 和 2012 - [在 Windows Server 2012 或 Windows 2008 R2 SP1 中透過 Proxy 驗證失敗](http://support.microsoft.com/kb/3094446)</span><span class="sxs-lookup"><span data-stu-id="2ffaa-127">Server 2008 R2 and 2012 - [Authentication through proxy fails in Windows Server 2012 or Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)</span></span>
>
>

## <span data-ttu-id="2ffaa-128">檢查是否需要更新憑證 <a name="managecerts"></a></span><span class="sxs-lookup"><span data-stu-id="2ffaa-128">Check if the certificates need to be updated <a name="managecerts"></a></span></span>
### <a name="step-1-check-the-autocertificaterollover-state"></a><span data-ttu-id="2ffaa-129">步驟 1︰檢查 AutoCertificateRollover 狀態</span><span class="sxs-lookup"><span data-stu-id="2ffaa-129">Step 1: Check the AutoCertificateRollover state</span></span>
<span data-ttu-id="2ffaa-130">在 AD FS 伺服器上開啟 Powershell。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-130">On your AD FS server, open PowerShell.</span></span> <span data-ttu-id="2ffaa-131">檢查 AutoCertificateRollover 值是否已設定為 True。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-131">Check that the AutoCertificateRollover value is set to True.</span></span>

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
><span data-ttu-id="2ffaa-133">如果您使用 AD FS 2.0，請先執行 Add-Pssnapin Microsoft.Adfs.Powershell。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-133">If you are using AD FS 2.0, first run Add-Pssnapin Microsoft.Adfs.Powershell.</span></span>

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a><span data-ttu-id="2ffaa-134">步驟 2︰確認 AD FS 和 Azure AD 已同步</span><span class="sxs-lookup"><span data-stu-id="2ffaa-134">Step 2: Confirm that AD FS and Azure AD are in sync</span></span>
<span data-ttu-id="2ffaa-135">在 AD FS 伺服器上開啟 Azure AD Powershell 提示字元，並連線到 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-135">On your AD FS server, open the Azure AD PowerShell prompt, and connect to Azure AD.</span></span>

> [!NOTE]
> <span data-ttu-id="2ffaa-136">您可以從 [這裡](https://technet.microsoft.com/library/jj151815.aspx)下載 Azure AD PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-136">You can download Azure AD PowerShell [here](https://technet.microsoft.com/library/jj151815.aspx).</span></span>
>
>

    Connect-MsolService

<span data-ttu-id="2ffaa-137">檢查 AD FS 和 Azure AD 信任屬性中針對指定網域所設定的憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-137">Check the certificates configured in AD FS and Azure AD trust properties for the specified domain.</span></span>

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

<span data-ttu-id="2ffaa-139">如果這兩個輸出中的指紋相符，您的憑證便已與 Azure AD 同步。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-139">If the thumbprints in both the outputs match, your certificates are in sync with Azure AD.</span></span>

### <a name="step-3-check-if-your-certificate-is-about-to-expire"></a><span data-ttu-id="2ffaa-140">步驟 3︰檢查憑證是否即將到期</span><span class="sxs-lookup"><span data-stu-id="2ffaa-140">Step 3: Check if your certificate is about to expire</span></span>
<span data-ttu-id="2ffaa-141">在 Get-MsolFederationProperty 或 Get-AdfsCertificate 的輸出中，檢查「不晚於」之下的日期。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-141">In the output of either Get-MsolFederationProperty or Get-AdfsCertificate, check for the date under "Not After."</span></span> <span data-ttu-id="2ffaa-142">如果日期相隔不到 30 天，您應採取動作。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-142">If the date is less than 30 days away, you should take action.</span></span>

| <span data-ttu-id="2ffaa-143">AutoCertificateRollover</span><span class="sxs-lookup"><span data-stu-id="2ffaa-143">AutoCertificateRollover</span></span> | <span data-ttu-id="2ffaa-144">憑證與 Azure AD 同步</span><span class="sxs-lookup"><span data-stu-id="2ffaa-144">Certificates in sync with Azure AD</span></span> | <span data-ttu-id="2ffaa-145">可公開取得同盟中繼資料</span><span class="sxs-lookup"><span data-stu-id="2ffaa-145">Federation metadata is publicly accessible</span></span> | <span data-ttu-id="2ffaa-146">有效期</span><span class="sxs-lookup"><span data-stu-id="2ffaa-146">Validity</span></span> | <span data-ttu-id="2ffaa-147">動作</span><span class="sxs-lookup"><span data-stu-id="2ffaa-147">Action</span></span> |
|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2ffaa-148">是</span><span class="sxs-lookup"><span data-stu-id="2ffaa-148">Yes</span></span> |<span data-ttu-id="2ffaa-149">是</span><span class="sxs-lookup"><span data-stu-id="2ffaa-149">Yes</span></span> |<span data-ttu-id="2ffaa-150">是</span><span class="sxs-lookup"><span data-stu-id="2ffaa-150">Yes</span></span> |- |<span data-ttu-id="2ffaa-151">不需採取動作。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-151">No action needed.</span></span> <span data-ttu-id="2ffaa-152">請參閱 [自動更新權杖簽署憑證](#autorenew)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-152">See [Renew token signing certificate automatically](#autorenew).</span></span> |
| <span data-ttu-id="2ffaa-153">是</span><span class="sxs-lookup"><span data-stu-id="2ffaa-153">Yes</span></span> |<span data-ttu-id="2ffaa-154">否</span><span class="sxs-lookup"><span data-stu-id="2ffaa-154">No</span></span> |- |<span data-ttu-id="2ffaa-155">小於 15 天</span><span class="sxs-lookup"><span data-stu-id="2ffaa-155">Less than 15 days</span></span> |<span data-ttu-id="2ffaa-156">立即更新。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-156">Renew immediately.</span></span> <span data-ttu-id="2ffaa-157">請參閱 [手動更新權杖簽署憑證](#manualrenew)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-157">See [Renew token signing certificate manually](#manualrenew).</span></span> |
| <span data-ttu-id="2ffaa-158">否</span><span class="sxs-lookup"><span data-stu-id="2ffaa-158">No</span></span> |- |- |<span data-ttu-id="2ffaa-159">少於 30 天</span><span class="sxs-lookup"><span data-stu-id="2ffaa-159">Less than 30 days</span></span> |<span data-ttu-id="2ffaa-160">立即更新。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-160">Renew immediately.</span></span> <span data-ttu-id="2ffaa-161">請參閱 [手動更新權杖簽署憑證](#manualrenew)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-161">See [Renew token signing certificate manually](#manualrenew).</span></span> |

<span data-ttu-id="2ffaa-162">\[-]  無關緊要</span><span class="sxs-lookup"><span data-stu-id="2ffaa-162">\[-]  Does not matter</span></span>

## <span data-ttu-id="2ffaa-163">自動更新權杖簽署憑證 (建議選項) <a name="autorenew"></a></span><span class="sxs-lookup"><span data-stu-id="2ffaa-163">Renew the token signing certificate automatically (recommended) <a name="autorenew"></a></span></span>
<span data-ttu-id="2ffaa-164">如果下列兩種情況成立，您不需要執行任何手動步驟︰</span><span class="sxs-lookup"><span data-stu-id="2ffaa-164">You don't need to perform any manual steps if both of the following are true:</span></span>

* <span data-ttu-id="2ffaa-165">您已部署能夠從外部網路存取同盟中繼資料的 Web 應用程式 Proxy。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-165">You have deployed Web Application Proxy, which can enable access to the federation metadata from the extranet.</span></span>
* <span data-ttu-id="2ffaa-166">您目前使用 AD FS 預設設定 (已啟用 AutoCertificateRollove)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-166">You are using the AD FS default configuration (AutoCertificateRollover is enabled).</span></span>

<span data-ttu-id="2ffaa-167">檢查下列各項，確認可以自動更新憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-167">Check the following to confirm that the certificate can be automatically updated.</span></span>

<span data-ttu-id="2ffaa-168">**1.AD FS 屬性 AutoCertificateRollover 必須設定為 True。**</span><span class="sxs-lookup"><span data-stu-id="2ffaa-168">**1. The AD FS property AutoCertificateRollover must be set to True.**</span></span> <span data-ttu-id="2ffaa-169">這表示 AD FS 會在舊憑證到期之前，自動產生新的權杖簽署和權杖解密憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-169">This indicates that AD FS will automatically generate new token signing and token decryption certificates, before the old ones expire.</span></span>

<span data-ttu-id="2ffaa-170">**2.可公開取得 AD FS 同盟中繼資料。**</span><span class="sxs-lookup"><span data-stu-id="2ffaa-170">**2. The AD FS federation metadata is publicly accessible.**</span></span> <span data-ttu-id="2ffaa-171">從公用網際網路 (離開公司網路) 的電腦瀏覽到下列 URL 檢查同盟中繼資料是否可公開存取：</span><span class="sxs-lookup"><span data-stu-id="2ffaa-171">Check that your federation metadata is publicly accessible by navigating to the following URL from a computer on the public internet (off of the corporate network):</span></span>

<span data-ttu-id="2ffaa-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="2ffaa-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span></span>

<span data-ttu-id="2ffaa-173">將其中的 `(your_FS_name) `取代為您的組織使用的同盟服務主機名稱，例如 fs.contoso.com。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-173">where `(your_FS_name) `is replaced with the federation service host name your organization uses, such as fs.contoso.com.</span></span>  <span data-ttu-id="2ffaa-174">如果您能夠成功確認上述兩個設定，您就不必執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-174">If you are able to verify both of these settings successfully, you do not have to do anything else.</span></span>  

<span data-ttu-id="2ffaa-175">範例：https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="2ffaa-175">Example: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span></span>

## <span data-ttu-id="2ffaa-176">手動更新權杖簽署憑證 <a name="manualrenew"></a></span><span class="sxs-lookup"><span data-stu-id="2ffaa-176">Renew the token signing certificate manually <a name="manualrenew"></a></span></span>
<span data-ttu-id="2ffaa-177">您可以選擇手動更新權杖簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-177">You may choose to renew the token signing certificates manually.</span></span> <span data-ttu-id="2ffaa-178">例如，下列案例可能比較適合進行手動更新︰</span><span class="sxs-lookup"><span data-stu-id="2ffaa-178">For example, the following scenarios might work better for manual renewal:</span></span>

* <span data-ttu-id="2ffaa-179">權杖簽署憑證不是自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-179">Token signing certificates are not self-signed certificates.</span></span> <span data-ttu-id="2ffaa-180">最常見的原因是您的組織管理從組織的憑證授權單位註冊的 AD FS 憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-180">The most common reason for this is that your organization manages AD FS certificates enrolled from an organizational certificate authority.</span></span>
* <span data-ttu-id="2ffaa-181">網路安全性不允許公開取得同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-181">Network security does not allow the federation metadata to be publicly available.</span></span>

<span data-ttu-id="2ffaa-182">在這些案例中，每當您更新權杖簽署憑證時，您還必須使用 PowerShell 命令 Update-MsolFederatedDomain 更新 Office 365 網域。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-182">In these scenarios, every time you update the token signing certificates, you must also update your Office 365 domain by using the PowerShell command, Update-MsolFederatedDomain.</span></span>

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a><span data-ttu-id="2ffaa-183">步驟 1︰確認 AD FS 具有新的權杖簽署憑證</span><span class="sxs-lookup"><span data-stu-id="2ffaa-183">Step 1: Ensure that AD FS has new token signing certificates</span></span>
<span data-ttu-id="2ffaa-184">**非預設設定**</span><span class="sxs-lookup"><span data-stu-id="2ffaa-184">**Non-default configuration**</span></span>

<span data-ttu-id="2ffaa-185">如果您處於非預設的 AD FS 設定 (也就是 **AutoCertificateRollover** 設定為 **False**)，則您想必也是使用自訂憑證 (非自我簽署)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-185">If you are using a non-default configuration of AD FS (where **AutoCertificateRollover** is set to **False**), you are probably using custom certificates (not self-signed).</span></span> <span data-ttu-id="2ffaa-186">如需如何更新 AD FS 權杖簽署憑證的詳細資訊，請參閱 [給未使用 AD FS 自我簽署憑證之客戶的指導方針](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-186">For more information about how to renew the AD FS token signing certificates, see [Guidance for customers not using AD FS self-signed certificates](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).</span></span>

<span data-ttu-id="2ffaa-187">**無法公開取得同盟中繼資料**</span><span class="sxs-lookup"><span data-stu-id="2ffaa-187">**Federation metadata is not publicly available**</span></span>

<span data-ttu-id="2ffaa-188">另一方面，如果 **AutoCertificateRollover** 設定為 **True**，但無法公開取得同盟中繼資料，請先確定 AD FS 已產生新的權杖簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-188">On the other hand, if **AutoCertificateRollover** is set to **True**, but your federation metadata is not publicly accessible, first make sure that new token signing certificates have been generated by AD FS.</span></span> <span data-ttu-id="2ffaa-189">遵循下列步驟，確認您有新的權杖簽署憑證：</span><span class="sxs-lookup"><span data-stu-id="2ffaa-189">Confirm you have new token signing certificates by taking the following steps:</span></span>

1. <span data-ttu-id="2ffaa-190">確認您已登入主要 AD FS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-190">Verify that you are logged on to the primary AD FS server.</span></span>
2. <span data-ttu-id="2ffaa-191">開啟 PowerShell 命令視窗並執行下列命令，檢查 AD FS 中目前的簽署憑證：</span><span class="sxs-lookup"><span data-stu-id="2ffaa-191">Check the current signing certificates in AD FS by opening a PowerShell command window, and running the following command:</span></span>

    <span data-ttu-id="2ffaa-192">PS C:\>Get-ADFSCertificate -CertificateType token-signing</span><span class="sxs-lookup"><span data-stu-id="2ffaa-192">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

   > [!NOTE]
   > <span data-ttu-id="2ffaa-193">如果您使用 AD FS 2.0，則必須先執行 Add-Pssnapin Microsoft.Adfs.Powershell。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-193">If you are using AD FS 2.0, you should run Add-Pssnapin Microsoft.Adfs.Powershell first.</span></span>
   >
   >
3. <span data-ttu-id="2ffaa-194">查看命令輸出中所列的任何憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-194">Look at the command output at any certificates listed.</span></span> <span data-ttu-id="2ffaa-195">如果 AD FS 已產生新的憑證，您應該會在輸出中看到兩個憑證：一個 **IsPrimary** 值是 **True**，而 **NotAfter** 日期是 5 天內，另一個 **IsPrimary** 是 **False**，而 **NotAfter** 大約在未來一年。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-195">If AD FS has generated a new certificate, you should see two certificates in the output: one for which the **IsPrimary** value is **True** and the **NotAfter** date is within 5 days, and one for which **IsPrimary** is **False** and **NotAfter** is about a year in the future.</span></span>
4. <span data-ttu-id="2ffaa-196">如果您只看到一個憑證，而 **NotAfter** 日期為 5 天內，您必須執行產生新的憑證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-196">If you only see one certificate, and the **NotAfter** date is within 5 days, you need to generate a new certificate.</span></span>
5. <span data-ttu-id="2ffaa-197">若要產生新憑證，請在 PowerShell 命令提示字元中執行下列命令： `PS C:\>Update-ADFSCertificate –CertificateType token-signing`。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-197">To generate a new certificate, execute the following command at a PowerShell command prompt: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.</span></span>
6. <span data-ttu-id="2ffaa-198">再次執行下列命令驗證更新：PS C:\>Get-ADFSCertificate -CertificateType token-signing</span><span class="sxs-lookup"><span data-stu-id="2ffaa-198">Verify the update by running the following command again: PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

<span data-ttu-id="2ffaa-199">現在應該會列出兩個憑證，一個的 **NotAfter** 日期大約在未來一年，且 **IsPrimary** 值是 **False**。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-199">Two certificates should be listed now, one of which has a **NotAfter** date of approximately one year in the future, and for which the **IsPrimary** value is **False**.</span></span>

### <a name="step-2-update-the-new-token-signing-certificates-for-the-office-365-trust"></a><span data-ttu-id="2ffaa-200">步驟 2︰更新 Office 365 信任的新權杖簽署憑證</span><span class="sxs-lookup"><span data-stu-id="2ffaa-200">Step 2: Update the new token signing certificates for the Office 365 trust</span></span>
<span data-ttu-id="2ffaa-201">使用要用於信任的新權杖簽署憑證更新 Office 365，如下所示。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-201">Update Office 365 with the new token signing certificates to be used for the trust, as follows.</span></span>

1. <span data-ttu-id="2ffaa-202">開啟適用於 Windows PowerShell 的 Microsoft Azure Active Directory 模組。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-202">Open the Microsoft Azure Active Directory Module for Windows PowerShell.</span></span>
2. <span data-ttu-id="2ffaa-203">執行 $cred=Get-Credential。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-203">Run $cred=Get-Credential.</span></span> <span data-ttu-id="2ffaa-204">當此 Cmdlet 提示您輸入認證時，請輸入您的雲端服務系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-204">When this cmdlet prompts you for credentials, type your cloud service administrator account credentials.</span></span>
3. <span data-ttu-id="2ffaa-205">執行 Connect-MsolService –Credential $cred。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-205">Run Connect-MsolService –Credential $cred.</span></span> <span data-ttu-id="2ffaa-206">此 Cmdlet 可讓您連線到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-206">This cmdlet connects you to the cloud service.</span></span> <span data-ttu-id="2ffaa-207">在您執行由工具安裝的任何其他 Cmdlet 之前，必須先建立讓您連線到雲端服務的環境。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-207">Creating a context that connects you to the cloud service is required before running any of the additional cmdlets installed by the tool.</span></span>
4. <span data-ttu-id="2ffaa-208">如果您不是在 AD FS 主要同盟伺服器的電腦上執行這些命令，請執行 Set-MSOLAdfscontext -Computer <AD FS primary server>，其中 <AD FS primary server> 是主要 AD FS 伺服器的內部 FQDN 名稱。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-208">If you are running these commands on a computer that is not the AD FS primary federation server, run Set-MSOLAdfscontext -Computer <AD FS primary server>, where <AD FS primary server> is the internal FQDN name of the primary AD FS server.</span></span> <span data-ttu-id="2ffaa-209">此 Cmdlet 會建立讓您連線到 AD FS 的環境。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-209">This cmdlet creates a context that connects you to AD FS.</span></span>
5. <span data-ttu-id="2ffaa-210">執行 Update-MSOLFederatedDomain –DomainName <domain>。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-210">Run Update-MSOLFederatedDomain –DomainName <domain>.</span></span> <span data-ttu-id="2ffaa-211">此 Cmdlet 會將 AD FS 的設定更新成雲端服務，並設定兩者之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-211">This cmdlet updates the settings from AD FS into the cloud service, and configures the trust relationship between the two.</span></span>

> [!NOTE]
> <span data-ttu-id="2ffaa-212">如果您需要支援多個頂層網域，例如 contoso.com 和 fabrikam.com，則您使用任何 Cmdlet 時必須搭配使用 **SupportMultipleDomain** 參數。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-212">If you need to support multiple top-level domains, such as contoso.com and fabrikam.com, you must use the **SupportMultipleDomain** switch with any cmdlets.</span></span> <span data-ttu-id="2ffaa-213">如需詳細資訊，請參閱 [支援多個頂層網域](active-directory-aadconnect-multiple-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-213">For more information, see [Support for Multiple Top Level Domains](active-directory-aadconnect-multiple-domains.md).</span></span>
>
>

## <span data-ttu-id="2ffaa-214">使用 Azure AD Connect 修復 Azure AD 信任 <a name="connectrenew"></a></span><span class="sxs-lookup"><span data-stu-id="2ffaa-214">Repair Azure AD trust by using Azure AD Connect <a name="connectrenew"></a></span></span>
<span data-ttu-id="2ffaa-215">如果您已使用 Azure AD Connect 設定 AD FS 伺服器陣列和 Azure AD 信任，則可以使用 Azure AD Connect 來偵測是否需要對權杖簽署憑證採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-215">If you configured your AD FS farm and Azure AD trust by using Azure AD Connect, you can use Azure AD Connect to detect if you need to take any action for your token signing certificates.</span></span> <span data-ttu-id="2ffaa-216">如果您需要更新憑證，可以使用 Azure AD Connect 這樣做。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-216">If you need to renew the certificates, you can use Azure AD Connect to do so.</span></span>

<span data-ttu-id="2ffaa-217">如需詳細資訊，請參閱 [修復信任](active-directory-aadconnect-federation-management.md)。</span><span class="sxs-lookup"><span data-stu-id="2ffaa-217">For more information, see [Repairing the trust](active-directory-aadconnect-federation-management.md).</span></span>
