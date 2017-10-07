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
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>開始在 Azure Active Directory 中使用憑證式驗證

憑證型驗證可讓您連接至您 Exchange online 帳戶時，由 Azure Active Directory 驗證 Windows、 Android 或 iOS 裝置上的用戶端憑證的 toobe: 

- Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word   

- Exchange ActiveSync (EAS) 用戶端 

設定此功能可減少 hello 需要 tooenter 使用者名稱和密碼組合成特定郵件和行動裝置上的 Microsoft Office 應用程式。 

本主題內容：

- 提供您以 hello 步驟 tooconfigure，並且使用憑證型驗證的使用者的租用戶在 Office 365 企業版、 企業、 教育版和美國政府計劃。 在 Office 365 China、US Government Defense 及 US Government Federal 方案中，這項功能處於預覽版。 

- 假設您已經設定[公開金鑰基礎結構 (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) 和 [AD FS](connect/active-directory-aadconnectfed-whatis.md)。    


## <a name="requirements"></a>需求

tooconfigure 憑證式驗證 hello 下列必須為真：  

- 只有瀏覽器應用程式或使用新式驗證 (ADAL) 之原生用戶端的同盟環境才支援憑證式驗證 (CBA)。 hello 一個例外狀況是 Exchange Active Sync (EAS)，如 EXO 可以用於兩者，同盟和受管理的帳戶。 

- hello 根憑證授權單位和任何中繼憑證授權單位必須設定 Azure Active Directory 中。  

- 每個憑證授權單位都必須有一份可透過網際網路對應 URL 來參考的憑證撤銷清單 (CRL)。  

- 您至少必須在 Azure Active Directory 中設定一個憑證授權單位。 您可以在 hello 找到相關的步驟[設定 hello 憑證授權單位](#step-2-configure-the-certificate-authorities)> 一節。  

- Exchange ActiveSync 用戶端，hello 用戶端憑證必須具有 hello 使用者路由傳送電子郵件中任一 hello 主體名稱位址在 Exchange online 或 hello RFC822 名稱值中的 hello 主體別名 欄位。 Azure Active Directory 對應 hello RFC822 值 toohello Proxy 位址屬性 hello 目錄中。  

- 用戶端裝置必須存取 tooat 至少有一個憑證授權單位所簽發用戶端憑證。  

- 用戶端驗證的用戶端憑證必須已發出 tooyour 用戶端。  




## <a name="step-1-select-your-device-platform"></a>步驟 1︰選取裝置平台

第一個步驟是針對 hello 裝置平台，您有興趣，您需要 tooreview hello 下列：

- hello Office 行動應用程式支援 
- hello 特定的實作需求  

hello 與相關的資訊有下列裝置平台的 hello:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>步驟 2： 設定 hello 憑證授權單位 

tooconfigure 在 Azure Active Directory 中，為每個憑證授權單位，您憑證授權單位上傳下列 hello: 

* 在 hello hello 憑證公開部分*.cer*格式 
* hello 網際網路對向的 Url，其中 hello 憑證撤銷清單 (Crl) 位於

憑證授權單位的 hello 結構描述看起來如下： 

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

Hello 設定，您可以使用 hello [Azure Active Directory PowerShell 版本 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. 以系統管理員權限啟動 Windows PowerShell。 
2. 安裝 hello Azure AD 模組。 您需要 tooinstall 版本[2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33)或更高版本。  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

在第一個組態步驟中，您會需要 tooestablish 連接與您的租用戶。 只要有連接 tooyour 租用戶，您可以檢閱、 新增、 刪除和修改您的目錄中所定義的 hello 受信任憑證授權單位。 

### <a name="connect"></a>連線

tooestablish 連接與您的租用戶使用 hello[連接 azure Ad](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>擷取 

tooretrieve hello 受信任憑證授權單位會定義在目錄中，使用 hello [Get AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet。 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>加

toocreate 受信任的憑證授權單位使用 hello[新增 AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet 和設定 hello **crlDistributionPoint**屬性 tooa 正確的值： 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>移除

tooremove 受信任的憑證授權單位使用 hello[移除 AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>修改

toomodify 受信任的憑證授權單位使用 hello[組 AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>步驟 3︰設定撤銷

用戶端憑證，Azure Active Directory toorevoke 提取 hello 憑證撤銷清單 (CRL) hello Url 中的憑證授權單位資訊的過程中上傳並快取。 hello 上次發行的時間戳記 (**生效日期**屬性) 中使用 CRL 的 hello tooensure hello CRL 是否仍然有效。 hello CRL 會定期參考的 toorevoke 存取 toocertificates 屬於 hello 清單。

如果需要 （例如，如果使用者遺失裝置） 更立即撤銷，可能會無效 hello 的 hello 使用者的授權權杖。 tooinvalidate hello 授權權杖，將 hello **StsRefreshTokenValidFrom**欄位以供這個特定的使用者使用 Windows PowerShell。 您必須更新 hello **StsRefreshTokenValidFrom**欄位以供您想要針對 toorevoke 存取每位使用者。

hello 撤銷保存 tooensure，您必須設定 hello**生效日期**hello CRL tooa 日期之後所設定的 hello 值的**StsRefreshTokenValidFrom**並確認 hello 憑證有問題hello CRL。

hello 更新，以及所設定的 hello 失效 hello 授權權杖的步驟大綱 hello 程序之後**StsRefreshTokenValidFrom**欄位。 

**tooconfigure 撤銷：** 

1. 連線管理員認證 toohello MSOL 服務： 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. 擷取使用者 hello 目前 StsRefreshTokensValidFrom 值： 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. 設定新的 StsRefreshTokensValidFrom hello 使用者等於 toohello 目前時間戳記值： 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

您所設定的 hello 日期必須在未來的 hello。 如果 hello 日期不是在未來的 hello，hello **StsRefreshTokensValidFrom**屬性未設定。 Hello 日期是否在未來，hello **StsRefreshTokensValidFrom**設定 toohello 目前時間 （而非 hello 日期 Set-msoluser 指令所指示）。 


## <a name="step-4-test-your-configuration"></a>步驟 4︰測試組態

### <a name="testing-your-certificate"></a>測試您的憑證

做為第一個組態測試，您應該試著在 toosign 太[Outlook Web Access](https://outlook.office365.com)或[SharePoint Online](https://microsoft.sharepoint.com)使用您**裝置上瀏覽器**。

如果登入成功，您便知道︰

- 已佈建的 tooyour 測試裝置 hello 使用者憑證。
- AD FS 已正確設定  


### <a name="testing-office-mobile-applications"></a>測試 Office 行動應用程式

**tootest 憑證式驗證您的 Office 行動應用程式上：** 

1. 在您的測試裝置上，安裝 Office 行動應用程式 (例如 OneDrive)。
3. 啟動 hello 應用程式。 
4. 輸入您的使用者名稱，然後選取您想要 toouse hello 使用者憑證。 

您應該可以順利登入。 

### <a name="testing-exchange-activesync-client-applications"></a>測試 Exchange ActiveSync 用戶端應用程式

透過使用憑證式驗證，其中包含 hello 用戶端憑證的 EAS 設定檔的 Exchange ActiveSync (EAS) tooaccess 必須可用 toohello 應用程式。 

hello EAS 設定檔必須包含下列資訊的 hello:

- hello 用於驗證的使用者憑證 toobe 

- hello EAS 端點 (例如，outlook.office365.com)

EAS 設定檔可以設定，並放在透過行動裝置管理 (MDM) 與 Intune 等，或以手動方式將 hello 憑證放入 hello hello 裝置上的 EAS 設定檔中的 hello 善用 hello 裝置中。  

### <a name="testing-eas-client-applications-on-android"></a>在 Android 上測試 EAS 用戶端應用程式

**tootest 憑證驗證：**  

1. Hello 滿足上述 hello 需求的應用程式中設定的 EAS 設定檔。  
2. 開啟 hello 應用程式，並確認郵件正在同步處理。 

