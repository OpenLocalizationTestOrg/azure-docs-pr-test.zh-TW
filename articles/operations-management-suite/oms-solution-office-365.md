---
title: "aaaOffice 365 方案 Operations Management Suite (OMS) |Microsoft 文件"
description: "這篇文章提供設定及使用 OMS 中的 hello Office 365 方案的詳細資料。  它包含記錄分析中建立的 Office 365 hello 記錄的詳細的的描述。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: bwren
ms.openlocfilehash: a1507745251ff015abb785bae8352fea7cea0734
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-solution-in-operations-management-suite-oms"></a>Operations Management Suite (OMS) 中的 Office 365 解決方案

![Office 365 標誌](media/oms-solution-office-365/icon.png)

hello Office 365 方案 Operations Management Suite (OMS) 可讓您 toomonitor Office 365 環境中記錄分析。  

- 監視使用者活動，在 Office 365 帳戶 tooanalyze 使用模式，以及識別趨勢，行為。 例如，您可以擷取特定使用案例，例如檔案共用之外，您的組織或 hello 最受歡迎的 SharePoint 網站。
- 監視系統管理員活動 tootrack 組態變更或極高權限作業。
- 偵測並調查的不必要的使用者行為，並可以針對貴組織的需求進行自訂。
- 示範稽核與合規性。 例如，您可以監視機密檔案，可協助您進行 hello 稽核和規範程序上的檔案存取作業。
- 針對組織的 Office 365 活動資料使用 OMS 搜尋，執行作業疑難排解。

## <a name="prerequisites"></a>必要條件
hello 以下是必要的先前 toothis 方案正在安裝和設定。

