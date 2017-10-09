---
title: "aaaUse hello Azure 儲存體模擬器進行開發和測試 |Microsoft 文件"
description: "hello Azure 儲存體模擬器會提供可用的本機開發環境，供開發及測試您的 Azure 儲存體應用程式。 了解如何驗證要求，如何從您的應用程式，以及如何 toouse hello 命令列工具 tooconnect toohello 模擬器。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 7cbe6ef5f172bb526c9d8a329b2fe9e6c0ec59d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>使用 hello Azure 儲存體模擬器進行開發和測試

hello Microsoft Azure 儲存體模擬器提供本機模擬的環境，供開發應用程式的 hello Azure Blob、 佇列和表格服務。 使用 hello 儲存體模擬器，您可以測試您的應用程式對 hello 儲存體服務在本機，而不需要建立 Azure 訂用帳戶，或支付任何費用。 當您滿意您的應用程式在 hello 模擬器中運作時，您可以切換 toousing hello 雲端中的 Azure 儲存體帳戶。

## <a name="get-hello-storage-emulator"></a>取得 hello 儲存體模擬器
hello 儲存體模擬器是可用的 hello 一部分[Microsoft Azure SDK](https://azure.microsoft.com/downloads/)。 您也可以安裝 hello 儲存體模擬器使用 hello[獨立安裝程式](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409)（直接下載）。 tooinstall hello 儲存體模擬器，您必須在電腦上有管理權限。

hello 儲存體模擬器目前只會在執行 Windows。 這些考量適用於 Linux 的儲存體模擬器的其中一個選項是 hello 社群維護，開放原始碼儲存體模擬器[Azurite](https://github.com/arafato/azurite)。

> [!NOTE]
> 建立在 hello 儲存體模擬器的其中一個版本的資料不保證 toobe 存取時使用不同版本。 如果您需要 toopersist 資料 hello 長期來看，我們建議您在 Azure 儲存體帳戶，而不是 hello 儲存體模擬器中儲存該資料。
> <p/>
> hello 儲存體模擬器 hello OData 程式庫的特定版本而定。 取代 hello 與其他版本的儲存體模擬器所用的 hello OData Dll 不支援，並可能會造成非預期的行為。 不過，任何版本的 hello 儲存體服務支援 OData 可能使用的 toosend 要求 toohello 模擬器。
>

## <a name="how-hello-storage-emulator-works"></a>Hello 儲存體模擬器的運作方式
hello 儲存體模擬器會使用本機 Microsoft SQL Server 執行個體和 hello 本機檔案系統 tooemulate Azure 儲存體服務。 根據預設，hello 儲存體模擬器會使用在 Microsoft SQL Server 2012 Express 的 LocalDB 資料庫。 您可以選擇 tooconfigure hello 儲存體模擬器 tooaccess 而 hello LocalDB 執行個體不是本機的 SQL Server 執行個體。 如需詳細資訊，請參閱 hello[開始和初始化 hello 儲存體模擬器](#start-and-initialize-the-storage-emulator)本文中稍後的章節。

hello 儲存體模擬器連接 tooSQL Server 或 LocalDB 使用 Windows 驗證。

Hello 儲存體模擬器和 Azure 儲存體服務之間，有一些功能差異。 如需有關這些差異的詳細資訊，請參閱 hello [hello 儲存體模擬器和 Azure 儲存體之間的差異](#differences-between-the-storage-emulator-and-azure-storage)本文中稍後的章節。

## <a name="start-and-initialize-hello-storage-emulator"></a>啟動並初始化 hello 儲存體模擬器
toostart hello Azure 儲存體模擬器：
1. 選取 hello**啟動**按鈕或按 hello **Windows**索引鍵。
1. 開始輸入 `Azure Storage Emulator`。
1. 從 hello 顯示應用程式清單中選取 hello 模擬器。

Hello 儲存體模擬器啟動時，會出現在命令提示字元視窗。 您可以使用此主控台視窗 toostart 和停止 hello 儲存體模擬器、 清除資料、 取得狀態，並初始化 hello 模擬器。 如需詳細資訊，請參閱 hello[儲存體模擬器命令列工具參考](#storage-emulator-command-line-tool-reference)本文中稍後的章節。

當 hello 模擬器正在執行時，您會看到 hello Windows 工作列通知區域中的圖示。

當您關閉 hello 儲存體模擬器命令提示字元視窗時，hello 儲存體模擬器會繼續 toorun。 toobring hello 儲存體模擬器的主控台視窗一次，請遵循先前步驟啟動 hello 儲存體模擬器的 hello。

hello 第一次執行 hello 儲存體模擬器，hello 本機儲存體環境會為您初始化。 hello 初始化處理程序會在 LocalDB 中建立資料庫，並保留為每個本機儲存體服務的 HTTP 連接埠。

hello 儲存體模擬器預設會安裝太`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`。

> [!TIP]
> 您可以使用 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)toowork 使用本機儲存體模擬器的資源。 尋找"（開發） 」 在 「 儲存體帳戶 」 hello 儲存體總管資源樹狀目錄中安裝及啟動 hello 儲存體模擬器之後。
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>初始化 hello 儲存體模擬器 toouse 不同的 SQL 資料庫
您可以使用 hello 儲存體模擬器命令列工具 tooinitialize hello 儲存體模擬器 toopoint tooa SQL 資料庫執行個體以外 hello 預設 LocalDB 執行個體：

1. 開啟 hello 的儲存體模擬器主控台視窗 hello 中所述[開始和初始化 hello 儲存體模擬器](#start-and-initialize-the-storage-emulator)> 一節。
1. 在 hello 主控台視窗中，輸入下列命令，hello 其中`<SQLServerInstance>`hello hello SQL Server 執行個體的名稱。 toouse LocalDB，指定`(localdb)\MSSQLLocalDb`與 hello SQL Server 執行個體。

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  您也可以使用下列命令，引導 hello 模擬器 toouse hello 預設 SQL Server 執行個體的 hello:

  `AzureStorageEmulator.exe init /server .\\`

  或者，您可以使用下列命令會重新初始化 hello 資料庫 toohello 預設 LocalDB 執行個體的 hello:

  `AzureStorageEmulator.exe init /forceCreate`

如需有關這些命令的詳細資訊，請參閱[儲存體模擬器命令列工具參考](#storage-emulator-command-line-tool-reference)。

> [!TIP]
> 您可以使用 hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) (SSMS) toomanage 您的 SQL Server 執行個體，包括 hello LocalDB 安裝。 在 [hello SMSS**連接 tooServer** ] 對話方塊中，指定`(localdb)\MSSQLLocalDb`hello 中**伺服器名稱：**欄位 tooconnect toohello LocalDB 執行個體。

## <a name="authenticating-requests-against-hello-storage-emulator"></a>驗證要求對 hello 儲存體模擬器
一旦您已安裝並啟動 hello 儲存體模擬器，您可以測試您對它的程式碼。 如同 hello 雲端中的 Azure 儲存體，對 hello 儲存體模擬器的每個要求必須經過驗證，除非它是匿名的要求。 您可以驗證要求對使用共用金鑰驗證的 hello 儲存體模擬器，或使用共用的存取簽章 (SAS)。

### <a name="authenticate-with-shared-key-credentials"></a>使用共用金鑰認證進行驗證
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

如需連接字串的詳細資訊，請參閱[設定 Azure 儲存體連接字串](../storage-configure-connection-string.md)。

### <a name="authenticate-with-a-shared-access-signature"></a>使用共用存取簽章進行驗證
某些 Azure 儲存體用戶端程式庫，例如 hello Xamarin 程式庫，僅支援使用共用的存取簽章 (SAS) 權杖的驗證。 您可以建立 hello SAS 權杖使用這類工具 hello[存放裝置總管](http://storageexplorer.com/)或其他支援共用金鑰驗證的應用程式。

您也可以使用 Azure PowerShell 來產生 SAS 權杖。 hello 下列範例會產生具有完整權限 tooa blob 容器的 SAS 權杖：

1. 如果您尚未安裝 Azure PowerShell （使用 hello 最新版 Azure PowerShell cmdlet hello 建議使用）。 如需安裝指示，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps)。
2. 開啟 Azure PowerShell，然後執行下列命令、 取代 hello`ACCOUNT_NAME`和`ACCOUNT_KEY==`您自己的認證，和`CONTAINER_NAME`與您所選擇的名稱：

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

hello 產生共用的存取簽章 URI hello 新的容器應該類似：

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

使用此範例中建立的 hello 共用的存取簽章有效期為一天。 hello 簽章會授與完整存取權 （讀取、 寫入、 刪除、 列出） tooblobs hello 容器內。

如需共用存取簽章的詳細資訊，請參閱[在 Azure 儲存體中使用共用存取簽章 (SAS)](../storage-dotnet-shared-access-signature-part-1.md)。

## <a name="addressing-resources-in-hello-storage-emulator"></a>Hello 儲存體模擬器中的資源定址
hello hello 儲存體模擬器的服務端點是不同的 Azure 儲存體帳戶。 hello 差異是因為 hello 本機電腦不會執行網域名稱解析，需要 hello 儲存體模擬器端點 toobe 本機位址。

當您定址 Azure 儲存體帳戶中的資源時，您可以使用下列配置 hello。 hello 帳戶名稱是部分 hello URI 主機名稱，而要定址的 hello 資源是 hello URI 路徑的一部分：

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

例如，hello 下列 URI 是有效的 Azure 儲存體帳戶中的 blob 位址：

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

不過，hello 儲存體模擬器，因為 hello 本機電腦不會執行網域名稱解析，hello 帳戶名稱是 hello URI 路徑，而不是 hello 主機名稱的一部分。 使用下列 URI 格式資源 hello 儲存體模擬器中的 hello:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

例如，hello 下列位址可能會用於存取 hello 儲存體模擬器中的 blob:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

hello hello 儲存體模擬器的服務端點如下：

* Blob 服務：`http://127.0.0.1:10000/<account-name>/<resource-path>`
* 佇列服務：`http://127.0.0.1:10001/<account-name>/<resource-path>`
* 表格服務：`http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>次要使用 RA-GRS 定址的 hello 帳戶
從 3.1 版開始，hello 儲存體模擬器支援讀取權限的地理備援複寫 (RA-GRS)。 如需 hello 雲端中與 hello 本機模擬器中的儲存體資源，您可以存取 hello 次要位置藉由附加-次要 toohello 帳戶名稱。 例如，下列位址的 hello 可能用於存取 blob，使用 hello 儲存體模擬器中的 hello 唯讀次要複本：

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> 以程式設計方式存取 toohello 次要與 hello 儲存體模擬器，使用 hello 儲存體用戶端程式庫適用於.NET 3.2 版或更新版本。 請參閱 hello [Microsoft Azure 儲存體用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)如需詳細資訊。
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>儲存體模擬器命令列工具參考
從 3.0 版開始，便會在啟動 hello 儲存體模擬器時，顯示在主控台視窗。 使用 hello 主控台視窗 toostart 和停止 hello 模擬器，以及查詢中的 hello 命令列狀態，並執行其他作業。

> [!NOTE]
> 如果您有 Microsoft Azure 計算模擬器安裝的 hello，當您啟動 hello 儲存體模擬器時，會出現系統匣圖示。 以滑鼠右鍵按一下 hello 圖示 tooreveal 提供圖形化方式 toostart 功能表，並停止 hello 儲存體模擬器。
>
>

### <a name="command-line-syntax"></a>命令列語法
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>選項
tooview hello 選項清單，型別`/help`hello 的命令提示字元。

| 選項 | 說明 | 命令 | 引數 |
| --- | --- | --- | --- |
| **啟動** |Hello 儲存體模擬器會啟動。 |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: hello 目前處理序而不是建立新的處理序中啟動 hello 模擬器。 |
| **停止** |停駐點 hello 儲存體模擬器。 |`AzureStorageEmulator.exe stop` | |
| **狀態** |列印 hello hello 儲存體模擬器的狀態。 |`AzureStorageEmulator.exe status` | |
| **Clear** |清除 hello hello 命令列上指定的所有服務中的資料。 |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*：清除 blob 資料。 <br/>*queue*：清除佇列資料。 <br/>*table*：清除資料表資料。 <br/>*all*：清除所有服務中的所有資料。 |
| **Init** |執行一次初始化 tooset 向上 hello 模擬器。 |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-server serverName\instanceName*： 指定 hello 伺服器裝載 hello SQL 執行個體。 <br/>*-sqlinstance instanceName*： 指定 hello hello 預設伺服器執行個體中使用的 SQL 執行個體 toobe hello 名稱。 <br/>*-forcecreate*： 強制建立 hello SQL 資料庫，即使它已經存在。 <br/>*-skipcreate*： 略過建立 hello SQL 資料庫。 其優先順序高於 -forcecreate。<br/>*-reserveports*： 嘗試 tooreserve hello HTTP 連接埠與 hello 服務相關聯。<br/>*-unreserveports*： 嘗試與 hello 服務相關聯的 hello HTTP 連接埠 tooremove 保留項目。 其優先順序高於 -reserveports。<br/>*-inprocess*: hello 目前處理序而不是產生新的處理序中執行初始化。 如果變更保留連接埠，必須以更高權限啟動 hello 目前處理序。 |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Hello 儲存體模擬器和 Azure 儲存體之間的差異
Hello 儲存體模擬器是模擬的環境，在本機的 SQL 執行個體中執行，因為有功能差異 hello 模擬器和 Azure 儲存體帳戶之間 hello 雲端中：

* hello 儲存體模擬器支援將只能使用單一固定的帳戶及已知的驗證金鑰。
* hello 儲存體模擬器不是可擴充的儲存體服務，並不支援大量並行用戶端。
* 中所述[hello 儲存體模擬器中的資源定址](#addressing-resources-in-the-storage-emulator)，資源會以不同的方式定址 hello 儲存體模擬器與 Azure 儲存體帳戶中。 這項差異是因為在 hello 雲端，但不是 hello 本機電腦上使用網域名稱解析。
* 從 3.1 版開始，hello 儲存體模擬器帳戶支援讀取權限的地理備援複寫 (RA-GRS)。 在 hello 模擬器中，所有帳戶都具有 RA-GRS 啟用，而且永遠不會有延遲之間 hello 主要和次要複本。 會支援 hello 帳戶次要 hello 取得 Blob 服務統計資料、 取得的佇列服務統計資料，並取得表格服務統計資料的作業，而且一律會傳回 hello hello 值`LastSyncTime`回應項目如 hello 目前時間相應 toohello 基礎SQL 資料庫。
* hello 檔案服務，並在 hello 儲存體模擬器目前不支援 SMB 通訊協定服務端點。
* 如果您使用尚未支援 hello 模擬器 hello 儲存體服務版本，hello 儲存體模擬器傳回 VersionNotSupportedByEmulator 錯誤 （HTTP 狀態碼 400-不正確的要求）。

### <a name="differences-for-blob-storage"></a>Blob 儲存體的差異
hello 下列差異適用於 tooBlob hello 模擬器中的儲存體：

* hello 儲存體模擬器僅支援向上 too2 GB 的 blob 大小。
* 累加式複製 」 可讓覆寫的 blob toobe 複製，它會傳回失敗 hello 服務上的快照集。
* 取得頁面範圍差異無法在使用累加複製 Blob 複製的快照之間運作。
* 即使尚未在 hello 要求中指定 hello 租用識別碼，可能會存在於儲存體模擬器，hello 作用中租用，blob 成功 Put Blob 作業。
* 附加的 Blob hello 模擬器不支援作業。 在附加 Blob 上嘗試作業會傳回 FeatureNotSupportedByEmulator 錯誤 (HTTP 狀態碼 400-不正確的要求)。

### <a name="differences-for-table-storage"></a>資料表儲存體的差異
hello 下列差異適用於 tooTable hello 模擬器中的儲存體：

* Hello hello 儲存體模擬器中的表格服務中的日期屬性支援只會 hello （它們是必要的 toobe 晚於 1753 年 1 月 1 日） 的 SQL Server 2005 所支援的範圍。 1753 年 1 月 1 日之前的所有日期已都變更 toothis 值。 hello 有效位數的日期是有限的 toohello 有效位數的 SQL Server 2005，亦即會精確 too1/300 秒。
* hello 儲存體模擬器支援小於 512 個位元組的每個資料分割索引鍵和資料列索引鍵屬性值。 此外，hello hello 帳戶名稱、 資料表名稱，以及索引鍵屬性名稱的大小總計一起不得超過 900 個位元組。
* hello hello 儲存體模擬器中的資料表中的資料列的大小總計為有限的 tooless 超過 1 MB。
* 在 hello 儲存體模擬器中，屬性的資料，請輸入`Edm.Guid`或`Edm.Binary`支援只 hello`Equal (eq)`和`NotEqual (ne)`比較運算子在查詢中的篩選字串。

### <a name="differences-for-queue-storage"></a>佇列儲存體的差異
Hello 模擬器中有任何差異特定 tooQueue 存放裝置。

## <a name="storage-emulator-release-notes"></a>儲存體模擬器版本資訊
### <a name="version-52"></a>5.2 版
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的 2017年-04-17 版 hello 儲存體服務。
* 已修正資料表屬性值未正確編碼的錯誤。

### <a name="version-51"></a>版本 5.1
* 修正的 bug 其中 hello 儲存體模擬器已傳回 hello`DataServiceVersion`其中 hello 服務未某些回應中的標頭。

### <a name="version-50"></a>版本 5.0
* hello 儲存體模擬器安裝程式不會再檢查現有的 MSSQL，.NET Framework 安裝。
* hello 儲存體模擬器的安裝程式不會再建立 hello 資料庫做為安裝的一部分。 必要時仍會隨著啟動建立資料庫。
* 建立資料庫不再需要提高權限。
* 啟動不再需要保留連接埠。
* 新增下列選項太 hello`init`: `-reserveports` （需要提高權限） `-unreserveports` （需要提高權限） `-skipcreate`。
* hello 儲存體模擬器 UI 選項 hello 系統匣圖示現在會啟動 hello 命令列介面。 hello 舊 GUI 已無法再使用。
* 某些 DLL 已移除或重新命名。

### <a name="version-46"></a>版本 4.6
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的 hello 儲存體服務版本 2016年-05-31。

### <a name="version-45"></a>版本 4.5
* 修正造成初始設定和安裝 hello 儲存體模擬器 toofail 時備份資料庫的 hello 已重新命名的 bug。

### <a name="version-44"></a>4.4 版
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的 hello 儲存體服務版本 2015年-12-11。
* hello blob 資料的儲存體模擬器回收時，現在更有效率地處理大量的 blob。
* 修正造成容器 ACL XML toobe 從解 hello 儲存體服務運作方式稍有不同驗證的 bug。
* 修正的 bug，有時會造成最大值和最小日期時間值 toobe 報告以 hello 正確時區為準。

### <a name="version-43"></a>版本 4.3
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的版本 2015年-07-08 hello 儲存體服務。

### <a name="version-42"></a>4.2 版
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的 hello 儲存體服務版本 2015年-04-05。

### <a name="version-41"></a>4.1 版
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點，除了 hello 新附加 Blob 功能上的版本 2015年-02-21 hello 儲存體服務。
* 如果您使用尚未支援 hello 模擬器 hello 儲存體服務版本，hello 模擬器就會傳回有意義的錯誤訊息。 我們建議使用 hello hello 模擬器最新版本。 如果您碰到 VersionNotSupportedByEmulator 錯誤 （HTTP 狀態碼 400-不正確的要求），請下載 hello hello 儲存體模擬器最新版本。
* 修正的 bug 其中競爭條件造成資料表實體資料 toobe 並行合併作業期間不正確。

### <a name="version-40"></a>4.0 版
* hello 儲存體模擬器，可執行檔已重新命名過*AzureStorageEmulator.exe*。

### <a name="version-32"></a>3.2 版
* hello 儲存體模擬器現在支援 Blob、 佇列和表格服務端點上的 2014年-02-14 版 hello 儲存體服務。 Hello 儲存體模擬器目前不支援檔案服務端點。 請參閱[hello Azure 儲存體服務進行版本設定](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services)2014年-02-14 版的詳細資料。

### <a name="version-31"></a>3.1 版
* Hello 儲存體模擬器現在支援讀取權限的地理備援儲存體 (RA-GRS)。 hello 取得 Blob 服務統計資料、 取得的佇列服務統計資料，以及取得表格服務統計資料 Api 支援次要 hello 帳戶，並且永遠會傳回 hello hello LastSyncTime 回應項目的值為 hello 目前時間相應 toohello 基礎 SQL資料庫。 以程式設計方式存取 toohello 次要與 hello 儲存體模擬器，使用 hello 儲存體用戶端程式庫適用於.NET 3.2 版或更新版本。 如需詳細資訊，如.NET 參考看到 hello Microsoft Azure 儲存體用戶端程式庫。

### <a name="version-30"></a>3.0 版
* hello Azure 儲存體模擬器不再隨附於 hello 相同封裝成 hello 計算模擬器。
* hello 儲存體模擬器圖形化使用者介面是由可編寫指令碼的命令列介面所取代。 如需 hello 命令列介面的詳細資訊，請參閱儲存體模擬器命令列工具的參考。 hello 圖形化介面將繼續 toobe 3.0 版中，但它只能存取 hello 計算模擬器安裝 hello 系統匣圖示上按一下滑鼠右鍵，然後選取 顯示儲存體模擬器 UI 時。
* 2013-08-15 版 hello Azure 儲存體服務現在完整支援。 (先前只有儲存體模擬器 2.2.1 版預覽才支援此版本)。

## <a name="next-steps"></a>後續步驟

* 評估 hello 開放原始碼跨平台、 社群維護儲存體模擬器[Azurite](https://github.com/arafato/azurite)。 
* [使用適用於.NET 的 azure 儲存體範例](../storage-samples-dotnet.md)包含開發應用程式時，您可以使用連結 tooseveral 程式碼範例。
* 您可以使用 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com)toowork hello 儲存體模擬器和您的雲端儲存體帳戶中的資源。
