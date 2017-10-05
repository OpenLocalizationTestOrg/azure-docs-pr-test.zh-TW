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
ms.openlocfilehash: 048697f87383662506fb851bb3ea510c2cddf043
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>使用 SAML 2.0 識別提供者 (IdP) 來進行單一登入

本主題所含的資訊是關於使用 SAML 2.0 相容 SP-Lite 設定檔型識別提供者來作為慣用的 Security Token Service (STS)/識別提供者。 在已有內部部署的使用者目錄和密碼存放區並可使用 SAML 2.0 來加以存取時，這種做法非常實用。 您可以使用這個現有的使用者目錄來登入 Office 365 和其他受到 Azure AD 保護的資源。 SAML 2.0 SP-Lite 設定檔是以廣為使用的安全性聲明標記語言 (SAML) 同盟身分識別標準作為基礎，以提供登入和屬性交換架構。

>[!NOTE]
>如需已通過測試可與 Azure AD 搭配使用的第 3 方 Idp 清單，請參閱 [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)

Microsoft 藉由整合 Microsoft 雲端服務 (例如 Office 365) 和您已正確設定的 SAML 2.0 設定檔型 IdP，來支援此登入體驗。 SAML 2.0 識別提供者是第三方產品，因此 Microsoft 不支援與這些識別提供者有關的部署、設定和疑難排解最佳做法。 與 SAML 2.0 識別提供者的整合在完成適當設定後，您可以使用 Microsoft 連線分析程式工具對整合結果進行測試，以了解所做的設定是否適當，詳情請見下面說明。 如需 SAML 2.0 SP-Lite 設定檔型識別提供者的詳細資訊，請向提供此識別提供者的組織詢問。

>[!IMPORTANT]
>在此登入案例中，只有一小部分的用戶端可與 SAML 2.0 識別提供者搭配使用，這些用戶端包括：

>- Web 型用戶端，例如 Outlook Web Access 和 SharePoint Online
- 豐富型電子郵件用戶端，其使用基本驗證和受支援的 Exchange 存取方法 (例如 IMAP、POP、Active Sync、MAPI 等) (必須有增強型用戶端通訊協定端點才能部署)，這些用戶端包括：
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016、Apple iPhone (各種 iOS 版本)
    - 各種 Google Android 裝置
    - Windows Phone 7、Windows Phone 7.8 及 Windows Phone 8.0
    - Windows 8 郵件用戶端和 Windows 8.1 郵件用戶端
    - Windows 10 郵件用戶端

在此登入案例中，其他所有用戶端則無法與 SAML 2.0 識別提供者搭配使用。 例如，若服務的設定是使用 SAML 2.0 識別提供者來進行單一登入，則 Lync 2010 桌面用戶端則無法登入該服務。

## <a name="azure-ad-saml-20-protocol-requirements"></a>Azure AD SAML 2.0 通訊協定需求
本主題會詳述為了與 Azure AD 同盟以便能夠登入一或多個 Microsoft 雲端服務 (例如 Office 365)，您的 SAML 2.0 識別提供者所必須實作之通訊協定和訊息格式的需求。 此案例所使用之 Microsoft 雲端服務的 SAML 2.0 信賴憑證者 (SP-STS) 是 Azure AD。

建議您務必要讓 SAML 2.0 識別提供者的輸出訊息盡可能地與所提供的追蹤範例類似。 此外，如有可能，也請使用來自所提供之 Azure AD 中繼資料的特定屬性值。 在對輸出訊息感到滿意後，您可以使用 Microsoft 連線分析程式來進行測試，方法如下所述。

您可以從此 URL 下載 Azure AD 中繼資料：[https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml)。
若您是使用中國專屬 Office 365 執行個體的中國客戶，則請使用下列同盟端點：[https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml)。

## <a name="saml-protocol-requirements"></a>SAML 通訊協定需求
本節詳述如何將要求和回應訊息成對放在一起，以協助您正確地設定訊息格式。

您可以對 Azure AD 進行設定，讓 Azure AD 與使用 SAML 2.0 SP Lite 設定檔 (具有如下所示的某些特定需求) 的識別提供者搭配運作。 透過使用 SAML 要求和回應訊息範例以及自動和手動的測試，您就可以實現與 Azure AD 的互通性。