- 組織的 Office 365 訂閱。
- 全域管理員的使用者帳戶認證。
- tooreceive 稽核資料，您必須[設定稽核](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&rs=en-US&ad=US#PickTab=Before_you_begin)您 Office 365 訂用帳戶中。  請注意，[信箱稽核](https://technet.microsoft.com/library/dn879651.aspx) \(機器翻譯\) 需要另行設定。  您仍然可以安裝 hello 方案，並收集其他資料，如果未設定稽核。
 


## <a name="management-packs"></a>管理組件
此解決方案不會在已連線的管理群組中安裝任何管理組件。
  

## <a name="configuration"></a>組態
一旦您[新增 hello Office 365 方案 tooyour 訂閱](../log-analytics/log-analytics-add-solutions.md)，您有 tooconnect 它 tooyour Office 365 訂用帳戶。

1. 新增使用 hello 程序的 OMS 工作區中所述的 hello 警示管理解決方案 tooyour[新增解決方案](../log-analytics/log-analytics-add-solutions.md)。
2. 跳過**設定**hello OMS 入口網站中。
3. 在 [連接的來源] 下，選取 [Office 365]。
4. 按一下 [連線至 Office 365]。<br>![連線至 Office 365](media/oms-solution-office-365/configure.png)
5. 登入 tooOffice 365 與您訂用帳戶的全域系統管理員帳戶。 
6. hello 訂用帳戶將會列出與 hello hello 解決方案將監視的工作負載。<br>![連線至 Office 365](media/oms-solution-office-365/connected.png) 


## <a name="data-collection"></a>資料收集
### <a name="supported-agents"></a>支援的代理程式
hello Office 365 方案不會擷取資料，從任何 hello [OMS 代理程式](../log-analytics/log-analytics-data-sources.md)。  它會直接從 Office 365 擷取資料。

### <a name="collection-frequency"></a>收集頻率
Office 365 傳送[webhook 通知](https://msdn.microsoft.com/office-365/office-365-management-activity-api-reference#receiving-notifications)與詳細的資料 tooLog 分析每次建立的記錄。

## <a name="using-hello-solution"></a>使用 hello 解決方案
當您新增 hello Office 365 方案 tooyour OMS 工作區時，hello **Office 365**磚加入 tooyour OMS 儀表板。 此磚會顯示在您的環境和其更新相容性的計數與 hello 電腦數目的圖形表示。<br><br>
![Office 365 摘要圖格](media/oms-solution-office-365/tile.png)  

按一下 hello **Office 365**磚 tooopen hello **Office 365**儀表板。

![Office 365 儀表板](media/oms-solution-office-365/dashboard.png)  

hello 儀表板會納入 hello 下表中的 hello 資料行。 每個資料行列出 hello 前十個警示計數比對資料行的準則 hello 指定領域和時間範圍。 您可以執行方法是按一下 hello hello 欄最底端的所有項目，請參閱或 hello 資料行標頭，即可提供 hello 整個清單的記錄搜尋。

| 資料欄 | 說明 |
|:--|:--|
| 作業 | 從所有受監視 Office 365 訂用帳戶的作用中使用者提供 hello 的相關資訊。 您也會經過一段時間，就可能發生的活動可以 toosee hello 數目。
| Exchange | 顯示 Exchange Server 的活動，例如新增信箱權限或 Set-mailbox hello 細目。 |
| SharePoint | 使用者執行 SharePoint 文件上會顯示 hello 最上層活動。 當您向下鑽研此磚，從 hello [搜尋] 頁面會顯示 hello 這些活動，例如 hello 目標文件和 hello 位置，此活動的詳細資料。 比方說，檔案存取事件，您就是可以 toosee hello 文件正在存取，其相關聯的帳戶名稱和 IP 位址。 |
| Azure Active Directory | 包含熱門使用者活動，例如「重設使用者密碼」和「登入嘗試」。 當您向下鑽研時，您將無法像 hello 結果狀態，這些活動可以 toosee hello 詳細資料。 這而言非常有幫助您在 Azure Active Directory 想 toomonitor 可疑活動。 |




## <a name="log-analytics-records"></a>Log Analytics 記錄

在 hello 記錄分析工作區中建立 hello Office 365 方案的所有記錄都有**類型**的**OfficeActivity**。  hello **OfficeWorkload**屬性會決定哪個 Office 365 服務的 hello 記錄是指太 Exchange、 AzureActiveDirectory、 SharePoint 或 OneDrive。  hello **RecordType**屬性指定之作業的 hello 類型。  hello 屬性每個作業類型而異，並顯示 hello 表中。

### <a name="common-properties"></a>通用屬性
下列屬性的 hello 屬於常見的 tooall Office 365 記錄。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 | *OfficeActivity* |
| ClientIP | hello hello 裝置 hello 活動記錄時所使用的 IP 位址。 在 IPv4 或 IPv6 位址的格式會顯示 hello IP 位址。 |
| OfficeWorkload | Hello 記錄指的是 office 365 服務。<br><br>AzureActiveDirectory<br>Exchange<br>SharePoint|
| 作業 | hello hello 使用者或系統管理員的活動名稱。  |
| OrganizationId | hello 貴組織的 Office 365 租用戶的 GUID。 這個值會一律是 hello 相同為您的組織，不論 hello Office 365 服務中發生。 |
| RecordType | 執行之作業的類型。 |
| ResultStatus | 指出 hello 動作 (指定在 hello 作業屬性) 是否已成功。 可能的值為 Succeeded、PartiallySucceded 或 Failed。 Exchange 系統管理員的活動，hello 值為 True 或 False。 |
| UserId | hello 執行導致記錄; hello 記錄的 hello 動作的 hello 使用者的 UPN （使用者主體名稱）例如， my_name@my_domain_name。 請注意，由系統帳戶 (例如 SHAREPOINT\system 或 NTAUTHORITY\SYSTEM) 所執行之活動的記錄也會包含在內。 | 
| UserKey | 替代 hello hello UserId 屬性中所識別的使用者識別碼。  例如，這個屬性會填入針對商務和 Exchange SharePoint、 OneDrive 中的使用者所執行的事件 hello passport 唯一識別碼 (PUID)。 這個屬性也可以指定的 hello 與 hello UserID 屬性中的其他服務和事件發生的事件相同的值執行的系統帳戶|
| UserType | hello hello 作業的使用者類型。<br><br>Admin<br>Application<br>DcAdmin<br>Regular<br>Reserved<br>ServicePrincipal<br>System |


### <a name="azure-active-directory-base"></a>Azure Active Directory 基底
下列屬性的 hello 屬於常見的 tooall Azure Active Directory 記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AzureActiveDirectory_EventType | Azure AD 事件 hello 型別。 |
| ExtendedProperties | hello 擴充事件 hello Azure AD 的屬性。 |


### <a name="azure-active-directory-account-logon"></a>Azure Active Directory 帳戶登入
Active Directory 使用者嘗試 toolog 上時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectoryAccountLogon |
| 應用程式 | 觸發程序 hello 帳戶登入事件，例如 Office 15 的 hello 應用程式。 |
| 用戶端 | 詳細 hello 用戶端裝置、 裝置作業系統和用於 hello hello 帳戶登入事件的裝置瀏覽器。 |
| LoginStatus | 此屬性直接來自 OrgIdLogon.LoginStatus。 無法執行的各種有趣的登入失敗的 hello 對應，藉由變更演算法。 |
| UserDomain | hello 租用戶身分識別資訊 (TII)。 | 


### <a name="azure-active-directory"></a>Azure Active Directory
變更或新增項目進行 tooAzure Active Directory 物件時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | AzureActiveDirectory |
| RecordType     | AzureActiveDirectory |
| AADTarget | hello hello 動作 （由 hello 作業屬性識別） 執行的使用者。 |
| Actor | hello 使用者或服務主體執行 hello 動作。 |
| ActorContextId | 所屬 hello hello 執行者的 hello 組織的 GUID。 |
| ActorIpAddress | hello 動作項目的 IPV4 或 IPV6 位址格式的 IP 位址。 |
| InterSystemsId | hello 追蹤 hello 動作 hello Office 365 服務中的元件之間的 GUID。 |
| IntraSystemId |   hello Azure Active Directory tootrack hello 動作所產生的 GUID。 |
| SupportTicketId | hello 客戶支援票證識別碼中的"act-代表的 」 情況 hello 動作。 |
| TargetContextId | 所屬 hello hello 目標的使用者的 hello 組織的 GUID。 |


### <a name="data-center-security"></a>資料中心安全性
這些記錄是從資料中心安全性稽核資料所建立。  

| 屬性 | 說明 |
|:--- |:--- |
| EffectiveOrganization | 已針對 hello 的 hello cmdlet 提高權限/hello 租用戶的名稱。 |
| ElevationApprovedTime | hello hello 提高權限時已認可時間戳記。 |
| ElevationApprover | hello Microsoft 管理員名稱。 |
| ElevationDuration | 哪些 hello 權限提高為作用中的 hello 持續時間。 |
| ElevationRequestId |  Hello 提高權限要求唯一識別碼。 |
| ElevationRole | hello 角色 hello 提高權限的要求。 |
| ElevationTime | hello 的開始時間 hello 提高權限。 |
| Start_Time | hello 啟動 hello cmdlet 執行的時間。 |


### <a name="exchange-admin"></a>Exchange 管理員
TooExchange 組態進行變更時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeAdmin |
| ExternalAccess |  指定使用者在您的組織，由 Microsoft 資料中心的人員或資料中心的服務帳戶，或是委派的系統管理員，是否已執行 hello cmdlet。 hello 值 False 表示 hello 指令程式由您組織中有人執行。 hello 值 True 表示 hello 指令程式由資料中心的人員、 資料中心的服務帳戶或委派系統管理員執行。 |
| ModifiedObjectResolvedName |  這是 hello hello 物件 hello 指令程式來修改過的使用者易記名稱。 這會記錄才 hello cmdlet 會修改 hello 物件。 |
| OrganizationName | hello hello 租用戶名稱。 |
| OriginatingServer | 執行 cmdlet，從哪些 hello hello 伺服器 hello 名稱。 |
| 參數 | hello 名稱，以識別 hello 作業屬性中的 hello 指令程式所使用的所有參數的值。 |


### <a name="exchange-mailbox"></a>Exchange 信箱
變更或新增項目進行 tooExchange 信箱時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| ClientInfoString | 已使用的 tooperform hello 作業，例如瀏覽器版本、 Outlook 版本和行動裝置資訊的 hello 電子郵件用戶端的相關資訊。 |
| Client_IPAddress | hello hello 裝置 hello 作業記錄時所使用的 IP 位址。 在 IPv4 或 IPv6 位址的格式會顯示 hello IP 位址。 |
| ClientMachineName | hello 裝載 hello Outlook 用戶端電腦名稱。 |
| ClientProcessName | 已使用的 tooaccess hello 信箱 hello 電子郵件用戶端。 |
| ClientVersion | hello hello 電子郵件用戶端版本。 |
| InternalLogonType | 保留供內部使用。 |
| Logon_Type | 表示使用者存取 hello 信箱，而且作業記錄的 hello hello 類型。 |
| LogonUserDisplayName |    執行 hello 作業的 hello 使用者 hello 易記名稱。 |
| LogonUserSid | hello 作業 hello hello 使用者 SID。 |
| MailboxGuid | hello 存取 hello 信箱的 Exchange GUID。 |
| MailboxOwnerMasterAccountSid | 信箱擁有者帳戶的主要帳戶 SID。 |
| MailboxOwnerSid | hello hello 信箱擁有者的 SID。 |
| MailboxOwnerUPN | hello 擁有 hello 信箱存取的 hello 人員的電子郵件地址。 |


### <a name="exchange-mailbox-audit"></a>Exchange 信箱稽核
這些記錄會在建立信箱稽核項目時建立。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| RecordType     | ExchangeItem |
| Item | 表示已執行作業時的 hello hello 項目 | 
| SendAsUserMailboxGuid | hello GUID hello 信箱的 Exchange 存取以 toosend 傳送電子郵件。 |
| SendAsUserSmtp | SMTP 位址 hello 使用者正被模擬。 |
| SendonBehalfOfUserMailboxGuid | hello GUID hello 信箱的 Exchange 存取代表 toosend 郵件。 |
| SendOnBehalfOfUserSmtp | 會傳送 hello 使用者上代表其 hello 電子郵件的 SMTP 位址。 |


### <a name="exchange-mailbox-audit-group"></a>Exchange 信箱稽核群組
變更或新增項目進行 tooExchange 群組時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | Exchange |
| OfficeWorkload | ExchangeItemGroup |
| AffectedItems | Hello 群組中的每個項目的相關資訊。 |
| CrossMailboxOperations | 指出是否 hello 作業中包含多個信箱。 |
| DestMailboxId | 只有當 hello CrossMailboxOperations 參數為 True 時，才設定。 指定 hello 目標信箱 GUID。 |
| DestMailboxOwnerMasterAccountSid | 只有當 hello CrossMailboxOperations 參數為 True 時，才設定。 指定 hello SID hello 主帳戶 SID hello 目標信箱擁有者。 |
| DestMailboxOwnerSid | 只有當 hello CrossMailboxOperations 參數為 True 時，才設定。 指定 hello hello 目標信箱的 SID。 |
| DestMailboxOwnerUPN | 只有當 hello CrossMailboxOperations 參數為 True 時，才設定。 指定 hello hello hello 目標信箱擁有者的 UPN。 |
| DestFolder | hello 目的地資料夾，例如移動作業。 |
| 資料夾 | hello 一組項目所在的資料夾。 |
| 資料夾 |     操作; 中的 hello 來源資料夾的相關資訊例如，如果資料夾都是選取，然後刪除。 |


### <a name="sharepoint-base"></a>SharePoint 基底
這些屬性是一般 tooall SharePoint 記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| EventSource | 識別事件在 SharePoint 中發生。 可能的值為 SharePoint 或 ObjectModel。 |
| ItemType | hello 的存取或修改的物件類型。 請參閱 hello ItemType hello 類型的物件上的詳細資料的資料表。 |
| MachineDomainInfo | 裝置同步作業的相關資訊。 只有當 hello 要求中存在這項資訊報告。 |
| MachineId |   裝置同步作業的相關資訊。 只有當 hello 要求中存在這項資訊報告。 |
| Site_ | hello hello hello 檔案或資料夾 hello 使用者存取的所在位置的站台的 GUID。 |
| Source_Name | 觸發 hello hello 實體稽核作業。 可能的值為 SharePoint 或 ObjectModel。 |
| UserAgent | Hello 使用者的瀏覽器或用戶端的相關資訊。 這項資訊是由 hello 用戶端或瀏覽器提供。 |


### <a name="sharepoint-schema"></a>SharePoint 結構描述
TooSharePoint 進行組態變更時，會建立這些記錄。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePoint |
| CustomEvent | 自訂事件的選擇性字串。 |
| Event_Data |  自訂事件的選擇性承載。 |
| ModifiedProperties | hello 屬性包含管理事件，例如將使用者新增為網站或網站集合管理員群組的成員。 hello 屬性包括 hello hello hello 新 hello 的值修改屬性 （這類 hello 新增的使用者以站台系統管理員），而且 hello 先前 hello 的值修改物件 （例如 hello 站台系統管理員群組），已修改的屬性名稱。 |


### <a name="sharepoint-file-operations"></a>SharePoint 檔案作業
這些記錄會在回應 toofile 作業，在 SharePoint 中建立。

| 屬性 | 說明 |
|:--- |:--- |
| OfficeWorkload | SharePoint |
| OfficeWorkload | SharePointFileOperation |
| DestinationFileExtension | hello 副檔名的檔案複製或移動。 此屬性僅針對 FileCopied 和 FileMoved 事件顯示。 |
| DestinationFileName | hello hello 複製或移動的檔案名稱。 此屬性僅針對 FileCopied 和 FileMoved 事件顯示。 |
| DestinationRelativeUrl | hello hello 目的資料夾，複製或移動檔案位置的 URL。 hello hello SiteURL、 DestinationRelativeURL 和 DestinationFileName 參數值組合是 hello 與 hello hello ObjectID 屬性，這是 hello 已複製的 hello 檔案的完整路徑名稱的值相同。 此屬性僅針對 FileCopied 和 FileMoved 事件顯示。 |
| SharingType | hello 類型共用指派 toohello 使用者 hello 資源共用與權限。 此使用者是 hello UserSharedWith 參數所識別。 |
| Site_Url | hello hello 檔案或資料夾 hello 使用者存取的所在位置的 hello 網站 URL。 |
| SourceFileExtension | hello 檔案副檔名 hello hello 使用者存取。 這個屬性是空白如果 hello 物件存取的資料夾。 |
| SourceFileName |  hello hello 檔案或資料夾的名稱 hello 使用者存取。 |
| SourceRelativeUrl | hello hello 資料夾包含 hello 檔案 hello 使用者存取的 URL。 hello hello hello SiteURL、 SourceRelativeURL 和 SourceFileName 參數值組合是 hello 與 hello hello ObjectID 屬性，這是 hello hello 使用者所存取的 hello 檔案的完整路徑名稱的值相同。 |
| UserSharedWith |  hello 與共用資源的使用者。 |




## <a name="sample-log-searches"></a>記錄檔搜尋範例
下表中的 hello 提供範例記錄檔搜尋更新這個解決方案所收集的記錄。

| 查詢 | 說明 |
| --- | --- |
|Office 365 訂用帳戶上的所有 hello 作業的計數 |`Type = OfficeActivity | measure count() by Operation` |
|SharePoint 網站的使用情況|`Type=OfficeActivity OfficeWorkload=sharepoint | measure count() as Count by SiteUrl | sort Count asc`|
|依使用者類型分類的檔案存取作業|`Type=OfficeActivity OfficeWorkload=sharepoint Operation=FileAccessed | measure count() by UserType`|
|使用特定關鍵字進行搜尋|`Type=OfficeActivity OfficeWorkload=azureactivedirectory "MyTest"`|
|監視 Exchange 上的外部動作|`Type=OfficeActivity OfficeWorkload=exchange ExternalAccess = true`|



## <a name="troubleshooting"></a>疑難排解

如果您的 Office 365 方案不會收集資料，如預期般，檢查其狀態在 hello OMS 入口網站**設定** -> **連線來源** -> **Office 365**. hello 下表描述每個狀態。

| 狀態 | 說明 |
|:--|:--|
| Active | hello Office 365 訂閱為作用中和 hello 工作負載是已成功連接的 tooyour OMS 工作區。 |
| Pending | hello Office 365 訂閱為作用中，但不是 hello 工作負載，但已成功連接 tooyour OMS 工作區。 hello 第一次連線 hello Office 365 訂用帳戶，所有的 hello 工作負載會在這個狀態直到它們成功連線。 請等待 24 小時，讓所有 hello 工作負載 tooswitch tooActive。 |
| 非使用中 | hello Office 365 訂用帳戶處於非作用中狀態。 請查看 Office 365 管理員頁面以取得詳細資料。 啟用 Office 365 訂用帳戶之後，取消其連結從 OMS 工作區，並連結到再次 toostart 接收資料。 |



## <a name="next-steps"></a>後續步驟
* 使用中的記錄搜尋[記錄分析](../log-analytics/log-analytics-log-searches.md)tooview 詳細的更新資料。
* [建立您自己的儀表板](../log-analytics/log-analytics-dashboards.md)toodisplay 您最喜愛的 Office 365 的搜尋查詢。
* [建立警示](../log-analytics/log-analytics-alerts.md)toobe 主動的重要的 Office 365 活動收到通知。  
