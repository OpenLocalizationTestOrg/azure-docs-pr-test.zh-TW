---
title: "aaaAuditing 和記錄-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
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
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>安全框架︰稽核和記錄 | 緩和措施 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[在您的解決方案中識別敏感性實體及實作變更稽核](#sensitive-entities)</li></ul> |
| **Web 應用程式** | <ul><li>[確保稽核和記錄會強制執行 hello 應用程式](#auditing)</li><li>[確保施行記錄輪替和區隔功能](#log-rotation)</li><li>[請確定 hello 應用程式不會記錄敏感的使用者資料](#log-sensitive-data)</li><li>[確保稽核和記錄檔有限制存取](#log-restricted-access)</li><li>[確保已記錄使用者管理事件](#user-management)</li><li>[請確認 hello 系統具有內建的防禦不當使用](#inbuilt-defenses)</li><li>[在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](#diagnostics-logging)</li></ul> |
| **資料庫** | <ul><li>[確保已在 SQL Server 上啟用登入稽核功能](#identify-sensitive-entities)</li><li>[在 Azure SQL 上啟用威脅偵測功能](#threat-detection)</li></ul> |
| **Azure 儲存體** | <ul><li>[使用 Azure 儲存體的 Azure 儲存體分析 tooaudit 存取](#analytics)</li></ul> |
| **WCF** | <ul><li>[實作足夠的記錄](#sufficient-logging)</li><li>[實作足夠的稽核失敗處理](#audit-failure-handling)</li></ul> |
| **Web API** | <ul><li>[確保在 Web API 上強制執行稽核和記錄功能](#logging-web-api)</li></ul> |
| **IoT 現場閘道** | <ul><li>[確保在現場閘道上強制執行適當的稽核和記錄功能](#logging-field-gateway)</li></ul> |
| **IoT 雲端閘道** | <ul><li>[確保在雲端閘道上強制執行適當的稽核和記錄功能](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>在您的解決方案中識別敏感性實體及實作變更稽核

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | 識別您的解決方案中包含敏感性資料的實體，以及在這些實體和現場實作變更稽核 |

## <a id="auditing"></a>確保稽核和記錄會強制執行 hello 應用程式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | 在所有元件上啟用稽核和記錄。 稽核記錄檔應擷取使用者內容。 識別所有重要的事件及記錄這些事件。 實作集中式記錄 |

## <a id="log-rotation"></a>確保施行記錄輪替和區隔功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | <p>記錄輪替是一個自動化程序，使用於封存過時記錄檔的系統管理作業中。 經常執行的大型應用程式伺服器會記錄每一個要求： 在 hello 表面之過於笨重的記錄檔，記錄檔輪替是方式 toolimit hello hello 記錄檔的大小總計同時，仍允許的最新事件的分析。 </p><p>記錄區隔基本上表示您需要的 toostore 記錄檔存放於不同的磁碟分割為 OS/應用程式執行所在中順序 tooavert 阻絕服務攻擊，或 hello 降級應用程式的效能</p>|

## <a id="log-sensitive-data"></a>請確定 hello 應用程式不會記錄敏感的使用者資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | <p>請檢查您不要登在使用者送出 tooyour 站台的任何機密資料。 檢查刻意的記錄，以及設計問題所造成的副作用。 敏感性資料的範例包括︰</p><ul><li>使用者認證</li><li>社會安全號碼或其他識別資訊</li><li>信用卡號碼或其他財務資訊</li><li>健康狀態資訊</li><li>私用金鑰或其他可能使用的 toodecrypt 加密資訊的資料</li><li>可用的系統或應用程式資訊 toomore 有效攻擊 hello 應用程式</li></ul>|

## <a id="log-restricted-access"></a>確保稽核和記錄檔有限制存取

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | <p>請檢查適當地設定 tooensure 存取權限 toolog 檔案。 應用程式帳戶應具有唯寫權限，而操作人員和支援人員應具有所需的唯讀權限。</p><p>系統管理員帳戶是 hello 唯一帳戶應該具有完整存取權。 請檢查記錄檔上的 Windows ACL 檔案 tooensure 會適當地限制：</p><ul><li>應用程式帳戶應具有唯寫權限</li><li>操作人員和支援人員應具有所需的唯讀存取權限</li><li>系統管理員是 hello 僅帳戶應該具有完整存取權</li></ul>|

## <a id="user-management"></a>確保已記錄使用者管理事件

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | <p>確定 hello 應用程式會監視使用者管理事件，例如成功和失敗的使用者登入，密碼重設密碼變更、 帳戶鎖定、 使用者註冊。 這樣可協助 toodetect 及回應 toopotentially 可疑的行為。 它也可以讓 toogather 作業資料。例如，tootrack 正在存取 hello 應用程式</p>|

## <a id="inbuilt-defenses"></a>請確認 hello 系統具有內建的防禦不當使用

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟**                   | <p>應備妥控制項，以便在發生應用程式誤用時擲回安全性例外狀況。 例如，如果輸入的驗證就定位，攻擊者嘗試 tooinject 惡意程式碼，不符合 hello regex，安全性例外狀況可能會擲回可能會誤用系統是用來指示</p><p>例如，我們建議 toohave 記錄的安全性例外狀況並採取行動的 hello 下列問題：</p><ul><li>輸入驗證</li><li>CSRF 違規</li><li>暴力密碼破解 (每項資源之每個使用者的要求數目上限)</li><li>檔案上傳違規</li><ul>|

## <a id="diagnostics-logging"></a>在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | EnvironmentType - Azure |
| **參考**              | N/A  |
| **步驟** | <p>Azure 提供內建的診斷 tooassist 與應用程式服務進行偵錯 web 應用程式。 它也適用於 tooAPI 應用程式和行動裝置應用程式。 App Service web 應用程式提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷的功能。</p><p>這些資訊邏輯上可區分為 Web 伺服器診斷和應用程式診斷</p>|

## <a id="identify-sensitive-entities"></a>確保已在 SQL Server 上啟用登入稽核功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [設定登入稽核](https://msdn.microsoft.com/library/ms175850.aspx) |
| **步驟** | <p>稽核登入資料庫伺服器必須啟用 toodetect/確認的密碼破解攻擊。 請務必 toocapture 失敗的登入。 擷取成功和失敗的登入嘗試，可在鑑識調查期間提供額外的好處</p>|

## <a id="threat-detection"></a>在 Azure SQL 上啟用威脅偵測功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | SQL Azure |
| **屬性**              | SQL 版本 - V12 |
| **參考**              | [開始使用 SQL Database 威脅偵測](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **步驟** |<p>威脅偵測偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。 它提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。</p><p>使用者可以瀏覽 hello 可疑使用 Azure SQL Database 稽核 toodetermine 如果他們未導致嘗試 tooaccess，破壞的事件，或利用 hello 資料庫中的資料。</p><p>威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階的安全性的監視系統</p>|

## <a id="analytics"></a>使用 Azure 儲存體的 Azure 儲存體分析 tooaudit 存取

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A |
| **參考**              | [使用儲存體分析 toomonitor 授權類型](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **步驟** | <p>每個儲存體帳戶，一個可啟用 Azure 儲存體分析 tooperform 記錄和度量資料存放區。 hello 儲存體分析記錄檔提供重要的資訊，例如當使用者存取儲存體時的其他人使用的驗證方法。</p><p>這可以是非常有幫助您緊密會保護存取 toostorage 如果項目。 比方說，在 Blob 儲存體中，您可以設定所有 hello 容器 tooprivate 和整個應用程式實作 hello SAS 服務使用。 然後您可以檢查 hello 記錄定期 toosee 如果使用 hello 儲存體帳戶金鑰，這可能表示有安全性的漏洞，存取您的 blob 或 hello blob 是公用的但它們不應該是。</p>|

## <a id="sufficient-logging"></a>實作足夠的記錄

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | <p>hello 缺乏適當的稽核記錄安全性事件之後，可能會妨礙鑑識投入時間。 Windows Communication Foundation (WCF) 提供 hello 能力 toolog 成功及/或失敗的驗證嘗試。</p><p>記錄失敗的驗證嘗試可以警告系統管理員可能的暴力破解攻擊。 同樣地，記錄成功的驗證事件可以在合法帳戶遭到入侵時提供有用的稽核線索。 啟用 WCF 的服務安全性稽核功能 |

### <a name="example"></a>範例
hello 以下是啟用稽核功能的範例組態
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>實作足夠的稽核失敗處理

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | .NET Framework |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | <p>開發的方案設定 toogenerate toowrite tooan 稽核記錄失敗時，例外狀況。 如果設定 WCF toothrow 無法 toowrite tooan 稽核記錄檔、 hello 程式將不會收到通知 hello 失敗，且時重要的安全性事件稽核的 ca 可能不會發生例外狀況。</p>|

### <a name="example"></a>範例
hello `<behavior/>` hello 底下的 WCF 組態檔項目會指示 WCF toonot WCF 失敗 toowrite tooan 稽核記錄檔時，通知 hello 應用程式。
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
設定 WCF toonotify hello 程式，每當它是無法 toowrite tooan 稽核記錄檔。 hello 程式應該都不會維持稽核記錄的地方 tooalert hello 組織中有替代通知配置。 

## <a id="logging-web-api"></a>確保在 Web API 上強制執行稽核和記錄功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 在 Web API 上啟用稽核和記錄功能。 稽核記錄檔應擷取使用者內容。 識別所有重要的事件及記錄這些事件。 實作集中式記錄 |

## <a id="logging-field-gateway"></a>確保在現場閘道上強制執行適當的稽核和記錄功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>當多個裝置連線 tooa 欄位閘道時，請確認連接嘗試和個別裝置 （成功或失敗） 的驗證狀態會記錄 hello 欄位閘道上進行維護。</p><p>此外，在欄位閘道維護 hello 的情況下 IoT 中樞認證的個別裝置，請確定這些認證擷取時，執行稽核。開發程序 tooperiodically 上載 hello 記錄 tooAzure IoT 中樞/儲存體長期保留的。</p> |

## <a id="logging-cloud-gateway"></a>確保在雲端閘道上強制執行適當的稽核和記錄功能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [簡介 tooIoT 中樞作業監視](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **步驟** | <p>設計用來收集及儲存透過 IoT 中樞作業監視所蒐集的稽核資料。 啟用下列監視類別目錄的 hello:</p><ul><li>裝置身分識別作業</li><li>裝置到雲端通訊</li><li>雲端到裝置通訊</li><li>連線</li><li>檔案上傳</li></ul>|
