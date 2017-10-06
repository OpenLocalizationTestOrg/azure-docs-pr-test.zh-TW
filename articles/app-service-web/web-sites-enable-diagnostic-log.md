---
title: "Azure App Service 中的 web 應用程式的 aaaEnable 診斷記錄"
description: "深入了解如何 tooenable 診斷記錄新增檢測 tooyour 應用程式，以及如何 tooaccess hello Azure 所記錄的資訊。"
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: c9da27b2-47d4-4c33-a3cb-1819955ee43b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b2903ff31cc93180552cf51196c33505ffbaf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-logging-for-web-apps-in-azure-app-service"></a>在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能。
## <a name="overview"></a>概觀
Azure 提供內建的診斷與偵錯的 tooassist [App Service web 應用程式](http://go.microsoft.com/fwlink/?LinkId=529714)。 在本文中，您將學習如何 tooenable 診斷記錄新增檢測 tooyour 應用程式，以及如何 tooaccess hello Azure 所記錄的資訊。

本文使用 hello [Azure 入口網站](https://portal.azure.com)，Azure PowerShell 及 hello Azure 命令列介面 (Azure CLI) toowork 與診斷記錄檔。 如需使用 Visual Studio 來處理診斷記錄的詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure](web-sites-dotnet-troubleshoot-visual-studio.md)。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="whatisdiag"></a>Web 伺服器診斷和應用程式診斷
App Service web 應用程式提供記錄資訊從 hello web 伺服器和 hello web 應用程式的診斷的功能。 這些資訊邏輯上可區分為 **Web 伺服器診斷**與**應用程式診斷**。

### <a name="web-server-diagnostics"></a>Web 伺服器診斷
您可以啟用或停用下列種類的記錄檔的 hello:

* **詳細的錯誤記錄** - 對於表示失敗的 HTTP 狀態碼 (狀態碼 400 或更大) 的詳細錯誤資訊。 這可能包含可協助您判斷為什麼 hello 伺服器傳回 hello 錯誤碼的資訊。
* **失敗要求追蹤**-詳細的失敗的要求，包括 hello IIS 使用的元件 tooprocess hello 要求和取得每個元件中的 hello 時間的追蹤資訊。 如果您正嘗試 tooincrease 站台效能或隔離造成特定的 HTTP 錯誤 toobe 傳回時，這可能會很有用。
* **Web 伺服器記錄**-HTTP 交易使用 hello 資訊[W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。 判斷整體站台的度量資訊，例如 hello 處理要求的數目或多少要求來自特定 IP 位址時，這非常有用。

### <a name="application-diagnostics"></a>應用程式診斷
應用程式診斷可讓您的 web 應用程式所產生的 toocapture 資訊。 ASP.NET 應用程式可以使用 hello [System.Diagnostics.Trace](http://msdn.microsoft.com/library/36hhw2t6.aspx)類別 toolog 資訊 toohello 應用程式診斷記錄。 例如：

    System.Diagnostics.Trace.TraceError("If you're seeing this, something bad happened");

在執行階段中，您可以擷取這些記錄檔 toohelp，進行疑難排解。 如需詳細資訊，請參閱 [在 Visual Studio 中疑難排解 Azure Web 應用程式](web-sites-dotnet-troubleshoot-visual-studio.md)。

當您發佈內容 tooa web 應用程式時，app Service web 應用程式也記錄部署資訊。 此動作會自動發生，因此無須任何組態設定即會記錄部署動作。 部署記錄可讓您 toodetermine 部署失敗的原因。 例如，如果您使用的自訂部署指令碼，您可能會使用部署記錄 toodetermine hello 指令碼失敗的原因。

## <a name="enablediag"></a>如何 tooenable 診斷
在 hello tooenable 診斷[Azure 入口網站](https://portal.azure.com)、 移 toohello 刀鋒視窗，web 應用程式，然後按一下**設定 > 診斷記錄檔**。

<!-- todo:cleanup dogfood addresses in screenshot -->
![記錄部分](./media/web-sites-enable-diagnostic-log/logspart.png)

當您啟用**應用程式診斷**您也可以選擇 hello**層級**。 此設定可讓您擷取太 toofilter hello 資訊**資訊**，**警告**或**錯誤**資訊。 將此設定太**verbose**會記錄 hello 應用程式所產生的所有資訊。

> [!NOTE]
> 不同於變更 hello web.config 檔，啟用應用程式診斷，或變更診斷記錄層級不會加以回收 hello hello 應用程式中執行的應用程式定義域。
>
>

在 hello[傳統入口網站](https://manage.windowsazure.com)Web 應用程式**設定**索引標籤上，您可以選取**儲存體**或**檔案系統**的**web 伺服器記錄**。 選取**儲存體**tooselect 儲存體帳戶，然後再 hello 記錄檔寫入的 blob 容器，可讓您。 所有其他記錄**網站診斷**寫入只 toohello 檔案系統。

hello[傳統入口網站](https://manage.windowsazure.com)Web 應用程式**設定** 索引標籤也有其他應用程式診斷設定：

* **檔案系統**-存放區 hello 應用程式診斷資訊 toohello web 應用程式檔案系統。 這些檔案可以存取的 FTP，或使用 hello Azure PowerShell 或 Azure 命令列介面 (Azure CLI) 下載的 Zip 封存。
* **資料表儲存體**-存放區 hello hello 指定 Azure 儲存體帳戶和資料表名稱中的應用程式的診斷資訊。
* **Blob 儲存體**-存放區 hello hello 指定的 Azure 儲存體帳戶和 blob 容器中的應用程式的診斷資訊。
* **保留週期** - 依預設，所有記錄不會自動從 [Blob 儲存體] 中刪除。 選取**設定保留**，然後輸入 hello 數天內，如果您想 tooautomatically tookeep 記錄刪除記錄檔。

> [!NOTE]
> 如果您[重新產生儲存體帳戶的存取金鑰](../storage/common/storage-create-storage-account.md)，您必須重設 hello 各自的記錄組態 toouse hello 更新金鑰。 toodo 這樣：
>
> 1. 在 hello**設定**索引標籤上，設定得 hello 各自的記錄功能**關閉**。 儲存您的設定。
> 2. 重新啟用記錄 toohello 儲存體帳戶 blob 或資料表。 儲存您的設定。
>
>

檔案系統中，資料表儲存體或 blob 儲存體的任何組合，可以在 hello 相同的時間，並有個別的記錄層級組態啟用。 比方說，您可能需要 toolog 錯誤和警告 tooblob 儲存體做為長期的記錄解決方案，同時也可讓檔案系統記錄的詳細資訊層級。

當所有三個儲存體位置提供 hello 時記錄的事件相同的基本資訊**資料表儲存體**和**blob 儲存體**記錄例如 hello 執行個體識別碼、 執行緒識別碼和更多的其他資訊細微的時間戳記 （刻度格式） 於記錄太**檔案系統**。

> [!NOTE]
> 儲存在 [資料表儲存體] 或 [Blob 儲存體] 內的資訊只能透過儲存用戶端，或是能夠直接使用這些儲存系統的應用程式來存取。 例如，Visual Studio 2013 包含可能是使用的 tooexplore 資料表或 blob 儲存體，儲存體總管，HDInsight 可以存取儲存在 blob 儲存體中的資料。 您也可以撰寫應用程式存取 Azure 儲存體使用其中一種 hello [Azure Sdk](/downloads/#)。
>
> [!NOTE]
> 診斷也可以啟用從 Azure PowerShell 中使用 hello**組 AzureWebsite** cmdlet。 如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。
>
>

## <a name="download"></a> 作法：下載記錄
儲存診斷資訊 toohello web 應用程式檔案系統可以直接使用 FTP 存取。 也可以使用 Azure PowerShell 或 hello Azure 命令列介面的 Zip 封存下載。

hello hello 記錄會儲存於的目錄結構如下所示：

* **應用程式記錄** - /LogFiles/Application/。 此資料夾內含有一或多個文字檔案，這些檔案涵蓋應用程式記錄所產生的資訊。
* **失敗要求追蹤** - /LogFiles/W3SVC#########/。 此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。 請確定您 hello XSL 檔下載到 hello 與 hello XML 檔案，因為 hello XSL 檔案提供了用來格式化和篩選 hello hello XML 內容的功能相同的目錄檔案中 Internet Explorer 檢視時。
* **詳細錯誤記錄** - /LogFiles/DetailedErrors/。 此資料夾包含一或多個 .htm 檔案，內含已經發生的任何 HTTP 錯誤之詳細資訊。
* **Web 伺服器記錄** - /LogFiles/http/RawLogs。 這個資料夾包含一個或多個文字檔案格式是 「 hello [W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。
* **部署記錄** - /LogFiles/Git。 此資料夾包含 hello Azure web 應用程式，所使用的內部部署處理序所產生的記錄檔，以及記錄檔中的 Git 部署。

### <a name="ftp"></a>FTP
使用 FTP，請瀏覽 hello tooaccess 診斷資訊**儀表板**hello 在 web 應用程式的[傳統入口網站](https://manage.windowsazure.com)。 在 hello**快速概覽**區段中，使用 hello **FTP 診斷記錄**連結使用 FTP tooaccess hello 記錄檔。 hello**部署/FTP 使用者**項目會列出 hello 應該使用的 tooaccess hello FTP 站台的使用者名稱。

> [!NOTE]
> 如果 hello**部署/FTP 使用者**未設定項目，或您忘了 hello 這個使用者的密碼，您可以建立新的使用者和密碼使用 hello**重設部署認證**hello中的連結**快速概覽**區段 hello**儀表板**。
>
>

### <a name="download-with-azure-powershell"></a>使用 Azure PowerShell 來下載
toodownload hello 記錄檔，啟動 Azure PowerShell 的新執行個體，並使用下列命令的 hello:

    Save-AzureWebSiteLog -Name webappname

這會將 hello hello hello 所指定的 web 應用程式的記錄檔儲存**-名稱**參數 tooa 檔名為**logs.zip** hello 目前目錄中。

> [!NOTE]
> 如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。
>
>

### <a name="download-with-azure-command-line-interface"></a>使用 Azure 命列列介面來下載
toodownload hello 記錄檔使用 hello Azure 命令列介面，開啟新的命令提示字元、 PowerShell、 Bash 或終端機工作階段，並輸入下列命令的 hello:

    azure site log download webappname

這樣會將儲存 hello 記錄檔中的 hello web 應用程式名為 'webappname' tooa 檔名為**diagnostics.zip** hello 目前目錄中。

> [!NOTE]
> 如果您尚未安裝 hello Azure 命令列介面 (Azure CLI)，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure CLI](../cli-install-nodejs.md)。
>
>

## <a name="how-to-view-logs-in-application-insights"></a>作法：在 Application Insights 中檢視記錄
Visual Studio Application Insights 提供工具來篩選和搜尋記錄檔和相關的 hello 記錄要求和其他事件。

1. Visual Studio 中加入 hello Application Insights SDK tooyour 專案。
   * 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選擇 [加入 Application Insights]。 系統將指導您完成包括建立 Application Insights 資源在內的所有步驟。 [深入了解](../application-insights/app-insights-asp-net.md)
2. 加入 hello 追蹤接聽項封裝 tooyour 專案。
   * 以滑鼠右鍵按一下專案，然後選擇 [管理 NuGet 套件]。 選取 `Microsoft.ApplicationInsights.TraceListener` [深入了解](../application-insights/app-insights-asp-net-trace-logs.md)
3. 上傳您的專案，然後執行 toogenerate 記錄資料。
4. 在 hello [Azure 入口網站](https://portal.azure.com/)，瀏覽 tooyour 新的 Application Insights 資源，並開啟**搜尋**。 您將會看到您的記錄資料，以及要求、使用情況及其他遙測。 某些遙測可能需要幾分鐘的時間 tooarrive： 按一下 重新整理。 [深入了解](../application-insights/app-insights-diagnostic-search.md)

[深入了解使用 Application Insights 的效能追蹤](../application-insights/app-insights-azure-web-apps.md)

## <a name="streamlogs"></a> 作法：串流記錄
在開發應用程式時，通常會很有用的 toosee 接近即時的記錄資訊。 這可以透過串流處理將記錄資訊 tooyour 開發環境中使用 Azure PowerShell 或 hello Azure 命令列介面完成。

> [!NOTE]
> 某些類型的記錄緩衝區寫入 toohello 記錄檔，可能會導致 hello 資料流中失序的事件。 例如，當使用者造訪網頁時，就會發生的應用程式記錄檔項目可能顯示 hello hello 相對應 HTTP 記錄項目 hello 網頁要求之前的資料流中。
>
> [!NOTE]
> 記錄檔資料流也會串流資訊寫入 tooany 文字檔案儲存在 hello **d:\\家用\\LogFiles\\** 資料夾。
>
>

### <a name="streaming-with-azure-powershell"></a>使用 Azure PowerShell 來串流
toostream 記錄資訊，請啟動 Azure PowerShell 的新執行個體，並使用下列命令的 hello:

    Get-AzureWebSiteLog -Name webappname -Tail

這會連接 toohello hello 所指定的 web 應用程式**-名稱**參數並開始串流處理資訊 toohello PowerShell 視窗，記錄檔事件發生於 hello web 應用程式。 將資料流寫入 toofiles 結尾.txt、.log 或.htm hello /LogFiles 目錄 （d: / 首頁/記錄檔） 中儲存的任何資訊 toohello 本機主控台。

toofilter 特定事件，例如錯誤，使用 hello **-訊息**參數。 例如：

    Get-AzureWebSiteLog -Name webappname -Tail -Message Error

toofilter 特定記錄類型，例如 HTTP、 使用 hello **-路徑**參數。 例如：

    Get-AzureWebSiteLog -Name webappname -Tail -Path http

toosee 的可用路徑，使用 hello-ListPath 參數清單。

> [!NOTE]
> 如果尚未安裝 Azure PowerShell，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure PowerShell](/develop/nodejs/how-to-guides/powershell-cmdlets/)。
>
>

### <a name="streaming-with-azure-command-line-interface"></a>使用 Azure 命令列介面來串流
toostream 記錄資訊，請開啟新的命令提示字元、 PowerShell、 Bash 或終端機工作階段，並輸入下列命令的 hello:

    azure site log tail webappname

將名為 'webappname' toohello web 應用程式連接，並開始串流處理資訊 toohello 視窗記錄事件發生於 hello web 應用程式。 將資料流寫入 toofiles 結尾.txt、.log 或.htm hello /LogFiles 目錄 （d: / 首頁/記錄檔） 中儲存的任何資訊 toohello 本機主控台。

toofilter 特定事件，例如錯誤，使用 hello **-篩選**參數。 例如：

    azure site log tail webappname --filter Error

toofilter 特定記錄類型，例如 HTTP、 使用 hello **-路徑**參數。 例如：

    azure site log tail webappname --path http

> [!NOTE]
> 如果您尚未安裝 hello Azure 命令列介面，或未設定它 toouse 您 Azure 訂用帳戶，請參閱[如何 tooUse Azure 命令列介面](../cli-install-nodejs.md)。
>
>

## <a name="understandlogs"></a> 作法：了解診斷記錄
### <a name="application-diagnostics-logs"></a>應用程式診斷記錄
應用程式診斷資訊是以特定格式儲存對於.NET 應用程式，根據您是否儲存記錄檔 toohello 檔案系統中，資料表儲存體，或 blob 儲存體。 hello 組基本的資料儲存為相同 hello 到所有的三個儲存體類型-hello 日期和時間 hello、 發生事件 hello 產生 hello 事件、 hello 事件類型 （資訊、 警告、 錯誤） 和 hello 事件訊息的處理序識別碼。

**檔案系統**

記錄的 toohello 檔案系統，或使用資料流接收的每一行將處於下列格式的 hello:

    {Date}  PID[{process id}] {event type/level} {message}

例如，錯誤事件會出現類似 toohello 下列：

    2014-01-30T16:36:59  PID[3096] Error       Fatal error on hello page!

記錄 toohello 檔案系統提供 hello 三個可用的方法，提供僅 hello 時間、 處理序識別碼、 事件層級，以及訊息的 hello 最基本的資訊。

**資料表儲存體**

當記錄 tootable 儲存體，其他屬性會使用的 toofacilitate 搜尋 hello 資料儲存在 hello 資料表，以及更細微 hello 事件的詳細資訊。 hello 下列屬性 （資料行） 會用於儲存在 hello 資料表中每個實體 （資料列）。

| 屬性名稱 | 值/格式 |
| --- | --- |
| PartitionKey |Hello 事件 yyyyMMddHH 格式的日期/時間。 |
| RowKey |可唯一識別此實體的 GUID 值 |
| Timestamp |發生 hello 日期和時間的 hello 事件 |
| EventTickCount |hello 發生日期和時間的 hello 事件，以刻度格式 （大於有效位數） |
| ApplicationName |hello web 應用程式名稱 |
| Level |事件層級 (例如，錯誤、警告、資訊) |
| EventId |這個事件的 hello 事件識別碼<p><p>如果沒有指定，預設 too0 |
| InstanceId |即使 hello hello web 應用程式的執行個體上發生 |
| Pid |處理序識別碼 |
| Tid |產生 hello 事件 hello 執行緒 hello 執行緒 ID |
| 訊息 |事件詳細資訊訊息 |

**Blob 儲存體**

當記錄 tooblob 儲存體，資料會儲存在逗號分隔值 (CSV) 格式。 類似的 tootable 儲存體的其他欄位會記錄的 tooprovide hello 事件的詳細資訊。 hello 下列屬性適用於在 hello CSV 的每個資料列：

| 屬性名稱 | 值/格式 |
| --- | --- |
| Date |發生 hello 日期和時間的 hello 事件 |
| Level |事件層級 (例如，錯誤、警告、資訊) |
| ApplicationName |hello web 應用程式名稱 |
| InstanceId |Hello 事件 hello web 應用程式的執行個體上發生 |
| EventTickCount |hello 發生日期和時間的 hello 事件，以刻度格式 （大於有效位數） |
| EventId |這個事件的 hello 事件識別碼<p><p>如果沒有指定，預設 too0 |
| Pid |處理序識別碼 |
| Tid |產生 hello 事件 hello 執行緒 hello 執行緒 ID |
| 訊息 |事件詳細資訊訊息 |

儲存在 blob 中的 hello 資料看起來類似 toohello 下列：

    date,level,applicationName,instanceId,eventTickCount,eventId,pid,tid,message
    2014-01-30T16:36:52,Error,mywebapp,6ee38a,635266966128818593,0,3096,9,An error occurred

> [!NOTE]
> hello hello 記錄檔的第一行會包含 hello 資料行標頭，此範例中所示。
>
>

### <a name="failed-request-traces"></a>失敗要求追蹤
失敗要求追蹤會儲存在名為 **fr######.xml**的 XML 檔案中。 toomake 它更容易 tooview hello 登入資訊、 名為的 XSL 樣式表**freb.xsl**所提供的 hello 相同目錄中如 hello XML 檔案。 在 Internet Explorer 中開啟其中一個 hello XML 檔案，將會使用 hello XSL 樣式表 tooprovide 格式化顯示 hello 追蹤資訊。 這會顯示類似 toohello 下列：

![hello 瀏覽器中檢視失敗的要求](./media/web-sites-enable-diagnostic-log/tws-failedrequestinbrowser.png)

### <a name="detailed-error-logs"></a>詳細錯誤記錄
詳細的錯誤記錄指的是可針對發生的 HTTP 錯誤提供更詳盡資訊的 HTML 文件。 由於它們都是單純的 HTML 文件，因此可以使用網頁瀏覽器來檢視。

### <a name="web-server-logs"></a>Web 伺服器記錄
hello web 伺服器記錄檔的格式是 hello [W3C 擴充的記錄檔格式](http://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)。 此項資訊可透過文字編輯器來讀取，或是運用 [記錄檔剖析器](http://go.microsoft.com/fwlink/?LinkId=246619)(英文) 之類的公用程式來剖析。

> [!NOTE]
> hello Azure web 應用程式所產生的記錄檔不支援 hello **s-computername**， **s ip**，或**cs 版本**欄位。
>
>

## <a name="nextsteps"></a> 後續步驟
* [如何 tooMonitor Web 應用程式](http://docs.microsoft.com/en-us/azure/app-service-web/web-sites-monitor)
* [在 Visual Studio 中疑難排解 Azure Web App](web-sites-dotnet-troubleshoot-visual-studio.md)
* [在 HDInsight 中分析 Web 應用程式記錄](http://gallery.technet.microsoft.com/scriptcenter/Analyses-Windows-Azure-web-0b27d413)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
>
>

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)
* Hello 舊入口網站 toohello 新入口網站的變更如指南 toohello:[巡覽參考 hello Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)
