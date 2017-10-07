---
title: "Azure AD Connect：使用 SAML 2.0 識別提供者來進行單一登入 | Microsoft Docs"
description: "本主題描述如何使用 SAML 2.0 相容 Idp 來進行單一登入。"
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>使用 SAML 2.0 識別提供者 (IdP) 來進行單一登入

本主題包含資訊使用 SAML 2.0 相容之 Sp-lite 設定檔身分識別提供者做為架構 hello 慣用安全性權杖服務 (STS) / 身分識別提供者。 在已有內部部署的使用者目錄和密碼存放區並可使用 SAML 2.0 來加以存取時，這種做法非常實用。 這個現有的使用者目錄可用來登入 tooOffice 365 和其他 Azure AD 保護的資源。 hello SAML 2.0 Sp-lite 設定檔根據 hello 廣泛使用安全性聲明標記語言 (SAML) 同盟識別身分標準 tooprovide 登入和屬性交換架構。

>[!NOTE]
>如需第 3 個合作對象的 Idps 過搭配 Azure AD，請參閱 hello [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)

Microsoft hello 整合，例如 Office 365 的 Microsoft 雲端服務的形式支援此登入體驗，您已正確設定 SAML 2.0 設定檔基礎 IdP。 SAML 2.0 身分識別提供者是第三方產品，因此 Microsoft 不提供支援的 hello 部署、 設定、 疑難排解最佳作法等項目的相關。 一次正確設定，與 hello SAML 2.0 身分識別提供者可以透過使用 hello 以下更詳細說明 Microsoft Connectivity Analyzer Tool 測試的適當組態的 hello 整合。 如需 SAML 2.0 Sp-lite 設定檔型身分識別提供者的詳細資訊，請詢問 hello 組織提供它。

>[!IMPORTANT]
>在此登入案例中，只有一小部分的用戶端可與 SAML 2.0 識別提供者搭配使用，這些用戶端包括：

>- Web 型用戶端，例如 Outlook Web Access 和 SharePoint Online
- 使用基本驗證和 IMAP、 POP、 Active Sync、 MAPI，例如支援的 Exchange 存取方法的電子郵件豐富型用戶端等 (hello 結束點是部署的必要的 toobe 增強用戶端通訊協定)，包括：
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016、Apple iPhone (各種 iOS 版本)
    - 各種 Google Android 裝置
    - Windows Phone 7、Windows Phone 7.8 及 Windows Phone 8.0
    - Windows 8 郵件用戶端和 Windows 8.1 郵件用戶端
    - Windows 10 郵件用戶端

在此登入案例中，其他所有用戶端則無法與 SAML 2.0 識別提供者搭配使用。 例如，hello Lync 2010 桌面用戶端不能 toologin hello 服務設定進行單一登入您 SAML 2.0 身分識別提供者。

## <a name="azure-ad-saml-20-protocol-requirements"></a>Azure AD SAML 2.0 通訊協定需求
本主題包含 hello 通訊協定和訊息格式與 Azure AD tooenable 登入 tooone toofederate 或多個 Microsoft 雲端服務 （例如 Office 365)，必須實作您的 SAML 2.0 身分識別提供者的詳細的需求。 hello SAML 2.0 信賴憑證者合作對象 (SP-STS) 在此案例中使用的 Microsoft 雲端服務是 Azure AD。

建議您確保 SAML 2.0 身分識別提供者輸出訊息是儘可能提供的範例追蹤相似 toohello 當做。 此外，請盡可能使用特定的屬性值從提供的 hello Azure AD 中繼資料。 一旦您滿意您的輸出訊息時，您可以測試以 hello Microsoft Connectivity Analyzer，如下所述。

