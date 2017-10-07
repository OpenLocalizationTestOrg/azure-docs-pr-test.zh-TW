---
title: "aaaAuthentication-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
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
ms.openlocfilehash: 06c1b1aebab25e6fb5b666d24ecd9d86085d656c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authentication--mitigations"></a>安全框架︰驗證 | 緩和措施 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Web 應用程式**    | <ul><li>[請考慮使用標準驗證機制 tooauthenticate tooWeb 應用程式](#standard-authn-web-app)</li><li>[應用程式必須安全地處理失敗的驗證案例](#handle-failed-authn)</li><li>[啟用升級或調適性驗證](#step-up-adaptive-authn)</li><li>[確保已適當地鎖定系統管理介面](#admin-interface-lockdown)</li><li>[安全地實作忘記密碼功能](#forgot-pword-fxn)</li><li>[確保已實作密碼和帳戶原則](#pword-account-policy)</li><li>[實作控制項 tooprevent username 列舉](#controls-username-enum)</li></ul> |
| **資料庫** | <ul><li>[可能的話，請使用 Windows 驗證來連接 tooSQL 伺服器](#win-authn-sql)</li><li>[盡可能使用 Azure Active Directory 驗證連線 tooSQL 資料庫](#aad-authn-sql)</li><li>[使用 SQL 驗證模式時，確保在 SQL Server 上強制執行帳戶和密碼原則](#authn-account-pword)</li><li>[請勿在自主資料庫中使用 SQL 驗證](#autn-contained-db)</li></ul> |
| **Azure 事件中樞** | <ul><li>[使用採用 SaS 權杖的每一裝置驗證認證](#authn-sas-tokens)</li></ul> |
| **Azure 信任邊界** | <ul><li>[啟用 Azure 系統管理員適用的 Azure Multi-Factor Authentication](#multi-factor-azure-admin)</li></ul> |
| **Service Fabric 信任邊界** | <ul><li>[限制匿名存取 tooService 網狀架構叢集](#anon-access-cluster)</li><li>[確保 Service Fabric 的用戶端對節點憑證不同於節點對節點憑證](#fabric-cn-nn)</li><li>[使用 AAD tooauthenticate 用戶端 tooservice 網狀架構叢集](#aad-client-fabric)</li><li>[確保從經過核准的憑證授權單位 (CA) 取得 Service Fabric 憑證](#fabric-cert-ca)</li></ul> |
| **Identity Server** | <ul><li>[使用 Identity Server 所支援的標準驗證案例](#standard-authn-id)</li><li>[覆寫 hello 預設身分識別伺服器權杖快取使用可擴充的替代項目](#override-token)</li></ul> |
| **電腦信任邊界** | <ul><li>[確保已數位簽署所部署應用程式的二進位檔](#binaries-signed)</li></ul> |
| **WCF** | <ul><li>[當連接 tooMSMQ WCF 中的佇列時啟用驗證](#msmq-queues)</li><li>[WCF 執行未設定郵件 clientCredentialType toonone](#message-none)</li><li>[WCF 執行未設定傳輸 clientCredentialType toonone](#transport-none)</li></ul> |
| **Web API** | <ul><li>[請確定標準驗證技術是使用的 toosecure Web 應用程式開發介面](#authn-secure-api)</li></ul> |
| **Azure AD** | <ul><li>[使用 Azure Active Directory 所支援的標準驗證案例](#authn-aad)</li><li>[覆寫 hello 預設 ADAL 權杖快取使用可擴充的替代項目](#adal-scalable)</li><li>[確保 TokenReplayCache 使用的 tooprevent hello ADAL 驗證權杖重新執行](#tokenreplaycache-adal)</li><li>[使用 ADAL 程式庫 toomanage 語彙基元要求從 OAuth2 用戶端 tooAAD （或在內部部署 AD）](#adal-oauth2)</li></ul> |
| **IoT 現場閘道** | <ul><li>[驗證連接 toohello 欄位閘道裝置](#authn-devices-field)</li></ul> |
| **IoT 雲端閘道** | <ul><li>[請確定會驗證連線 tooCloud 閘道裝置](#authn-devices-cloud)</li><li>[使用每一裝置驗證認證](#authn-cred)</li></ul> |
| **Azure 儲存體** | <ul><li>[確認該只有 hello 必要容器和 blob 指定匿名讀取權限](#req-containers-anon)</li><li>[授與有限的存取 tooobjects 中使用 SAS 或 SAP 的 Azure 儲存體](#limited-access-sas)</li></ul> |

## <a id="standard-authn-web-app"></a>請考慮使用標準驗證機制 tooauthenticate tooWeb 應用程式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | <p>驗證是一個實體證明其身分識別，通常是透過使用者名稱和密碼等認證的 hello 程序。 有多個驗證通訊協定可列入考量。 下列是其中一些通訊協定︰</p><ul><li>Client certificates</li><li>Windows 架構</li><li>表單架構</li><li>同盟 - ADFS</li><li>同盟 - Azure AD</li><li>同盟 - Identity Server</li></ul><p>請考慮使用標準驗證機制 tooidentify hello 來源處理序</p>|

## <a id="handle-failed-authn"></a>應用程式必須安全地處理失敗的驗證案例

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | <p>明確地驗證使用者的應用程式必須處理失敗的驗證案例 securely.hello 驗證機制必須：</p><ul><li>驗證失敗時拒絕存取 tooprivileged 資源</li><li>驗證失敗後會顯示一般錯誤訊息，並發生存取遭拒</li></ul><p>測試：</p><ul><li>登入失敗後的特殊權限資源保護</li><li>一般錯誤訊息會顯示於驗證失敗和存取遭拒事件</li><li>帳戶會在過多失敗嘗試後停用</li><ul>|

## <a id="step-up-adaptive-authn"></a>啟用升級或調適性驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | <p>確認 hello 應用程式具有額外的授權 （例如步驟或透過多因素驗證，例如傳送 OTP SMS、 電子郵件等或重新驗證提示中的自動調整驗證） 讓 hello 使用者受到挑戰之前被授與存取權toosensitive 資訊。 此規則也適用於進行重大變更 tooan 帳戶或動作</p><p>這也表示 hello 配接的驗證已實 toobe hello 應用程式正確強制執行即時線上授權的方式，以 toonot 允許未經授權的操作，藉由在範例中，參數遭到竄改</p>|

## <a id="admin-interface-lockdown"></a>確保已適當地鎖定系統管理介面

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | hello 第一個解決方式是只從特定來源 IP 範圍 toohello 系統管理介面 toogrant 存取。 如果該方案就會無法將永遠是比，建議 tooenforce hello 系統管理介面到記錄的加強或調整驗證 |

## <a id="forgot-pword-fxn"></a>安全地實作忘記密碼功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | <p>hello 首先是忘了密碼和其他的復原路徑傳送的連結，包括時間限制的啟用 token，而不是 hello 密碼本身的 tooverify。 根據軟 token （例如 SMS 語彙基元，原生行動應用程式等） 的其他驗證可能會需要也才能透過傳送嗨連結。 第二，您應該不鎖定 hello 使用者帳戶而 hello 的新密碼的程序正在進行中。</p><p>只要攻擊者決定 toointentionally 鎖定 hello 使用者與自動化的攻擊，這可能會導致 tooa 阻絕服務攻擊。 第三，每當 hello 新密碼的要求已設定進行中，您顯示 hello 訊息應該一般化順序 tooprevent username 列舉型別中。 第四個，永遠不允許使用舊密碼的 hello 並實作的強式密碼原則。</p> |

## <a id="pword-account-policy"></a>確保已實作密碼和帳戶原則

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| 詳細資料 | <p>必須實作符合組織原則和最佳作法的密碼和帳戶原則。</p><p>針對暴力和字典 toodefend 基礎猜測： 增強式密碼原則必須實作的 tooensure 使用者建立複雜的密碼 （例如，12 個字元的最小長度、 字母及特殊字元）。</p><p>帳戶鎖定原則可能會在 hello 下列方式來實作：</p><ul><li>**軟式鎖定︰**這是保護使用者以對抗暴力密碼破解攻擊的理想選項。 例如，每當 hello 使用者輸入錯誤密碼 3 次 hello 應用程式無法鎖定 hello 帳戶中關閉的強制進行利潤較低的 hello 攻擊者 tooproceed 其密碼的暴力密碼破解 hello 處理程序的順序 tooslow 一分鐘。 如果您是此範例中，就會達到 tooimplement 硬鎖定對策"Dos"由永久鎖定帳戶。 或者，應用程式可能會產生 OTP （一次密碼） 並將它傳送不足的頻外 (透過電子郵件，sms 等) toohello 使用者。 達到臨界值數目的失敗嘗試後，另一種方法可能是 tooimplement CAPTCHA。</li><li>**永久鎖定：**應套用此類型的鎖定，每當您偵測攻擊您的應用程式的使用者，並透過永久鎖定其帳戶，直到回應小組時間 toodo 其鑑識計數器他。 此程序之後，您可以決定回到 toogive hello 使用者鎖定帳戶，或採取進一步的合法動作對他。 此類型的方法可避免從您的應用程式和基礎結構，進一步 penetrating hello 攻擊。</li></ul><p>toodefend 攻擊，在預設和可預測的帳戶，確認所有金鑰和密碼所取代，並會產生或之後安裝期間，已取代。</p><p>如果 hello 應用程式具有 tooauto-產生的密碼，請確定產生的 hello 密碼是隨機的且具有高熵。</p>|

## <a id="controls-username-enum"></a>實作控制項 tooprevent username 列舉

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 所有的錯誤訊息應該一般化順序 tooprevent username 列舉型別中。 而且，您有時無法避免註冊頁面等功能的資訊洩漏。 您需要在這裡等 CAPTCHA tooprevent 自動化的攻擊，攻擊者的 toouse 速率限制方法。 |

## <a id="win-authn-sql"></a>可能的話，請使用 Windows 驗證來連接 tooSQL 伺服器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | OnPrem |
| **屬性**              | SQL 版本 - 全部 |
| **參考**              | [SQL Server - 選擇驗證模式](https://msdn.microsoft.com/library/ms144284.aspx) |
| **步驟** | Windows 驗證使用 Kerberos 安全性通訊協定，可提供密碼原則強制執行強式密碼，而考慮 toocomplexity 驗證與帳戶鎖定，提供支援，而且支援密碼逾期。|

## <a id="aad-authn-sql"></a>盡可能使用 Azure Active Directory 驗證連線 tooSQL 資料庫

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure |
| **屬性**              | SQL 版本 - V12 |
| **參考**              | [連接 tooSQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/) |
| **步驟** | **最小版本：** Azure SQL Database V12 所需針對 hello Microsoft Directory tooallow Azure SQL Database toouse AAD 驗證 |

## <a id="authn-account-pword"></a>使用 SQL 驗證模式時，確保在 SQL Server 上強制執行帳戶和密碼原則

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [SQL Server 密碼原則](https://technet.microsoft.com/library/ms161959(v=sql.110).aspx) |
| **步驟** | 使用 SQL Server 驗證時，系統會在 SQL Server 中建立不是以 Windows 使用者帳戶為基礎的登入。 Hello 使用者名稱和密碼 hello 建立使用 SQL Server 和 SQL Server 中儲存。 SQL Server 可以使用 Windows 密碼原則機制。 它可以套用相同複雜性和過期原則用於 SQL Server 內使用的 Windows toopasswords hello。 |

## <a id="autn-contained-db"></a>請勿在自主資料庫中使用 SQL 驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Sql Azure、OnPrem |
| **屬性**              | SQL 版本 - MSSQL2012、SQL 版本 - V12 |
| **參考**              | [自主資料庫的安全性最佳作法](http://msdn.microsoft.com/library/ff929055.aspx) |
| **步驟** | hello 缺乏的強制執行的密碼原則可能會增加弱式認證，建立自主資料庫中的 hello 的可能性。 利用 Windows 驗證。 |

## <a id="authn-sas-tokens"></a>使用採用 SaS 權杖的每一裝置驗證認證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 事件中樞 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [事件中樞驗證和安全性模型概觀](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **步驟** | <p>hello 事件中心的安全性模型根據共用存取簽章 (SAS) 權杖與事件發行者的組合。 hello 發行者名稱代表 hello DeviceID 接收 hello 語彙基元。 這樣有助於關聯產生與 hello 個別裝置的 hello 語彙基元。</p><p>在允許偵測承載內部原始來源詐騙嘗試的服務端上，所有訊息都會標示建立者。 當驗證裝置時，會產生每個裝置 SaS 權杖的已設定領域的 tooa 唯一發行者。</p>|

## <a id="multi-factor-azure-admin"></a>啟用 Azure 系統管理員適用的 Azure Multi-Factor Authentication

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [什麼是 Azure Multi-Factor Authentication？](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) |
| **步驟** | <p>多因素驗證 (MFA) 是驗證的程式需要一個以上的驗證方法，並將重要的第二層的安全性 toouser 登入和交易方法。 其運作方式是要求任何兩個或多個下列驗證方法的 hello:</p><ul><li>您知道的某些資訊 (通常是密碼)</li><li>您擁有的某些東西 (不容易輕易複製的信任裝置，例如電話)</li><li>您身上的某些特徵 (生物識別技術)</li><ul>|

## <a id="anon-access-cluster"></a>限制匿名存取 tooService 網狀架構叢集

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure  |
| **參考**              | [Service Fabric 叢集安全性案例](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security) |
| **步驟** | <p>叢集應該一律是從連接 tooyour 叢集，尤其是當它已在其上執行的實際執行工作負載的安全的 tooprevent 未經授權的使用者。</p><p>在建立 service fabric 叢集時，請確定該 hello 安全性模式設定太 「 安全的 」，並設定所需的 hello X.509 伺服器憑證。 建立 「 安全 」 的叢集將會允許任何匿名使用者 tooconnect tooit，如果它會公開管理端點 toohello 公用網際網路。</p>|

## <a id="fabric-cn-nn"></a>確保 Service Fabric 的用戶端對節點憑證不同於節點對節點憑證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure、環境 - 獨立 |
| **參考**              | [Service Fabric 節點用戶端憑證安全性](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#_client-to-node-certificate-security)，[連接 tooa 安全叢集使用用戶端憑證](https://azure.microsoft.com/documentation/articles/service-fabric-connect-to-secure-cluster/) |
| **步驟** | <p>用戶端對節點憑證的安全性設定時指定的系統管理員用戶端憑證及/或使用者的用戶端憑證，藉以建立 hello 叢集透過 hello Azure 入口網站中，資源管理員範本或獨立 JSON 範本。</p><p>hello 管理用戶端和使用者用戶端憑證指定應該不同於您指定的節點到節點安全性 hello 主要和次要憑證。</p>|

## <a id="aad-client-fabric"></a>使用 AAD tooauthenticate 用戶端 tooservice 網狀架構叢集

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure |
| **參考**              | [叢集安全性案例 - 安全性建議](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#security-recommendations) |
| **步驟** | 在 Azure 上執行的叢集也可以保護存取 toohello 管理端點，使用 Azure Active Directory (AAD)，除了用戶端憑證。 Azure 的叢集，建議您使用用戶端的安全性 tooauthenticate AAD 和憑證節點對節點的安全性。|

## <a id="fabric-cert-ca"></a>確保從經過核准的憑證授權單位 (CA) 取得 Service Fabric 憑證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure |
| **參考**              | [X.509 憑證和 Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/#x509-certificates-and-service-fabric) |
| **步驟** | <p>Service Fabric 會使用 X.509 伺服器憑證驗證節點和用戶端。</p><p>服務網狀架構中使用憑證時的一些重要事項 tooconsider:</p><ul><li>執行生產環境工作負載之叢集中所使用的憑證應該是使用已正確設定的 Windows Server 憑證服務來建立，或是從已核准的憑證授權單位 (CA) 取得。 hello CA 可以核准外部 CA 或妥善管理內部公開金鑰基礎結構 (PKI)</li><li>絕對不要在生產環境中使用以 MakeCert.exe 這類工具建立的暫時或測試憑證</li><li>您可以使用自我簽署憑證，但應該只用於測試叢集，不應該在生產環境中使用</li></ul>|

## <a id="standard-authn-id"></a>使用 Identity Server 所支援的標準驗證案例

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [IdentityServer3-hello 大的圖片](https://identityserver.github.io/Documentation/docsv2/overview/bigPicture.html) |
| **步驟** | <p>以下是識別伺服器所支援的一般互動 hello:</p><ul><li>瀏覽器與 Web 應用程式通訊</li><li>Web 應用程式與 Web API 通訊 (有時靠自己，有時代表使用者)</li><li>瀏覽器架構應用程式與 Web API 通訊</li><li>原生應用程式與 Web API 通訊</li><li>伺服器架構應用程式與 Web API 通訊</li><li>Web API 與 Web API 通訊 (有時靠自己，有時代表使用者)</li></ul>|

## <a id="override-token"></a>覆寫 hello 預設身分識別伺服器權杖快取使用可擴充的替代項目

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Identity Server | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Identity Server 部署 - 快取](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **步驟** | <p>IdentityServer 已內建簡單的記憶體內部快取。 雖然這是適用於小型規模原生應用程式，它不能擴充 mid 層和後端應用程式的 hello 下列原因：</p><ul><li>這些應用程式是由許多使用者同時存取。 所有存取權杖都儲存在相同的存放區建立隔離的問題和當大規模運作的挑戰的 hello： 許多使用者，各有許多的語彙基元為 hello 資源 hello 應用程式存取其行為，可能表示很大的數字和費時的查詢作業</li><li>這些應用程式通常會部署在分散式拓撲中，其中多個節點必須具有存取 toohello 相同的快取</li><li>快取的權杖必須在程序回收和停用後存留下來</li><li>如需所有 hello 上述原因，同時實作 web 應用程式，建議使用可擴充的替代項目，例如 Azure Redis 快取的 toooverride hello 預設識別伺服器的權杖快取</li></ul>|

## <a id="binaries-signed"></a>確保已數位簽署所部署應用程式的二進位檔

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確保已部署的應用程式二進位檔經過數位簽署，如此可以檢查 hello hello 二進位檔的完整性|

## <a id="msmq-queues"></a>當連接 tooMSMQ WCF 中的佇列時啟用驗證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx) |
| **步驟** | 程式失敗 tooenable 驗證連接 tooMSMQ 佇列時，攻擊者可以匿名方式提交訊息 toohello 佇列中的進行處理。 如果驗證不是使用的 tooconnect tooan MSMQ 佇列使用 toodeliver 訊息 tooanother 程式，攻擊者無法送出惡意的匿名訊息。|

### <a name="example"></a>範例
hello `<netMsmqBinding/>` hello 底下的 WCF 組態檔項目會指示 WCF toodisable 驗證時連接 tooan MSMQ 佇列訊息傳遞。
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""None"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```
設定 MSMQ toorequire Windows 網域或憑證驗證在任何內送或外寄訊息的所有時間。

### <a name="example"></a>範例
hello`<netMsmqBinding/>`連接 tooan MSMQ 佇列時，下方的 hello WCF 組態檔元素會指示 WCF tooenable 憑證驗證。 hello 用戶端會使用 X.509 憑證進行驗證。 hello 用戶端憑證必須要有 hello 伺服器 hello 憑證存放區中。
```
<bindings>
    <netMsmqBinding>
        <binding>
            <security>
                <transport msmqAuthenticationMode=""Certificate"" />
            </security>
        </binding>
    </netMsmqBinding>
</bindings>
```

## <a id="message-none"></a>WCF 執行未設定郵件 clientCredentialType toonone

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework 3 |
| **屬性**              | 用戶端認證類型 - None |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | hello 驗證表示每個人都是可以 tooaccess 這項服務。 不會驗證其用戶端的服務可讓 tooall 使用者存取。 設定 hello 應用程式 tooauthenticate 對用戶端認證。 設定 hello 訊息 clientCredentialType tooWindows 或憑證可以完成此作業。 |

### <a name="example"></a>範例
```
<message clientCredentialType=""Certificate""/>
```

## <a id="transport-none"></a>WCF 執行未設定傳輸 clientCredentialType toonone

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、.NET Framework 3 |
| **屬性**              | 用戶端認證類型 - None |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | hello 驗證表示每個人都是可以 tooaccess 這項服務。 不會驗證其用戶端的服務可讓所有使用者 tooaccess 其功能。 設定 hello 應用程式 tooauthenticate 對用戶端認證。 設定 hello 傳輸 clientCredentialType tooWindows 或憑證可以完成此作業。 |

### <a name="example"></a>範例
```
<transport clientCredentialType=""Certificate""/>
```

## <a id="authn-secure-api"></a>請確定標準驗證技術是使用的 toosecure Web 應用程式開發介面

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [ASP.NET Web API 中的驗證和授權](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api)、[外部驗證服務與 ASP.NET Web API (C#)](http://www.asp.net/web-api/overview/security/external-authentication-services) |
| **步驟** | <p>驗證是一個實體證明其身分識別，通常是透過使用者名稱和密碼等認證的 hello 程序。 有多個驗證通訊協定可列入考量。 下列是其中一些通訊協定︰</p><ul><li>Client certificates</li><li>Windows 架構</li><li>表單架構</li><li>同盟 - ADFS</li><li>同盟 - Azure AD</li><li>同盟 - Identity Server</li></ul><p>Hello 參考一節中的連結提供低階的詳細資料，在這種 hello 驗證配置可以採用的方式實作 toosecure Web API。</p>|

## <a id="authn-aad"></a>使用 Azure Active Directory 所支援的標準驗證案例

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure AD | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Azure AD 的驗證案例](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/)、[Azure Active Directory 程式碼範例](https://azure.microsoft.com/documentation/articles/active-directory-code-samples/)、[Azure Active Directory 開發人員指南](https://azure.microsoft.com/documentation/articles/active-directory-developers-guide/) |
| **步驟** | <p>Azure Active Directory (Azure AD) 提供身分識別做為服務，支援業界標準通訊協定 (例如 OAuth 2.0 和 OpenID Connect)，以簡化開發人員的驗證工作。 以下是 hello Azure AD 支援的五個主要的應用程式案例：</p><ul><li>Web 瀏覽器 tooWeb 應用程式： 使用者需要在 Azure AD 所保護的 tooa web 應用程式的 toosign</li><li>使用者需要 toosign tooa 單一頁面應用程式中，Azure AD 所保護的單一頁面應用程式 (SPA):</li><li>原生應用程式 tooWeb API: 原生應用程式上執行的電話、 平板電腦或電腦的需求 tooauthenticate 使用者 tooget 資源 web API 從 Azure AD 所保護</li><li>Web 應用程式 tooWeb API: web 應用程式需要從 Azure AD 所保護的 web API 的 tooget 資源</li><li>精靈或伺服器應用程式 tooWeb API： 需要從 Azure AD 所保護的 web API 的 tooget 資源精靈應用程式或伺服器應用程式與 web 使用者介面</li></ul><p>請針對低層級的實作詳細資料，參閱 toohello hello 參考一節中的連結</p>|

## <a id="adal-scalable"></a>覆寫 hello 預設 ADAL 權杖快取使用可擴充的替代項目

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure AD | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/)、[使用 Redis 作為 ADAL 權杖快取](https://blogs.msdn.microsoft.com/mrochon/2016/09/19/using-redis-as-adal-token-cache/)  |
| **步驟** | <p>使用 ADAL （Active Directory 驗證程式庫） 會依賴靜態儲存區，可用的整個處理序的記憶體中快取 hello 預設快取。 雖然這適用於原生應用程式，它不能擴充 mid 層和後端應用程式的 hello 下列原因：</p><ul><li>這些應用程式是由許多使用者同時存取。 所有存取權杖都儲存在相同的存放區建立隔離的問題和當大規模運作的挑戰的 hello： 許多使用者，各有許多的語彙基元為 hello 資源 hello 應用程式存取其行為，可能表示很大的數字和費時的查詢作業</li><li>這些應用程式通常會部署在分散式拓撲中，其中多個節點必須具有存取 toohello 相同的快取</li><li>快取的權杖必須在程序回收和停用後存留下來</li></ul><p>如需所有 hello 上方實作 web 應用程式時的考量，建議 toooverride hello 預設 ADAL 權杖快取使用可擴充的替代項目，例如 Azure Redis 快取。</p>|

## <a id="tokenreplaycache-adal"></a>確保 TokenReplayCache 使用的 tooprevent hello ADAL 驗證權杖重新執行

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure AD | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [Modern Authentication with Azure Active Directory for Web Applications](https://blogs.msdn.microsoft.com/microsoft_press/2016/01/04/new-book-modern-authentication-with-azure-active-directory-for-web-applications/) |
| **步驟** | <p>hello TokenReplayCache 屬性可讓開發人員 toodefine 權杖重新執行快取，可用於儲存的 hello 目的是要驗證的權杖沒有語彙基元的存放區可以使用一次以上。</p><p>這是常見的攻擊，對 hello 名符其實權杖重新執行攻擊： 攻擊者攔截在登入時傳送 hello 語彙基元可能會嘗試 toosend 它再次 toohello 應用程式 （「 重新執行 」 它），建立新的工作階段。 例如，在 OIDC 碼-授與流程中，使用者驗證成功後，要求太"/ signin oidc"hello 信賴憑證者的合作對象的端點就會加入與 「 id_token 」，「 程式碼 」 和 「 州 」 參數。</p><p>hello 信賴憑證者合作對象會驗證此要求，並建立新的工作階段。 如果敵人會擷取此要求，並重新執行它，他可以建立成功的工作階段和詐騙 hello 使用者。 hello OpenID Connect 中的 hello nonce 存在可以限制，但不是完全排除 hello 情況可以成功制定 hello 攻擊。 tooprotect 他們的應用程式開發人員可以提供 ITokenReplayCache 的實作，並指派執行個體 tooTokenReplayCache。</p>|

### <a name="example"></a>範例
```C#
// ITokenReplayCache defined in ADAL
public interface ITokenReplayCache
{
bool TryAdd(string securityToken, DateTime expiresOn);
bool TryFind(string securityToken);
}
```

### <a name="example"></a>範例
以下是 hello ITokenReplayCache 介面的範例實作。 (請自訂並實作您的專案特定快取架構)
```C#
public class TokenReplayCache : ITokenReplayCache
{
    private readonly ICacheProvider cache; // Your project-specific cache provider
    public TokenReplayCache(ICacheProvider cache)
    {
        this.cache = cache;
    }
    public bool TryAdd(string securityToken, DateTime expiresOn)
    {
        if (this.cache.Get<string>(securityToken) == null)
        {
            this.cache.Set(securityToken, securityToken);
            return true;
        }
        return false;
    }
    public bool TryFind(string securityToken)
    {
        return this.cache.Get<string>(securityToken) != null;
    }
}
```
hello 實作快取的 toobe OIDC 選項透過 hello"TokenValidationParameters"屬性中參考的如下所示。
```C#
OpenIdConnectOptions openIdConnectOptions = new OpenIdConnectOptions
{
    AutomaticAuthenticate = true,
    ... // other configuration properties follow..
    TokenValidationParameters = new TokenValidationParameters
    {
        TokenReplayCache = new TokenReplayCache(/*Inject your cache provider*/);
    }
}
```

請注意這項設定，本機 OIDC 保護應用程式的登入該 tootest hello 效益，和擷取 hello 要求太`"/signin-oidc"`fiddler 中的端點。 當就地不 hello 保護時，重新執行此要求 fiddler 中的會設定新的工作階段 cookie。 Hello 要求重新加入 hello TokenReplayCache 保護之後，當 hello 應用程式將會擲回例外狀況，如下所示：`SecurityTokenReplayDetectedException: IDX10228: hello securityToken has previously been validated, securityToken: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ1......`

## <a id="adal-oauth2"></a>使用 ADAL 程式庫 toomanage 語彙基元要求從 OAuth2 用戶端 tooAAD （或在內部部署 AD）

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure AD | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) |
| **步驟** | <p>hello Azure AD 驗證程式庫 (ADAL) 可讓用戶端應用程式開發人員 tooeasily 驗證使用者 toocloud 或在內部部署 Active Directory (AD)，然後取得存取權杖來保護 API 呼叫。</p><p>ADAL 有許多功能可使開發人員的驗證更容易，例如非同步支援、儲存存取權杖和更新權杖的可設定權杖快取、當存取權杖到期並且更新權杖可供使用時自動更新權杖等等。</p><p>處理最多的 hello 複雜性，ADAL 可以協助開發人員專注於他們的應用程式中的商務邏輯，並輕鬆地保護資源，而不用安全性的專家。 不同的程式庫適用於 .NET、JavaScript (用戶端和 Node.js)、iOS、Android 和 Java。</p>|

## <a id="authn-devices-field"></a>驗證連接 toohello 欄位閘道裝置

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請確定每個裝置需經過 hello 欄位閘道之前接受其資料以及之前促進上游通訊以 hello 雲端閘道。 此外，確保裝置與每一裝置認證連線，即可唯一識別個別裝置。|

## <a id="authn-devices-cloud"></a>請確定會驗證連線 tooCloud 閘道裝置

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、C#、Node.JS  |
| **屬性**              | N/A、閘道選擇 - Azure IoT 中樞 |
| **參考**              | N/A、[採用 .NET 的 Azure IoT 中樞](https://azure.microsoft.com/documentation/articles/iot-hub-csharp-csharp-getstarted/)、[開始使用 IoT 中樞和 Node JS](https://azure.microsoft.com/documentation/articles/iot-hub-node-node-getstarted)、[使用 SAS 和憑證保護 IoT](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/)、[Git 儲存機制](https://github.com/Azure/azure-iot-sdks/tree/master/node) |
| **步驟** | <ul><li>**泛型：**驗證 hello 裝置使用傳輸層安全性 (TLS) 或 IPSec。 如果裝置無法處理完整的非對稱密碼編譯，則基礎結構應該支援在這些裝置上使用預先共用金鑰 (PSK)。 利用 Azure AD、Oauth。</li><li>**C# 中：** hello Create 方法建立時是 DeviceClient 執行個體中，依預設，建立使用 hello AMQP 通訊協定 toocommunicate 與 IoT 中樞的 DeviceClient 執行個體。 toouse hello HTTPS 通訊協定，使用覆寫 hello hello 建立方法，可讓您 toospecify hello 通訊協定。 如果您使用 hello HTTPS 通訊協定，您也應該加入 hello `Microsoft.AspNet.WebApi.Client` NuGet 封裝 tooyour 專案 tooinclude hello`System.Net.Http.Formatting`命名空間。</li></ul>|

### <a name="example"></a>範例
```C#
static DeviceClient deviceClient;

static string deviceKey = "{device key}";
static string iotHubUri = "{iot hub hostname}";

var messageString = "{message in string format}";
var message = new Message(Encoding.ASCII.GetBytes(messageString));

deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey("myFirstDevice", deviceKey));

await deviceClient.SendEventAsync(message);
```

### <a name="example"></a>範例
**Node.JS：驗證**
#### <a name="symmetric-key"></a>對稱金鑰
* 在 Azure 上建立 IoT 中樞
* 建立 hello 裝置身分識別登錄項目
    ```javascript
    var device = new iothub.Device(null);
    device.deviceId = <DeviceId >
    registry.create(device, function(err, deviceInfo, res) {})
    ```
* 建立模擬裝置
    ```javascript
    var clientFromConnectionString = require('azure-iot-device-amqp').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>SharedAccessKey=<SharedAccessKey>';
    var client = clientFromConnectionString(connectionString);
    ```
#### <a name="sas-token"></a>SAS 權杖
* 取得使用對稱金鑰時在內部產生的權杖，但我們也可以明確地產生和使用權杖
* 定義通訊協定︰`var Http = require('azure-iot-device-http').Http;`
* 建立 SAS 權杖：
    ```javascript
    resourceUri = encodeURIComponent(resourceUri.toLowerCase()).toLowerCase();
    var deviceName = "<deviceName >";
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    var toSign = resourceUri + '\n' + expires;
    // using crypto
    var decodedPassword = new Buffer(signingKey, 'base64').toString('binary');
    const hmac = crypto.createHmac('sha256', decodedPassword);
    hmac.update(toSign);
    var base64signature = hmac.digest('base64');
    var base64UriEncoded = encodeURIComponent(base64signature);
    // construct authorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "%2fdevices%2f"+deviceName+"&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
    ```
* 使用 SAS 權杖進行連線︰ 
    ```javascript
    Client.fromSharedAccessSignature(sas, Http); 
    ```
#### <a name="certificates"></a>憑證
* 產生自我簽署的 X509 憑證使用任何工具例如 OpenSSL toogenerate.cert 和.key 檔案 toostore hello 憑證和 hello 金鑰分別
* 使用憑證佈建可接受安全連線的裝置。
    ```javascript
    var connectionString = '<connectionString>';
    var registry = iothub.Registry.fromConnectionString(connectionString);
    var deviceJSON = {deviceId:"<deviceId>",
    authentication: {
        x509Thumbprint: {
        primaryThumbprint: "<PrimaryThumbprint>",
        secondaryThumbprint: "<SecondaryThumbprint>"
        }
    }}
    var device = deviceJSON;
    registry.create(device, function (err) {});
    ```
* 使用憑證連接裝置
    ```javascript
    var Protocol = require('azure-iot-device-http').Http;
    var Client = require('azure-iot-device').Client;
    var connectionString = 'HostName=<HostName>DeviceId=<DeviceId>x509=true';
    var client = Client.fromConnectionString(connectionString, Protocol);
    var options = {
        key: fs.readFileSync('./key.pem', 'utf8'),
        cert: fs.readFileSync('./server.crt', 'utf8')
    }; 
    // Calling setOptions with hello x509 certificate and key (and optionally, passphrase) will configure hello client //transport toouse x509 when connecting tooIoT Hub
    client.setOptions(options);
    //call fn tooexecute after hello connection is set up
    client.open(fn);
    ```

## <a id="authn-cred"></a>使用每一裝置驗證認證

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道  | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | 閘道選擇 - Azure IoT 中樞 |
| **參考**              | [Azure IoT 中樞安全性權杖](https://azure.microsoft.com/documentation/articles/iot-hub-sas-tokens/) |
| **步驟** | 使用每一裝置驗證認證搭配以裝置金鑰或用戶端憑證為基礎的 SaS 權杖，而不是 IoT 中樞共用存取原則。 這會防止另一個 hello 重複使用的裝置或欄位的一個閘道的驗證權杖 |

## <a id="req-containers-anon"></a>確認該只有 hello 必要容器和 blob 指定匿名讀取權限

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | StorageType - Blob |
| **參考**              | [管理匿名讀取權限 toocontainers 和 blob](https://azure.microsoft.com/documentation/articles/storage-manage-access-to-resources/)，[共用存取簽章，第 1 部分： 了解 hello SAS 模型](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/) |
| **步驟** | <p>根據預設，容器和內部任何 blob 能存取只能由 hello hello 儲存體帳戶的擁有者。 toogive 匿名使用者的讀取權限 tooa 容器和其 blob，其中一個可以設定 hello 容器的權限 tooallow 公用存取。 匿名使用者可以讀取可公開存取容器中的 blob，而不需驗證 hello 要求。</p><p>容器會提供下列選項來管理容器存取 hello:</p><ul><li>完整的公開讀取權限：可以透過匿名要求讀取容器和 Blob 資料。 用戶端透過匿名要求，hello 容器內的 blob，但無法列舉 hello 儲存體帳戶中的容器。</li><li>僅對 Blob 有公開讀取權限：您可以透過匿名要求讀取此容器內的 Blob 資料，但您無法使用容器資料。 用戶端無法列舉 hello 透過匿名要求的容器中的 blob</li><li>沒有公開讀取權限： hello 帳戶擁有者可以讀取容器和 blob 資料</li></ul><p>匿名存取適用於某些 Blob 應永遠可供匿名讀取存取的狀況。 其中一個可以進行更精細的控制，建立共用的存取簽章，可讓您使用不同的權限的 toodelegate 限制存取和一段指定的時間間隔。 確保容器和 blob (可能包含敏感性資料) 不會意外取得匿名存取權</p>|

## <a id="limited-access-sas"></a>授與有限的存取 tooobjects 中使用 SAS 或 SAP 的 Azure 儲存體

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A |
| **參考**              | [共用存取簽章，第 1 部分： 了解 hello SAS 模型](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)，[共用存取簽章，第 2 部分： 建立和使用 Blob 儲存體使用 SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-2/)， [toodelegate 存取 tooobjects 在帳戶中使用的方式共用的存取簽章和預存的存取原則](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_how-to-delegate-access-to-objects-in-your-account-using-shared-access-signatures-and-stored-access-policies) |
| **步驟** | <p>使用共用的存取簽章 (SAS) 是在儲存體帳戶 tooother 用戶端，而不需要 tooexpose 帳戶存取金鑰的強大的方式 toogrant 有限存取 tooobjects。 hello SAS 是 URI 包含在其查詢參數中的所有 hello 資訊所需的已驗證存取 tooa 儲存體資源。 tooaccess 以 hello SAS 存放裝置資源，hello 用戶端只需要 toopass hello SAS toohello 適當建構函式或方法中。</p><p>當您想 tooprovide 存取 tooresources 無法信任 hello 帳戶金鑰與程式儲存體帳戶 tooa 用戶端中，您可以使用 SAS。 儲存體帳戶金鑰包含兩者的主要和次要索引鍵，這兩種授與系統管理存取 tooyour 帳戶和所有中的 hello 資源。 您的帳戶金鑰的公開會開啟您帳戶 toohello 的可能性惡意或疏忽使用。 共用的存取簽章提供安全的替代方案，可讓其他用戶端 tooread、 寫入和刪除資料中根據 toohello 權限已授與，儲存體帳戶，而需要在 hello 帳戶金鑰。</p><p>如果您每次都有一組類似的邏輯參數，使用預存存取原則 (SAP) 會是個不錯的做法。 因為使用 SAS，衍生自預存存取原則讓您 hello 能力 toorevoke SAS 立即，它是 hello 建議的最佳作法 tooalways 使用盡可能，預存存取原則。</p>|
