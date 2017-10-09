---
title: "aaaFix SQL 連線錯誤，暫時性錯誤 |Microsoft 文件"
description: "了解 tootroubleshoot、 診斷及避免 SQL 連接錯誤，或是 Azure SQL Database 中的暫時性錯誤的方式。 "
keywords: "sql 連接, 連接字串, 連接問題, 暫時性錯誤, 連接錯誤"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>排解、診斷和防止 SQL Database 的 SQL 連接錯誤和暫時性錯誤
本文說明 tooprevent、 疑難排解、 診斷和減少連接錯誤及用戶端應用程式在它與 Azure SQL Database 互動時所發生的暫時性錯誤的方式。 了解 tooconfigure 如何重試邏輯，建立 hello 連接字串，以及調整其他連線設定。

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>暫時性錯誤 (暫時性故障)
暫時性錯誤 (又稱暫時性故障) 具有很快就會自行解決的根本原因。 暫時性錯誤的可能偶爾的原因是 hello Azure 系統快速切換硬體資源 toobetter 負載平衡各種工作負載時。 其中大部分重新設定事件通常會在不到 60 秒內完成。 在此重新設定時間範圍內，您可能有連線問題 tooAzure SQL 資料庫。 建立應用程式連接 SQL 資料庫應位於的 tooAzure tooexpect 這些暫時性錯誤，其藉由實作重試邏輯，而不是面對它們做為應用程式錯誤 toousers 標定程式碼中的控制代碼。

如果您的用戶端程式使用 ADO.NET，程式就會通知有關 hello 暫時性錯誤 hello 擲回由**SqlException**。 hello**數目**屬性可以針對 hello hello hello 主題頂端附近的暫時性錯誤清單進行比較： [SQL 資料庫用戶端應用程式的 SQL 錯誤代碼，](sql-database-develop-error-messages.md)。

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>連接與命令
您將 hello SQL 連接重試一次或一次，根據 hello 下列建立：

* **連接嘗試期間，發生暫時性錯誤**: hello 連接應該重試後幾秒鐘的延遲。
* **SQL 查詢命令期間，發生暫時性錯誤**: hello 命令應該不會立即重試。 相反地的延遲之後，hello 應該重新建立連線。 然後可以重試 hello 命令。

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>暫時性錯誤的重試邏輯
用戶端程式若包含重試邏輯，在偶爾遇到暫時性錯誤時就會更可靠。

您的程式通訊時使用 Azure SQL Database 透過第 3 個合作對象的中介軟體，查詢與 hello 廠商是否 hello 中介軟體中包含的暫時性錯誤重試邏輯。

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>重試原則
* 如果 hello 錯誤是暫時性，應該重試嘗試 tooopen 連接。
* 不應該直接重試由於暫時性錯誤而失敗的 SQL SELECT 陳述式。
  
  * 相反地，建立全新的連線，然後再重試 hello 選取。
* 當 SQL UPDATE 陳述式失敗，發生暫時性的錯誤時，應該在重試更新的 hello 之前先建立全新的連接。
  
  * hello 重試邏輯必須確保 hello 整個資料庫的交易完成或該 hello 整個異動會復原。

#### <a name="other-considerations-for-retry"></a>其他重試考量
* 批次程式上班時間之後自動啟動的且它會先完成早上，能夠負擔 toovery 病患和長時間間隔之間的重試次數。
* 使用者介面程式應該考量 hello 傾向 toogive 向上之後等候太長。
  
  * 不過，hello 方案不能 tooretry 每幾秒鐘，因為該原則可以填滿 hello 系統的要求。

#### <a name="interval-increase-between-retries"></a>增加重試之間的間隔
我們建議您在您第一次重試前延遲 5 秒鐘。 少於 5 秒的延遲之後重試風險非常龐大的 hello 雲端服務。 每個後續的重試 hello 延遲應該指數成長，向上 tooa 60 秒的最大值。

討論的 hello*封鎖期間*使用 ADO.NET 的用戶端會提供[SQL Server 連接共用 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)。

Hello 程式自我終止之前，您可能也想 tooset 重試次數上限。

#### <a name="code-samples-with-retry-logic"></a>具有重試邏輯的程式碼範例
各種程式設計語言中具有重試邏輯的程式碼範例位於：