hello Azure AD 中繼資料可以從此 URL 下載： [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml)。
針對客戶在中國使用 hello 的 Office 365 的中國特定執行個體，應該使用 hello 遵循同盟端點： [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>SAML 通訊協定需求
本節詳述如何 hello 要求和回應訊息配對會放在一起的順序 toohelp 您 tooformat 郵件正確。

Azure AD 可與使用特定需求的 hello SAML 2.0 SP Lite 設定檔，如下所示的身分識別提供者設定的 toowork。 使用 hello 範例 SAML 要求和回應訊息搭配自動化和手動測試，您可以使用與 Azure AD 的 tooachieve 互通性。

## <a name="signature-block-requirements"></a>簽章區塊需求
在 SAML 回應 hello 訊息 hello 簽章節點會包含 hello hello 訊息本身的數位簽章的相關資訊。 hello 簽章區塊具有下列需求的 hello:

1. hello 宣告節點本身必須經過簽署。
2.  hello rsa-sha1 演算法必須當做 hello DigestMethod。 不接受其他數位簽章演算法。
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  您也可以簽署 hello XML 文件。 
4.  hello Transform Algorithm 必須符合 hello 遵循範例中的 hello 值：`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  hello SignatureMethod Algorithm 必須符合下列範例中的 hello:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>支援的繫結
繫結是 hello 傳輸相關通訊所需的參數。 下列需求的 hello 套用 toohello 繫結

1. HTTPS 是必要的 hello 傳輸。
2.  在登入期間，Azure AD 需要 HTTP POST 以便提交權杖
3.  Azure AD 會將 HTTP POST hello 驗證要求 toohello 身分識別提供者] 和 [重新導向 hello 登出訊息 toohello 身分識別提供者。

## <a name="required-attributes"></a>必要的屬性
下表會顯示 hello SAML 2.0 訊息中的特定屬性的需求。
 
|屬性|說明|
| ----- | ----- |
|NameID|此宣告 hello 值必須 hello 與 hello Azure AD 使用者的 ImmutableID 的相同。 它可以是 too64 英數字元組成。 若為非 HTML 安全字元就必須編碼，例如，"+" 字元將會顯示為 ".2B"。|
|IDPEmail|hello 使用者主體名稱 (UPN) 會列在 hello SAML 回應 hello 的項目名稱 IDPEmail 這是 hello 使用者的 UserPrincipalName (UPN) 在 Azure AD/Office 365 中。 hello UPN 的電子郵件地址格式。 Windows Office 365 (Azure Active Directory) 中的 UPN 值。|
|簽發者|這是必要的 toobe hello 身分識別提供者的 URI。 您不應該重複使用 hello 簽發者從 hello 範例訊息。 如果您有多個頂層網域，Issuer 必須符合您 Azure AD 租用戶 hello 中 hello 指定 URI 設定每個網域。|

>[!IMPORTANT]
>Azure AD 目前支援 hello 依照 SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid NameID 格式 URI 的格式： 持續性。

## <a name="sample-saml-request-and-response-messages"></a>SAML 要求和回應訊息範例
要求和回應訊息配對則會顯示 hello 登入訊息交換。
這是從 Azure AD tooa 範例 SAML 2.0 身分識別提供者傳送的範例要求訊息。 hello 範例 SAML 2.0 身分識別提供者是 Active Directory Federation Services (AD FS) 設定 toouse SAML-P 通訊協定。 此範例也已經對其他 SAML 2.0 識別提供者完成互通性測試。

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

這是範例回應訊息所送出的 hello 範例 SAML 2.0 相容身分識別提供者 tooAzure AD / Office 365。

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>設定 SAML 2.0 相容識別提供者
本主題包含如何 tooconfigure 您 SAML 2.0 身分識別提供者 toofederate 的 Azure AD tooenable 單一登入存取 tooone 或多個 Microsoft 雲端服務 （例如 Office 365) 的指導方針使用 hello SAML 2.0 通訊協定。 hello SAML 2.0 信賴憑證者在此案例中使用的 Microsoft 雲端服務的合作對象是 Azure AD。

## <a name="add-azure-ad-metadata"></a>新增 Azure AD 中繼資料
您的 SAML 2.0 身分識別提供者需要 tooadhere tooinformation 有關 hello Azure AD 信賴憑證者的合作對象。 Azure AD 會在 https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml 發佈中繼資料。

建議您一律匯入 hello 最新的 Azure AD 中繼資料時在設定 SAML 2.0 身分識別提供者。 請注意，Azure AD 不會讀取 hello 身分識別提供者中繼資料。

## <a name="add-azure-ad-as-a-relying-party"></a>將 Azure AD 新增為信賴憑證者
您有 tooenable SAML 2.0 身分識別提供者和 Azure AD 之間的通訊。 這項設定將會相依於您特定的身分識別提供者，您應該參閱 toodocumentation 它。 您需要設定信賴憑證者合作對象識別碼 toohello hello 與 hello 從 hello Azure AD 中繼資料內的 entityID 相同。

>[!NOTE]
>確認 SAML 2.0 身分識別提供者伺服器上的 hello 時鐘同步的 tooan 準確的時間來源。 錯誤的時鐘時間可能會導致同盟登入 toofail。

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行登入
您已設定您的 SAML 2.0 身分識別提供者以使用 Azure AD 登入之後，hello 下一個步驟是 toodownload 和安裝 hello Azure Active Directory 的 Windows PowerShell 模組。 安裝之後，您將使用這些 cmdlet tooconfigure 將 Azure AD 網域為同盟網域。

hello Azure Active Directory 的 Windows PowerShell 模組是在 Azure AD 中管理組織資料的下載。 此模組會安裝一組 cmdlet tooWindows PowerShell;執行這些 cmdlet tooset，設定單一登入存取 tooAzure AD 和依次 tooall hello 的雲端的服務訂閱。 如需有關 toodownload 並安裝 hello cmdlet 的指示，請參閱[http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>設定 SAML 識別提供者與 Azure AD 的信任關係
在 Azure AD 網域中設定同盟之前，您必須先設定自訂網域。 您無法將由 Microsoft 所提供的 hello 預設網域加入同盟。 microsoft hello 預設網域結尾是"onmicrosoft.com"。
您將會在 hello Windows PowerShell 命令列介面 tooadd 中執行一系列的 cmdlet，或轉換網域的單一登入。

每個您想要使用 SAML 2.0 身分識別提供者的 toofederate 必須下列其中一個的 Azure Active Directory 網域新增為單一登入網域或轉換的 toobe 單一登入網域從標準網域。 新增或轉換網域會設定 SAML 2.0 識別提供者和 Azure AD 之間的信任關係。

hello 下列程序引導您轉換現有標準網域 tooa 的同盟的網域使用 SAML 2.0 Sp-lite。 請注意您的網域可能會遇到會影響使用者 too2 時數在執行此步驟之後中斷。

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>在 Azure AD 目錄中設定用於同盟的網域


1. 連接 Azure AD 目錄租用戶系統管理員身分 tooyour： 連接 Connect-msolservice。
2.  設定您所需的 Office 365 網域 toouse 同盟和 SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  您可以取得 hello 簽署憑證從 IDP 中繼資料檔案的 base64 編碼字串。 我們提供了此位置的範例，但此範例可能會隨您的實作方式而略有不同。

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

如需「Set-msoldomainauthentication」的詳細資訊，請參閱：[http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx)。

>[!NOTE]
>只有在已經為識別提供者設定了 ECP 擴充功能時，才必須執行使用「$ecpUrl = "https://WS2012R2-0.contoso.com/PAOS"」。 Exchange Online 用戶端 (Outlook Web App (OWA) 除外) 仰賴以 POST 為基礎的作用中端點。 如果 SAML 2.0 STS 實作的作用中的結束點作用中端點類似 tooShibboleth ECP 實作它可能會以 hello Exchange Online 服務這些豐富型用戶端 toointeract。

設定同盟後，即可切換後太 「 非同盟 」 （或 「 受管理 」），不過這項變更會佔用 tootwo 小時 toocomplete 且其需要指派新的隨機密碼，雲端型登入 tooeach 使用者。 切換回太 「 受管理 」 可能會在某些案例 tooreset 需要您的設定中的錯誤。 如需網域轉換的詳細資訊，請參閱：[http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx)。

## <a name="provision-user-principals-tooazure-ad--office-365"></a>佈建使用者主體 tooAzure AD / Office 365
您可以驗證您的使用者 tooOffice 365 之前您必須與對應 toohello hello SAML 2.0 中的判斷提示的主體宣告的使用者佈建 Azure AD。 如果這些使用者主體未知的 tooAzure 事先 AD 然後它們無法用於同盟登入。 Azure AD Connect 或 Windows PowerShell 可以使用的 tooprovision 使用者主體。

Azure AD Connect 可從 hello 內部部署 Active Directory 您 Azure AD 目錄中的使用的 tooprovision 主體 tooyour 網域。 如需詳細資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](active-directory-aadconnect.md)。

Windows PowerShell 也可以使用的 tooautomate 加入新使用者 tooAzure AD 並 toosynchronize 變更從 hello 在內部部署目錄。 toouse hello Windows PowerShell cmdlet，您必須下載 hello [Azure Active Directory 模組](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0)。

此程序示範如何 tooadd 單一使用者 tooAzure AD。


1. 連接 Azure AD 目錄租用戶系統管理員身分 tooyour： 連接 Connect-msolservice。
2.  建立新的使用者主體：` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

如需「New-MsolUser」的詳細資訊，請參閱 [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>hello"UserPrinciplName"值必須符合您將會傳送為"IDPEmail"hello"ImmutableID"值必須符合您"NameID"宣告中傳送的 hello 值和 SAML 2.0 宣告中的 hello 值。

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>使用 SAML 2.0 IDP 驗證單一登入
Hello 系統管理員，您驗證及管理單一登入 （也稱為身分識別同盟） 之前，檢閱 hello 資訊，在下列單一登入與 SAML 2.0 Sp-lite 型身分識別提供者的發行項 tooset hello 執行 hello 步驟：


1.  您已檢閱 hello Azure AD SAML 2.0 通訊協定需求
2.  您已設定 SAML 2.0 識別提供者
3.  安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行單一登入
4.  設定 SAML 2.0 識別提供者與 Azure AD 的信任關係
5.  透過 Windows PowerShell 或 Azure AD Connect 使用者佈建已知的測試使用者主體 tooAzure Active Directory (Office 365)。
6.  使用 [Azure AD Connect](active-directory-aadconnect.md) 來設定目錄同步作業。

在設定了使用 SAML 2.0 SP-Lite 型識別提供者來進行的單一登入後，您應該確認它是否能正常運作。

>[!NOTE]
>如果您轉換網域，而非新增網域，就會在 too24 小時 tooset 單一登入。
在驗證單一登入之前，請先完成 Active Directory 同步作業的設定、對目錄進行同步處理，並啟用已同步處理的使用者。

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>單一登入使用 hello 工具 tooverify 已正確設定
tooverify 單一登入已正確設定，您可以執行下列程序 tooconfirm 您利用公司認證所能 toosign toohello 雲端服務中的 hello。

Microsoft 已提供一種工具，您可以使用 tootest SAML 2.0 型身分識別提供者。 執行 hello 之前測試工具，您必須設定 Azure AD 租用戶 toofederate 與您的身分識別提供者。

>[!NOTE]
>hello Connectivity Analyzer 需要 Internet Explorer 10 或更新版本。



1. 下載 hello Connectivity Analyzer， [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client)。
2.  按一下 立即安裝 toobegin 下載及安裝 hello 工具。
3.  選取 [我無法設定與 Office 365、Azure 或其他使用 Azure Active Directory 之服務的同盟]。
4.  一旦 hello 工具下載及執行，您會看到 hello 連線診斷 視窗。 hello 工具會逐步完成同盟連線的測試。
5.  hello Connectivity Analyzer 會開啟您 SAML 2.0 IDP 以供您 toologon，輸入您要測試的 hello 使用者主體 hello 認證： ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  在 hello 同盟測試登入視窗應該會與您的 SAML 2.0 身分識別提供者同盟設定的 toobe hello Azure AD 租用戶輸入帳戶名稱和密碼。 hello 工具會嘗試 toosign 中使用這些認證，而且 hello 登入嘗試期間執行之測試的詳細的結果將會提供做為輸出。
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. 此視窗顯示失敗的測試結果。 按一下 檢閱詳細的結果將會顯示針對每個已執行的測試 hello 結果的相關資訊。 您也可以儲存 hello 結果 toodisk 中順序 tooshare 它們。
 
>[!NOTE]
>hello Connectivity analyzer 還會測試作用中的同盟，使用 hello WS *-型和 ECP/PAOS 通訊協定。 如果您不使用這些可以忽略下列錯誤 hello： 測試 hello 作用中登入流程使用身分識別提供者的作用中同盟端點。

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>手動驗證系統是否已正確設定單一登入
手動驗證提供額外的步驟，您可在許多情況下您的 SAML 2.0 身分識別提供者正常運作的 tooensure。
單一登入的 tooverify 是否已正確設定，請完成 hello 下列步驟：


1. 已加入網域的電腦上，登入 tooyour 雲端服務使用的 hello 相同登入您的公司認證所使用的名稱。
2.  Hello 密碼方塊內按一下。 如果單一登入設定，hello 密碼方塊將呈陰影狀，而且您會看到下列訊息的 hello: 「 您已在中的必要的 toosign <your company>。 」
3.  按一下 hello 登入<your company>連結。 如果您不能 toosign 中的，然後單一登入具有已設定。

## <a name="next-steps"></a>後續步驟


- [使用 Azure AD Connect 管理和自訂 Active Directory Federation Services](active-directory-aadconnect-federation-management.md)
- [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)
- [Azure AD Connect 自訂安裝](active-directory-aadconnect-get-started-custom.md)
