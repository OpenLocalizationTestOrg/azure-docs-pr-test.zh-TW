---
title: "安全性-Microsoft 威脅模型化工具-Azure aaaCommunication |Microsoft 文件"
description: "hello 威脅模型化工具中公開的威脅防護功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>安全性架構︰通訊安全性 | 風險降低 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Azure 事件中樞** | <ul><li>[安全通訊 tooEvent 使用 SSL/TLS 的中樞](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[檢查服務帳戶的權限和 hello 自訂服務或 ASP.NET 網頁的核取尊重 CRM 的安全性](#priv-aspnet)</li></ul> |
| **Azure Data Factory** | <ul><li>[使用資料管理閘道器時連線的內部部署 SQL Server 上 tooAzure Data Factory](#sqlserver-factory)</li></ul> |
| **Identity Server** | <ul><li>[請確定所有流量 tooIdentity 伺服器透過 HTTPS 連線](#identity-https)</li></ul> |
| **Web 應用程式** | <ul><li>[驗證 X.509 憑證使用 tooauthenticate SSL、 TLS 及 DTLS 的連線](#x509-ssltls)</li><li>[在 Azure App Service 中設定自訂網域的 SSL 憑證](#ssl-appservice)</li><li>[強制所有流量 tooAzure 應用程式服務透過 HTTPS 連線](#appservice-https)</li><li>[啟用 HTTP Strict Transport Security (HSTS)](#http-hsts)</li></ul> |
| **資料庫** | <ul><li>[啟用 SQL Server 連線加密和憑證驗證](#sqlserver-validation)</li><li>[強制加密通訊 tooSQL 伺服器](#encrypted-sqlserver)</li></ul> |
| **Azure 儲存體** | <ul><li>[請確定該存放裝置是透過 HTTPS 的通訊 tooAzure](#comm-storage)</li><li>[如果無法啟用 HTTPS，則在下載 Blob 之後驗證 MD5 雜湊](#md5-https)</li><li>[使用 SMB 3.0 相容的用戶端 tooensure 傳輸中資料加密 tooAzure 檔案共用](#smb-shares)</li></ul> |
| **行動用戶端** | <ul><li>[實作憑證釘選](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[啟用 HTTPS - 安全傳輸通道](#https-transport)</li><li>[WCF： 集訊息安全性保護層級 tooEncryptAndSign](#message-protection)</li><li>[WCF： 使用最低權限帳戶 toorun WCF 服務](#least-account-wcf)</li></ul> |
| **Web API** | <ul><li>[強制所有流量 tooWeb Api 透過 HTTPS 連線](#webapi-https)</li></ul> |
| **Azure Redis 快取** | <ul><li>[請確定是透過 SSL 的 Redis 快取該通訊 tooAzure](#redis-ssl)</li></ul> |
| **IoT 現場閘道** | <ul><li>[保護裝置 tooField 閘道通訊](#device-field)</li></ul> |
| **IoT 雲端閘道** | <ul><li>[保護裝置 tooCloud 使用 SSL/TLS 的閘道通訊](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>安全通訊 tooEvent 使用 SSL/TLS 的中樞

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 事件中樞 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [事件中樞驗證和安全性模型概觀](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **步驟** | AMQP 或 HTTP 連線 tooEvent 集線器使用 SSL/TLS 的安全 |

## <a id="priv-aspnet"></a>檢查服務帳戶的權限和 hello 自訂服務或 ASP.NET 網頁的核取尊重 CRM 的安全性

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 檢查服務帳戶的權限和 hello 自訂服務或 ASP.NET 網頁的核取尊重 CRM 的安全性 |

## <a id="sqlserver-factory"></a>使用資料管理閘道器時連線的內部部署 SQL Server 上 tooAzure Data Factory

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Data Factory | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 連結服務類型 - Azure 和內部部署 |
| **參考**              |[在內部部署與 Azure Data Factory 之間移動資料](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway)、[資料管理閘道](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **步驟** | <p>hello 資料管理閘道 (DMG) 工具是必要的 tooconnect toodata 來源公司網路或防火牆的後面。</p><ol><li>Hello 機器鎖定會隔離 hello DMG 工具，並防止故障程式損壞或窺探 hello 資料來源電腦上。 (例如， 必須安裝最新的更新，啟用最低需求連接埠、受控制的帳戶佈建、啟用稽核、啟用磁碟加密等。)</li><li>頻繁的間隔，或每當 hello DMG 服務帳戶密碼更新，必須要旋轉資料閘道器金鑰</li><li>必須加密透過連結服務傳輸的資料</li></ol> |

## <a id="identity-https"></a>請確定所有流量 tooIdentity 伺服器透過 HTTPS 連線

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [IdentityServer3 - 金鑰、簽章和密碼編譯](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html)、[IdentityServer3 - 部署](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **步驟** | 根據預設，IdentityServer 會要求所有的連入連線 toocome 透過 HTTPS。 與 IdentityServer 的通訊絕對必須只透過安全的傳輸來進行。 某些部署案例 (例如 SSL 卸載) 可以放寬這項需求。 請參閱 hello 識別伺服器部署 頁面 hello 參考，如需詳細資訊。 |

## <a id="x509-ssltls"></a>驗證 X.509 憑證使用 tooauthenticate SSL、 TLS 及 DTLS 的連線

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>使用 SSL、 TLS 或 DTLS 的應用程式必須完全確認 hello X.509 憑證的 hello 所連接的實體。 這包括 hello 憑證的驗證：</p><ul><li>網域名稱</li><li>有效日期 (開始日期和到期日期)</li><li>撤銷狀態</li><li>使用方式 (例如，伺服器使用伺服器驗證、用戶端使用用戶端驗證)</li><li>信任鏈結。 憑證必須鏈結 tooa 根憑證授權單位 (CA) 信任 hello 平台或 hello 系統管理員明確地設定</li><li>憑證的公開金鑰長度必須 > 2048 位元</li><li>雜湊演算法必須是 SHA256 或以上版本 |

## <a id="ssl-appservice"></a>在 Azure App Service 中設定自訂網域的 SSL 憑證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | EnvironmentType - Azure |
| **參考**              | [針對 Azure App Service 中的 App 啟用 HTTPS](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **步驟** | 根據預設，Azure 已啟用 HTTPS 的 hello 的萬用字元憑證每一個應用程式 *。 azurewebsites.net 網域。 但是，就像所有萬用字元網域一樣，這並不如使用自訂網域搭配自己的憑證那麼安全。[參閱](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/)。 建議 tooenable SSL hello 哪一個部署的 hello 應用程式會透過存取的自訂網域|

## <a id="appservice-https"></a>強制所有流量 tooAzure 應用程式服務透過 HTTPS 連線

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | EnvironmentType - Azure |
| **參考**              | [對 Azure App Service 強制使用 HTTPS]https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **步驟** | <p>雖然 Azure hello 網域的萬用憑證與 Azure 應用程式服務已經啟用 HTTPS *。 名稱是.azurewebsites.net，它不會強制進行 HTTPS。 訪客可能仍然會存取 hello 應用程式使用 HTTP，可能會危及 hello 應用程式的安全性，且因此 HTTPS toobe 明確強制執行。 ASP.NET MVC 應用程式應該使用 hello [RequireHttps 篩選](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)，會強制透過 HTTPS 重新傳送不安全的 HTTP 要求 toobe。</p><p>或者，hello URL Rewrite 模組，其隨附於 Azure 應用程式服務可以使用的 tooenforce HTTPS。 URL Rewrite 模組可讓開發人員 toodefine 規則 hello 要求散發 tooyour 應用程式之前，所套用的 tooincoming 要求。 存放在 hello hello 應用程式根目錄的 web.config 檔案中定義 URL 重寫規則</p>|

### <a name="example"></a>範例
hello 下列範例包含基本的 URL 重寫規則，會強制所有連入流量 toouse HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
此規則的運作方式是傳回 HTTP 狀態碼 301 （永久重新導向） 當 hello 使用者要求使用 HTTP 的網頁。 hello 301 重新導向 hello 要求 toohello hello 訪客相同的 URL 要求，但 hello 要求使用 HTTPS 來取代 hello HTTP 部分。 例如，HTTP://contoso.com 會重新導向的 tooHTTPS://contoso.com。 

## <a id="http-hsts"></a>啟用 HTTP Strict Transport Security (HSTS)

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [OWASP HTTP Strict Transport Security 功能提要](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **步驟** | <p>HTTP 嚴格的傳輸安全性 (HSTS) 是透過 hello 使用特殊的回應標頭的 web 應用程式所指定的選擇加入的安全性增強功能。 一旦支援的瀏覽器接收此標頭該瀏覽器會防止任何從透過 HTTP toohello 指定網域所傳送的通訊，而會改為傳送透過 HTTPS 的所有通訊。 它也可以防止瀏覽器上出現 HTTPS 點選提示。</p><p>tooimplement HSTS，遵循回應標頭的 hello 有 toobe 網站的全域設定，在程式碼或組態中。Strict 傳輸安全性： 最大 age = 300。includeSubDomains HSTS 解決下列潛在威脅的 hello:</p><ul><li>使用者設定為書籤或手動輸入 http://example.com，然後是主體 tooa 攔截攻擊者： HSTS 將自動重新導向 hello 目標網域的 HTTP 要求 tooHTTPS</li><li>Web 應用程式所預期的 toobe 純粹 HTTPS 不小心包含 HTTP 連結，或透過 HTTP 提供內容： HSTS 將自動重新導向 hello 目標網域的 HTTP 要求 tooHTTPS</li><li>攔截攻擊者嘗試 toointercept 流量犧牲者使用者使用了無效的憑證，並且希望 hello 使用者將會接受 hello 不正確的憑證： HSTS 不允許使用者 toooverride hello 無效的憑證訊息</li></ul>|

## <a id="sqlserver-validation"></a>啟用 SQL Server 連線加密和憑證驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure  |
| **屬性**              | SQL 版本 - V12 |
| **參考**              | [為 SQL Database 撰寫安全連接字串的最佳作法](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **步驟** | <p>SQL Database 和用戶端應用程式之間的所有通訊永遠都會使用安全通訊端層 (SSL) 來加密。 SQL Database 不支援未加密連線。 toovalidate 憑證與應用程式程式碼或工具，明確地要求加密的連接，並不信任 hello 伺服器憑證。 即使您的應用程式程式碼或工具未要求加密連線，它們仍然會接收加密的連線</p><p>不過，可能不會驗證 hello 伺服器憑證，因此可能受到太 「 攔截 hello 中間 」 攻擊。 使用 ADO.NET 應用程式程式碼，toovalidate 憑證設定`Encrypt=True`和`TrustServerCertificate=False`hello 資料庫連接字串中。 toovalidate 憑證，透過 SQL Server Management Studio，開啟 hello 連接 tooServer 對話方塊。 按一下 hello 連接屬性 索引標籤上的加密連接</p>|

## <a id="encrypted-sqlserver"></a>強制加密通訊 tooSQL 伺服器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | OnPrem |
| **屬性**              | SQL 版本 - MsSQL2016、SQL 版本 - MsSQL2012、SQL 版本 - MsSQL2014 |
| **參考**              | [啟用加密連接 toohello Database Engine](https://msdn.microsoft.com/library/ms191192)  |
| **步驟** | 啟用 SSL 加密可提高 hello 安全性的 SQL Server 執行個體和應用程式之間透過網路傳輸的資料。 |

## <a id="comm-storage"></a>請確定該存放裝置是透過 HTTPS 的通訊 tooAzure

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Azure 儲存體傳輸層級加密 – 使用 HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **步驟** | tooensure hello 安全性的 Azure 儲存體的資料傳輸中，在呼叫 hello REST Api 或存取物件的儲存體中時，一律會使用 hello HTTPS 通訊協定。 此外，共用存取簽章，可使用的 toodelegate 存取 tooAzure 儲存物件，包含選項 toospecify 時使用共用存取簽章，確保送出連結使用 SAS 權杖的任何人將可以使用 HTTPS 通訊協定，只有 hello使用 hello 適當的通訊協定。|

## <a id="md5-https"></a>如果無法啟用 HTTPS，則在下載 Blob 之後驗證 MD5 雜湊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | StorageType - Blob |
| **參考**              | [Windows Azure Blob MD5 概觀](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **步驟** | <p>Windows Azure Blob 服務會提供在 hello 應用程式和傳輸層機制 tooensure 資料完整性。 如果因故需要的 toouse HTTP 而非 HTTPS 與您正在使用區塊 blob，您可以使用 MD5 檢查 toohelp 驗證傳送嗨 blob hello 完整性</p><p>這有助於提供保護以防止發生網路/傳輸層錯誤，但不一定是媒介攻擊。 如果您可以使用 HTTPS 來提供傳輸層安全性，則使用 MD5 檢查是多餘且不必要的。</p>|

## <a id="smb-shares"></a>使用 SMB 3.0 相容的用戶端 tooensure 傳輸中資料加密 tooAzure 檔案共用

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 行動用戶端 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | StorageType - 檔案 |
| **參考**              | [Azure 檔案儲存體](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931)、[Windows 用戶端的 Azure 檔案儲存體 SMB 支援](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **步驟** | Azure 檔案儲存體使用 hello REST API 時，支援 HTTPS，但已為 SMB 檔案共用附加 tooa VM 更常使用。 SMB 2.1 不支援加密，因此連線之內，才允許 hello 相同 Azure 中的區域。 不過，SMB 3.0 支援加密，以及可以搭配 Windows Server 2012 R2、 Windows 8、 Windows 8.1 和 Windows 10 中，允許跨區域存取甚至 hello 桌面上的存取。 |

## <a id="cert-pinning"></a>實作憑證釘選

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、Windows Phone |
| **屬性**              | N/A  |
| **參考**              | [憑證和公開金鑰釘選](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **步驟** | <p>憑證釘選可防止攔截式 (MITM) 攻擊。 Pin 是 hello 程序主機關聯其預期的 X509 憑證或公開金鑰。 一旦憑證或公開金鑰已知或看過的主機，hello 憑證或公開金鑰是關聯或 '固定' toohello 主機。 </p><p>因此，當對手嘗試的 toodo SSL MITM 攻擊，攻擊者的伺服器中的 SSL 交握 hello 金鑰期間將會不同於 hello 釘選憑證的金鑰，且 hello 要求將會被捨棄，因此防止 MITM 憑證釘選可藉由實作 ServicePointManager 的`ServerCertificateValidationCallback`委派。</p>|

### <a name="example"></a>範例
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>啟用 HTTPS - 安全傳輸通道

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | hello 應用程式設定應該確認 HTTPS 用於存取 toosensitive 的所有資訊。<ul><li>**說明：**如果應用程式處理機密資訊，而且不會使用訊息層級加密，則它應該只允許 toocommunicate 透過加密的傳輸通道。</li><li>**建議︰**確定已停用 HTTP 傳輸，並改為啟用 HTTPS 傳輸。 例如，取代 hello`<httpTransport/>`與`<httpsTransport/>`標記。 請勿依賴網路組態 （防火牆） tooguarantee hello 應用程式只能存取透過安全通道。 從明智觀點來看，hello 應用程式不應依賴其安全性的 hello 網路。</li></ul><p>從實際的觀點，hello 人員負責保護 hello 網路不要一律追蹤 hello hello 應用程式安全性需求而進展。</p>|

## <a id="message-protection"></a>WCF： 集訊息安全性保護層級 tooEncryptAndSign

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **步驟** | <ul><li>**說明：**時保護層級設定太"none"，它會停用訊息保護。 機密性和完整性要有適當的設定層級才能實現。</li><li>**建議︰**<ul><li>當 `Mode=None` 時 - 停用訊息保護</li><li>當`Mode=Sign`-符號但不會加密 hello 訊息，是重要的資料完整性時使用</li><li>當`Mode=EncryptAndSign`-簽署並加密 hello 訊息</li></ul></li></ul><p>請考慮關閉加密，而且只能簽署訊息時，您只需要 toovalidate hello 完整性的機密性的 hello 資訊而不需擔心。 這可能是適用於作業或服務合約，您需要 toovalidate hello 原始傳送者，但沒有機密資料傳輸。 當減少 hello 保護層級，請小心該 hello 訊息未包含任何個人識別資訊 (PII)。</p>|

### <a name="example"></a>範例
設定 hello 服務及 hello 作業 tooonly 簽署 hello 訊息會顯示 hello 遵循範例。 服務合約範例`ProtectionLevel.Sign`: hello 以下是使用 ProtectionLevel.Sign hello 服務合約層級的範例： 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>範例
作業合約範例`ProtectionLevel.Sign`（適用於更細微的控制）： hello 以下是示範如何使用`ProtectionLevel.Sign`在 hello OperationContract 層級：

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF： 使用最低權限帳戶 toorun WCF 服務

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **步驟** | <ul><li>**說明︰**請勿使用系統管理員或高權限帳戶執行 WCF 服務。 萬一發生服務入侵，這會造成很大的影響。</li><li>**建議：**使用最低權限帳戶 toohost 您的 WCF 服務，因為它會減少應用程式的受攻擊面並降低 hello 可能造成的損害，如果您受到攻擊。 如果 hello 服務帳戶需要額外的存取權限，例如 MSMQ 基礎結構資源上，hello 事件記錄檔、 效能計數器，以及 hello 檔案系統中，適當的權限也應該有 toothese 資源，可以執行 hello WCF 服務已成功。</li></ul><p>如果您的服務需要 tooaccess 特定資源代表 hello 原始呼叫端，使用模擬和委派 tooflow hello 呼叫者身分識別的下游的授權檢查。 在開發案例中，使用 hello 區域網路服務帳戶，這是特殊的內建帳戶擁有較小的權限。 在生產案例中，請建立最低權限的自訂網域服務帳戶。</p>|

## <a id="webapi-https"></a>強制所有流量 tooWeb Api 透過 HTTPS 連線

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | [在 Web API 控制器中強制執行 SSL](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **步驟** | 如果某個應用程式的 HTTPS 和 HTTP 繫結，用戶端仍然可以使用 HTTP tooaccess hello 站台。 tooprevent 要求 tooprotected Api 動作篩選條件 tooensure 都透過 HTTPS，使用。|

### <a name="example"></a>範例 
hello 下列程式碼將示範會檢查有 SSL 的 Web API 驗證篩選條件： 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
加入 ssl 此篩選器 tooany Web API 的動作： 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>請確定是透過 SSL 的 Redis 快取該通訊 tooAzure

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Redis 快取 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Azure Redis SSL 支援](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **步驟** | Redis 伺服器不支援 SSL 超出 hello 方塊中，但 Azure Redis 快取。 如果您要連接 tooAzure Redis 快取，而且您的用戶端支援 SSL，例如 StackExchange.Redis，您應該使用 SSL。 新的 Azure Redis 快取執行個體已預設停用非 SSL 連接埠。 請確定 SSL 支援 redis 用戶端上沒有相依性不會變更 hello 安全的預設值。 |

請注意 Redis 是設計的 toobe 受信任的用戶端受信任的環境內存取。 這表示，通常不好想法 tooexpose hello Redis 執行直接個體 toohello 網際網路或一般情況下，不受信任的用戶端可以直接存取 tooan 環境 hello Redis 的 TCP 連接埠或 UNIX 通訊端。 

## <a id="device-field"></a>保護裝置 tooField 閘道通訊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 針對以 IP 為主的裝置，hello 通訊協定通常無法封裝在傳輸中的 SSL/TLS 通道 tooprotect 資料。 其他通訊協定不支援 SSL/TLS 調查是否有 hello 通訊協定提供傳輸或訊息層級安全性的安全版本。 |

## <a id="device-cloud"></a>保護裝置 tooCloud 使用 SSL/TLS 的閘道通訊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [選擇您的通訊協定](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **步驟** | 使用 SSL/TLS 的安全 HTTP/AMQP 或 MQTT 通訊協定。 |
