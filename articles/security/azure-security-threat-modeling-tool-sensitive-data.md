---
title: "aaaSensitive 資料-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>安全性架構︰敏感性資料 | 風險降低 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **電腦信任邊界** | <ul><li>[確定包含敏感性資訊的二進位檔已經過模糊處理](#binaries-info)</li><li>[請考慮使用加密檔案系統 (EFS) 是使用的 tooprotect 機密使用者特定的資料](#efs-user)</li><li>[請確定 hello hello 檔案系統上的應用程式所儲存的敏感性資料已加密](#filesystem)</li></ul> | 
| **Web 應用程式** | <ul><li>[確保機密內容不會在 hello 瀏覽器上快取](#cache-browser)</li><li>[加密包含敏感性資料的 Web 應用程式組態檔區段](#encrypt-data)</li><li>[明確停用機密的表單和輸入中的 hello 自動完成 HTML 屬性](#autocomplete-input)</li><li>[請確定 hello 使用者螢幕上顯示的敏感性資料加上遮罩](#data-mask)</li></ul> | 
| **資料庫** | <ul><li>[實作動態資料遮罩 toolimit 機密資料暴露非特殊權限的使用者](#dynamic-users)</li><li>[確定密碼是以 salted 雜湊格式儲存](#salted-hash)</li><li>[確定資料庫資料行中的敏感性資料已加密](#db-encrypted)</li><li>[確定已啟用資料庫層級加密 (TDE)](#tde-enabled)</li><li>[確定資料庫備份已加密](#backup)</li></ul> | 
| **Web API** | <ul><li>[請確定該應用程式開發介面不會在瀏覽器的儲存體中儲存的敏感性資料相關 tooWeb](#api-browser)</li></ul> | 
| Azure Document DB | <ul><li>[將儲存在 DocumentDB 中的敏感性資料加密](#encrypt-docdb)</li></ul> | 
| **Azure IaaS VM 信任邊界** | <ul><li>[使用 Azure 磁碟加密 tooencrypt 磁碟的虛擬機器使用](#disk-vm)</li></ul> | 
| **Service Fabric 信任邊界** | <ul><li>[將 Service Fabric 應用程式中的密碼加密](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[執行安全性模型化並視需要使用業務單位/團隊](#modeling-teams)</li><li>[最小化在重要的實體存取 tooshare 功能](#entities)</li><li>[定型使用者 hello hello Dynamics CRM 共用功能及良好的安全性做法的相關的風險](#good-practices)</li><li>[包含開發標準規則來禁止在例外狀況管理中顯示組態詳細資料](#exception-mgmt)</li></ul> | 
| **Azure 儲存體** | <ul><li>[針對待用資料使用 Azure 儲存體服務加密 (SSE) (預覽)](#sse-preview)</li><li>[使用 Azure 儲存體中的用戶端加密 toostore 機密資料](#client-storage)</li></ul> | 
| **行動用戶端** | <ul><li>[加密敏感或 PII 資料寫入 toophones 本機儲存體](#pii-phones)</li><li>[模糊化散發 tooend 使用者之前產生的二進位檔](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[設定 clientCredentialType tooCertificate 或視窗](#cert)</li><li>[未啟用 WCF 安全性模式](#security)</li></ul> | 

## <a id="binaries-info"></a>確定包含敏感性資訊的二進位檔已經過模糊處理

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確定包含敏感性資訊的二進位檔已經過模糊處理，例如不應反轉的商業機密、敏感性商業邏輯。 這是 toostop 反向工程的組件。 `CryptoObfuscator` 之類的工具可用於此用途。 |

## <a id="efs-user"></a>請考慮使用加密檔案系統 (EFS) 是使用的 tooprotect 機密使用者特定的資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請考慮使用加密檔案系統 (EFS) 是從與實體存取 toohello 電腦對手使用的 tooprotect 機密使用者專屬資料。 |

## <a id="filesystem"></a>請確定 hello hello 檔案系統上的應用程式所儲存的敏感性資料已加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請確定已加密 hello hello 檔案系統上的應用程式所儲存的敏感性資料 （例如，使用 DPAPI），如果無法強制執行 EFS |

## <a id="cache-browser"></a>確保機密內容不會在 hello 瀏覽器上快取

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、Web Form、MVC5、MVC6 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 瀏覽器可以儲存資訊以便進行快取和記錄歷程。 這些快取的檔案儲存在資料夾中，像是在 Internet Explorer 的 hello 案例中的 hello Temporary Internet Files 資料夾。 這些頁面會再次參考，當 hello 瀏覽器會顯示它們從其快取。 如果機密資訊會顯示的 toohello 使用者 （例如其地址、 信用卡詳細資料、 身分證號碼或使用者名稱），則這項資訊可能是儲存在瀏覽器的快取，以及透過檢查 hello 瀏覽器的快取，因此可擷取或只要按下 hello 瀏覽器的 [上一頁] 按鈕。 設定快取控制回應標頭值太 「 否-存放區 」 的所有頁面。 |

### <a name="example"></a>範例
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>範例
這可透過篩選來實作。 可使用的範例如下︰ 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>加密包含敏感性資料的 Web 應用程式組態檔區段

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [如何： 加密組態區段，在 ASP.NET 2.0 使用 DPAPI](https://msdn.microsoft.com/library/ff647398.aspx)，[指定受保護的組態提供者](https://msdn.microsoft.com/library/68ze1hb2.aspx)，[使用 Azure 金鑰保存庫 tooprotect 應用程式密碼](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **步驟** | 例如 hello Web.config 組態檔，appsettings.json 通常會使用 toohold 機密資訊，包括使用者名稱、 密碼、 資料庫連接字串，以及加密金鑰。 如果不保護這項資訊，您的應用程式是很容易遭受 tooattackers 或惡意使用者取得敏感性資訊，例如帳戶使用者名稱和密碼、 資料庫名稱和伺服器名稱。 根據 hello 部署類型 （azure/內部），加密 hello 機密使用 DPAPI 或服務，例如 Azure 金鑰保存庫的組態檔區段。 |

## <a id="autocomplete-input"></a>明確停用機密的表單和輸入中的 hello 自動完成 HTML 屬性

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [MSDN︰自動完成屬性](http://msdn.microsoft.com/library/ms533486(VS.85).aspx)、[在 HTML 中使用自動完成](http://msdn.microsoft.com/library/ms533032.aspx)[HTML 清理弱點](http://technet.microsoft.com/security/bulletin/MS10-071)、[再次自動完成？！](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) |
| **步驟** | hello 自動完成屬性會指定表單是否應該在開啟或關閉具有 「 自動完成 」。 開啟 「 自動完成 」 時，根據值的 hello 瀏覽器會自動完成值該 hello 使用者輸入之前。 比方說，當表單中輸入新名稱和密碼，hello 表單送出 hello 瀏覽器會要求是否應該儲存 hello 密碼。此後 hello 表單顯示時，hello 名稱和密碼會自動填入，或輸入 hello 名稱已完成。 本機存取的攻擊者無法從 hello 瀏覽器快取取得 hello 純文字密碼。 預設會啟用自動完成，但您必須明確地加以停用。 |

### <a name="example"></a>範例
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>請確定 hello 使用者螢幕上顯示的敏感性資料加上遮罩

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | Hello 螢幕上顯示時，應該遮罩機密資料，例如密碼、 信用卡號碼，SSN 等。 這是 tooprevent 未經授權的人員存取 hello 資料 （例如 shoulder 瀏覽密碼，檢視 SSN 使用者數目的支援人員）。 請確定這些資料元素不會以純文字顯示，並會適當地加上遮罩。 這會有 toobe 處理同時接受做為輸入 （例如，。 輸入類型 = 「 密碼 」) 以及回 hello 螢幕上顯示 (例如，顯示只 hello hello 信用卡號碼的末 4 位數字)。 |

## <a id="dynamic-users"></a>實作動態資料遮罩 toolimit 機密資料暴露非特殊權限的使用者

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Sql Azure、OnPrem |
| **屬性**              | SQL 版本 - V12、SQL 版本 - MsSQL2016 |
| **參考**              | [動態資料遮罩](https://msdn.microsoft.com/library/mt130841) |
| **步驟** | hello 動態資料遮罩的目的是 toolimit 公開機密資料，防止不應該存取 toohello 資料檢視該使用者。 動態資料遮罩並不是用 tooprevent 資料庫使用者直接連接 toohello 資料庫以及執行公開 hello 機密資料片段的全面查詢。 動態資料遮罩旨在互補 tooother 的 SQL Server 安全性功能 （稽核、 加密、 資料列層級安全性 …），並強烈建議 toouse 額外搭配這些這項功能此外在順序 toobetter 保護 hello hello 中的機密資料資料庫。 請注意，SQL Server 2016 (含) 以上版本和 Azure SQL Database 才支援此功能。 |

## <a id="salted-hash"></a>確定密碼是以 salted 雜湊格式儲存

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [使用 .NET Crypto API 的密碼雜湊](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **步驟** | 密碼不應該儲存在自訂的使用者存放區資料庫中。 應改為使用 salt 值來儲存密碼雜湊。 請確定 hello salt hello 使用者一定是唯一且前儲存 hello 密碼，以最少工作因素反覆項目計數 150,000 迴圈 tooeliminate hello 可能性破解強制套用 b crypt、 s crypt 或 PBKDF2。| 

## <a id="db-encrypted"></a>確定資料庫資料行中的敏感性資料已加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | SQL 版本 - 全部 |
| **參考**              | [加密 SQL Server 中的敏感性資料](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx)、[加密 SQL Server 中的一欄資料](https://msdn.microsoft.com/library/ms179331)、[以憑證加密](https://msdn.microsoft.com/library/ms188061) |
| **步驟** | 機密資料，例如信用卡號碼有 toobe hello 資料庫中加密。 資料可以使用資料行層級加密進行加密，或使用 hello 的加密功能的應用程式函式。 |

## <a id="tde-enabled"></a>確定已啟用資料庫層級加密 (TDE)

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [了解 SQL Server 的透明資料加密 (TDE)](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **步驟** | 透明資料加密 (TDE) 功能的 SQL server 可以協助在資料庫中加密機密資料，並保護 hello 索引鍵，則使用的 tooencrypt hello 資料使用的憑證。 這會防止 hello 索引鍵沒有任何人使用 hello 資料。 TDE 保護的資料 」 在其餘部分 」，這表示 hello 資料和記錄檔。 它提供許多的法律、 規定與方針各種產業中建立 hello 能力 toocomply。 |

## <a id="backup"></a>確定資料庫備份已加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure、OnPrem |
| **屬性**              | SQL 版本 - V12、SQL 版本 - MsSQL2014 |
| **參考**              | [SQL Database 備份加密](https://msdn.microsoft.com/library/dn449489) |
| **步驟** | SQL Server 建立備份時有 hello 能力 tooencrypt hello 資料。 藉由指定 hello 加密演算法與 hello 加密程式 （憑證或非對稱金鑰） 時建立的備份，其中可以建立加密的備份檔案。 |

## <a id="api-browser"></a>請確定該應用程式開發介面不會在瀏覽器的儲存體中儲存的敏感性資料相關 tooWeb

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | MVC 5、MVC 6 |
| **屬性**              | 識別提供者 - ADFS、識別提供者 - Azure AD |
| **參考**              | N/A  |
| **步驟** | <p>在某些實作中，瀏覽器的本機儲存體中儲存機密成品相關 tooWeb API 的驗證。 例如，Azure AD 驗證構件，像是 adal.idtoken、adal.nonce.idtoken、adal.access.token.key、adal.token.keys、adal.state.login、adal.session.state、adal.expiration.key 等。</p><p>即使在登出或瀏覽器關閉之後，仍可使用這些構件。 如果敵人取得 toothese 成品，他可以重複使用它們 tooaccess hello 受保護資源 (Api)。 請確定所有機密成品相關的 tooWeb 應用程式開發介面不會儲存在瀏覽器的儲存體。 在用戶端的儲存體無法避免的案例 （例如，單一頁面應用程式 (SPA) 運用隱含的 OpenIdConnect OAuth 流程需要在本機 toostore 存取語彙基元），與使用的儲存選項並沒有持續性。 例如，喜歡 SessionStorage tooLocalStorage。</p>| 

### <a name="example"></a>範例
hello 以下 JavaScript 程式碼片段是從本機儲存體中儲存驗證成品的自訂驗證程式庫。 請避免這類實作。 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>將儲存在 Cosmos DB 中的敏感性資料加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Document DB | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請先在應用程式層級加密敏感性資料再儲存於 DocumentDB，或將敏感性資料儲存在其他儲存體解決方案，例如 Azure 儲存體或 Azure SQL| 

## <a id="disk-vm"></a>使用 Azure 磁碟加密 tooencrypt 磁碟的虛擬機器使用

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure IaaS VM 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [使用 Azure 磁碟加密 tooencrypt 磁碟供您的虛擬機器](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **步驟** | <p>Azure 磁碟加密是目前預覽版中的新功能。 這項功能可讓您 tooencrypt hello OS 磁碟和 IaaS 虛擬機器使用的資料磁碟。 適用於 Windows、 hello 磁碟會使用業界標準的 BitLocker 加密技術來加密。 適用於 Linux，hello 磁碟會使用 hello DM Crypt 技術來加密。 這是與整合 Azure 金鑰保存庫 tooallow 您 toocontrol 和管理 hello 磁碟加密金鑰。 hello Azure 磁碟加密解決方案支援下列三個客戶加密案例的 hello:</p><ul><li>在透過客戶加密的 VHD 檔案和客戶提供的加密金鑰 (儲存於 Azure 金鑰保存庫中) 建立的新 IaaS VM 上啟用加密。</li><li>啟用新建立的 hello Azure Marketplace 的 IaaS Vm 上的加密。</li><li>在 Azure 中已執行的現有 IaaS VM 上啟用加密。</li></ul>| 

## <a id="fabric-apps"></a>將 Service Fabric 應用程式中的密碼加密

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure |
| **參考**              | [管理 Service Fabric 應用程式中的密碼](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **步驟** | 密碼可以是任何機密資訊，例如儲存體連接字串、密碼或其他不會以純文字處理的值。 服務網狀架構應用程式中使用 Azure 金鑰保存庫 toomanage 金鑰和密碼。 |

## <a id="modeling-teams"></a>執行安全性模型化並視需要使用業務單位/團隊

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 執行安全性模型化並視需要使用業務單位/團隊 |

## <a id="entities"></a>最小化在重要的實體存取 tooshare 功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 最小化在重要的實體存取 tooshare 功能 |

## <a id="good-practices"></a>定型使用者 hello hello Dynamics CRM 共用功能及良好的安全性做法的相關的風險

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 定型使用者 hello hello Dynamics CRM 共用功能及良好的安全性做法的相關的風險 |

## <a id="exception-mgmt"></a>包含開發標準規則來禁止在例外狀況管理中顯示組態詳細資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 包含開發標準規則來禁止在開發外的例外狀況管理中顯示組態詳細資料。 請在檢閱程式碼或定期檢查時對此進行測試。|

## <a id="sse-preview"></a>針對待用資料使用 Azure 儲存體服務加密 (SSE) (預覽)

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | StorageType - Blob |
| **參考**              | [待用資料的 Azure 儲存體服務加密 (預覽)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **步驟** | <p>Azure 儲存體服務加密 (SSE) 中的靜止資料可協助您保護與防衛資料 toomeet 您組織的安全性和相容性的承諾。 利用此功能，Azure 儲存體，自動將加密您的資料之前 toopersisting toostorage，並解密先前 tooretrieval。 hello 加密、 解密和金鑰管理是完全透明 toousers。 SSE 適用於僅 tooblock blob 時，分頁 blob，並附加 blob。 hello 其他類型的資料，包括資料表、 佇列和檔案，將不會加密。</p><p>加密和解密工作流程：</p><ul><li>hello 客戶上啟用加密 hello 儲存體帳戶</li><li>Hello 客戶時寫入新的資料 （PUT Blob，將區塊、 PUT Page 等） tooBlob 存放裝置。使用 256 位元 AES 加密，其中一個 hello 最強區塊密碼可用來加密每次寫入</li><li>當 hello 客戶需要 tooaccess 資料 （取得 Blob 等） 時，資料會自動解密後再傳回 toohello 使用者</li><li>如果已停用加密，已不再加密新的寫入，直到 hello 使用者來重新撰寫現有加密的資料仍會維持加密。 雖然加密啟用狀態，將會加密寫入 tooBlob 儲存體。 hello 狀態的資料不會變更與 hello 切換 啟用/停用加密 hello 儲存體帳戶的使用者</li><li>所有加密金鑰會由 Microsoft 儲存、加密及管理</li></ul><p>請注意，此時，hello hello 加密所使用的索引鍵由 Microsoft 管理。 Microsoft 一開始會產生 hello 金鑰，並管理內部 Microsoft 原則所定義的 hello 索引鍵為 hello 規則旋轉 hello 安全的儲存體。 在未來的 hello，客戶會收到 hello 能力 toomanage 自己 > 加密金鑰，並提供 Microsoft 管理的金鑰的移轉路徑 toocustomer 管理的金鑰。</p>| 

## <a id="client-storage"></a>使用 Azure 儲存體中的用戶端加密 toostore 機密資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Microsoft Azure 儲存體的用戶端加密和 Azure Key Vault 金鑰保存庫](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/)、[教學課程：在 Microsoft Azure 儲存體中使用 Azure 金鑰保存庫加密和解密 Blob](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/)、[在 Azure Blob 儲存體中使用 Azure 加密擴充功能安全地存放資料](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) |
| **步驟** | <p>hello Azure 儲存體用戶端程式庫.NET Nuget 套件的支援上傳 tooAzure 存放裝置，並下載 toohello 用戶端時解密資料之前加密用戶端應用程式內的資料。 hello 程式庫也支援儲存體帳戶金鑰管理與 Azure 金鑰保存庫的整合。 以下是用戶端加密運作方式的簡短描述：</p><ul><li>hello Azure 儲存體用戶端 SDK 產生的內容加密金鑰 (CEK)，這是一次性單次使用對稱金鑰</li><li>客戶資料是使用此 CEK 加密</li><li>hello CEK 然後再包裝 （加密） 使用 hello 金鑰的加密金鑰 (KEK)。 hello KEK 索引鍵的識別項所識別，可非對稱金鑰組或對稱金鑰，可以是本機管理或儲存在 Azure 金鑰保存庫中。 hello 儲存體用戶端本身完全不需要存取 toohello KEK。 它只叫用所提供的金鑰保存庫 hello 金鑰包裝演算法。 客戶可以選擇 toouse 包裝/解除包裝如果他們想要的索引鍵的自訂提供者</li><li>hello 加密的資料是然後上傳 toohello Azure 儲存體服務。 檢查在低層級的實作詳細資料的 hello references 區段中的 hello 連結。</li></ul>|

## <a id="pii-phones"></a>加密敏感或 PII 資料寫入 toophones 本機儲存體

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 行動用戶端 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、Xamarin  |
| **屬性**              | N/A  |
| **參考**              | [使用 Microsoft Intune 原則管理裝置上的設定和功能](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy)、[金鑰鏈貼身](https://components.xamarin.com/view/square.valet) |
| **步驟** | <p>如果 hello 應用程式寫入 （電子郵件、 電話號碼、 名字、 姓氏、 喜好設定等） 的使用者的 PII 等機密資訊-行動裝置版的檔案系統上，然後它應該加密之前寫入 toohello 本機檔案系統。 如果 hello 應用程式是企業應用程式，然後瀏覽 hello 可能會使用 Windows Intune 發行應用程式。</p>|

### <a name="example"></a>範例
Intune 可以設定下列安全性原則 toosafeguard 的機密資料： 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>範例
如果 hello 應用程式不是企業應用程式，則使用平台提供的金鑰存放區，可能會在 hello 檔案系統上執行鏈 toostore 加密金鑰，使用的密碼編譯作業。 下列程式碼片段會示範 tooaccess 從使用 xamarin 的金鑰鏈的機碼： 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>模糊化散發 tooend 使用者之前產生的二進位檔

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 行動用戶端 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [適用於 .Net 的 CryptoObfuscator](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **步驟** | 產生的二進位檔 （組件內 apk） 應該是模糊化的 toostop 反向工程的組件。工具喜歡`CryptoObfuscator`可能用於此目的。 |

## <a id="cert"></a>設定 clientCredentialType tooCertificate 或視窗

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | 透過未加密的通道使用純文字密碼的使用者名稱權杖公開 hello 密碼 tooattackers 者竊聽 hello SOAP 訊息。 使用 hello UsernameToken 的服務提供者可能會接受以純文字傳送密碼。 透過未加密的通道傳送純文字密碼，可以公開 hello 認證 tooattackers 者竊聽 hello SOAP 訊息。 | 

### <a name="example"></a>範例
hello 下列 WCF 服務提供者組態會使用 hello UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
設定 clientCredentialType tooCertificate 或視窗。 

## <a id="security"></a>未啟用 WCF 安全性模式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、.NET Framework 3 |
| **屬性**              | 安全性模式 - 傳輸、安全性模式 - 訊息 |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)、[WCF 安全性基礎概念 CoDe Magazine](http://www.codemag.com/article/0611051) |
| **步驟** | 尚未定義任何傳輸或訊息安全性。 不具傳輸的訊息或安全性 hello 完整性或 hello 訊息的機密性，無法保證的訊息傳輸的應用程式。 當 WCF 安全性繫結設定 tooNone 時，會停用傳輸和訊息安全性。 |

### <a name="example"></a>範例
hello 下列組態設定 hello 安全性模式 tooNone。 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>範例
所有服務繫結的安全性模式有五個可能選項︰ 
* 無。 關閉安全性。 
* 傳輸。 使用傳輸安全性來互相保護驗證和訊息。 
* Message. 使用訊息安全性來互相保護驗證和訊息。 
* 兩者。 可讓您 toosupply 設定傳輸與訊息層級安全性 （只有 MSMQ 支援此）。 
* TransportWithMessageCredential。 認證會隨 hello 訊息和訊息保護和伺服器驗證都提供 hello 傳輸層級。 
* TransportCredentialOnly。 用戶端的認證會與 hello 傳輸層，並且沒有訊息保護。 使用訊息的傳輸與訊息安全性 tooprotect hello 完整性與機密性。 下列的 hello 組態會告知 hello service toouse 搭配訊息認證的傳輸安全性。
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
