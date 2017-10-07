---
title: "Office 365 和 Azure AD 使用者能夠 aaaCertificate 更新 |Microsoft 文件"
description: "本文說明如何 tooresolve 問題的電子郵件，通知他們續約憑證 tooOffice 365 使用者。"
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
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a><span data-ttu-id="19672-103">更新 Office 365 和 Azure Active Directory 的同盟憑證</span><span class="sxs-lookup"><span data-stu-id="19672-103">Renew federation certificates for Office 365 and Azure Active Directory</span></span>
## <a name="overview"></a><span data-ttu-id="19672-104">概觀</span><span class="sxs-lookup"><span data-stu-id="19672-104">Overview</span></span>
<span data-ttu-id="19672-105">Azure Active Directory (Azure AD) 與 Active Directory Federation Services (AD FS) 之間成功的同盟，使用的 AD FS toosign 安全性語彙基元 tooAzure AD 的 hello 憑證應該符合 Azure AD 中的設定。</span><span class="sxs-lookup"><span data-stu-id="19672-105">For successful federation between Azure Active Directory (Azure AD) and Active Directory Federation Services (AD FS), hello certificates used by AD FS toosign security tokens tooAzure AD should match what is configured in Azure AD.</span></span> <span data-ttu-id="19672-106">任何不相符，可能會導致 toobroken 信任。</span><span class="sxs-lookup"><span data-stu-id="19672-106">Any mismatch can lead toobroken trust.</span></span> <span data-ttu-id="19672-107">Azure AD 會確保這項資訊在您部署 AD FS 和 Web 應用程式 Proxy (適用於外部網路存取) 時保持同步。</span><span class="sxs-lookup"><span data-stu-id="19672-107">Azure AD ensures that this information is kept in sync when you deploy AD FS and Web Application Proxy (for extranet access).</span></span>

<span data-ttu-id="19672-108">這篇文章提供額外資訊 toomanage 權杖簽署憑證並將它們與 Azure AD 同步 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="19672-108">This article provides you additional information toomanage your token signing certificates and keep them in sync with Azure AD, in hello following cases:</span></span>