* [SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>測試您的重試邏輯
tootest 重試邏輯，您必須模擬或非可以更正錯誤，您的程式仍在執行時，會導致錯誤。

##### <a name="test-by-disconnecting-from-hello-network"></a>測試 hello 網路連線中斷
您可以測試重試邏輯的一個方式是的 toodisconnect hello 程式執行時，用戶端電腦從 hello 網路。 hello 錯誤為：

* **SqlException.Number** = 11001
* 訊息：「未知的主機」

Hello 一部分第一次重試嘗試，因為您的程式就可以修正 hello 拼字錯誤，，，然後嘗試 tooconnect。

這個實用 toomake 您拔下從 hello 網路電腦之前啟動您的程式。 然後您的程式會辨識造成 hello 程式的執行的階段參數：

1. 暫時將錯誤 tooconsider 11001 tooits 清單新增為暫時性。
2. 如往常般嘗試其第一個連接。
3. 會攔截 hello 錯誤之後，請從 hello 清單移除 11001。
4. 顯示一則訊息告訴 hello 使用者 tooplug hello 電腦進入 hello 網路。
   * 使用任一個 hello 暫停進一步執行**Console.ReadLine**方法或具有 [確定] 按鈕的對話方塊。 hello 電腦插入 hello 網路之後，hello 使用者按下 hello Enter 鍵。
5. 嘗試再次 tooconnect，必須成功。

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>連線時以測試拼字錯誤 hello 資料庫名稱
您的程式可以刻意拼錯 hello hello 第一次連接嘗試之前的使用者名稱。 hello 錯誤為：

* **SqlException.Number** = 18456
* 錯誤將為：「使用者 'WRONG_MyUserName' 登入失敗。」

Hello 一部分第一次重試嘗試，因為您的程式就可以修正 hello 拼字錯誤，，，然後嘗試 tooconnect。

這個實用 toomake，您的程式無法辨識造成 hello 程式的執行的階段參數：

1. 暫時將錯誤 tooconsider 18456 tooits 清單新增為暫時性。
2. 刻意新增 'WRONG_' toohello 使用者名稱。
3. 會攔截 hello 錯誤之後，請從 hello 清單移除 18456。
4. 請移除 'WRONG_' hello 使用者名稱中。
5. 嘗試再次 tooconnect，必須成功。

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>進行連線重試的.NET SqlConnection 參數
如果用戶端程式 tootooAzure SQL Database 會使用連接 hello.NET Framework 類別**System.Data.SqlClient.SqlConnection**，您應該使用.NET 4.6.1 或更新版本 （或.NET Core） 讓您可以利用其連接重試功能。 Hello 功能的詳細資料會[這裡](http://go.microsoft.com/fwlink/?linkid=393996)。

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


當您建置 hello[連接字串](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx)如您**SqlConnection**物件，您應該協調 hello 值之間 hello 下列參數：

* ConnectRetryCount &nbsp;&nbsp;*(預設值為 1。範圍是 0 到 255)。*
* ConnectRetryInterval &nbsp;&nbsp;*(預設值為 1 秒。範圍是 1 到 60)。*
* Connection Timeout &nbsp;&nbsp;*(預設值為 15 秒。範圍是 0 到 2147483647)*

具體來說，您所選擇的值應該做下列等號比較為 true 的 hello:

* Connection Timeout = ConnectRetryCount * ConnectionRetryInterval

例如，如果 hello 計數 = 3，且間隔 = 10 秒，逾時，只有 29 秒可能不完全賦予 hello 系統足夠的時間進行連線時的第 3 個和最後一個重試： 29 < 3 * 10。

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>連接與命令
hello **ConnectRetryCount**和**ConnectRetryInterval**參數可讓您**SqlConnection**物件重試 hello 連線作業而不需要通知或終究您程式，例如傳回 tooyour 控制程式。 hello 重試可能會發生下列情況下的 hello:

* mySqlConnection.Open 方法呼叫
* mySqlConnection.Execute 方法呼叫

有一些微妙的差異。 如果發生暫時性錯誤時您*查詢*正在執行，您**SqlConnection**物件不重試 hello 是否連接作業，與它一定不會重試您的查詢。 不過， **SqlConnection**非常快速地檢查 hello 傳送您的查詢執行之前的連接。 如果 hello 快速檢查偵測到的連線問題， **SqlConnection**重試 hello 連接作業。 如果 hello 重試成功，您的查詢會傳送給執行中。

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>是否應該將 ConnectRetryCount 與應用程式重試邏輯結合？
假設您的應用程式有健全的自訂重試邏輯。 它可能會重試 hello 4 次的連線作業。 如果您將加入**ConnectRetryInterval**和**ConnectRetryCount** = 3 tooyour 連接字串中，您會增加 hello 重試計數 too4 * 3 = 12 重試。 您可能不會想要這麼多的重試次數。

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>連線 tooAzure SQL 資料庫
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>連接：連接字串
hello 連接字串連接 tooAzure 需要 SQL Database 是從連接 SQL Server tooMicrosoft hello 字串稍有不同。 您可以為您的資料庫複製 hello 連接字串從 hello [Azure 入口網站](https://portal.azure.com/)。

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>連接：IP 位址
您必須設定 hello SQL Database 伺服器 tooaccept 通訊 hello IP 位址從 hello 裝載電腦的用戶端程式。 您可以編輯 hello 防火牆設定，透過 hello [Azure 入口網站](https://portal.azure.com/)。

如果您忘記 tooconfigure hello IP 位址，您的程式會失敗並方便的錯誤訊息，指出 hello 所需的 IP 位址。

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

如需詳細資訊，請參閱： [作法：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>連接：連接埠
通常您只需要 tooensure 通訊埠 1433年是供 hello 裝載您的用戶端程式的電腦上的連出通訊開啟。

例如，若當用戶端程式裝載在 Windows 電腦上，hello 主機上的 Windows 防火牆 hello 可讓您 tooopen 通訊埠 1433年:

1. 開啟控制台 hello
2. &gt;所有控制台項目
3. &gt;Windows 防火牆
4. &gt;進階設定
5. &gt; 輸出規則
6. &gt;動作
7. &gt;新增規則

如果您的用戶端程式裝載在 Azure 虛擬機器 (VM) 上，您應該閱讀：<br/>[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)。

如需設定連接埠及 IP 位址的背景資訊，請參閱： [Azure SQL Database 防火牆](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>連接：ADO.NET 4.6.1
如果您的程式使用 ADO.NET 類別，例如**System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL 資料庫，建議您先使用.NET Framework 4.6.1 版或更高版本。

ADO.NET 4.6.1：

* Azure SQL database，沒有可靠性當開啟連接時使用 hello **SqlConnection.Open**方法。 hello**開啟**方法現已加入最佳投入時間的重試機制回應 tootransient 錯誤中的 hello 連接逾時期間內的特定錯誤。
* 支援連接共用。 這包括 hello 連接有效驗證物件，它可讓您的程式是否正常運作。

當您從連接集區使用的連接物件時，我們建議您的程式暫時關閉 hello 連線時不會立即使用它。 重新開啟連接不是高成本 hello 方法建立新的連接是。

如果您使用 ADO.NET 4.0 或更早版本，我們建議您升級 toohello 最新的 ADO.NET。

* 從 2015 年 11 月開始，您可以 [下載 ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)。

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>診斷
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>診斷：測試公用程式是否可以連接
如果您的程式無法 tooconnect tooAzure SQL 資料庫，一個診斷的選項會是 tootry tooconnect 與公用程式。 在理想情況下 hello 公用程式會使用連接 hello 程式所使用的相同文件庫。

您可以在任何 Windows 電腦上，嘗試這些公用程式：

* SQL Server Management Studio (SSMS.exe)，連接時使用 ADO.NET。
* sqlcmd.exe，連接時使用 [ODBC](http://msdn.microsoft.com/library/jj730308.aspx)。

一旦完成連接，就會測試簡短的 SQL SELECT 查詢是否可以運作。

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>診斷： 檢查 hello 開放的連接埠
假設您懷疑連線嘗試會因為 tooport 問題失敗。 在您的電腦上，您可以執行報告的 hello 連接埠組態的公用程式。

在 Linux hello 下列公用程式可能會很有幫助：

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * （變更 hello 範例值 toobe 您的 IP 位址）。

在 Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148)公用程式可能會很有幫助。 以下是範例執行的查詢 hello 連接埠的情況下於 Azure SQL Database 伺服器上，而且這已在膝上型電腦上執行：

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>診斷：記錄您的錯誤
有時診斷間歇問題的最好方式，就是數天或數週偵測一般模式。

您的用戶端可以記錄其遇到的所有錯誤來協助診斷。 您可能會無法 toocorrelate hello 記錄項目，使用 Azure SQL 資料庫記錄檔本身內部的錯誤資料。

Enterprise Library 6 (EntLib60) 提供.NET managed 類別 tooassist 記錄：

* [5-以輕鬆為下降關閉記錄： 使用 hello 記錄應用程式區塊](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>診斷：檢查系統記錄找出錯誤
以下是一些查詢錯誤記錄和其他資訊的 Transact-SQL SELECT 陳述式。

| 記錄查詢 | 說明 |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx)檢視提供有關個別事件，包括某些可能會導致暫時性錯誤或連線失敗的資訊。<br/><br/>在理想情況下相互關聯 hello **start_time**或**end_time**當用戶端程式發生問題的相關資訊的值。<br/><br/>**提示：** ，您必須連接 toohello**主要**toorun 這的資料庫。 |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx)檢視提供的事件類型，取得詳細診斷資訊彙總計的數。<br/><br/>**提示：** ，您必須連接 toohello**主要**toorun 這的資料庫。 |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>診斷： 搜尋 hello SQL 資料庫記錄檔中的問題事件
您可以搜尋有關問題的事件，Azure SQL Database 的 hello 記錄檔中的項目。 再試一次下列 TRANSACT-SQL SELECT 陳述式中 hello hello**主要**資料庫：

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>數個從 sys.fn_xe_telemetry_blob_target_read_file 傳回的資料列
接下來是傳回的資料列可能的樣子。 顯示 hello null 值通常不是 null 的其他資料列中的。

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise Library 6
Enterprise Library 6 (EntLib60) 是的架構的.NET 類別，可協助您實作強固的用戶端的雲端服務，其中是 hello Azure SQL Database 服務。 您可以找到所在 EntLib60 可協助第一次瀏覽主題專用的 tooeach 區域：

* [Enterprise Library 6 - 2013 年 4 月](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

在 EntLib60 可以協助的一個領域中用於處理暫時性錯誤的重試邏輯：

* [4-堅持不懈、 密碼的所有勝利： 使用 hello 暫時性錯誤處理應用程式區塊](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> hello EntLib60 的原始程式碼可針對公用[下載](http://go.microsoft.com/fwlink/p/?LinkID=290898)。 Microsoft 有無計劃 toomake 進一步功能更新或維護更新 tooEntLib。
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>用於暫時性錯誤和重試的 EntLib60 類別
hello 遵循 EntLib60 類別是適合用來重試邏輯。 所有這些包括 in、 或，更進一步 hello 命名空間**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*Hello 命名空間中**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **RetryPolicy** 類別
  
  * **ExecuteAction** 方法
* **ExponentialBackoff** 類別
* **SqlDatabaseTransientErrorDetectionStrategy** 類別
* **ReliableSqlConnection** 類別
  
  * **ExecuteCommand** 方法

Hello 命名空間中**Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** 類別
* **NeverTransientErrorDetectionStrategy** 類別

以下是連結 tooinformation EntLib60 相關：

* 免費[活頁簿下載： 開發人員指南 tooMicrosoft 企業程式庫中，第 2 版](http://www.microsoft.com/download/details.aspx?id=41145)
* 最佳作法： [重試一般指引](../best-practices-retry-general.md) 深入探討重試邏輯。
* 可在 NuGet 下載 [Enterprise Library - 暫時性錯誤處理應用程式區塊 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: hello 記錄區塊
* hello 記錄區塊是高彈性和可設定的解決方案，可讓您：
  
  * 建立記錄訊息，並儲存在各種不同的位置中。
  * 分類與篩選訊息。
  * 收集有助於偵錯和追蹤的內容資訊，以及用於稽核和一般記錄需求的內容資訊。
* hello 記錄區塊會擷取 hello hello 記錄目的地從記錄功能，使 hello 應用程式程式碼會一致，無論 hello 位置和類型的 hello 目標記錄存放區。

如需詳細資訊，請參閱： [5-以輕鬆為落關閉記錄： 使用 hello 記錄應用程式區塊](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>EntLib60 IsTransient 方法的原始程式碼
接下來，從 hello **SqlDatabaseTransientErrorDetectionStrategy**類別，是 hello hello C# 原始程式碼**IsTransient**方法。 hello 原始程式碼將釐清哪些錯誤 toobe 暫時性和重試 」，於 2013 年 4 月的考量。

許多**//comment**行已從這個複製 tooemphasize 可讀性。

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>後續步驟
* 如需疑難排解其他常見的 Azure SQL Database 連線問題，請瀏覽[疑難排解連接問題 tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md)。
* [SQL Server 連接集區 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*正在重試*是一般用途的重試一次程式庫，以撰寫的 Apache 2.0 授權**Python**，新增任何項目有關的重試行為 toojust toosimplify hello 工作。](https://pypi.python.org/pypi/retrying)