## <a name="signature-block-requirements"></a>簽章區塊需求
在 SAML 回應訊息內，簽章節點含有訊息本身的數位簽章相關資訊。 簽章區塊具有下列需求︰

1. 判斷提示節點本身必須經過簽署
2.  必須使用 RSA-sha1 演算法來作為 DigestMethod。 不接受其他數位簽章演算法。
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  您也可以簽署 XML 文件。 
4.  Transform Algorithm 必須符合下列範例中的值：`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  SignatureMethod Algorithm 必須符合下列範例：`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>支援的繫結
繫結就是所需的傳輸相關通訊參數。 下列需求適用於繫結

1. HTTPS 是必要的傳輸。
2.  在登入期間，Azure AD 需要 HTTP POST 以便提交權杖
3.  Azure AD 會對識別提供者的驗證要求使用 HTTP POST，並對識別提供者的登出訊息使用 REDIRECT。

## <a name="required-attributes"></a>必要的屬性
下表顯示 SAML 2.0 訊息中特定屬性的需求。
 
|屬性|說明|
| ----- | ----- |
|NameID|這個判斷提示的值必須與 Azure AD 使用者的 ImmutableID 相同。 此值最多可以有 64 個英數字元。 若為非 HTML 安全字元就必須編碼，例如，"+" 字元將會顯示為 ".2B"。|
|IDPEmail|在 SAML 回應中，使用者主體名稱 (UPN) 會列示為名稱是 IDPEmail 的項目。這是使用者在 Azure AD/Office 365 中的 UserPrincipalName (UPN)。 此 UPN 會使用電子郵件地址格式。 Windows Office 365 (Azure Active Directory) 中的 UPN 值。|
|簽發者|需要有此屬性來作為識別提供者的 URI。 請勿重複使用訊息範例中的 Issuer 屬性。 如果您的 Azure AD 租用戶有多個頂層網域，Issuer 必須符合針對每個網域所設定的指定 URI 設定。|

>[!IMPORTANT]
>針對 SAML 2.0，Azure AD 目前支援下列 NameID 格式的 URI：urn:oasis:names:tc:SAML:2.0:nameid-format:persistent。

## <a name="sample-saml-request-and-response-messages"></a>SAML 要求和回應訊息範例
下面顯示了一對用來交換登入訊息的要求和回應訊息。
這個要求訊息範例會從 Azure AD 傳送到 SAML 2.0 識別提供者範例。 SAML 2.0 識別提供者範例是設定為使用 SAML-P 通訊協定的 Active Directory 同盟服務 (AD FS)。 此範例也已經對其他 SAML 2.0 識別提供者完成互通性測試。

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

這個回應訊息範例會從 SAML 2.0 相容識別提供者範例傳送到 Azure AD/Office 365。

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
本主題含有相關指導方針，可指出該如何設定 SAML 2.0 識別提供者，讓它與 Azure AD 建立同盟關係，以便能夠使用 SAML 2.0 通訊協定，以單一登入的方式存取一或多個 Microsoft 雲端服務 (例如 Office 365)。 此案例所使用之 Microsoft 雲端服務的 SAML 2.0 信賴憑證者是 Azure AD。

## <a name="add-azure-ad-metadata"></a>新增 Azure AD 中繼資料
您的 SAML 2.0 識別提供者需要遵守 Azure AD 信賴憑證者的相關資訊。 Azure AD 會在 https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml 發佈中繼資料。

當您在設定 SAML 2.0 識別提供者時，建議您一律匯入最新的 Azure AD 中繼資料。 請注意，Azure AD 不會從識別提供者讀取中繼資料。

## <a name="add-azure-ad-as-a-relying-party"></a>將 Azure AD 新增為信賴憑證者
您必須讓 SAML 2.0 識別提供者能夠與 Azure AD 通訊。 這項設定會根據您使用的特定識別提供者而有所不同，因此請參閱其相關文件。 一般來說，您會將信賴憑證者識別碼設定為和來自 Azure AD 中繼資料的 entityID 相同。

>[!NOTE]
>請確認 SAML 2.0 識別提供者伺服器上的時鐘已和正確的時間來源同步。 時鐘時間不正確將可能導致同盟登入失敗。

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行登入
在設定了 SAML 2.0 識別提供者以便用於 Azure AD 登入之後，下一步是下載並安裝適用於 Windows PowerShell 的 Azure Active Directory 模組。 安裝完成後，您將會使用這些 Cmdlet 來將 Azure AD 網域設定為同盟網域。

