---
title: "開始使用 Active Directory 憑證型驗證-aaaAzure |Microsoft 文件"
description: "深入了解如何在您的環境中的 tooconfigure 憑證式驗證"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="ffda1-103">開始在 Azure Active Directory 中使用憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="ffda1-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="ffda1-104">憑證型驗證可讓您連接至您 Exchange online 帳戶時，由 Azure Active Directory 驗證 Windows、 Android 或 iOS 裝置上的用戶端憑證的 toobe:</span><span class="sxs-lookup"><span data-stu-id="ffda1-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="ffda1-105">Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="ffda1-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="ffda1-106">Exchange ActiveSync (EAS) 用戶端</span><span class="sxs-lookup"><span data-stu-id="ffda1-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="ffda1-107">設定此功能可減少 hello 需要 tooenter 使用者名稱和密碼組合成特定郵件和行動裝置上的 Microsoft Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffda1-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="ffda1-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="ffda1-108">This topic:</span></span>

- <span data-ttu-id="ffda1-109">提供您以 hello 步驟 tooconfigure，並且使用憑證型驗證的使用者的租用戶在 Office 365 企業版、 企業、 教育版和美國政府計劃。</span><span class="sxs-lookup"><span data-stu-id="ffda1-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="ffda1-110">在 Office 365 China、US Government Defense 及 US Government Federal 方案中，這項功能處於預覽版。</span><span class="sxs-lookup"><span data-stu-id="ffda1-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="ffda1-111">假設您已經設定[公開金鑰基礎結構 (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) 和 [AD FS](connect/active-directory-aadconnectfed-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ffda1-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="ffda1-112">需求</span><span class="sxs-lookup"><span data-stu-id="ffda1-112">Requirements</span></span>

<span data-ttu-id="ffda1-113">tooconfigure 憑證式驗證 hello 下列必須為真：</span><span class="sxs-lookup"><span data-stu-id="ffda1-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="ffda1-114">只有瀏覽器應用程式或使用新式驗證 (ADAL) 之原生用戶端的同盟環境才支援憑證式驗證 (CBA)。</span><span class="sxs-lookup"><span data-stu-id="ffda1-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="ffda1-115">hello 一個例外狀況是 Exchange Active Sync (EAS)，如 EXO 可以用於兩者，同盟和受管理的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ffda1-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="ffda1-116">hello 根憑證授權單位和任何中繼憑證授權單位必須設定 Azure Active Directory 中。</span><span class="sxs-lookup"><span data-stu-id="ffda1-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="ffda1-117">每個憑證授權單位都必須有一份可透過網際網路對應 URL 來參考的憑證撤銷清單 (CRL)。</span><span class="sxs-lookup"><span data-stu-id="ffda1-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="ffda1-118">您至少必須在 Azure Active Directory 中設定一個憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="ffda1-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="ffda1-119">您可以在 hello 找到相關的步驟[設定 hello 憑證授權單位](#step-2-configure-the-certificate-authorities)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ffda1-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="ffda1-120">Exchange ActiveSync 用戶端，hello 用戶端憑證必須具有 hello 使用者路由傳送電子郵件中任一 hello 主體名稱位址在 Exchange online 或 hello RFC822 名稱值中的 hello 主體別名 欄位。</span><span class="sxs-lookup"><span data-stu-id="ffda1-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="ffda1-121">Azure Active Directory 對應 hello RFC822 值 toohello Proxy 位址屬性 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="ffda1-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="ffda1-122">用戶端裝置必須存取 tooat 至少有一個憑證授權單位所簽發用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="ffda1-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="ffda1-123">用戶端驗證的用戶端憑證必須已發出 tooyour 用戶端。</span><span class="sxs-lookup"><span data-stu-id="ffda1-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="ffda1-124">步驟 1︰選取裝置平台</span><span class="sxs-lookup"><span data-stu-id="ffda1-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="ffda1-125">第一個步驟是針對 hello 裝置平台，您有興趣，您需要 tooreview hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ffda1-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="ffda1-126">hello Office 行動應用程式支援</span><span class="sxs-lookup"><span data-stu-id="ffda1-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="ffda1-127">hello 特定的實作需求</span><span class="sxs-lookup"><span data-stu-id="ffda1-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="ffda1-128">hello 與相關的資訊有下列裝置平台的 hello:</span><span class="sxs-lookup"><span data-stu-id="ffda1-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="ffda1-129">Android</span><span class="sxs-lookup"><span data-stu-id="ffda1-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="ffda1-130">iOS</span><span class="sxs-lookup"><span data-stu-id="ffda1-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="ffda1-131">步驟 2： 設定 hello 憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="ffda1-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="ffda1-132">tooconfigure 在 Azure Active Directory 中，為每個憑證授權單位，您憑證授權單位上傳下列 hello:</span><span class="sxs-lookup"><span data-stu-id="ffda1-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="ffda1-133">在 hello hello 憑證公開部分*.cer*格式</span><span class="sxs-lookup"><span data-stu-id="ffda1-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="ffda1-134">hello 網際網路對向的 Url，其中 hello 憑證撤銷清單 (Crl) 位於</span><span class="sxs-lookup"><span data-stu-id="ffda1-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="ffda1-135">憑證授權單位的 hello 結構描述看起來如下：</span><span class="sxs-lookup"><span data-stu-id="ffda1-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="ffda1-136">Hello 設定，您可以使用 hello [Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="ffda1-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="ffda1-137">以系統管理員權限啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ffda1-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="ffda1-138">安裝 hello Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="ffda1-138">Install hello Azure AD module.</span></span> <span data-ttu-id="ffda1-139">您需要 tooinstall 版本[2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33)或更高版本。</span><span class="sxs-lookup"><span data-stu-id="ffda1-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="ffda1-140">在第一個組態步驟中，您會需要 tooestablish 連接與您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="ffda1-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="ffda1-141">只要有連接 tooyour 租用戶，您可以檢閱、 新增、 刪除和修改您的目錄中所定義的 hello 受信任憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="ffda1-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="ffda1-142">連線</span><span class="sxs-lookup"><span data-stu-id="ffda1-142">Connect</span></span>

<span data-ttu-id="ffda1-143">tooestablish 連接與您的租用戶使用 hello[連接 azure Ad](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ffda1-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="ffda1-144">擷取</span><span class="sxs-lookup"><span data-stu-id="ffda1-144">Retrieve</span></span> 

<span data-ttu-id="ffda1-145">tooretrieve hello 受信任憑證授權單位會定義在目錄中，使用 hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="ffda1-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="ffda1-146">加</span><span class="sxs-lookup"><span data-stu-id="ffda1-146">Add</span></span>

<span data-ttu-id="ffda1-147">toocreate 受信任的憑證授權單位使用 hello[新增 AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet 和設定 hello **crlDistributionPoint**屬性 tooa 正確的值：</span><span class="sxs-lookup"><span data-stu-id="ffda1-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="ffda1-148">移除</span><span class="sxs-lookup"><span data-stu-id="ffda1-148">Remove</span></span>

<span data-ttu-id="ffda1-149">tooremove 受信任的憑證授權單位使用 hello[移除 AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ffda1-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="ffda1-150">修改</span><span class="sxs-lookup"><span data-stu-id="ffda1-150">Modfiy</span></span>

<span data-ttu-id="ffda1-151">toomodify 受信任的憑證授權單位使用 hello[組 AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ffda1-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="ffda1-152">步驟 3︰設定撤銷</span><span class="sxs-lookup"><span data-stu-id="ffda1-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="ffda1-153">用戶端憑證，Azure Active Directory toorevoke 提取 hello 憑證撤銷清單 (CRL) hello Url 中的憑證授權單位資訊的過程中上傳並快取。</span><span class="sxs-lookup"><span data-stu-id="ffda1-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="ffda1-154">hello 上次發行的時間戳記 (**生效日期**屬性) 中使用 CRL 的 hello tooensure hello CRL 是否仍然有效。</span><span class="sxs-lookup"><span data-stu-id="ffda1-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="ffda1-155">hello CRL 會定期參考的 toorevoke 存取 toocertificates 屬於 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="ffda1-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="ffda1-156">如果需要 （例如，如果使用者遺失裝置） 更立即撤銷，可能會無效 hello 的 hello 使用者的授權權杖。</span><span class="sxs-lookup"><span data-stu-id="ffda1-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="ffda1-157">tooinvalidate hello 授權權杖，將 hello **StsRefreshTokenValidFrom**欄位以供這個特定的使用者使用 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ffda1-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="ffda1-158">您必須更新 hello **StsRefreshTokenValidFrom**欄位以供您想要針對 toorevoke 存取每位使用者。</span><span class="sxs-lookup"><span data-stu-id="ffda1-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="ffda1-159">hello 撤銷保存 tooensure，您必須設定 hello**生效日期**hello CRL tooa 日期之後所設定的 hello 值的**StsRefreshTokenValidFrom**並確認 hello 憑證有問題hello CRL。</span><span class="sxs-lookup"><span data-stu-id="ffda1-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="ffda1-160">hello 更新，以及所設定的 hello 失效 hello 授權權杖的步驟大綱 hello 程序之後**StsRefreshTokenValidFrom**欄位。</span><span class="sxs-lookup"><span data-stu-id="ffda1-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="ffda1-161">**tooconfigure 撤銷：**</span><span class="sxs-lookup"><span data-stu-id="ffda1-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="ffda1-162">連線管理員認證 toohello MSOL 服務：</span><span class="sxs-lookup"><span data-stu-id="ffda1-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="ffda1-163">擷取使用者 hello 目前 StsRefreshTokensValidFrom 值：</span><span class="sxs-lookup"><span data-stu-id="ffda1-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="ffda1-164">設定新的 StsRefreshTokensValidFrom hello 使用者等於 toohello 目前時間戳記值：</span><span class="sxs-lookup"><span data-stu-id="ffda1-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="ffda1-165">您所設定的 hello 日期必須在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="ffda1-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="ffda1-166">如果 hello 日期不是在未來的 hello，hello **StsRefreshTokensValidFrom**屬性未設定。</span><span class="sxs-lookup"><span data-stu-id="ffda1-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="ffda1-167">Hello 日期是否在未來，hello **StsRefreshTokensValidFrom**設定 toohello 目前時間 （而非 hello 日期 Set-msoluser 指令所指示）。</span><span class="sxs-lookup"><span data-stu-id="ffda1-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="ffda1-168">步驟 4︰測試組態</span><span class="sxs-lookup"><span data-stu-id="ffda1-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="ffda1-169">測試您的憑證</span><span class="sxs-lookup"><span data-stu-id="ffda1-169">Testing your certificate</span></span>

<span data-ttu-id="ffda1-170">做為第一個組態測試，您應該試著在 toosign 太[Outlook Web Access](https://outlook.office365.com)或[SharePoint Online](https://microsoft.sharepoint.com)使用您**裝置上瀏覽器**。</span><span class="sxs-lookup"><span data-stu-id="ffda1-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="ffda1-171">如果登入成功，您便知道︰</span><span class="sxs-lookup"><span data-stu-id="ffda1-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="ffda1-172">已佈建的 tooyour 測試裝置 hello 使用者憑證。</span><span class="sxs-lookup"><span data-stu-id="ffda1-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="ffda1-173">AD FS 已正確設定</span><span class="sxs-lookup"><span data-stu-id="ffda1-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="ffda1-174">測試 Office 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="ffda1-174">Testing Office mobile applications</span></span>

<span data-ttu-id="ffda1-175">**tootest 憑證式驗證您的 Office 行動應用程式上：**</span><span class="sxs-lookup"><span data-stu-id="ffda1-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="ffda1-176">在您的測試裝置上，安裝 Office 行動應用程式 (例如 OneDrive)。</span><span class="sxs-lookup"><span data-stu-id="ffda1-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="ffda1-177">啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffda1-177">Launch hello application.</span></span> 
4. <span data-ttu-id="ffda1-178">輸入您的使用者名稱，然後選取您想要 toouse hello 使用者憑證。</span><span class="sxs-lookup"><span data-stu-id="ffda1-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="ffda1-179">您應該可以順利登入。</span><span class="sxs-lookup"><span data-stu-id="ffda1-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="ffda1-180">測試 Exchange ActiveSync 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="ffda1-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="ffda1-181">透過使用憑證式驗證，其中包含 hello 用戶端憑證的 EAS 設定檔的 Exchange ActiveSync (EAS) tooaccess 必須可用 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffda1-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="ffda1-182">hello EAS 設定檔必須包含下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="ffda1-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="ffda1-183">hello 用於驗證的使用者憑證 toobe</span><span class="sxs-lookup"><span data-stu-id="ffda1-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="ffda1-184">hello EAS 端點 (例如，outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="ffda1-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="ffda1-185">EAS 設定檔可以設定，並放在透過行動裝置管理 (MDM) 與 Intune 等，或以手動方式將 hello 憑證放入 hello hello 裝置上的 EAS 設定檔中的 hello 善用 hello 裝置中。</span><span class="sxs-lookup"><span data-stu-id="ffda1-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="ffda1-186">在 Android 上測試 EAS 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="ffda1-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="ffda1-187">**tootest 憑證驗證：**</span><span class="sxs-lookup"><span data-stu-id="ffda1-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="ffda1-188">Hello 滿足上述 hello 需求的應用程式中設定的 EAS 設定檔。</span><span class="sxs-lookup"><span data-stu-id="ffda1-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="ffda1-189">開啟 hello 應用程式，並確認郵件正在同步處理。</span><span class="sxs-lookup"><span data-stu-id="ffda1-189">Open hello application, and verify that mail is synchronizing.</span></span> 

