---
title: "使用診斷和 Message Analyzer aaaTroubleshooting Azure 儲存體 |Microsoft 文件"
description: "示範使用 Azure Storage Analytics、AzCopy 和 Microsoft Message Analyzer 進行端對端疑難排解的教學課程"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 643372a3-1c07-4e88-b4ef-042512a43086
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/15/2017
ms.author: robinsh
ms.openlocfilehash: f0b7886911c35de1fdc0bcbe6f83c220ddb38cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>使用 Azure 儲存體計量和記錄、AzCopy 及 Message Analyzer 進行端對端疑難排解
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

診斷與疑難排解是透過 Microsoft Azure 儲存體建置和支援用戶端應用程式的關鍵技術。 Azure 應用程式 toohello 分散式本質，因為診斷和疑難排解錯誤和效能問題可能是比傳統部署環境更為複雜。

在本教學課程中，我們將示範如何 tooidentify 的特定錯誤，可能會影響效能，以及疑難排解這些錯誤從端對端使用順序 toooptimize hello 用戶端應用程式在 Microsoft Azure 儲存體，所提供的工具。

本教學課程提供端對端疑難排解案例的實際操作探勘。 深入了解概念指南 tootroubleshooting Azure 儲存體的應用程式，請參閱[監視、 診斷和疑難排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)。

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>對 Azure 儲存體應用程式進行疑難排解的工具
使用 Microsoft Azure 儲存體 tootroubleshoot 用戶端應用程式，您可以使用工具 toodetermine 發生問題時，哪些 hello 問題的原因 hello 可能的組合。 這些工具包括：

* **Azure Storage Analytics**。 [Azure Storage Analytics](/rest/api/storageservices/Storage-Analytics) 提供 Azure 儲存體的度量和記錄。
  
  * **儲存體度量** 可追蹤儲存體帳戶的交易度量和容量度量。 使用度量，您可以判斷您的應用程式不同的量值的相應 tooa 各種的表現。 請參閱[儲存體分析度量資料表結構描述](/rest/api/storageservices/Storage-Analytics-Metrics-Table-Schema)如 hello 種度量追蹤儲存體分析所需詳細資訊。
  * **儲存體記錄**記錄每個要求 toohello Azure 儲存體服務 tooa 伺服器端記錄檔。 針對每個要求，包括 hello 作業的 hello 記錄追蹤詳細的資料執行 hello 狀態 hello 作業和延遲資訊。 請參閱[儲存體分析記錄格式](/rest/api/storageservices/Storage-Analytics-Log-Format)如需有關儲存體分析所寫入 toohello 記錄檔的 hello 要求和回應資料。

> [!NOTE]
> 區域備援儲存體 (ZRS) 的複寫類型的儲存體帳戶沒有 hello 度量或記錄功能在此時間內啟用。 
> 
> 

* **Azure 入口網站**。 您可以設定的度量和記錄儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。 您也可以檢視圖表及圖形，顯示經過一段時間，如何執行您的應用程式，並設定警示 toonotify，如果您的應用程式不同的方式執行比預期指定標準。
  
    請參閱[監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)設定 hello Azure 入口網站中監視的資訊。
