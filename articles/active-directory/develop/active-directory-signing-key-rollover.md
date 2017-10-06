---
title: "在 Azure AD 中的金鑰變換 aaaSigning |Microsoft 文件"
description: "這篇文章討論 hello Azure Active Directory 的簽署金鑰變換的最佳作法"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Azure Active Directory 中的簽署金鑰變換
本主題討論您需要 tooknow 有關 hello Azure Active Directory (Azure AD) toosign 安全性權杖中所使用的公用金鑰。 這些金鑰變換，定期執行，並在發生緊急狀況，無法回復透過立即的重要 toonote 它。 使用 Azure AD 的所有應用程式應該可以 tooprogrammatically 控制代碼 hello 金鑰變換程序或建立定期手動變換程序。 繼續閱讀 toounderstand hello 金鑰的運作，如何 tooassess hello hello 變換 tooyour 應用程式的影響以及如何 tooupdate 您的應用程式或必要時，建立定期手動變換程序 toohandle 金鑰變換。

## <a name="overview-of-signing-keys-in-azure-ad"></a>Azure AD 中簽署金鑰的概觀
Azure AD 使用公開金鑰加密中根據業界標準 tooestablish 信任本身與 hello 之間使用它的應用程式。 實際上，這適用於下列方式 hello: Azure AD 使用公開和私密金鑰的金鑰組所組成的簽署金鑰。 當使用者登入時 tooan 應用程式使用 Azure AD 進行驗證時，Azure AD 會建立包含 hello 使用者的相關資訊的安全性權杖。 這個權杖是由 Azure AD 傳送後 toohello 應用程式之前，請使用其私密金鑰簽署。 hello 語彙基元的 tooverify 有效且確實來自 Azure AD，hello 應用程式必須驗證 hello 權杖之簽章使用 hello hello 租用戶中所包含的 Azure AD 所公開的公開金鑰[OpenID Connect 探索文件](http://openid.net/specs/openid-connect-discovery-1_0.html)或 SAML/Ws-fed[同盟中繼資料文件](active-directory-federation-metadata.md)。

基於安全性考量，Azure AD 簽署金鑰彙定期執行，並在發生緊急狀況，hello 情況下無法回復立即。 任何與 Azure AD 整合的應用程式應該準備的 toohandle 金鑰變換事件無論就可能發生的頻率。 如果沒有，您的應用程式嘗試 toouse 權杖已過期的索引鍵 tooverify hello 簽章，hello 登入要求將會失敗。

很多個有效的金鑰 hello OpenID Connect 探索文件與 hello 同盟中繼資料文件中可用。 您的應用程式應該準備的 toouse hello 機碼中任何指定的 hello 文件，由於其中一個索引鍵可能會過期，所以另一個可能是一個取代，等等。

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>如何 tooassess 如果會影響您的應用程式和資訊，請參閱哪些 toodo
您的應用程式處理金鑰變換的方式取決於變數，例如 hello 類型的應用程式，或使用何種身分識別通訊協定和文件庫。 下列各節 hello 評估是否 hello 最常見的應用程式類型會受到 hello 金鑰變換並且提供指引 tooupdate hello toosupport 自動變換時，應用程式或手動更新 hello 機碼的方式。

* [存取資源的原生用戶端應用程式](#nativeclient)
* [存取資源的 Web 應用程式 / API](#webclient)
* [保護資源且使用 Azure App Service 建置的 Web 應用程式 / API](#appservices)
* [使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API](#owin)
* [使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API](#owincore)
* [使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API](#passport)
* [保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API](#vs2015)
* [保護資源且使用 Visual Studio 2013 建立的 Web 應用程式](#vs2013)
* [保護資源且使用 Visual Studio 2013 建立的 Web API](#vs2013_webapi)
* [保護資源且使用 Visual Studio 2012 建立的 Web 應用程式](#vs2012)
* [保護資源且使用 Visual Studio 2010、2008 或使用 Windows Identity Foundation 建立的 Web 應用程式](#vs2010)
* [Web 應用程式/保護資源的應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定](#other)

本指南 **不** 適用於︰

* 從 Azure AD 應用程式庫 （包括自訂） 加入的應用程式的相關事宜 toosigning 索引鍵的個別的指引。 [相關資訊。](../active-directory-sso-certs.md)
* 內部透過應用程式 proxy 發行應用程式都沒有 tooworry 有關簽署金鑰。

### <a name="nativeclient"></a>存取資源的原生用戶端應用程式
只存取資源 (亦即 Microsoft Graph、 KeyVault、 Outlook 應用程式開發介面和其他 Microsoft 應用程式開發介面） 通常只以取得權杖，並沿著傳遞 toohello 資源擁有者。 假設它們沒有保護的任何資源，它們不會檢查 hello 語彙基元，並因此不需要的 tooensure 正確地簽署。

原生用戶端應用程式，桌面或行動裝置，是否歸類到此類別，並因此不會受到 hello 換用。

### <a name="webclient"></a>存取資源的 Web 應用程式 / API
只存取資源 (亦即 Microsoft Graph、 KeyVault、 Outlook 應用程式開發介面和其他 Microsoft 應用程式開發介面） 通常只以取得權杖，並沿著傳遞 toohello 資源擁有者。 假設它們沒有保護的任何資源，它們不會檢查 hello 語彙基元，並因此不需要的 tooensure 正確地簽署。

Web 應用程式和 web 應用程式開發介面中使用 hello 僅限應用程式流程 (用戶端認證 / 用戶端憑證) 歸類到此類別，因此不會受到 hello 換用。

### <a name="appservices"></a>保護資源且使用 Azure App Service 建置的 Web 應用程式 / API
Azure 應用程式服務的驗證 / 授權 (EasyAuth) 功能已擁有 hello 必要的邏輯 toohandle 金鑰變換自動。

### <a name="owin"></a>使用 .NET OWIN OpenID Connect、WS-Fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API
如果您的應用程式正在使用 hello.NET OWIN OpenID Connect，Ws-fed 或 WindowsAzureActiveDirectoryBearerAuthentication 中介軟體，它已經 hello 必要的邏輯 toohandle 金鑰變換自動。

您可以確認您的應用程式正在使用任何這些尋找任何下列程式碼片段，在您的應用程式 Startup.cs 或 Startup.Auth.cs hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>使用 .NET Core OpenID Connect 或 JwtBearerAuthentication 中介軟體保護資源的 Web 應用程式 / API
如果您的應用程式使用.NET 核心 OWIN OpenID Connect 的 hello 或 JwtBearerAuthentication 中介軟體，它已經 hello 必要的邏輯 toohandle 金鑰變換自動。

您可以確認您的應用程式正在使用任何這些尋找任何下列程式碼片段，在您的應用程式 Startup.cs 或 Startup.Auth.cs hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>使用 Node.js passport-azure-ad 模組保護資源的 Web 應用程式 / API
如果您的應用程式使用 hello Node.js passport ad 模組，它已經有 hello 必要的邏輯 toohandle 金鑰變換自動。

您可以確認您的應用程式 passport ad 藉由搜尋下列程式碼片段，在您的應用程式 app.js hello

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>保護資源且使用 Visual Studio 2015 或 Visual Studio 2017 建立的 Web 應用程式 / API
如果使用 Visual Studio 2015 或 Visual Studio 2017 中的 web 應用程式範本建置您的應用程式，而且您選取**工作及學校帳戶**從 hello**變更驗證**功能表上，它已經會自動擁有 hello 必要的邏輯 toohandle 金鑰變換。 這個邏輯內嵌在 hello OWIN OpenID Connect 中介軟體，擷取和快取 hello hello OpenID Connect 探索文件中的索引鍵，而且會定期重新整理。

如果您手動加入驗證 tooyour 解決方案，您的應用程式可能沒有 hello 必要金鑰變換邏輯。 您將需要 toowrite 它自己，或遵循 hello 中的步驟[Web 應用程式 / 應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定。](#other)。

### <a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web 應用程式
如果使用 Visual Studio 2013 中的 web 應用程式範本建置您的應用程式，而且您選取**組織帳戶**從 hello**變更驗證**功能表上，已有 hello 必要邏輯 toohandle 自動金鑰變換。 此邏輯會儲存您的組織唯一識別碼和簽署金鑰資訊與 hello 專案相關聯的兩個資料庫資料表中的 hello。 您可以在 hello 專案的 Web.config 檔案中找到 hello 資料庫 hello 連接字串。

如果您手動加入驗證 tooyour 解決方案，您的應用程式可能沒有 hello 必要金鑰變換邏輯。 您將需要 toowrite 它自己，或遵循 hello 中的步驟[Web 應用程式 / 應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定。](#other)。

hello 下列步驟將協助您確認 hello 邏輯正常運作，您的應用程式中。

1. 在 Visual Studio 2013 中，開啟 hello 方案，然後按一下 hello**伺服器總管**hello 右側視窗上的索引標籤。
2. 依序展開 [資料連線]、[DefaultConnection]、[資料表]。 找出 hello **IssuingAuthorityKeys**資料表，以滑鼠右鍵按一下，然後按**顯示資料表資料**。
3. 在 hello **IssuingAuthorityKeys**資料表中，會有至少一個資料列，對應 toohello hello 金鑰的憑證指紋值。 刪除 hello 資料表中的任何資料列。
4. 以滑鼠右鍵按一下 hello**租用戶**資料表，然後按一下**顯示資料表資料**。
5. 在 hello**租用戶**資料表中，會有對應 tooa 唯一的目錄租用戶識別碼的至少一個資料列。 刪除 hello 資料表中的任何資料列。 如果您未刪除 hello 資料列，在這兩個 hello**租用戶**資料表和**IssuingAuthorityKeys**資料表，就會在執行階段發生錯誤。
6. 建置並執行 hello 應用程式。 您已登入 tooyour 帳戶之後，您可以停止 hello 應用程式。
7. 傳回 toohello**伺服器總管**並查看 hello 中的 hello 值**IssuingAuthorityKeys**和**租用戶**資料表。 您會發現，他們具有已自動重新擴展 hello hello 同盟中繼資料文件的適當資訊。

### <a name="vs2013"></a>保護資源且使用 Visual Studio 2013 建立的 Web API
如果您使用 hello Web API 範本時，Visual Studio 2013 中建立 web API 應用程式，然後選取**組織帳戶**從 hello**變更驗證**功能表上，您已擁有 hello必要應用程式中的邏輯。

如果您手動設定驗證，請遵循以下 toolearn hello 指示如何 tooconfigure Web API tooautomatically 更新金鑰資訊。

hello 下列程式碼片段示範如何 tooget hello hello 同盟中繼資料文件，取得最新的金鑰，然後再使用 hello [JWT 權杖處理常式](https://msdn.microsoft.com/library/dn205065.aspx)toovalidate hello 語彙基元。 hello 程式碼片段假設您將使用您自己的快取機制來保存 hello 金鑰 toovalidate 未來語彙基元從 Azure AD，無論在資料庫、 組態檔或其他位置。

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>保護資源且使用 Visual Studio 2012 建立的 Web 應用程式
如果在 Visual Studio 2012 中建置您的應用程式時，您可能使用 hello 身分識別和存取工具 tooconfigure 您的應用程式。 也很可能您使用 hello[驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx)。 hello VINR 負責維護關於信任的身分識別提供者 (Azure AD) 的資訊和 hello 金鑰用於其所發行的 toovalidate 語彙基元。 hello VINR 也很容易 tooautomatically 更新 hello 金鑰資訊儲存在 Web.config 檔案中下載 hello 最新的同盟中繼資料文件與您的目錄，檢查是否 hello 組態 hello 與最新相關聯文件和更新 hello 應用程式 toouse hello 新索引鍵為必要。

如果您建立使用 hello 程式碼範例或 Microsoft 所提供的逐步解說文任何的件應用程式，您的專案中已經包含 hello 金鑰變換邏輯。 您會發現以下的 hello 程式碼已經存在專案中。 如果您的應用程式尚無此邏輯，步驟 hello 下方 tooadd 它，它正常運作的 tooverify。

1. 在**方案總管 中**，新增參考 toohello **System.IdentityModel** hello 適當的專案的組件。
2. 開啟 hello **Global.asax.cs**檔案，然後加入 hello 下列 using 指示詞：
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. 新增下列方法 toohello hello **Global.asax.cs**檔案：
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. 叫用 hello **Refreshvalidationsettings**方法在 hello **application_start （)**方法中的**Global.asax.cs**所示：
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

一旦您已遵循下列步驟，將會 hello 最新資訊 hello 同盟中繼資料文件，包括 hello 最新的金鑰更新應用程式的 Web.config。 每次應用程式集區回收 IIS; 中，會進行更新根據預設 IIS 設定 toorecycle 應用程式每 29 小時。

請遵循以下 hello 金鑰變換邏輯運作的 tooverify hello 步驟。

1. 確認您的應用程式正在使用 hello 開啟 hello 上面的程式碼之後**Web.config**檔案，並瀏覽 toohello  **<issuerNameRegistry>** 區塊，並特別尋找下列幾行 hello:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. 在 hello  **<add thumbprint=””>** 設定，以不同的字元完全取代將 hello 指紋值。 儲存 hello **Web.config**檔案。
3. 建置 hello 應用程式，然後執行它。 如果您可以完成 hello 登入程序，您的應用程式已成功更新 hello 金鑰您目錄中的同盟中繼資料文件下載 hello 所需的資訊。 如果您有登入的問題，請確認您的應用程式中的 hello 變更是否正確讀取 hello[加入登入 tooYour Web 應用程式使用 Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)主題，或是下載並檢查下列程式碼範例的 hello: [多租用戶雲端應用程式的 Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b)。

### <a name="vs2010"></a>保護資源且使用 Visual Studio 2008 或 2010 和 Windows Identity Foundation (WIF) v1.0 for .NET 3.5 建立的 Web 應用程式
如果建置 WIF v1.0 上的應用程式時，就沒有提供的機制 tooautomatically 重新整理您的應用程式組態 toouse 新的金鑰。

* *最簡單的方式*使用 hello FedUtil 工具 hello WIF SDK，它可以擷取 hello 最新的中繼資料文件並更新您的組態中。
* 更新您的應用程式 too.NET 4.5，其中包括 hello 位於 hello 系統命名空間的 WIF 最新版本。 然後，您可以使用 hello[驗證簽發者名稱登錄 (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform hello 應用程式之組態的自動更新。
* 執行手動的換用根據 hello 指示 hello 指引文件結尾。

Toouse hello FedUtil tooupdate 您設定的指示：

1. 確認您擁有 hello WIF v1.0 SDK 開發電腦上安裝 Visual Studio 2008 或 2010年。 如果尚未安裝，您可以[從這裡下載](https://www.microsoft.com/en-us/download/details.aspx?id=4451)。
2. 在 Visual Studio 中，開啟 hello 方案然後 hello 適用的專案上按一下滑鼠右鍵並選取**更新同盟中繼資料**。 如果不使用此選項，則尚未安裝 FedUtil 和/或 hello WIF v1.0 SDK。
3. 從 hello 提示字元中，選取**更新**toobegin 更新您的同盟中繼資料。 如果您有存取 toohello 伺服器環境中裝載 hello 應用程式，您可以選擇使用 FedUtil 的[中繼資料自動更新排程器](https://msdn.microsoft.com/library/ee517272.aspx)。
4. 按一下**完成**toocomplete hello 更新程序。

### <a name="other"></a>Web 應用程式/保護資源的應用程式開發介面使用任何其他程式庫，或手動實作的 hello 任何支援的通訊協定
如果您使用其他程式庫，或手動實作的任何支援的 hello 通訊協定，您將需要 tooreview hello 文件庫或 hello 金鑰您實作 tooensure 會從 hello OpenID Connect 探索文件或 hello同盟中繼資料文件。 針對這其中一種方式 toocheck 是 toodo tooeither hello OpenID 探索文件或 hello 同盟中繼資料文件的任何呼叫您的程式碼或 hello 程式庫程式碼中的搜尋。

如果索引鍵某處儲存或硬式編碼應用程式中的，您可以手動擷取 hello 金鑰和它據以執行手動的換用根據 hello 指示在 hello 結尾此指引文件的更新。 **強烈鼓勵您加強您的應用程式 toosupport 自動變換**如果 Azure AD 會增加它的容錯移轉模式，或者使用任何 hello 接近這個發行項 tooavoid 未來中斷與額外負荷外的框緊急的頻外換用。

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>如何 tootest 會受到影響，如果您的應用程式 toodetermine
您可以驗證您的應用程式支援自動金鑰變換下載 hello 指令碼和中的 hello 指示是否[這個 GitHub 儲存機制。](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>如何 tooperform 手動變換，如果您的應用程式不支援自動變換
如果應用程式**不**支援自動變換，您將需要的處理序，定期監視 Azure AD 的簽署金鑰，並執行手動的換用 tooestablish 據以。 [此 GitHub 儲存機制](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)包含指令碼和指示 toodo 這。

