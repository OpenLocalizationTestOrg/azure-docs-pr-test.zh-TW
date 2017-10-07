---
title: "aaaAuthorization-Microsoft 威脅模型化工具-Azure |Microsoft 文件"
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
ms.openlocfilehash: 3ea7ae2b46baa8578e574e6006b98dfe172829e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-authorization--mitigations"></a>安全框架︰授權 | 緩和措施 
| 產品/服務 | 文章 |
| --------------- | ------- |
| **電腦信任邊界** | <ul><li>[請確定正確的 Acl 會設定的 toorestrict 未經授權存取 toodata hello 裝置上](#acl-restricted-access)</li><li>[確保敏感性使用者特有應用程式內容會儲存在使用者設定檔目錄中](#sensitive-directory)</li><li>[確保使用最低權限，會執行部署的 hello 應用程式](#deployed-privileges)</li></ul> |
| **Web 應用程式** | <ul><li>[在處理商務邏輯流程時強制執行循序步驟順序](#sequential-logic)</li><li>[實作速率限制機制 tooprevent 列舉](#rate-enumeration)</li><li>[確保施行適當的授權並遵循最低權限的原則](#principle-least-privilege)</li><li>[商務邏輯和資源存取授權決策不應以傳入的要求參數為基礎](#logic-request-parameters)</li><li>[確保無法透過強迫瀏覽來列舉或存取內容和資源](#enumerable-browsing)</li></ul> |
| **資料庫** | <ul><li>[確定最低權限的帳戶都使用的 tooconnect tooDatabase 伺服器](#privileged-server)</li><li>[實作資料列層級安全性 RLS tooprevent 租用戶存取彼此的資料](#rls-tenants)</li><li>[系統管理員角色只能具備有效的必要使用者](#sysadmin-users)</li></ul> |
| **IoT 雲端閘道** | <ul><li>[連接 tooCloud 閘道使用最低權限語彙基元](#cloud-least-privileged)</li></ul> |
| **Azure 事件中樞** | <ul><li>[使用僅限傳送權限 SAS 金鑰來產生裝置權杖](#sendonly-sas)</li><li>[不使用存取權杖可直接存取 toohello 事件中樞](#access-tokens-hub)</li><li>[連接的 tooEvent 集線器使用 SAS 金鑰，擁有 hello 最低所需權限](#sas-minimum-permissions)</li></ul> |
| **Azure Document DB** | <ul><li>[使用資源的語彙基元 tooconnect tooDocumentDB 盡可能](#resource-docdb)</li></ul> |
| **Azure 信任邊界** | <ul><li>[啟用更細緻的存取權管理 tooAzure 訂用帳戶使用 RBAC](#grained-rbac)</li></ul> |
| **Service Fabric 信任邊界** | <ul><li>[限制用戶端存取 toocluster 作業使用 RBAC](#cluster-rbac)</li></ul> |
| **Dynamics CRM** | <ul><li>[執行安全性模型化並視需要使用欄位層級安全性](#modeling-field)</li></ul> |
| **Dynamics CRM 入口網站** | <ul><li>[執行 記住這個 hello 安全性模型中的 hello 入口網站與不同於 CRM hello 其餘部分的帳戶入口網站的安全性模型](#portal-security)</li></ul> |
| **Azure 儲存體** | <ul><li>[在 Azure 表格儲存體中授與某個實體範圍的精細權限](#permission-entities)</li><li>[啟用使用 Azure 資源管理員的角色型存取控制 (RBAC) tooAzure 儲存體帳戶](#rbac-azure-manager)</li></ul> |
| **行動用戶端** | <ul><li>[實作隱含的越獄或 Root 權限入侵偵測](#rooting-detection)</li></ul> |
| **WCF** | <ul><li>[WCF 中的弱式類別參考](#weak-class-wcf)</li><li>[WCF 實作授權控制](#wcf-authz)</li></ul> |
| **Web API** | <ul><li>[在 ASP.NET Web API 中實作適當的授權機制](#authz-aspnet)</li></ul> |
| **IoT 裝置** | <ul><li>[在 hello 裝置執行授權檢查，如果支援需要不同的權限層級的各種動作](#device-permission)</li></ul> |
| **IoT 現場閘道** | <ul><li>[執行授權檢查 hello 閘道欄位中，如果支援需要不同的權限層級的各種動作](#field-permission)</li></ul> |

## <a id="acl-restricted-access"></a>請確定正確的 Acl 會設定的 toorestrict 未經授權存取 toodata hello 裝置上

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 請確定正確的 Acl 會設定的 toorestrict 未經授權存取 toodata hello 裝置上|

## <a id="sensitive-directory"></a>確保敏感性使用者特有應用程式內容會儲存在使用者設定檔目錄中

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確保敏感性使用者特有應用程式內容會儲存在使用者設定檔目錄中。 這是的 tooprevent hello 的多個使用者電腦存取彼此的資料。|

## <a id="deployed-privileges"></a>確保使用最低權限，會執行部署的 hello 應用程式

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 電腦信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確定部署的 hello 應用程式使用最低權限執行。 |

## <a id="sequential-logic"></a>在處理商務邏輯流程時強制執行循序步驟順序

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 順序中的這個階段的使用者執行的正版 tooenforce hello 應用程式 tooonly 程序商務邏輯流程順序循序步驟，在實際的人力時間，正在處理的所有步驟並不會處理順序，tooverify 略過步驟，或處理其他使用者時，從步驟太快提交交易。|

## <a id="rate-enumeration"></a>實作速率限制機制 tooprevent 列舉

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 確保敏感性識別碼是隨機的。 在匿名頁面上實作 CAPTCHA 控制。 確保錯誤和例外狀況不得顯示特定資料|

## <a id="principle-least-privilege"></a>確保施行適當的授權並遵循最低權限的原則

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>hello 原則表示只有那些權限也就是不可或缺的 toothat 使用者工作中，提供使用者帳戶。 例如，備份的使用者不需要 tooinstall 軟體： hello 備份使用者因此，有權限只有 toorun 備份與備份相關應用程式。 任何其他權限 (例如安裝新的軟體) 都會遭到封鎖。 hello 原則也適用於 tooa 個人電腦使用者通常運作的一般使用者帳戶，並開啟權限，受密碼保護帳戶 （也就是超級使用者） 只有當 hello 情況絕對需要它。 </p><p>此原則也可以套用的 tooyour web 應用程式。 而非單獨取決於使用工作階段，以角色為基礎的驗證方法，我們而不是想 tooassign 權 toousers 透過資料庫為基礎的驗證系統。 我們仍然使用順序 tooidentify 中的工作階段，如果 hello 使用者已登入正確，只是現在，而是該使用者與特定角色，我們會將指派他與權限 tooverify 他是哪些動作特殊權限的 tooperform hello 系統上。 也大 pro 這個方法是，每當使用者具有 toobe 指派較少的權限將 hello 立即套用您的變更，因為 hello 指派不會依賴 hello 工作階段的其他方式 tooexpire 第一次。</p>|

## <a id="logic-request-parameters"></a>商務邏輯和資源存取授權決策不應以傳入的要求參數為基礎

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 每當您檢查使用者是否限制的 tooreview 特定資料，hello 存取應該限制處理伺服器端。 hello userID 應該儲存登入工作階段變數內，而且應該使用的 tooretrieve hello 資料庫的使用者資料 |

### <a name="example"></a>範例
```SQL
SELECT data 
FROM personaldata 
WHERE userID=:id < - session var 
```
現在可能的攻擊者可以未損害，由於 hello 識別碼來擷取資料的 hello 處理伺服器端變更 hello 應用程式作業。

## <a id="enumerable-browsing"></a>確保無法透過強迫瀏覽來列舉或存取內容和資源

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web 應用程式 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>Hello web 根目錄中，應該不會保留機密的靜態和組態檔案。 內容不需要 toobe 公用，控制項應該套用適當的存取權或移除 hello 內容本身。</p><p>此外，強制瀏覽通常會結合暴力技術 toogather 資訊嘗試 tooaccess Url 可能 tooenumerate 目錄以及伺服器上的檔案數目。 攻擊者可能會檢查常見現有檔案的所有變化。 例如，密碼檔案搜尋會包含下列檔案：psswd.txt、password.htm、password.dat 和其他變化。</p><p>此功能來偵測的暴力嘗試 toomitigate 都應該被包含。</p>|

## <a id="privileged-server"></a>確定最低權限的帳戶都使用的 tooconnect tooDatabase 伺服器

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [SQL Database 權限階層](https://msdn.microsoft.com/library/ms191465)、[SQL Database 安全性實體](https://msdn.microsoft.com/library/ms190401) |
| **步驟** | 最低權限的帳戶應該是使用的 tooconnect toohello 資料庫。 應用程式登入應該限制 hello 資料庫中，並只應執行所選的預存程序。 應用程式的登入應該沒有直接的資料表存取權。 |

## <a id="rls-tenants"></a>實作資料列層級安全性 RLS tooprevent 租用戶存取彼此的資料

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | Sql Azure、OnPrem |
| **屬性**              | SQL 版本 - V12、SQL 版本 - MsSQL2016 |
| **參考**              | [SQL Server 資料列層級安全性 (RLS)](https://msdn.microsoft.com/library/azure/dn765131.aspx) |
| **步驟** | <p>資料列層級安全性可讓客戶 toocontrol 存取 toorows 根據 hello 特性 hello 使用者執行查詢 （例如，群組成員資格或執行內容） 的資料庫資料表中。</p><p>資料列層級安全性 (RLS) 簡化 hello 設計和編碼您的應用程式中的安全性。 RLS 可讓您在資料列存取 tooimplement 限制。 例如，確保工作者只能存取相關 tootheir 部門的資料列，或限制客戶的資料存取 tooonly hello 資料相關的 tootheir 公司。</p><p>hello 存取限制邏輯是位於 hello 資料庫層，而不是離開 hello 資料，另一個應用程式層。 hello 資料庫系統會在每次從任何層嘗試存取該資料套用 hello 存取限制。 這樣就可以 hello 安全性系統更可靠且健全減少 hello hello 安全性系統的介面區。</p><p>|

請注意該 RLS 做為之 跨資料庫的功能是適用於只有 tooSQL 從 2016年開始的伺服器和 Azure SQL database。 如果未實作 hello 的方塊外 RLS 功能，則應該被確保資料存取是受限制使用檢視和程序

## <a id="sysadmin-users"></a>系統管理員角色只能具備有效的必要使用者

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 資料庫 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [SQL Database 權限階層](https://msdn.microsoft.com/library/ms191465)、[SQL Database 安全性實體](https://msdn.microsoft.com/library/ms190401) |
| **步驟** | 要非常有限的 hello SysAdmin 固定伺服器角色的成員，而且永遠不會包含應用程式所使用的帳戶。  請檢閱 hello hello 角色中的使用者清單，並移除任何不必要的帳戶|

## <a id="cloud-least-privileged"></a>連接 tooCloud 閘道使用最低權限語彙基元

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 雲端閘道 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 閘道選擇 - Azure IoT 中樞 |
| **參考**              | [IoT 中樞存取控制](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#Security) |
| **步驟** | 提供最低權限連接 tooCloud 閘道 （IoT 中樞） 的權限 toovarious 元件。 典型範例 – 裝置管理/佈建元件使用登錄讀取/寫入時、事件處理器 (ASA) 使用服務連線。 使用裝置認證的個別裝置連接|

## <a id="sendonly-sas"></a>使用僅限傳送權限 SAS 金鑰來產生裝置權杖

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 事件中樞 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [事件中樞驗證和安全性模型概觀](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **步驟** | SAS 金鑰是使用的 toogenerate 個別裝置權杖。 僅限傳送的權限的 SAS 金鑰產生 hello 裝置權杖時用於指定的發行者|

## <a id="access-tokens-hub"></a>不使用存取權杖可直接存取 toohello 事件中樞

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 事件中樞 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [事件中樞驗證和安全性模型概觀](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **步驟** | 授與直接存取 toohello 事件中心的語彙基元不應該授予 toohello 裝置。 Hello 裝置可存取只有 tooa 發行者可協助識別及列入它封鎖清單，如果使用的最小權限語彙基元 toobe 惡意或危害的裝置。|

## <a id="sas-minimum-permissions"></a>連接的 tooEvent 集線器使用 SAS 金鑰，擁有 hello 最低所需權限

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 事件中樞 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [事件中樞驗證和安全性模型概觀](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **步驟** | 最小權限的權限 toovarious 後端應用程式提供連接 toohello 事件中心。 產生個別的 SAS 金鑰，每個後端應用程式，並只提供傳送、 接收或管理 toothem hello 所需的權限。|

## <a id="resource-docdb"></a>使用資源語彙基元 tooconnect tooCosmos DB 盡可能

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure Document DB | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 為資源語彙基元與 DocumentDB 權限資源相關聯，且會擷取 hello 之間的關聯性的資料庫和 hello 的權限的 hello 使用者該使用者具有特定 DocumentDB 應用程式資源 （例如集合、 文件）。 如果無法信任處理主要或唯讀金鑰-就像一般使用者應用程式，類似行動或桌面用戶端 hello 用戶端，永遠使用 DocumentDB 資源語彙基元 tooaccess hello。使用主要金鑰或從後端應用程式可以安全地儲存這些金鑰的唯讀機碼。|

## <a id="grained-rbac"></a>啟用更細緻的存取權管理 tooAzure 訂用帳戶使用 RBAC

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 信任邊界 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [使用角色指派 toomanage 存取 tooyour Azure 訂用帳戶資源](https://azure.microsoft.com/documentation/articles/role-based-access-control-configure/)  |
| **步驟** | Azure 角色型存取控制 (RBAC) 可以對 Azure 進行更細緻的存取權管理。 使用 RBAC 時，您可以授與只 hello 少量的存取權，使用者需要 tooperform 他們的工作。|

## <a id="cluster-rbac"></a>限制用戶端存取 toocluster 作業使用 RBAC

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Service Fabric 信任邊界 | 
| **SDL 階段**               | 部署 |  
| **適用的技術** | 泛型 |
| **屬性**              | 環境 - Azure |
| **參考**              | [Service Fabric 用戶端的角色型存取控制](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security-roles/) |
| **步驟** | <p>Azure Service Fabric 支援兩種不同的存取控制類型的用戶端的連線的 tooa Service Fabric 叢集： 系統管理員和使用者。 存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。</p><p>系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。</p><p>您指定 hello 兩個用戶端角色 （系統管理員和用戶端），您可以在 hello 階段建立叢集的每個提供不同的憑證。</p>|

## <a id="modeling-field"></a>執行安全性模型化並視需要使用欄位層級安全性

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 執行安全性模型化並視需要使用欄位層級安全性|

## <a id="portal-security"></a>執行 記住這個 hello 安全性模型中的 hello 入口網站與不同於 CRM hello 其餘部分的帳戶入口網站的安全性模型

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Dynamics CRM 入口網站 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | 執行 記住這個 hello 安全性模型中的 hello 入口網站與不同於 CRM hello 其餘部分的帳戶入口網站的安全性模型|

## <a id="permission-entities"></a>在 Azure 表格儲存體中授與某個實體範圍的精細權限

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | StorageType - 資料表 |
| **參考**              | [Toodelegate 存取 tooobjects 使用 SAS Azure 儲存體帳戶中的方式](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_data-plane-security) |
| **步驟** | 在特定商務案例中，Azure 資料表儲存體可能需要的 toostore 皆代表 toodifferent 合作對象的機密資料。 例如，敏感資料與有關 toodifferent 國家 （地區）。 在這種情況下，SAS 簽章可以建構藉由指定 hello 磁碟分割和資料列的索引鍵範圍，以便使用者可以存取資料特定 tooa 特定國家/地區。| 

## <a id="rbac-azure-manager"></a>啟用使用 Azure 資源管理員的角色型存取控制 (RBAC) tooAzure 儲存體帳戶

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Azure 儲存體 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | [如何 toosecure 您的儲存體帳戶使用角色型存取控制 (RBAC)](https://azure.microsoft.com/documentation/articles/storage-security-guide/#management-plane-security) |
| **步驟** | <p>當您建立新的儲存體帳戶時，可以選取傳統或 Azure Resource Manager 的部署模型。 在 Azure 中建立資源的 hello 傳統模式只允許想到存取 toohello 訂用帳戶和依次 hello 儲存體帳戶。</p><p>使用 hello Azure Resource Manager 模型時，您可以將 hello 儲存體帳戶資源群組和控制存取 toohello 管理平面中的該特定的儲存體帳戶，使用 Azure Active Directory。 例如，您可以提供特定使用者 hello 能力 tooaccess hello 儲存體帳戶金鑰，而其他使用者可以檢視 hello 儲存體帳戶資訊，但無法存取 hello 儲存體帳戶金鑰。</p>|

## <a id="rooting-detection"></a>實作隱含的越獄或 Root 權限入侵偵測

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | 行動用戶端 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>如果電話遭到 Root 權限或越獄入侵，應用程式應保護其本身的組態和使用者資料。 Root 權限/越獄入侵意味著未經授權的存取，一般使用者不會在自己的電話上這麼做。 因此應用程式應該在應用程式啟動時，如果已進行 root 破解 hello 電話 toodetect 具有隱含的偵測邏輯。</p><p>hello 偵測邏輯可以直接存取的檔案通常只有根使用者可以存取，例如：</p><ul><li>/system/app/Superuser.apk</li><li>/sbin/su</li><li>/system/bin/su</li><li>/system/xbin/su</li><li>/data/local/xbin/su</li><li>/data/local/bin/su</li><li>/system/sd/xbin/su</li><li>/system/bin/failsafe/su</li><li>/data/local/su</li></ul><p>如果 hello 應用程式可以存取這些檔案，它代表 hello 應用程式以根使用者身分執行。</p>|

## <a id="weak-class-wcf"></a>WCF 中的弱式類別參考

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | <p>hello 系統會使用弱式的類別參考，可能會讓攻擊者 tooexecute 未經授權的程式碼。 hello 程式會參考不唯一識別使用者定義的類別。 當.NET 載入這個弱式識別的類別，在下列位置中 hello hello hello 類別 hello CLR 型別載入器搜尋指定順序：</p><ol><li>如果已知 hello hello 類型組件，hello 載入器搜尋 hello 組態檔重新導向位置、 GAC、 hello 目前組件的組態資訊和 hello 應用程式基底目錄</li><li>Hello 載入器搜尋的 hello hello 組件為未知，如果目前組件、 mscorlib 和 hello hello TypeResolve 事件處理常式所傳回的位置</li><li>這個 CLR 搜尋順序可以修改 hello 型別轉送機制等攔截程序與 hello AppDomain.TypeResolve 事件</li></ol><p>如果攻擊者利用 hello CLR 搜尋順序，藉由建立具有的替代類別 hello 相同名稱，並將其置於其他位置 CLR 會先載入該 hello、 hello CLR 會不小心執行 hello 攻擊者提供的程式碼</p>|

### <a name="example"></a>範例
hello `<behaviorExtensions/>` hello 底下的 WCF 組態檔項目會指示 WCF tooadd 自訂行為類別 tooa 特定 WCF 延伸模組。
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""MyBehavior"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```
使用完整 (強式) 名稱來唯一識別類型，可進一步提高您系統的安全性。 Hello machine.config 與 app.config 檔中註冊型別時，請使用完整組件名稱。

### <a name="example"></a>範例
hello `<behaviorExtensions/>` hello 底下的 WCF 組態檔項目會指示 WCF tooadd 強式參考自訂行為類別 tooa 特定 WCF 延伸模組。
```
<system.serviceModel>
    <extensions>
        <behaviorExtensions>
            <add name=""myBehavior"" type=""Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,
            Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"" />
        </behaviorExtensions>
    </extensions>
</system.serviceModel>
```

## <a id="wcf-authz"></a>WCF 實作授權控制

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | WCF | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、NET Framework 3 |
| **屬性**              | N/A  |
| **參考**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx)、[Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **步驟** | <p>此服務並不會使用授權控制。 當用戶端會呼叫特定的 WCF 服務時，WCF 會提供各種授權配置來確認該 hello 呼叫端在 hello 伺服器上具有權限 tooexecute hello 服務方法。 如果未針對 WCF 服務啟用授權控制，經過驗證的使用者可以獲得權限提升。</p>|

### <a name="example"></a>範例
下列組態的 hello 執行 hello 服務時，會指示 WCF toonot 核取 hello 授權層級的 hello 用戶端：
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""None"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
使用服務授權配置 tooverify hello hello 服務方法的呼叫端，因此是授權的 toodo。 WCF 提供兩種模式，並允許 hello 定義的自訂授權配置。 hello UseWindowsGroups 模式會使用 Windows 角色和使用者和 hello UseAspNetRoles 模式會使用 ASP.NET 角色提供者，例如 SQL Server，tooauthenticate。

### <a name="example"></a>範例
hello 下列組態會指示 WCF toomake 確定該 hello 用戶端 hello Administrators 群組的一部分執行 hello 新增服務之前：
```
<behaviors>
    <serviceBehaviors>
        <behavior>
            ...
            <serviceAuthorization principalPermissionMode=""UseWindowsGroups"" />
        </behavior>
    </serviceBehaviors>
</behaviors>
```
hello 服務然後宣告為 hello 下列：
```
[PrincipalPermission(SecurityAction.Demand,
Role = ""Builtin\\Administrators"")]
public double Add(double n1, double n2)
{
double result = n1 + n2;
return result;
}
```

## <a id="authz-aspnet"></a>在 ASP.NET Web API 中實作適當的授權機制

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | Web API | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型、MVC5 |
| **屬性**              | N/A、識別提供者 - ADFS、識別提供者 - Azure AD |
| **參考**              | [ASP.NET Web API 中的驗證與授權](http://www.asp.net/web-api/overview/security/authentication-and-authorization-in-aspnet-web-api) |
| **步驟** | <p>Hello 應用程式使用者的角色資訊可以從 Azure AD 或 ADFS 宣告如果 hello 應用程式身分識別提供者依賴它們或 hello 應用程式本身可能會提供它。 在上述任一情況，hello 自訂授權實作應該驗證 hello 的使用者角色資訊。</p><p>Hello 應用程式使用者的角色資訊可以從 Azure AD 或 ADFS 宣告如果 hello 應用程式身分識別提供者依賴它們或 hello 應用程式本身可能會提供它。 在上述任一情況，hello 自訂授權實作應該驗證 hello 的使用者角色資訊。</p>

### <a name="example"></a>範例
```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
public class ApiAuthorizeAttribute : System.Web.Http.AuthorizeAttribute
{
        public async override Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            if (actionContext == null)
            {
                throw new Exception();
            }

            if (!string.IsNullOrEmpty(base.Roles))
            {
                bool isAuthorized = ValidateRoles(actionContext);
                if (!isAuthorized)
                {
                    HandleUnauthorizedRequest(actionContext);
                }
            }

            base.OnAuthorization(actionContext);
        }

public bool ValidateRoles(actionContext)
{
   //Authorization logic here; returns true or false
}

}
```
所有 hello 控制器和動作方法需要 tooprotected 應該可以使用裝飾屬性上方。
```C#
[ApiAuthorize]
public class CustomController : ApiController
{
     //Application code goes here
}
```

## <a id="device-permission"></a>在 hello 裝置執行授權檢查，如果支援需要不同的權限層級的各種動作

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 裝置 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | <p>裝置 hello 應該授權 hello 呼叫端 toocheck hello 呼叫端是否要求 hello 所需的權限 tooperform hello 動作。 例如讓假設 hello 裝置是可從 hello 雲端監視 Smart 門 Lock 加上它提供功能，例如從遠端鎖定 hello 媒體櫃門。</p><p>hello 智慧門鎖定在有人實際隨附附近 hello 門卡片時，才提供解除鎖定功能。 在此情況下，hello hello 遠端命令和控制項的實作應該完成的方式，它不提供任何功能 toounlock hello 門因為 hello 雲端閘道無法授權的 toosend 命令 toounlock hello 媒體櫃門。</p>|

## <a id="field-permission"></a>執行授權檢查 hello 閘道欄位中，如果支援需要不同的權限層級的各種動作

| Title                   | 詳細資料      |
| ----------------------- | ------------ |
| **元件**               | IoT 現場閘道 | 
| **SDL 階段**               | 建置 |  
| **適用的技術** | 泛型 |
| **屬性**              | N/A  |
| **參考**              | N/A  |
| **步驟** | hello 欄位閘道應該授權 hello 呼叫端 toocheck hello 呼叫端是否要求 hello 所需的權限 tooperform hello 動作。 例如有應該是不同的權限的系統管理員使用者介面/API 使用 tooconfigure 連接 tooit 欄位閘道 v/s 的裝置。|