* **AzCopy**。 Azure 儲存體的伺服器記錄檔會儲存為 blob，因此您可以使用 Microsoft Message Analyzer 分析使用 AzCopy toocopy hello 記錄 blob tooa 本機目錄。 請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)如需 AzCopy。
* **Microsoft Message Analyzer**。 Message Analyzer 是一種工具，會消耗記錄檔，並輕鬆 toofilter、 搜尋和為您可以使用 tooanalyze 錯誤和效能問題的有用集記錄資料的群組可讓以視覺格式顯示記錄資料。 如需 Message Analyzer 的詳細資訊，請參閱 [Microsoft Message Analyzer 操作指南](http://technet.microsoft.com/library/jj649776.aspx)。

## <a name="about-hello-sample-scenario"></a>關於 hello 範例案例
在本教學課程中，我們將檢驗一個案例，其中的 Azure 儲存體度量表示應用程式呼叫 Azure 儲存體的成功率很低。 hello 低成功百分比速率度量 (顯示為**PercentSuccess**在 hello [Azure 入口網站](https://portal.azure.com)和 hello 度量資料表中) 會追蹤的作業的成功，但會傳回 HTTP 狀態碼，使其大於比 299。 在 hello 伺服器端儲存記錄檔，這些作業會記錄交易狀態為**ClientOtherErrors**。 如需 hello 低成功百分比度量的詳細資訊，請參閱[度量顯示低 PercentSuccess 或分析記錄檔項目有作業的交易狀態的 ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success)。

Azure 儲存體作業可能會傳回大於 299 的 HTTP 狀態碼為其正常功能的一部分。 但在某些情況下，這些錯誤表示您可能會無法 toooptimize 用戶端應用程式的更佳的效能。

在此案例中，我們會考慮低成功百分比率 toobe 低於 100%的任何項目。 您可以選擇不同度量層級，不過，根據 tooyour 需求。 我們建議您在應用程式的測試期間，建立關鍵效能指標的基準容錯。 例如，您可能會根據測試，決定您的應用程式應具有 90% 或 85% 的穩定成功率。 如果度量資料會顯示 hello 應用程式偏離該數字，您可以調查可能造成 hello 增加。

我們的範例案例，我們已經建立 hello 成功百分比速率度量低於 100%，我們會檢查 hello 記錄 toofind hello 錯誤相互關聯 toohello 度量，並使用它們之後 toofigure 出造成 hello 下限百分比的成功率。 我們將探討特別 hello 400 範圍中的錯誤。 然後我們將更仔細調查 404 (找不到) 錯誤。

### <a name="some-causes-of-400-range-errors"></a>400 範圍錯誤的某些原因
以下的 hello 範例會顯示取樣，以對 Azure Blob 儲存體，要求一些 400 範圍錯誤和可能的原因。 這些錯誤，以及錯誤在 hello 300 範圍和 hello 500 範圍內，任何可以參與 tooa 低百分比成功率。

請注意，下列的 hello 清單並非完整。 請參閱[狀態和錯誤碼](http://msdn.microsoft.com/library/azure/dd179382.aspx)如需詳細資訊錯誤特定 tooeach hello 儲存體服務以及一般的 Azure 儲存體錯誤相關的 MSDN 上。

**狀態碼 404 (找不到) 範例**

發生於對容器或 blob 的讀取的作業會失敗，因為 hello blob 或容器找不到。

* 如果在其他用戶端此要求前刪除了容器或 Blob，就會發生。
* 如果您使用 API 呼叫，檢查它是否存在之後建立 hello 容器或 blob，就會發生。 hello CreateIfNotExists Api 進行呼叫第一個 toocheck hello 容器或 blob; hello 存在的標頭如果不存在，會傳回 404 錯誤，而且 toowrite hello 容器或 blob，然後進行第二個 PUT 呼叫。

**狀態碼 409 (衝突) 範例**

* 如果您使用建立 API toocreate 新的容器或 blob，而不檢查存在，且容器或 blob，具有該名稱已存在，就會發生。
* 如果正在刪除容器，且您嘗試 toocreate hello 刪除作業完成之前名稱相同的 hello 與新的容器，就會發生。
* 如果您在容器或 Blob 上指定租用，而且已經有租用存在，就會發生。

**狀態碼 412 (先決條件失敗) 範例**

* 發生於指定的條件式標頭的 hello 條件不符合。
* 指定的租用識別碼 hello 與 hello hello 容器或 blob 上的租用識別碼不相符時，就會發生。

## <a name="generate-log-files-for-analysis"></a>產生記錄檔以供分析
在此教學課程中，我們使用郵件分析器 toowork 有三種不同類型的記錄檔，雖然您可以選擇使用其中任何一個 toowork:

* hello **server 記錄檔**，這您啟用 Azure 儲存體記錄時所建立。 hello server 記錄檔包含每個作業呼叫 hello Azure 儲存體服務-blob、 佇列、 表格和檔案的其中一個相關資料。 hello 伺服器記錄檔指出呼叫的作業和狀態程式碼已傳回，以及其他有關 hello 要求和回應的詳細資料。
* hello **.NET 用戶端記錄檔**，這您在.NET 應用程式中啟用用戶端記錄從時所建立。 hello 用戶端記錄檔包含 hello 用戶端如何準備 hello 要求和接收和處理 hello 回應的詳細的資訊。
* hello **HTTP 網路追蹤記錄檔**，以 HTTP/HTTPS 要求和回應資料，包括對 Azure 儲存體的作業上收集資料。 在本教學課程中，我們將會產生郵件分析器透過 hello 網路追蹤。

### <a name="configure-server-side-logging-and-metrics"></a>設定伺服器端記錄和度量
首先，我們需要 tooconfigure Azure 儲存體記錄和度量資訊，如此我們需要從 hello 用戶端應用程式 tooanalyze 的資料。 您可以設定記錄檔和度量的各種不同的方式-透過 hello [Azure 入口網站](https://portal.azure.com)，使用 PowerShell，或以程式設計的方式。 如需設定記錄和度量的詳細資訊，請參閱 MSDN 上的[啟用儲存體度量和檢視度量資料](http://msdn.microsoft.com/library/azure/dn782843.aspx)和[啟用儲存體記錄和存取記錄檔資料](http://msdn.microsoft.com/library/azure/dn782840.aspx)。

**透過 hello Azure 入口網站**

tooconfigure 記錄和度量資訊，用於您儲存體帳戶使用 hello [Azure 入口網站](https://portal.azure.com)，請遵循指示 hello[監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)。

> [!NOTE]
> 不可能 tooset 分鐘度量使用 hello Azure 入口網站。 不過，我們建議您不要設定它們基於此教學課程中的 hello 和調查與您的應用程式的效能問題。 您可以設定分鐘度量使用 PowerShell，如下所示，或以程式設計方式使用 hello 儲存體用戶端程式庫。
> 
> 請注意該 hello Azure 入口網站無法顯示分鐘度量，只為每小時度量。
> 
> 

**透過 PowerShell**

請參閱 < 開始使用 azure PowerShell tooget[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

1. 使用 hello [Add-azureaccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) cmdlet tooadd 您 Azure 的使用者帳戶 toohello PowerShell 視窗：
   
    ```powershell
    Add-AzureAccount
    ```

2. 在 hello**登入 tooMicrosoft Azure**視窗、 型別 hello 電子郵件地址和您的帳戶相關聯的密碼。 Azure 驗證並儲存 hello 認證資訊，，然後關閉 [hello] 視窗。
3. 設定 hello 預設儲存體帳戶 toohello 儲存體帳戶在 hello PowerShell 視窗中執行這些命令使用 hello 教學課程：
   
    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. 啟用儲存體記錄 hello Blob 服務：
   
    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. 啟用儲存體度量 hello Blob 服務，讓確定 tooset **-MetricsType**太`Minute`:
   
    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>設定 .NET 用戶端記錄
tooconfigure 用戶端.NET 應用程式的記錄功能可讓.NET 診斷 hello 應用程式組態檔 （web.config 或 app.config） 中。 請參閱[用戶端以 hello.NET 儲存體用戶端程式庫記錄](http://msdn.microsoft.com/library/azure/dn782839.aspx)和[記錄以 hello Microsoft Azure 儲存體 SDK for Java 用戶端](http://msdn.microsoft.com/library/azure/dn782844.aspx)msdn 如需詳細資訊。

hello 用戶端記錄檔包含 hello 用戶端如何準備 hello 要求和接收和處理 hello 回應的詳細的資訊。

hello 儲存體用戶端程式庫會將用戶端記錄檔資料儲存在 hello hello 應用程式組態檔 （web.config 或 app.config） 中指定的位置。

### <a name="collect-a-network-trace"></a>收集網路追蹤
用戶端應用程式執行時，您可以使用郵件分析器 toocollect HTTP/HTTPS 網路追蹤。 訊息分析師會使用[Fiddler](http://www.telerik.com/fiddler) hello 在後端。 收集 hello 網路追蹤之前，我們建議您設定 Fiddler toorecord 未加密的 HTTPS 流量：

1. 安裝 [Fiddler](http://www.telerik.com/download/fiddler)。
2. 啟動 Fiddler。
3. 選取 [工具] | [Fiddler 選項]。
4. 在 hello 選項 對話方塊，請確認**擷取 HTTPS 連線**和**解密 HTTPS 流量**都已選取，如下所示。

![設定 Fiddler 選項](./media/storage-e2e-troubleshooting/fiddler-options-1.png)

Hello 教學課程中，收集和郵件分析器中的第一次儲存網路追蹤，然後建立分析工作階段 tooanalyze hello 追蹤並 hello 記錄檔。 toocollect 網路追蹤，在郵件分析器：

1. 在 Message Analyzer 中，選取 [檔案] | [快速追蹤] | [未加密的 HTTPS]。
2. hello 追蹤會立即開始。 選取**停止**toostop hello 追蹤，以便我們可以設定它僅 tootrace 儲存體流量。
3. 選取**編輯**tooedit hello 追蹤工作階段。
4. 選取 hello**設定**連結權限的 hello toohello **Microsoft-Pef-WebProxy** ETW 提供者。
5. 在 hello**進階設定** 對話方塊中，按一下 hello**提供者** 索引標籤。
6. 在 hello**主機名稱篩選**欄位中，指定您的儲存體端點，以空格分隔。 例如，您可以指定您的端點，如下所示。變更`storagesample`toohello 您的儲存體帳戶名稱：

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. 結束 [hello] 對話方塊中，然後按一下**重新啟動**toobegin hello 主機名稱的篩選器的位置，以收集 hello 追蹤，以便 hello 追蹤中包含 Azure 儲存體網路流量。

> [!NOTE]
> 當您完成收集網路追蹤之後，我們強烈建議您還原 hello 設定，您可能已在 Fiddler toodecrypt HTTPS 流量。 在 hello Fiddler 選項對話方塊中，取消選取 hello**擷取 HTTPS 連線**和**解密 HTTPS 流量**核取方塊。
> 
> 

請參閱[使用 hello 網路追蹤功能](http://technet.microsoft.com/library/jj674819.aspx)如需詳細資訊的 Technet 上。

## <a name="review-metrics-data-in-hello-azure-portal"></a>檢閱 hello Azure 入口網站中的度量資料
一旦您的應用程式已經執行了一段時間，您可以檢閱 hello 度量出現之圖表的 hello [Azure 入口網站](https://portal.azure.com)tooobserve 如何會執行您的服務。

首先，瀏覽 tooyour hello Azure 入口網站中的儲存體帳戶。 根據預設，監視圖表以 hello**成功百分比**度量會顯示 hello 帳戶 刀鋒視窗。 如果您先前已經修改 hello 圖表 toodisplay 不同度量，新增 hello**成功百分比**度量。

您現在會看到**成功百分比**hello 監視圖表，以及任何其他度量您可能已經在加入。 在 hello 案例中我們將調查接著藉由分析 hello 郵件分析器中的記錄檔，hello 百分比成功率有點低於 100%。

如需新增與自訂計量圖表的詳細資訊，請參閱[自訂計量圖表](storage-monitor-storage-account.md#customize-metrics-charts)。

> [!NOTE]
> 啟用儲存體度量之後，可能需要一些時間，您的度量資料 tooappear hello Azure 入口網站中。 這是因為每小時度量 hello 前一小時不會顯示在 Azure 入口網站的 hello hello 目前的小時經過之前。 此外，每分鐘度量是目前沒有顯示在 hello Azure 入口網站。 因此根據當您啟用度量時，它可能會佔用 tootwo 小時 toosee 度量資料。
> 
> 

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>使用 AzCopy toocopy 伺服器記錄檔 tooa 本機目錄
Azure 儲存體寫入伺服器記錄檔資料 tooblobs，度量資訊會寫入 tootables 時。 記錄檔 blob 位於 hello 已知`$logs`儲存體帳戶的容器。 記錄檔 blob 命名以階層方式依年、 月、 日和小時，讓您輕鬆地找出 hello 想 tooinvestigate 的時間範圍。 例如，在 hello `storagesample` hello 01/02/2015 中，從上午 8-9 點的 hello 記錄檔 blob 容器的帳戶是`https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`。 此容器中的 hello 個別 blob 循序命名，開頭為`000000.log`。

您可以在本機電腦上使用 hello AzCopy 命令列工具 toodownload 您選擇這些伺服器端記錄檔案 tooa 位置。 例如，您可以使用下列命令 toodownload hello 記錄檔的 blob 作業所需的置於 hello 2015 年 1 月 2 日 toohello 資料夾`C:\Temp\Logs\Server`; 取代`<storageaccountname>`hello 儲存體帳戶名稱和`<storageaccountkey>`與您帳戶存取金鑰：

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```
AzCopy 可供下載 hello [Azure 下載](https://azure.microsoft.com/downloads/)頁面。 如需有關使用 AzCopy 的詳細資訊，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

如需下載伺服器端記錄檔的詳細資訊，請參閱 [下載儲存體記錄記錄檔資料](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata)。

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>使用 Microsoft Message Analyzer tooanalyze 記錄資料
Microsoft Message Analyzer 是在疑難排解與診斷案例中用於擷取、顯示及分析通訊協定訊息流量、事件和其他系統或應用程式訊息的工具。 郵件分析器也可讓您彙總，tooload 和分析記錄檔中的資料並儲存追蹤檔案。 如需 Message Analyzer 的詳細資訊，請參閱 [Microsoft Message Analyzer 操作指南](http://technet.microsoft.com/library/jj649776.aspx)。

郵件分析器所含資產的 tooanalyze 伺服器、 用戶端和網路的記錄檔，協助您的 Azure 儲存體。 在本節中，我們將討論如何 toouse 這些工具 tooaddress hello 問題的低百分比成功 hello 儲存體記錄。

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>下載並安裝郵件分析器和 hello Azure 儲存體資產
1. 下載[Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226)從 hello Microsoft 下載中心，並執行 hello 安裝程式。
2. 啟動 Message Analyzer。
3. 從 hello**工具**功能表上，選取**資產管理員**。 在 hello**資產管理員**對話方塊中，選取**下載**，然後篩選**Azure 儲存體**。 Hello 圖所示，您會看到 hello Azure 儲存體資產。
4. 按一下**同步處理所有顯示的項目**tooinstall hello Azure 儲存體資產。 hello 可用資產包括：
   * **Azure 儲存體的色彩規則：** Azure 儲存體色彩規則可讓您 toodefine 特殊篩選條件，用文字的色彩和字型樣式 toohighlight 訊息包含在追蹤中的特定資訊。
   * **Azure 儲存體圖表** ：Azure 儲存體圖表是圖形伺服器記錄資料的預先定義的圖表。 請注意，此時圖表上 toouse Azure 儲存體，貴用戶只載入 hello 伺服器記錄到 hello 分析方格。
   * **Azure 儲存體分析：** hello Azure 儲存體的剖析器剖析 hello Azure 儲存體用戶端、 伺服器和 HTTP 記錄在順序 toodisplay 在 hello 分析方格。
   * **Azure 儲存體篩選：** Azure 儲存體的篩選是預先定義的準則，您可以使用 tooquery 資料 hello 分析方格中。
   * **Azure 儲存體檢視版面配置：** Azure 儲存體 檢視的配置是預先定義的資料行配置和 hello 分析方格中的群組。
5. 您已安裝 hello 資產之後，請重新啟動郵件分析器。

![訊息分析器資產管理員](./media/storage-e2e-troubleshooting/mma-start-page-1.png)

> [!NOTE]
> 安裝所有顯示基於此教學課程的 hello hello Azure 儲存體資產。
> 
> 

### <a name="import-your-log-files-into-message-analyzer"></a>將記錄檔匯入 Message Analyzer 中
您可以將所有已儲存的記錄檔 (伺服器端、用戶端和網路) 匯入 Microsoft Message Analyzer 的單一工作階段中進行分析。

1. 在 hello**檔案**Microsoft Message Analyzer 功能表按一下**新的工作階段**，然後按一下**空白的工作階段**。 在 [hello**新的工作階段**] 對話方塊中，輸入您的分析工作階段的名稱。 在 hello**工作階段詳細資料** 面板中，按一下 hello**檔案** 按鈕。
2. 按一下郵件分析器所產生的 tooload hello 網路追蹤資料**加入檔案**、 瀏覽 toohello 您儲存的位置.matp 檔案從您網頁追蹤活動中，選取 hello.matp 檔案，然後按一下**開啟**.
3. tooload hello 伺服器端記錄資料，按一下**加入檔案**，瀏覽 toohello 下載您的伺服器端記錄檔的位置，選取 hello hello 時間範圍內 tooanalyze，然後按一下的記錄檔**開啟**. 然後，在 hello**工作階段詳細資料**面板、 組 hello**文字記錄檔設定**下拉式清單每個伺服器端記錄檔太**AzureStorageLog** tooensure，Microsoft郵件分析器可以正確地剖析 hello 記錄檔。
4. tooload hello 用戶端記錄檔資料，按一下**加入檔案**，瀏覽 toohello 位置儲存您的用戶端記錄檔的位置，選取您想 tooanalyze，然後按一下 hello 記錄檔**開啟**。 然後，在 hello**工作階段詳細資料**面板、 組 hello**文字記錄檔設定**下拉式清單每個用戶端記錄檔太**AzureStorageClientDotNetV4** tooensure，Microsoft Message Analyzer 可正確剖析 hello 記錄檔。
5. 按一下**啟動**在 hello**新的工作階段**對話方塊 tooload 和剖析 hello 記錄資料。 hello 記錄資料會顯示 hello 訊息分析師分析方格中。

hello 圖會顯示 「 範例 」 工作階段設定伺服器、 用戶端和網路追蹤記錄檔。

![設定 Message Analyzer 工作階段](./media/storage-e2e-troubleshooting/configure-mma-session-1.png)

請注意，Message Analyzer 會將記錄檔載入記憶體中。 如果您有大量記錄資料，您會想 toofilter 它從郵件分析器的順序 tooget hello 最佳效能。

首先，判斷您有興趣檢視的 hello 時間範圍，並讓此時段保持越小越好。 在許多情況下，您會想 tooreview 分鐘或小時最多的句號。 匯入 hello 可符合您需求的記錄檔的最小的集合。

如果仍有大量的記錄檔資料，然後您可以 toospecify 工作階段篩選 toofilter 記錄資料之前將其載入。 在 hello**工作階段篩選器** 方塊中，選取 hello**文件庫**按鈕 toochoose 預先定義的篩選; 例如，選擇**全域時間篩選 I**從 Azure 儲存體篩選的 hello在時間間隔內 toofilter。 接著，您可以編輯 hello 篩選準則 toospecify hello 啟動且 hello 間隔的結束時間戳記想 toosee。 您也可以篩選特定狀態的程式碼;例如，您可以選擇其中 hello 狀態碼為 404 tooload 只記錄項目。

如需將記錄檔資料匯入 Microsoft Message Analyzer 的詳細資訊，請參閱 TechNet 上的 [擷取訊息資料](http://technet.microsoft.com/library/dn772437.aspx) 。

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>使用 hello 用戶端要求 ID toocorrelate 記錄檔資料
hello Azure 儲存體用戶端程式庫會自動產生的每個要求的唯一用戶端要求識別碼。 此值會寫 toohello 用戶端記錄檔、 hello server 記錄檔，與 hello 網路追蹤，因此您可以使用它 toocorrelate 資料跨郵件分析器中的所有三個記錄檔。 請參閱[用戶端要求 ID](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) hello 用戶端的其他資訊的要求識別碼。

hello 下列各節說明如何 toouse 預先設定和自訂版面配置檢視 toocorrelate 與群組資料根據 hello 用戶端要求識別碼。

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>在 hello 分析方格中選取檢視配置 toodisplay
郵件分析器的 hello 儲存體資產包括 Azure 儲存體檢視版面配置，也就是預先設定的檢視，您可以搭配 toodisplay 資料很有用的群組和資料行針對不同的案例。 您也可以建立自訂檢視版面配置並儲存起來以便重複使用。

hello 圖會顯示 hello**檢視配置**功能表上，選取可用**檢視配置**從 hello 工具列功能區。 Azure 儲存體的 hello 檢視配置進行分組 hello **Azure 儲存體**hello 功能表中的節點。 您可以搜尋`Azure Storage`hello 搜尋方塊 toofilter 在 Azure 儲存體中檢視僅版面配置。 您也可以選取 hello 星狀下一步 tooa 檢視配置 toomake 為我的最愛，並在 [hello] 功能表的 hello 頂端顯示。

![檢視版面配置功能表](./media/storage-e2e-troubleshooting/view-layout-menu.png)

搭配 select toobegin **ClientRequestID 及模組所分組**。 此檢視版面配置會先依用戶端要求識別碼，再依來源記錄檔 (或 Message Analyzer 中的 [模組]  )，將全部三個記錄檔中的記錄檔資料分組。 與此檢視中，您可以向下切入到特定用戶端要求識別碼，並查看所有三個記錄檔中該用戶端要求識別碼的資料。

hello 圖會顯示此版面配置檢視套用 toohello 範例記錄檔資料，以顯示的資料行的子集。 您可以查看特定用戶端要求識別碼的 hello 分析方格顯示 hello 用戶端記錄檔、 伺服器記錄檔和網路追蹤的資料。

![Azure 儲存體檢視版面配置](./media/storage-e2e-troubleshooting/view-layout-client-request-id-module.png)

> [!NOTE]
> 不同的記錄檔有不同的資料行，因此在 hello 分析方格中顯示來自多個記錄檔的資料時，某些資料行可能不會包含任何資料，對於給定的資料列。 比方說，在上面的 hello 圖片，用戶端記錄檔資料列執行不顯示任何資料 hello**時間戳記**， **TimeElapsed**，**來源**，和**目的地**資料行，因為這些資料行不存在於 hello 用戶端記錄檔，但確實存在 hello 網路追蹤中。 同樣地，hello**時間戳記**資料行顯示時間戳記資料從 hello 伺服器記錄檔，但沒有資料會顯示 hello **TimeElapsed**，**來源**，和**目的地**資料行，並不屬於 hello server 記錄檔。
> 
> 

此外 toousing hello Azure 儲存體檢視版面配置，您可以也定義並儲存您自己的檢視配置。 您可以選取其他所需的欄位來分組資料，並儲存 hello 群組做為您自訂的配置的一部分。

### <a name="apply-color-rules-toohello-analysis-grid"></a>套用色彩規則 toohello 分析方格
hello 儲存體資產也包含色彩規則，提供視覺表示 tooidentify 不同類型的 hello 分析方格中的錯誤。 hello 預先定義的色彩規則套用 tooHTTP 錯誤，所以它們只會出現 hello 伺服器記錄檔和網路追蹤。

tooapply 色彩規則、 選取**色彩規則**從 hello 工具列功能區。 您會看見 hello 功能表中的 hello Azure 儲存體色彩規則。 Hello 教學課程中，選取**用戶端錯誤 (介於 400 到 499 StatusCode)**hello 圖所示。

![Azure 儲存體檢視版面配置](./media/storage-e2e-troubleshooting/color-rules-menu.png)

此外 toousing hello Azure 儲存體色彩規則，您也可以定義及儲存您自己的色彩規則。

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>群組和篩選記錄檔資料 toofind 400 範圍錯誤
接下來，我們將分組，並篩選 hello 記錄資料 toofind hello 400 範圍中的所有錯誤。

1. 找出 hello **StatusCode**中 hello 分析方格中，以滑鼠右鍵按一下 hello 資料行標題，並選取資料行**群組**。
2. 接下來，群組 hello **ClientRequestId**資料行。 您會看到的 hello 分析方格現在依狀態中的 hello 資料程式碼，並由用戶端要求識別碼。
3. 如果尚未顯示，請顯示 hello 檢視篩選器 工具視窗。 在 hello 工具列功能區中，選取 **工具視窗**，然後**檢視篩選器**。
4. toofilter hello 記錄資料 toodisplay 只 400 範圍錯誤，加入下列篩選準則 toohello hello**檢視篩選器**視窗，並按一下**套用**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

hello 圖會顯示 hello 這個群組和篩選的結果。 擴充的 hello **ClientRequestID**欄位下方的狀態碼 409，比方說，分組顯示 hello 導致該狀態碼的作業。

![Azure 儲存體檢視版面配置](./media/storage-e2e-troubleshooting/400-range-errors1.png)

之後套用此篩選之後，您會看到 hello 用戶端記錄檔資料列會排除，hello 為用戶端記錄檔不包含**StatusCode**資料行。 與 toobegin，我們會檢閱 hello 伺服器和網路追蹤記錄檔 toolocate 404 錯誤，並接著我們將傳回 toohello 用戶端記錄 tooexamine hello 用戶端操作，導致 toothem。

> [!NOTE]
> 您可以篩選 hello **StatusCode**資料行和仍然顯示的資料，從所有三個記錄檔，包括 hello 用戶端記錄檔，如果您將加入運算式 toohello 篩選，其中包含記錄項目，其中 hello 狀態碼是 null。 tooconstruct 這個篩選條件運算式，使用：
> 
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
> 
> 此篩選條件傳回所有資料列從 hello 用戶端記錄檔和 hello server 記錄檔和 HTTP 記錄檔中的只有資料列 hello 狀態碼大於 400。 如果您套用 toohello 檢視配置用戶端要求 ID 及模組所分組，您可以搜尋或 hello 捲動記錄項目 toofind 是表示所有三個記錄檔位置。   
> 
> 

### <a name="filter-log-data-toofind-404-errors"></a>篩選記錄檔資料 toofind 404 錯誤
hello 儲存體資產包含預先定義的篩選，您可以使用 toonarrow 記錄檔資料 toofind hello 錯誤或您所需的趨勢。 接下來，我們會在這裡套用兩個預先定義的篩選條件： hello 伺服器和 404 錯誤，網路追蹤記錄檔篩選的一個，篩選 hello 資料在指定的時間範圍的一個。

1. 如果尚未顯示，請顯示 hello 檢視篩選器 工具視窗。 在 hello 工具列功能區中，選取 **工具視窗**，然後**檢視篩選器**。
2. 在 hello 檢視篩選器 視窗中，選取 **文件庫**，然後搜尋`Azure Storage`toofind hello Azure 儲存體篩選。 選取 hello 篩選**404 （找不到） 訊息中的所有記錄**。
3. 顯示 hello**文件庫**功能表，然後找出並選取 hello**全域時間篩選器**。
4. 編輯您想 tooview 顯示 hello 篩選 toohello 範圍中的 hello 時間戳記。 這有助於資料 tooanalyze toonarrow hello 範圍。
5. 您的篩選條件應該會出現類似以下的 toohello 範例。 按一下**套用**tooapply hello 篩選 toohello 分析方格。

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

    ![Azure 儲存體檢視版面配置](./media/storage-e2e-troubleshooting/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>分析記錄檔資料
現在，您有分組，並篩選您的資料，您可以檢查個別要求而產生 404 錯誤 hello 詳細資料。 在目前檢視配置 hello，hello 資料是依用戶端要求 ID，然後由記錄檔來源分組。 因為我們要在要求中篩選其中 hello StatusCode 欄位包含 404，我們會看到只 hello 伺服器和網路追蹤資料，不 hello 用戶端記錄的資料。

hello 圖會顯示特定要求位置取得 Blob 作業產生 404 因為 hello blob 不存在。 請注意，某些資料行已從順序 toodisplay hello 相關資料中的 hello 標準檢視中移除。

![已篩選的伺服器和網路追蹤記錄檔](./media/storage-e2e-troubleshooting/server-filtered-404-error.png)

接下來，我們將與交互關聯此用戶端要求識別碼 hello 用戶端記錄檔資料 toosee hello 錯誤發生時執行何種動作 hello 用戶端。 您可以顯示為此工作階段 tooview hello 用戶端記錄檔資料，這會在第二個索引標籤中開啟新的分析方格檢視：

1. 首先，複製 hello hello 值**ClientRequestId**欄位 toohello 剪貼簿。 您可以選取其中一個資料列中，找出 hello **ClientRequestId**  欄位中，以滑鼠右鍵按一下 hello 資料值，然後選擇**複製 'ClientRequestId'**。
2. 在 hello 工具列功能區中，選取 **新的檢視器**，然後選取**分析方格**tooopen 新的索引 hello 新索引標籤會顯示所有資料在記錄檔，而不分組、 篩選或色彩規則。
3. Hello 工具列功能區上，選取**檢視配置**，然後選取**所有.NET 用戶端的資料行**下 hello **Azure 儲存體**> 一節。 此檢視的配置顯示資料 hello 用戶端記錄檔，以及 hello 伺服器和網路追蹤記錄檔。 依預設它排序 hello **MessageNumber**資料行。
4. 接下來，將 hello 用戶端記錄檔搜尋 hello 用戶端要求識別碼。 在 hello 工具列功能區中，選取 **尋找郵件**，然後 hello hello 用戶端要求 ID 來指定自訂篩選器**尋找**欄位。 使用此語法 hello 篩選器，指定您自己的用戶端要求 ID:

    ```
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

郵件分析器找出並選取 hello 第一個記錄檔項目，其中 hello 搜尋準則符合 hello 用戶端要求識別碼。 在 hello 用戶端記錄檔中，有數個項目，每個用戶端要求識別碼，因此您可能需要 toogroup 在 hello **ClientRequestId**欄位 toomake 它更容易 toosee 它們一起出現。 hello 圖片所示在 hello 用戶端 hello 訊息的所有記錄檔以取得 hello 指定用戶端要求識別碼。

![顯示 404 錯誤的用戶端記錄檔](./media/storage-e2e-troubleshooting/client-log-analysis-grid1.png)

使用這些兩個索引標籤中的 hello 檢視版面配置中所顯示的 hello 資料，您可以分析 hello 要求資料 toodetermine 可能造成 hello 錯誤。 您也可以查看要求之前的此一 toosee 如果先前的事件可能會使 toohello 404 錯誤。 例如，您可以檢閱 hello 用戶端記錄檔項目之前此用戶端要求 ID toodetermine 是否 hello blob 可能已遭到刪除，或如果 hello 錯誤是因為 toohello 容器或 blob 上呼叫 CreateIfNotExists API 的用戶端應用程式。 在 hello 用戶端記錄檔，您可以在 hello 找到 hello blob 位址**描述**欄位; 在 hello 伺服器和網路追蹤記錄檔，這項資訊會出現在 hello**摘要**欄位。

一旦您知道產生 hello 404 錯誤的 hello blob hello 位址時，您可以進一步調查。 如果您搜尋 hello 與相關聯的其他訊息的記錄項目相同 blob hello 上的作業時，您可以檢查是否 hello 用戶端先前刪除 hello 實體。

## <a name="analyze-other-types-of-storage-errors"></a>分析其他類型的儲存體錯誤
既然您已熟悉如何使用郵件分析器 tooanalyze 記錄資料，您可以分析使用 檢視錯誤的其他類型配置、 色彩規則，以及搜尋/篩選。 hello 資料表底下列出一些問題，您可能會遇到與 hello 篩選準則，您可以使用 toolocate 它們。 如需有關建構篩選條件和 hello 訊息分析師篩選語言，請參閱[篩選訊息資料](http://technet.microsoft.com/library/jj819365.aspx)。

| tooInvestigate... | 使用篩選運算式… | 運算式適用於 tooLog (用戶端、 伺服器、 網路、 所有) |
| --- | --- | --- |
| 佇列上未預期的訊息傳遞延遲 |AzureStorageClientDotNetV4.Description 包含「正在重試失敗的作業」。 |用戶端 |
| PercentThrottlingError 的 HTTP 增加 |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |網路 |
| PercentTimeoutError 增加 |HTTP.Response.StatusCode   == 500 |網路 |
| PercentTimeoutError 增加 (全部) |*StatusCode   == 500 |全部 |
| PercentNetworkError 增加 |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |用戶端 |
| HTTP 403 (禁止) 訊息 |HTTP.Response.StatusCode   == 403 |網路 |
| HTTP 404 (找不到) 訊息 |HTTP.Response.StatusCode   == 404 |網路 |
| 404 (全部) |*StatusCode   == 404 |全部 |
| 共用存取簽章 (SAS) 授權問題 |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |網路 |
| HTTP 409 (衝突) 訊息 |HTTP.Response.StatusCode   == 409 |網路 |
| 409 (全部) |*StatusCode   == 409 |全部 |
| 低 PercentSuccess，或是分析記錄項目內含具有 ClientOtherErrors 交易狀態的作業 |AzureStorageLog.RequestStatus ==   "ClientOtherError" |伺服器 |
| Nagle 警告 |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) 和 (AzureStorageLog.RequestPacketSize <1460) 和 (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |伺服器 |
| 伺服器和網路記錄檔中的時間範圍 |#Timestamp   >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39 |伺服器、網路 |
| 伺服器記錄檔中的時間範圍 |AzureStorageLog.Timestamp   >= 2014-10-20T16:36:38 和 AzureStorageLog.Timestamp <=   2014-10-20T16:36:39 |伺服器 |

## <a name="next-steps"></a>後續步驟
如需在 Azure 儲存體中進行端對端案例疑難排解的詳細資訊，請參閱下列資源：

* [監視、診斷與疑難排解 Microsoft Azure 儲存體](storage-monitoring-diagnosing-troubleshooting.md)
* [Storage Analytics](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [監視 hello Azure 入口網站的儲存體帳戶](storage-monitor-storage-account.md)
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)
* [Microsoft Message Analyzer 操作指南](http://technet.microsoft.com/library/jj649776.aspx)