適用於 Windows PowerShell 的 Azure Active Directory 模組可供下載以便管理組織在 Azure AD 中的資料。 此模組會在 Windows PowerShell 中安裝一組 Cmdlet；您必須執行這些 Cmdlet 來設定 Azure AD 的單一登入存取權，進而設定您所訂閱之所有雲端服務的單一登入存取權。 如需有關如何下載及安裝 Cmdlet 的指示，請參閱 [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>設定 SAML 識別提供者與 Azure AD 的信任關係
在 Azure AD 網域中設定同盟之前，您必須先設定自訂網域。 您無法為 Microsoft 所提供的預設網域建立同盟關係。 Microsoft 的預設網域會以 "onmicrosoft.com" 結尾。
您將會在 Windows PowerShell 命令列介面中執行一系列的 Cmdlet，以新增或轉換用於進行單一登入的網域。

每個您想要使用 SAML 2.0 識別提供者來建立同盟的 Azure Active Directory 網域，都必須新增為單一登入網域，或從標準網域轉換為單一登入網域。 新增或轉換網域會設定 SAML 2.0 識別提供者和 Azure AD 之間的信任關係。

下列程序可逐步引導您將現有的標準網域轉換為使用 SAML 2.0 SP-Lite 的同盟網域。 請注意，在您執行此步驟之後，您的網域可能會發生中斷從而影響使用者，時間可能長達 2 小時。

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>在 Azure AD 目錄中設定用於同盟的網域


1. 以租用戶管理員的身分連線到您的 Azure AD 目錄：Connect-MsolService。
2.  設定要用來搭配使用同盟功能和 SAML 2.0 的 Office 365 網域：`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  您可以從 IDP 中繼資料檔案取得簽署憑證的 base64 編碼字串。 我們提供了此位置的範例，但此範例可能會隨您的實作方式而略有不同。

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

如需「Set-msoldomainauthentication」的詳細資訊，請參閱：[http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx)。

>[!NOTE]
>只有在已經為識別提供者設定了 ECP 擴充功能時，才必須執行使用「$ecpUrl = "https://WS2012R2-0.contoso.com/PAOS"」。 Exchange Online 用戶端 (Outlook Web App (OWA) 除外) 仰賴以 POST 為基礎的作用中端點。 如果您的 SAML 2.0 STS 所實作的作用中端點，類似於 Shibboleth 以 ECP 實作的作用中端點，則這些豐富型用戶端可能可以和 Exchange Online 服務互動。

設定好同盟之後，您可以切換回「非同盟」(或「受管理」) 模式，不過，系統最多需要兩個小時才能完成這項變更，而且您必須對每位使用者指派新的隨機密碼以便用於雲端式登入。 在某些情況下，您可能需要切換回「受管理」模式，以將設定中的錯誤重設。 如需網域轉換的詳細資訊，請參閱：[http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx)。

## <a name="provision-user-principals-to-azure-ad--office-365"></a>將使用者主體佈建到 Azure AD/Office 365
您必須先以使用者主體 (對應到 SAML 2.0 宣告中的判斷提示) 佈建 Azure AD，然後才能向 Office 365 驗證您的使用者。 如果 Azure AD 事先不知道這些使用者主體，您就無法使用這些主體來進行同盟登入。 Azure AD Connect 或 Windows PowerShell 均可用來佈建使用者主體。

您可以使用 Azure AD Connect 將主體從內部部署 Active Directory 佈建到您在 Azure AD 目錄中的網域。 如需詳細資訊，請參閱[整合您的內部部署目錄與 Azure Active Directory](active-directory-aadconnect.md)。

您也可以使用 Windows PowerShell 來自動將新的使用者新增至 Azure AD，並從內部部署目錄同步處理變更。 若要使用 Windows PowerShell Cmdlet，您必須下載 [Azure Active Directory 模組](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0)。

此程序示範如何將單一使用者新增至 Azure AD。


1. 以租用戶管理員的身分連線到您的 Azure AD 目錄：Connect-MsolService。
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
>「UserPrinciplName」值必須符合您會為 SAML 2.0 宣告中的「IDPEmail」傳送的值，而「ImmutableID」值則必須符合「NameID」判斷提示中所傳送的值。

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>使用 SAML 2.0 IDP 驗證單一登入
若您是系統管理員，請在驗證和管理單一登入 (也稱為身分識別同盟) 之前，先檢閱相關資訊並執行下列文章中的步驟，以設定使用 SAML 2.0 SP-Lite 型識別提供者來進行的單一登入：


1.  您已檢閱 Azure AD SAML 2.0 通訊協定需求
2.  您已設定 SAML 2.0 識別提供者
3.  安裝 Windows PowerShell 以使用 SAML 2.0 識別提供者來進行單一登入
4.  設定 SAML 2.0 識別提供者與 Azure AD 的信任關係
5.  透過 Windows PowerShell 或 Azure AD Connect 將已知的測試使用者主體佈建到 Azure Active Directory (Office 365)。
6.  使用 [Azure AD Connect](active-directory-aadconnect.md) 來設定目錄同步作業。

在設定了使用 SAML 2.0 SP-Lite 型識別提供者來進行的單一登入後，您應該確認它是否能正常運作。

>[!NOTE]
>如果您轉換網域而非新增網域，系統最多可能需要 24 小時才能設定好單一登入。
在驗證單一登入之前，請先完成 Active Directory 同步作業的設定、對目錄進行同步處理，並啟用已同步處理的使用者。

### <a name="use-the-tool-to-verify-that-single-sign-on-has-been-set-up-correctly"></a>使用工具來驗證系統是否已正確設定單一登入
若要驗證系統是否已正確設定單一登入，您可以執行下列程序來確認您能夠使用公司認證來登入雲端服務。

Microsoft 已提供一項工具供您用來測試 SAML 2.0 型識別提供者。 在執行這項測試工具之前，您必須已將 Azure AD 租用戶設定為與您的識別提供者建立同盟。

>[!NOTE]
>連線分析程式需要使用 Internet Explorer 10 或更新版本。



1. 請從 [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client) 下載連線分析程式。
2.  按一下 [立即安裝] 以開始下載及安裝此工具。
3.  選取 [我無法設定與 Office 365、Azure 或其他使用 Azure Active Directory 之服務的同盟]。
4.  工具開始下載並執行後，您會看到 [連線診斷] 視窗。 此工具會逐步引導您完成同盟連線的測試。
5.  連線分析程式會開啟您的 SAML 2.0 IDP 以供您登入，請輸入您要測試之使用者主體的認證：![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  請在 [同盟測試登入] 視窗中，輸入所設定來與 SAML 2.0 識別提供者同盟之 Azure AD 租用戶的帳戶名稱和密碼。 此工具會嘗試使用這些認證來進行登入，而系統則會在輸出中提供登入嘗試期間所執行之測試的詳細結果。
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. 此視窗顯示失敗的測試結果。 按一下 [檢閱詳細結果] 將會顯示所執行之每項測試結果的相關資訊。 您也可以將結果儲存至磁碟中以便共用。
 
>[!NOTE]
>連線分析程式也會使用 WS* 型通訊協定和 ECP/PAOS 通訊協定來測試作用中的同盟。 如果您沒有使用這些通訊協定，則可以忽略下列錯誤：使用識別提供者的作用中同盟端點來測試作用中登入流程。

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>手動驗證系統是否已正確設定單一登入
手動驗證提供了額外的步驟供您執行，以確保您的 SAML 2.0 識別提供者在許多情況下皆可正常運作。
若要驗證系統是否已正確設定單一登入，請完成下列步驟：


1. 在已加入網域的電腦上，使用和您用於公司認證相同的登入名稱來登入雲端服務。
2.  在密碼方塊內按一下。 如果您已設定單一登入，密碼方塊將呈陰影狀，而且您會看到下列訊息：「您現在必須在 <your company> 登入。」
3.  在 <your company> 連結按一下 [登入]。 如果您能夠登入，則表示您已設定好單一登入。

## <a name="next-steps"></a>後續步驟


- [使用 Azure AD Connect 管理和自訂 Active Directory Federation Services](active-directory-aadconnect-federation-management.md)
- [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)
- [Azure AD Connect 自訂安裝](active-directory-aadconnect-get-started-custom.md)
