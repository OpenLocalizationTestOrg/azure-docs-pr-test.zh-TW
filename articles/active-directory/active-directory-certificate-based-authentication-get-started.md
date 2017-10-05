---
title: "Azure Active Directory 憑證式驗證 | Microsoft Docs"
description: "了解如何在環境中設定憑證式驗證"
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="80ea2-103">開始在 Azure Active Directory 中使用憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="80ea2-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="80ea2-104">在將您的 Exchange Online 帳戶連線到下列各項時，憑證式驗證可讓您由 Azure Active Directory 透過用戶端憑證在 Windows、Android 或 iOS 裝置上驗證您的身分︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="80ea2-105">Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="80ea2-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="80ea2-106">Exchange ActiveSync (EAS) 用戶端</span><span class="sxs-lookup"><span data-stu-id="80ea2-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="80ea2-107">設定這項功能之後，就不需要在行動裝置上的特定郵件和 Microsoft Office 應用程式中，輸入使用者名稱和密碼的組合。</span><span class="sxs-lookup"><span data-stu-id="80ea2-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="80ea2-108">本主題內容：</span><span class="sxs-lookup"><span data-stu-id="80ea2-108">This topic:</span></span>

- <span data-ttu-id="80ea2-109">提供為 Office 365 企業版、商務版、教育版、美國政府方案的租用戶使用者，設定和使用憑證式驗證的步驟。</span><span class="sxs-lookup"><span data-stu-id="80ea2-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="80ea2-110">在 Office 365 China、US Government Defense 及 US Government Federal 方案中，這項功能處於預覽版。</span><span class="sxs-lookup"><span data-stu-id="80ea2-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="80ea2-111">假設您已經設定[公開金鑰基礎結構 (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) 和 [AD FS](connect/active-directory-aadconnectfed-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="80ea2-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="80ea2-112">需求</span><span class="sxs-lookup"><span data-stu-id="80ea2-112">Requirements</span></span>

<span data-ttu-id="80ea2-113">若要設定憑證式驗證，必須符合以下要件：</span><span class="sxs-lookup"><span data-stu-id="80ea2-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="80ea2-114">只有瀏覽器應用程式或使用新式驗證 (ADAL) 之原生用戶端的同盟環境才支援憑證式驗證 (CBA)。</span><span class="sxs-lookup"><span data-stu-id="80ea2-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="80ea2-115">唯一的例外狀況是適用於 EXO 的 Exchange Active Sync (EAS)，可以用於同盟和受管理兩種帳戶。</span><span class="sxs-lookup"><span data-stu-id="80ea2-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="80ea2-116">務必要在 Azure Active Directory 中設定根憑證授權單位和任何中繼憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="80ea2-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="80ea2-117">每個憑證授權單位都必須有一份可透過網際網路對應 URL 來參考的憑證撤銷清單 (CRL)。</span><span class="sxs-lookup"><span data-stu-id="80ea2-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="80ea2-118">您至少必須在 Azure Active Directory 中設定一個憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="80ea2-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="80ea2-119">您可以在[設定憑證授權單位](#step-2-configure-the-certificate-authorities)一節中找到相關步驟。</span><span class="sxs-lookup"><span data-stu-id="80ea2-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="80ea2-120">(僅 Exchange ActiveSync 用戶端適用) 用戶端憑證必須將 Exchange Online 中可路由傳送的使用者電子郵件地址，放在 [主體別名] 欄位的 [主體名稱] 或 [RFC822 名稱] 值中。</span><span class="sxs-lookup"><span data-stu-id="80ea2-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="80ea2-121">Azure Active Directory 要將 RFC822 值對應到目錄中的 [Proxy 位址] 屬性。</span><span class="sxs-lookup"><span data-stu-id="80ea2-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="80ea2-122">您的用戶端裝置必須至少可以存取一個發出用戶端憑證的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="80ea2-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="80ea2-123">用於戶端驗證的用戶端憑證必須已經發給您的用戶端。</span><span class="sxs-lookup"><span data-stu-id="80ea2-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="80ea2-124">步驟 1︰選取裝置平台</span><span class="sxs-lookup"><span data-stu-id="80ea2-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="80ea2-125">第一個步驟中，針對您要處理的裝置平台，您需要檢閱下列項目︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="80ea2-126">Office 行動應用程式支援</span><span class="sxs-lookup"><span data-stu-id="80ea2-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="80ea2-127">特定的實作需求</span><span class="sxs-lookup"><span data-stu-id="80ea2-127">The specific implementation requirements</span></span>  

<span data-ttu-id="80ea2-128">下列裝置平台有相關的資訊︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="80ea2-129">Android</span><span class="sxs-lookup"><span data-stu-id="80ea2-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="80ea2-130">iOS</span><span class="sxs-lookup"><span data-stu-id="80ea2-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="80ea2-131">步驟 2︰設定憑證授權單位</span><span class="sxs-lookup"><span data-stu-id="80ea2-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="80ea2-132">若要在 Azure Active Directory 中設定您的憑證授權單位，為每個憑證授權單位下載下列項目：</span><span class="sxs-lookup"><span data-stu-id="80ea2-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="80ea2-133">憑證的公開部分 (「.cer」  格式)</span><span class="sxs-lookup"><span data-stu-id="80ea2-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="80ea2-134">憑證撤銷清單 (CRl) 所在的網際網路對應 URL</span><span class="sxs-lookup"><span data-stu-id="80ea2-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="80ea2-135">憑證授權單位的結構描述看起來像這樣︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="80ea2-136">設定時，您可以使用 [Azure Active Directory PowerShell 第 2 版](/powershell/azure/install-adv2?view=azureadps-2.0)：</span><span class="sxs-lookup"><span data-stu-id="80ea2-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="80ea2-137">以系統管理員權限啟動 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="80ea2-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="80ea2-138">安裝 Azure AD 模組。</span><span class="sxs-lookup"><span data-stu-id="80ea2-138">Install the Azure AD module.</span></span> <span data-ttu-id="80ea2-139">您必須安裝 [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="80ea2-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="80ea2-140">設定的第一個步驟，您需要與您的租用戶建立連線。</span><span class="sxs-lookup"><span data-stu-id="80ea2-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="80ea2-141">一旦您與租用戶的連線存在，您可以檢閱、新增、刪除、修改在您的目錄中定義的受信任的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="80ea2-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="80ea2-142">連線</span><span class="sxs-lookup"><span data-stu-id="80ea2-142">Connect</span></span>

<span data-ttu-id="80ea2-143">若要與您的租用戶建立連線，使用 [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="80ea2-144">擷取</span><span class="sxs-lookup"><span data-stu-id="80ea2-144">Retrieve</span></span> 

<span data-ttu-id="80ea2-145">若要擷取您的目錄中所定義的受信任的憑證授權單位，使用 [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="80ea2-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="80ea2-146">加</span><span class="sxs-lookup"><span data-stu-id="80ea2-146">Add</span></span>

<span data-ttu-id="80ea2-147">若要建立受信任的憑證授權單位，使用 [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) Cmdlet 並將 **crlDistributionPoint** 屬性設為正確值：</span><span class="sxs-lookup"><span data-stu-id="80ea2-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="80ea2-148">移除</span><span class="sxs-lookup"><span data-stu-id="80ea2-148">Remove</span></span>

<span data-ttu-id="80ea2-149">若要移除受信任的憑證授權單位，使用 [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="80ea2-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="80ea2-150">修改</span><span class="sxs-lookup"><span data-stu-id="80ea2-150">Modfiy</span></span>

<span data-ttu-id="80ea2-151">若要修改受信任的憑證授權單位，使用 [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="80ea2-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="80ea2-152">步驟 3︰設定撤銷</span><span class="sxs-lookup"><span data-stu-id="80ea2-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="80ea2-153">若要撤銷用戶端憑證，Azure Active Directory 會從和憑證授權單位資訊一起上傳的 URL 中，擷取憑證撤銷清單 (CRL) 並加以快取。</span><span class="sxs-lookup"><span data-stu-id="80ea2-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="80ea2-154">在 CRL 中，上次發佈的時間戳記 ([生效日期] 屬性) 是用來確保 CRL 依然有效。</span><span class="sxs-lookup"><span data-stu-id="80ea2-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="80ea2-155">定期參考 CRL 以撤銷對清單所列憑證的存取權。</span><span class="sxs-lookup"><span data-stu-id="80ea2-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="80ea2-156">如果需要立即撤銷 (例如，使用者遺失裝置)，可以讓使用者的授權權杖失效。</span><span class="sxs-lookup"><span data-stu-id="80ea2-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="80ea2-157">使用 Windows PowerShell 設定這位特定使用者的 **StsRefreshTokenValidFrom** 欄位，即可讓授權權杖失效。</span><span class="sxs-lookup"><span data-stu-id="80ea2-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="80ea2-158">您必須為想要撤銷其存取權的每位使用者更新其 **StsRefreshTokenValidFrom** 欄位。</span><span class="sxs-lookup"><span data-stu-id="80ea2-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="80ea2-159">為了確保撤銷持續有效，您必須將 CRL 的 [生效日期] 設定為 **StsRefreshTokenValidFrom** 所設值之後的日期，並確保有問題的憑證位於 CRL 中。</span><span class="sxs-lookup"><span data-stu-id="80ea2-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="80ea2-160">下列步驟概述藉由設定 **StsRefreshTokenValidFrom** 欄位，來更新授權權杖並讓它失效的程序。</span><span class="sxs-lookup"><span data-stu-id="80ea2-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="80ea2-161">**設定撤銷：**</span><span class="sxs-lookup"><span data-stu-id="80ea2-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="80ea2-162">使用管理員認證連線到 MSOL 服務：</span><span class="sxs-lookup"><span data-stu-id="80ea2-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="80ea2-163">擷取使用者目前的 StsRefreshTokensValidFrom 值︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="80ea2-164">將目前的時間戳記設定為使用者新的 StsRefreshTokensValidFrom 值︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="80ea2-165">您設定的日期必須是未來的日期。</span><span class="sxs-lookup"><span data-stu-id="80ea2-165">The date you set must be in the future.</span></span> <span data-ttu-id="80ea2-166">如果不是未來的日期，則不會設定 **StsRefreshTokensValidFrom** 屬性。</span><span class="sxs-lookup"><span data-stu-id="80ea2-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="80ea2-167">如果是未來的日期，才會將 **StsRefreshTokensValidFrom** 設定為目前的時間 (而非 Set-MsolUser 命令指示的日期)。</span><span class="sxs-lookup"><span data-stu-id="80ea2-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="80ea2-168">步驟 4︰測試組態</span><span class="sxs-lookup"><span data-stu-id="80ea2-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="80ea2-169">測試您的憑證</span><span class="sxs-lookup"><span data-stu-id="80ea2-169">Testing your certificate</span></span>

<span data-ttu-id="80ea2-170">您應該試著使用您**裝置上的瀏覽器**登入 [Outlook Web Access](https://outlook.office365.com) 或 [SharePoint Online](https://microsoft.sharepoint.com)，這是第一個組態測試。</span><span class="sxs-lookup"><span data-stu-id="80ea2-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="80ea2-171">如果登入成功，您便知道︰</span><span class="sxs-lookup"><span data-stu-id="80ea2-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="80ea2-172">使用者憑證已佈建到您的測試裝置</span><span class="sxs-lookup"><span data-stu-id="80ea2-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="80ea2-173">AD FS 已正確設定</span><span class="sxs-lookup"><span data-stu-id="80ea2-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="80ea2-174">測試 Office 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="80ea2-174">Testing Office mobile applications</span></span>

<span data-ttu-id="80ea2-175">**在您的行動 Office 應用程式上測試憑證式驗證︰**</span><span class="sxs-lookup"><span data-stu-id="80ea2-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="80ea2-176">在您的測試裝置上，安裝 Office 行動應用程式 (例如 OneDrive)。</span><span class="sxs-lookup"><span data-stu-id="80ea2-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="80ea2-177">啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="80ea2-177">Launch the application.</span></span> 
4. <span data-ttu-id="80ea2-178">輸入您的使用者名稱，然後選取想要使用的使用者憑證。</span><span class="sxs-lookup"><span data-stu-id="80ea2-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="80ea2-179">您應該可以順利登入。</span><span class="sxs-lookup"><span data-stu-id="80ea2-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="80ea2-180">測試 Exchange ActiveSync 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="80ea2-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="80ea2-181">若要透過憑證式驗證來存取 Exchange ActiveSync (EAS)，必須要有包含用戶端憑證的 EAS 設定檔供應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="80ea2-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="80ea2-182">EAS 設定檔必須包含下列資訊：</span><span class="sxs-lookup"><span data-stu-id="80ea2-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="80ea2-183">要用於驗證的使用者憑證</span><span class="sxs-lookup"><span data-stu-id="80ea2-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="80ea2-184">EAS 端點 (例如，outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="80ea2-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="80ea2-185">您可以用行動裝置管理 (MDM)，例如 Intune，在裝置上設定和放置 EAS 設定檔，或以手動方式將憑證放在裝置的 EAS 設定檔中。</span><span class="sxs-lookup"><span data-stu-id="80ea2-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="80ea2-186">在 Android 上測試 EAS 用戶端應用程式</span><span class="sxs-lookup"><span data-stu-id="80ea2-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="80ea2-187">**測試憑證驗證：**</span><span class="sxs-lookup"><span data-stu-id="80ea2-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="80ea2-188">設定應用程式中符合上述需求的 EAS 設定檔。</span><span class="sxs-lookup"><span data-stu-id="80ea2-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="80ea2-189">開啟應用程式，然後確認正在同步處理郵件。</span><span class="sxs-lookup"><span data-stu-id="80ea2-189">Open the application, and verify that mail is synchronizing.</span></span> 