* <span data-ttu-id="19672-109">您並不會部署 hello Web 應用程式 Proxy，並因此 hello 同盟中繼資料就無法用於外部網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="19672-109">You are not deploying hello Web Application Proxy, and therefore hello federation metadata is not available in hello extranet.</span></span>
* <span data-ttu-id="19672-110">您不使用 hello 預設組態，AD fs 權杖簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="19672-110">You are not using hello default configuration of AD FS for token signing certificates.</span></span>
* <span data-ttu-id="19672-111">您要使用協力廠商的識別提供者。</span><span class="sxs-lookup"><span data-stu-id="19672-111">You are using a third-party identity provider.</span></span>

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a><span data-ttu-id="19672-112">權杖簽署憑證的預設 AD FS 設定</span><span class="sxs-lookup"><span data-stu-id="19672-112">Default configuration of AD FS for token signing certificates</span></span>
<span data-ttu-id="19672-113">hello 權杖簽署和權杖解密憑證通常是自我簽署的憑證，並且也適合用來一年。</span><span class="sxs-lookup"><span data-stu-id="19672-113">hello token signing and token decrypting certificates are usually self-signed certificates, and are good for one year.</span></span> <span data-ttu-id="19672-114">根據預設，AD FS 包含名為 **AutoCertificateRollover**的自動更新程序。</span><span class="sxs-lookup"><span data-stu-id="19672-114">By default, AD FS includes an auto-renewal process called **AutoCertificateRollover**.</span></span> <span data-ttu-id="19672-115">如果您使用 AD FS 2.0 或更新版本，Office 365 和 Azure AD 在您的憑證到期之前會自動進行更新。</span><span class="sxs-lookup"><span data-stu-id="19672-115">If you are using AD FS 2.0 or later, Office 365 and Azure AD automatically update your certificate before it expires.</span></span>

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a><span data-ttu-id="19672-116">從 hello Office 365 入口網站或電子郵件的更新通知</span><span class="sxs-lookup"><span data-stu-id="19672-116">Renewal notification from hello Office 365 portal or an email</span></span>
> [!NOTE]
> <span data-ttu-id="19672-117">如果您收到一封電子郵件或要求您 toorenew 入口網站通知您的憑證適用於 Office，請參閱[管理變更簽署憑證的 tootoken](#managecerts) toocheck，如果您需要 tootake 任何動作。</span><span class="sxs-lookup"><span data-stu-id="19672-117">If you received an email or a portal notification asking you toorenew your certificate for Office, see [Managing changes tootoken signing certificates](#managecerts) toocheck if you need tootake any action.</span></span> <span data-ttu-id="19672-118">Microsoft 了解可能的問題，可能會導致 toonotifications 進行傳送，即使不不需要任何動作的憑證更新。</span><span class="sxs-lookup"><span data-stu-id="19672-118">Microsoft is aware of a possible issue that can lead toonotifications for certificate renewal being sent, even when no action is required.</span></span>
>
>

<span data-ttu-id="19672-119">Azure AD 會嘗試 toomonitor hello 同盟中繼資料，以及更新 hello 權杖簽署憑證，此中繼資料所示。</span><span class="sxs-lookup"><span data-stu-id="19672-119">Azure AD attempts toomonitor hello federation metadata, and update hello token signing certificates as indicated by this metadata.</span></span> <span data-ttu-id="19672-120">hello hello 權杖簽署憑證到期前 30 天會檢查 Azure AD，新的憑證是否可用，藉由輪詢 hello 同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="19672-120">30 days before hello expiration of hello token signing certificates, Azure AD checks if new certificates are available by polling hello federation metadata.</span></span>

* <span data-ttu-id="19672-121">如果成功，它可以輪詢 hello 同盟中繼資料，並擷取 hello 新的憑證，沒有電子郵件通知或 hello Office 365 入口網站中的警告會發出 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="19672-121">If it can successfully poll hello federation metadata and retrieve hello new certificates, no email notification or warning in hello Office 365 portal is issued toohello user.</span></span>
* <span data-ttu-id="19672-122">如果它無法擷取 hello 新權杖簽署憑證，可能是因為找不到 hello 同盟中繼資料，或未啟用自動憑證變換，Azure AD 會發出電子郵件通知和 hello Office 365 入口網站中的警告。</span><span class="sxs-lookup"><span data-stu-id="19672-122">If it cannot retrieve hello new token signing certificates, either because hello federation metadata is not reachable or automatic certificate rollover is not enabled, Azure AD issues an email notification and a warning in hello Office 365 portal.</span></span>

![Office 365 入口網站通知](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> <span data-ttu-id="19672-124">如果您使用 AD FS，tooensure 業務持續性，請確認您的伺服器有 hello 下列更新，因此不會發生的已知問題的驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="19672-124">If you are using AD FS, tooensure business continuity, please verify that your servers have hello following updates so that authentication failures for known issues do not occur.</span></span> <span data-ttu-id="19672-125">這可減少在此更新和未來更新期間的已知 AD FS Proxy 伺服器問題︰</span><span class="sxs-lookup"><span data-stu-id="19672-125">This mitigates known AD FS proxy server issues for this renewal and future renewal periods:</span></span>
>
> <span data-ttu-id="19672-126">Server 2012 R2 - [Windows Server 2014 年 5 月彙總套件](http://support.microsoft.com/kb/2955164)</span><span class="sxs-lookup"><span data-stu-id="19672-126">Server 2012 R2 - [Windows Server May 2014 rollup](http://support.microsoft.com/kb/2955164)</span></span>
>
> <span data-ttu-id="19672-127">Server 2008 R2 和 2012 - [在 Windows Server 2012 或 Windows 2008 R2 SP1 中透過 Proxy 驗證失敗](http://support.microsoft.com/kb/3094446)</span><span class="sxs-lookup"><span data-stu-id="19672-127">Server 2008 R2 and 2012 - [Authentication through proxy fails in Windows Server 2012 or Windows 2008 R2 SP1](http://support.microsoft.com/kb/3094446)</span></span>
>
>

## <span data-ttu-id="19672-128">檢查 hello 憑證是否需要更新 toobe<a name="managecerts"></a></span><span class="sxs-lookup"><span data-stu-id="19672-128">Check if hello certificates need toobe updated <a name="managecerts"></a></span></span>
### <a name="step-1-check-hello-autocertificaterollover-state"></a><span data-ttu-id="19672-129">步驟 1： 檢查 hello AutoCertificateRollover 狀態</span><span class="sxs-lookup"><span data-stu-id="19672-129">Step 1: Check hello AutoCertificateRollover state</span></span>
<span data-ttu-id="19672-130">在 AD FS 伺服器上開啟 Powershell。</span><span class="sxs-lookup"><span data-stu-id="19672-130">On your AD FS server, open PowerShell.</span></span> <span data-ttu-id="19672-131">請檢查確定 hello AutoCertificateRollover 值設定 tooTrue。</span><span class="sxs-lookup"><span data-stu-id="19672-131">Check that hello AutoCertificateRollover value is set tooTrue.</span></span>

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
><span data-ttu-id="19672-133">如果您使用 AD FS 2.0，請先執行 Add-Pssnapin Microsoft.Adfs.Powershell。</span><span class="sxs-lookup"><span data-stu-id="19672-133">If you are using AD FS 2.0, first run Add-Pssnapin Microsoft.Adfs.Powershell.</span></span>

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a><span data-ttu-id="19672-134">步驟 2︰確認 AD FS 和 Azure AD 已同步</span><span class="sxs-lookup"><span data-stu-id="19672-134">Step 2: Confirm that AD FS and Azure AD are in sync</span></span>
<span data-ttu-id="19672-135">在 AD FS 伺服器上，開啟 hello Azure AD PowerShell 命令提示字元，並連接 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="19672-135">On your AD FS server, open hello Azure AD PowerShell prompt, and connect tooAzure AD.</span></span>

> [!NOTE]
> <span data-ttu-id="19672-136">您可以從 [這裡](https://technet.microsoft.com/library/jj151815.aspx)下載 Azure AD PowerShell。</span><span class="sxs-lookup"><span data-stu-id="19672-136">You can download Azure AD PowerShell [here](https://technet.microsoft.com/library/jj151815.aspx).</span></span>
>
>

    Connect-MsolService

<span data-ttu-id="19672-137">請檢查設定 AD FS 中的 hello 憑證以及 hello 的 Azure AD 信任屬性指定的網域。</span><span class="sxs-lookup"><span data-stu-id="19672-137">Check hello certificates configured in AD FS and Azure AD trust properties for hello specified domain.</span></span>

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

<span data-ttu-id="19672-139">如果在 hello 指紋 hello 輸出相符項目，您的憑證會與 Azure AD 同步。</span><span class="sxs-lookup"><span data-stu-id="19672-139">If hello thumbprints in both hello outputs match, your certificates are in sync with Azure AD.</span></span>

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a><span data-ttu-id="19672-140">步驟 3： 檢查您的憑證是否需 tooexpire</span><span class="sxs-lookup"><span data-stu-id="19672-140">Step 3: Check if your certificate is about tooexpire</span></span>
<span data-ttu-id="19672-141">Get-msolfederationproperty 或 Get AdfsCertificate hello 輸出，在檢查 hello 日期下 「 不之後。 」</span><span class="sxs-lookup"><span data-stu-id="19672-141">In hello output of either Get-MsolFederationProperty or Get-AdfsCertificate, check for hello date under "Not After."</span></span> <span data-ttu-id="19672-142">如果 hello 日期為小於 30 天內改變了，您應該採取動作。</span><span class="sxs-lookup"><span data-stu-id="19672-142">If hello date is less than 30 days away, you should take action.</span></span>

| <span data-ttu-id="19672-143">AutoCertificateRollover</span><span class="sxs-lookup"><span data-stu-id="19672-143">AutoCertificateRollover</span></span> | <span data-ttu-id="19672-144">憑證與 Azure AD 同步</span><span class="sxs-lookup"><span data-stu-id="19672-144">Certificates in sync with Azure AD</span></span> | <span data-ttu-id="19672-145">可公開取得同盟中繼資料</span><span class="sxs-lookup"><span data-stu-id="19672-145">Federation metadata is publicly accessible</span></span> | <span data-ttu-id="19672-146">有效期</span><span class="sxs-lookup"><span data-stu-id="19672-146">Validity</span></span> | <span data-ttu-id="19672-147">動作</span><span class="sxs-lookup"><span data-stu-id="19672-147">Action</span></span> |
|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="19672-148">是</span><span class="sxs-lookup"><span data-stu-id="19672-148">Yes</span></span> |<span data-ttu-id="19672-149">是</span><span class="sxs-lookup"><span data-stu-id="19672-149">Yes</span></span> |<span data-ttu-id="19672-150">是</span><span class="sxs-lookup"><span data-stu-id="19672-150">Yes</span></span> |- |<span data-ttu-id="19672-151">不需採取動作。</span><span class="sxs-lookup"><span data-stu-id="19672-151">No action needed.</span></span> <span data-ttu-id="19672-152">請參閱 [自動更新權杖簽署憑證](#autorenew)。</span><span class="sxs-lookup"><span data-stu-id="19672-152">See [Renew token signing certificate automatically](#autorenew).</span></span> |
| <span data-ttu-id="19672-153">是</span><span class="sxs-lookup"><span data-stu-id="19672-153">Yes</span></span> |<span data-ttu-id="19672-154">否</span><span class="sxs-lookup"><span data-stu-id="19672-154">No</span></span> |- |<span data-ttu-id="19672-155">小於 15 天</span><span class="sxs-lookup"><span data-stu-id="19672-155">Less than 15 days</span></span> |<span data-ttu-id="19672-156">立即更新。</span><span class="sxs-lookup"><span data-stu-id="19672-156">Renew immediately.</span></span> <span data-ttu-id="19672-157">請參閱 [手動更新權杖簽署憑證](#manualrenew)。</span><span class="sxs-lookup"><span data-stu-id="19672-157">See [Renew token signing certificate manually](#manualrenew).</span></span> |
| <span data-ttu-id="19672-158">否</span><span class="sxs-lookup"><span data-stu-id="19672-158">No</span></span> |- |- |<span data-ttu-id="19672-159">少於 30 天</span><span class="sxs-lookup"><span data-stu-id="19672-159">Less than 30 days</span></span> |<span data-ttu-id="19672-160">立即更新。</span><span class="sxs-lookup"><span data-stu-id="19672-160">Renew immediately.</span></span> <span data-ttu-id="19672-161">請參閱 [手動更新權杖簽署憑證](#manualrenew)。</span><span class="sxs-lookup"><span data-stu-id="19672-161">See [Renew token signing certificate manually](#manualrenew).</span></span> |

<span data-ttu-id="19672-162">\[-]  無關緊要</span><span class="sxs-lookup"><span data-stu-id="19672-162">\[-]  Does not matter</span></span>

## <span data-ttu-id="19672-163">更新 hello 權杖簽署憑證自動 （建議選項）<a name="autorenew"></a></span><span class="sxs-lookup"><span data-stu-id="19672-163">Renew hello token signing certificate automatically (recommended) <a name="autorenew"></a></span></span>
<span data-ttu-id="19672-164">如果 hello 下列都符合您不需要指定 tooperform 任何手動操作步驟：</span><span class="sxs-lookup"><span data-stu-id="19672-164">You don't need tooperform any manual steps if both of hello following are true:</span></span>

* <span data-ttu-id="19672-165">您已部署 Web 應用程式 Proxy，可啟用從 hello 外部網路存取 toohello 同盟中繼資料。</span><span class="sxs-lookup"><span data-stu-id="19672-165">You have deployed Web Application Proxy, which can enable access toohello federation metadata from hello extranet.</span></span>
* <span data-ttu-id="19672-166">您正在使用 hello AD FS 預設組態 （AutoCertificateRollover 已啟用）。</span><span class="sxs-lookup"><span data-stu-id="19672-166">You are using hello AD FS default configuration (AutoCertificateRollover is enabled).</span></span>

<span data-ttu-id="19672-167">請檢查下列 hello 憑證的 tooconfirm hello 可以自動更新。</span><span class="sxs-lookup"><span data-stu-id="19672-167">Check hello following tooconfirm that hello certificate can be automatically updated.</span></span>

<span data-ttu-id="19672-168">**1.hello AutoCertificateRollover 的 AD FS 屬性必須設定 tooTrue。**</span><span class="sxs-lookup"><span data-stu-id="19672-168">**1. hello AD FS property AutoCertificateRollover must be set tooTrue.**</span></span> <span data-ttu-id="19672-169">這表示 AD FS 會自動產生新的權杖簽署和權杖解密憑證，hello 舊的到期之前。</span><span class="sxs-lookup"><span data-stu-id="19672-169">This indicates that AD FS will automatically generate new token signing and token decryption certificates, before hello old ones expire.</span></span>

<span data-ttu-id="19672-170">**2.hello AD FS 同盟中繼資料是可公開存取。**</span><span class="sxs-lookup"><span data-stu-id="19672-170">**2. hello AD FS federation metadata is publicly accessible.**</span></span> <span data-ttu-id="19672-171">檢查您的同盟中繼資料瀏覽 toohello 是可公開存取的電腦中的下列 URL，hello 公用網際網路 （開 hello 企業網路）：</span><span class="sxs-lookup"><span data-stu-id="19672-171">Check that your federation metadata is publicly accessible by navigating toohello following URL from a computer on hello public internet (off of hello corporate network):</span></span>

<span data-ttu-id="19672-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="19672-172">https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml</span></span>

<span data-ttu-id="19672-173">其中`(your_FS_name) `取代為您的組織使用，例如 fs.contoso.com hello federation service 主機名稱。如果您無法 tooverify 這兩個的這些設定成功，您不需要 toodo 任何其他項目。</span><span class="sxs-lookup"><span data-stu-id="19672-173">where `(your_FS_name) `is replaced with hello federation service host name your organization uses, such as fs.contoso.com.  If you are able tooverify both of these settings successfully, you do not have toodo anything else.</span></span>  

<span data-ttu-id="19672-174">範例：https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span><span class="sxs-lookup"><span data-stu-id="19672-174">Example: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml</span></span>

## <span data-ttu-id="19672-175">更新 hello 權杖簽署憑證，以手動方式<a name="manualrenew"></a></span><span class="sxs-lookup"><span data-stu-id="19672-175">Renew hello token signing certificate manually <a name="manualrenew"></a></span></span>
<span data-ttu-id="19672-176">您可以選擇 toorenew hello 權杖簽署憑證以手動方式。</span><span class="sxs-lookup"><span data-stu-id="19672-176">You may choose toorenew hello token signing certificates manually.</span></span> <span data-ttu-id="19672-177">例如，hello 下列案例可能更適合手動更新：</span><span class="sxs-lookup"><span data-stu-id="19672-177">For example, hello following scenarios might work better for manual renewal:</span></span>

* <span data-ttu-id="19672-178">權杖簽署憑證不是自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="19672-178">Token signing certificates are not self-signed certificates.</span></span> <span data-ttu-id="19672-179">hello 最常見的原因是您的組織管理組織的憑證授權單位從註冊的 AD FS 憑證。</span><span class="sxs-lookup"><span data-stu-id="19672-179">hello most common reason for this is that your organization manages AD FS certificates enrolled from an organizational certificate authority.</span></span>
* <span data-ttu-id="19672-180">網路安全性不允許 hello 同盟中繼資料 toobe 公開使用。</span><span class="sxs-lookup"><span data-stu-id="19672-180">Network security does not allow hello federation metadata toobe publicly available.</span></span>

<span data-ttu-id="19672-181">在這些情況下，每次您更新 hello 權杖簽署憑證，您也必須更新您的 Office 365 網域使用 hello PowerShell 命令，Update-msolfederateddomain。</span><span class="sxs-lookup"><span data-stu-id="19672-181">In these scenarios, every time you update hello token signing certificates, you must also update your Office 365 domain by using hello PowerShell command, Update-MsolFederatedDomain.</span></span>

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a><span data-ttu-id="19672-182">步驟 1︰確認 AD FS 具有新的權杖簽署憑證</span><span class="sxs-lookup"><span data-stu-id="19672-182">Step 1: Ensure that AD FS has new token signing certificates</span></span>
<span data-ttu-id="19672-183">**非預設設定**</span><span class="sxs-lookup"><span data-stu-id="19672-183">**Non-default configuration**</span></span>

<span data-ttu-id="19672-184">如果您使用 AD FS 的非預設組態 (其中**AutoCertificateRollover**設定得**False**)，您可能想要使用自訂憑證 （不是自我簽署）。</span><span class="sxs-lookup"><span data-stu-id="19672-184">If you are using a non-default configuration of AD FS (where **AutoCertificateRollover** is set too**False**), you are probably using custom certificates (not self-signed).</span></span> <span data-ttu-id="19672-185">如需有關如何 toorenew hello AD FS 權杖簽署憑證的詳細資訊，請參閱[指導的客戶未使用 AD FS 自我簽署憑證](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert)。</span><span class="sxs-lookup"><span data-stu-id="19672-185">For more information about how toorenew hello AD FS token signing certificates, see [Guidance for customers not using AD FS self-signed certificates](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).</span></span>

<span data-ttu-id="19672-186">**無法公開取得同盟中繼資料**</span><span class="sxs-lookup"><span data-stu-id="19672-186">**Federation metadata is not publicly available**</span></span>

<span data-ttu-id="19672-187">如果在 hello 相反地， **AutoCertificateRollover**設定得**True**，但您的同盟中繼資料不是可公開存取，首先請確定是否已由 AD 產生新的權杖簽署憑證FS。</span><span class="sxs-lookup"><span data-stu-id="19672-187">On hello other hand, if **AutoCertificateRollover** is set too**True**, but your federation metadata is not publicly accessible, first make sure that new token signing certificates have been generated by AD FS.</span></span> <span data-ttu-id="19672-188">確認您有新的權杖簽署憑證的步驟採取 hello:</span><span class="sxs-lookup"><span data-stu-id="19672-188">Confirm you have new token signing certificates by taking hello following steps:</span></span>

1. <span data-ttu-id="19672-189">請確認您已登入 toohello 主要 AD FS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="19672-189">Verify that you are logged on toohello primary AD FS server.</span></span>
2. <span data-ttu-id="19672-190">檢查開啟 PowerShell 命令視窗中，並執行下列命令的 hello hello 目前的簽署憑證中 AD FS:</span><span class="sxs-lookup"><span data-stu-id="19672-190">Check hello current signing certificates in AD FS by opening a PowerShell command window, and running hello following command:</span></span>

    <span data-ttu-id="19672-191">PS C:\>Get-ADFSCertificate -CertificateType token-signing</span><span class="sxs-lookup"><span data-stu-id="19672-191">PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

   > [!NOTE]
   > <span data-ttu-id="19672-192">如果您使用 AD FS 2.0，則必須先執行 Add-Pssnapin Microsoft.Adfs.Powershell。</span><span class="sxs-lookup"><span data-stu-id="19672-192">If you are using AD FS 2.0, you should run Add-Pssnapin Microsoft.Adfs.Powershell first.</span></span>
   >
   >
3. <span data-ttu-id="19672-193">查看 hello 命令輸出，在列出任何憑證。</span><span class="sxs-lookup"><span data-stu-id="19672-193">Look at hello command output at any certificates listed.</span></span> <span data-ttu-id="19672-194">如果 AD FS 已產生新的憑證，您應該會看到 hello 輸出中的兩個憑證： 一個用於哪些 hello **IsPrimary**值是**True**和 hello **NotAfter**日期在 5 天，而另一個用於其**IsPrimary**是**False**和**NotAfter**是關於在 hello 未來一年。</span><span class="sxs-lookup"><span data-stu-id="19672-194">If AD FS has generated a new certificate, you should see two certificates in hello output: one for which hello **IsPrimary** value is **True** and hello **NotAfter** date is within 5 days, and one for which **IsPrimary** is **False** and **NotAfter** is about a year in hello future.</span></span>
4. <span data-ttu-id="19672-195">如果您只有一個憑證，請參閱 < 和 hello **NotAfter**日期為 5 天內，您需要 toogenerate 新憑證。</span><span class="sxs-lookup"><span data-stu-id="19672-195">If you only see one certificate, and hello **NotAfter** date is within 5 days, you need toogenerate a new certificate.</span></span>
5. <span data-ttu-id="19672-196">toogenerate 新憑證時，執行下列 PowerShell 命令提示字元命令的 hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`。</span><span class="sxs-lookup"><span data-stu-id="19672-196">toogenerate a new certificate, execute hello following command at a PowerShell command prompt: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.</span></span>
6. <span data-ttu-id="19672-197">執行下列命令一次的 hello 驗證 hello 更新： PS c:\>Get ADFSCertificate – Token-encryption 權杖簽署</span><span class="sxs-lookup"><span data-stu-id="19672-197">Verify hello update by running hello following command again: PS C:\>Get-ADFSCertificate –CertificateType token-signing</span></span>

<span data-ttu-id="19672-198">現在應該會列出兩個憑證，其中具有**NotAfter**日期大約一年中 hello 未來，以及哪些 hello **IsPrimary**值是**False**。</span><span class="sxs-lookup"><span data-stu-id="19672-198">Two certificates should be listed now, one of which has a **NotAfter** date of approximately one year in hello future, and for which hello **IsPrimary** value is **False**.</span></span>

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a><span data-ttu-id="19672-199">步驟 2： 更新 hello 新權杖簽署憑證 hello Office 365 信任</span><span class="sxs-lookup"><span data-stu-id="19672-199">Step 2: Update hello new token signing certificates for hello Office 365 trust</span></span>
<span data-ttu-id="19672-200">更新 hello 新權杖簽署憑證 toobe，如下所示為 hello 信任使用 Office 365。</span><span class="sxs-lookup"><span data-stu-id="19672-200">Update Office 365 with hello new token signing certificates toobe used for hello trust, as follows.</span></span>

1. <span data-ttu-id="19672-201">開啟 hello Microsoft Azure Active Directory 的 Windows PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="19672-201">Open hello Microsoft Azure Active Directory Module for Windows PowerShell.</span></span>
2. <span data-ttu-id="19672-202">執行 $cred=Get-Credential。</span><span class="sxs-lookup"><span data-stu-id="19672-202">Run $cred=Get-Credential.</span></span> <span data-ttu-id="19672-203">當此 Cmdlet 提示您輸入認證時，請輸入您的雲端服務系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="19672-203">When this cmdlet prompts you for credentials, type your cloud service administrator account credentials.</span></span>
3. <span data-ttu-id="19672-204">執行 Connect-MsolService –Credential $cred。此 cmdlet 會將您連線 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="19672-204">Run Connect-MsolService –Credential $cred. This cmdlet connects you toohello cloud service.</span></span> <span data-ttu-id="19672-205">建立會將您連線的內容 toohello 雲端服務都必須先執行任何 hello hello 工具所安裝的其他 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="19672-205">Creating a context that connects you toohello cloud service is required before running any of hello additional cmdlets installed by hello tool.</span></span>
4. <span data-ttu-id="19672-206">如果您不是 AD FS hello 主要同盟伺服器的電腦上執行這些命令，執行 Set-msoladfscontext-電腦<AD FS primary server>，其中<AD FS primary server>是 hello 主要 AD FS 伺服器的 hello 內部 FQDN 名稱。</span><span class="sxs-lookup"><span data-stu-id="19672-206">If you are running these commands on a computer that is not hello AD FS primary federation server, run Set-MSOLAdfscontext -Computer <AD FS primary server>, where <AD FS primary server> is hello internal FQDN name of hello primary AD FS server.</span></span> <span data-ttu-id="19672-207">此 cmdlet 會建立 tooAD FS 會將您連線的內容。</span><span class="sxs-lookup"><span data-stu-id="19672-207">This cmdlet creates a context that connects you tooAD FS.</span></span>
5. <span data-ttu-id="19672-208">執行 Update-MSOLFederatedDomain –DomainName <domain>。</span><span class="sxs-lookup"><span data-stu-id="19672-208">Run Update-MSOLFederatedDomain –DomainName <domain>.</span></span> <span data-ttu-id="19672-209">此 cmdlet 會更新到 hello 的雲端服務，從 AD FS 的 hello 設定，並設定 hello hello 兩者之間的信任關係。</span><span class="sxs-lookup"><span data-stu-id="19672-209">This cmdlet updates hello settings from AD FS into hello cloud service, and configures hello trust relationship between hello two.</span></span>

> [!NOTE]
> <span data-ttu-id="19672-210">如果您需要 toosupport 多個最上層網域的詳細資訊，例如 contoso.com 和 fabrikam.com，您必須使用 hello **SupportMultipleDomain**參數搭配任何 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="19672-210">If you need toosupport multiple top-level domains, such as contoso.com and fabrikam.com, you must use hello **SupportMultipleDomain** switch with any cmdlets.</span></span> <span data-ttu-id="19672-211">如需詳細資訊，請參閱 [支援多個頂層網域](active-directory-aadconnect-multiple-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="19672-211">For more information, see [Support for Multiple Top Level Domains](active-directory-aadconnect-multiple-domains.md).</span></span>
>
>

## <span data-ttu-id="19672-212">使用 Azure AD Connect 修復 Azure AD 信任 <a name="connectrenew"></a></span><span class="sxs-lookup"><span data-stu-id="19672-212">Repair Azure AD trust by using Azure AD Connect <a name="connectrenew"></a></span></span>
<span data-ttu-id="19672-213">如果您使用 Azure AD Connect 設定您的 AD FS 伺服器陣列和 Azure AD 信任，您可以使用 Azure AD Connect toodetect，如果您對於您的權杖簽署憑證需要 tootake 任何動作。</span><span class="sxs-lookup"><span data-stu-id="19672-213">If you configured your AD FS farm and Azure AD trust by using Azure AD Connect, you can use Azure AD Connect toodetect if you need tootake any action for your token signing certificates.</span></span> <span data-ttu-id="19672-214">如果您需要 toorenew hello 憑證時，您可以使用 Azure AD Connect toodo 因此。</span><span class="sxs-lookup"><span data-stu-id="19672-214">If you need toorenew hello certificates, you can use Azure AD Connect toodo so.</span></span>

<span data-ttu-id="19672-215">如需詳細資訊，請參閱[修復 hello 信任](active-directory-aadconnect-federation-management.md)。</span><span class="sxs-lookup"><span data-stu-id="19672-215">For more information, see [Repairing hello trust](active-directory-aadconnect-federation-management.md).</span></span>
