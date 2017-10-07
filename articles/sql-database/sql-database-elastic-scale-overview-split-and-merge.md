---
title: "向外延展雲端資料庫之間的 aaaMoving 資料 |Microsoft 文件"
description: "說明如何 toomanipulate 分區移動資料，透過使用彈性的自我裝載服務資料庫和應用程式開發介面。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>在向外延展的雲端資料庫之間移動資料
如果您是軟體即服務開發人員，而且您的應用程式突然經過極大的需求，您會需要 tooaccommodate hello 成長。 所以，您加入了更多的資料庫 (分區)。 如何發佈 hello 資料 toohello 新資料庫而不會中斷 hello 資料完整性？ 使用 hello**分割合併工具**toomove 資料從受條件約束資料庫 toohello 新資料庫。  

為 Azure web 服務會執行 hello 分割合併工具。 系統管理員或開發人員會使用 hello 工具 toomove shardlet 不同的資料庫 （分區） 間 （從分區資料）。 hello 工具會使用分區對應管理 toomaintain hello 服務中繼資料資料庫中，並確保一致的對應。

![概觀][1]

## <a name="download"></a>下載
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>文件
1. [彈性資料庫分割合併工具教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Split-Merge 安全性設定](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [分割合併安全性考量](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [分區對應管理](sql-database-elastic-scale-shard-map-management.md)
5. [移轉現有的資料庫 tooscale 外](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [彈性資料庫功能概觀](sql-database-elastic-scale-introduction.md)
7. [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>為何要使用 hello 分割合併工具嗎？
**彈性**

應用程式需要 toostretch 超出 hello 限制單一 Azure SQL DB 資料庫的彈性。 使用 hello 工具 toomove 資料做為所需的 toonew 資料庫，同時保有完整性。

**分割 toogrow** 

您需要 tooincrease 整體容量 toohandle 爆炸性成長。 toodo 分區化 hello 資料和散發以累加方式多個資料庫，直到符合容量需求，因此，建立額外的容量。 這是基本的使用範例 hello 'split' 功能。 

**合併 tooshrink**

容量必須壓縮 toohello 商務的季節性本質上到期。 hello 工具可讓商務會變慢時 toofewer 延展單位調降規模。 hello 彈性延展分割合併服務中的 hello 'merge' 功能涵蓋這項需求。 

**移動 Shardlet 來管理作用區**

與每個資料庫的多個租用戶，shardlet tooshards hello 配置可能會導致 toocapacity 瓶頸，在某些分區。 這需要重新配置 shardlet 或移動忙碌的 shardlet toonew 或較少使用的分區。 

## <a name="concepts--key-features"></a>概念和重要功能
**客戶主控式服務**

以的客戶裝載服務的形式提供 hello 分割合併。 您必須部署並裝載在 Microsoft Azure 訂用帳戶中的 hello 服務。 您從 NuGet 下載的 hello 套件包含您的特定部署的 hello 資訊與組態範本 toocomplete。 請參閱 hello[分割合併教學課程](sql-database-elastic-scale-configure-deploy-split-and-merge.md)如需詳細資訊。 因為 hello 服務以執行您的 Azure 訂用帳戶中，您可以控制和設定大部分的 hello 服務的安全性層面。 hello 預設範本包含 hello 選項 tooconfigure SSL 憑證為基礎的用戶端驗證、 加密的預存的認證、 DoS 保護和 IP 限制。 您可以找到更多有關 hello 安全性層面 hello 下列文件中[分割合併安全性組態](sql-database-elastic-scale-split-merge-security-configuration.md)。

hello 預設部署一個背景工作與一個 web 角色執行的服務。 每個 Azure 雲端服務中使用 hello A1 VM 大小。 雖然部署 hello 封裝時，您無法修改這些設定，您無法在 hello （透過 hello Azure 入口網站) 執行雲端服務中的成功部署之後變更它們。 請注意該 hello 背景工作角色都不應該設定用於多個單一執行個體若是技術原因。 

**分區對應整合**

hello 分割合併服務互動的 hello 應用程式的 hello 分區對應。 當使用 hello 分割合併服務 toosplit 或合併的範圍或 toomove shardlet 分區之間，hello 服務會自動保留向上 toodate hello 分區對應。 toodo 因此 hello 服務連接 toohello 分區對應管理員 hello 應用程式資料庫，然後當作分割/合併/移動要求正在進行維護範圍和對應。 這可確保該 hello 分區對應一律顯示最新的檢視時分割合併作業會繼續。 分割時，merge range 和 shardlet 移動作業是移動 hello 來源分區 toohello 目標分區的 shardlet 批次來實作。 Hello shardlet 移動作業 hello shardlet 主旨 toohello 目前批次期間會標示為離線 hello 分區對應中，且無法使用資料依存路由連線使用 hello **OpenConnectionForKey**應用程式開發介面。 

**一致的 Shardlet 連線**

任何分區對應提供資料依存路由連線 toohello 分區儲存 hello shardlet 時開始一個新的批次的 shardlet 移動資料，會從 hello 分區對應這些 shardlet 遭到封鎖的應用程式開發介面 toohello 已清除和後續連線時hello 資料移動是順序 tooavoid 不一致的問題進行中。 在 hello 相同分區化也會取得清除時，但會一次成功連線 tooother shardlet 立即在重試。 移動 hello 批次時，一旦 hello shardlet 標記為線上，再為 hello 目標分區，並從 hello 來源分區移除 hello 來源資料。 hello 服務會執行下列步驟，每個批次，直到所有 shardlet 已都移動。 這會導致 tooseveral 連線終止作業 hello 課程 hello 完成分割/合併/移動作業的期間。  

**管理 Shardlet 可用性**

限制 hello 連接終止的 shardlet 如同上面所討論的 toohello 目前批次會無法使用 tooone 批次的 shardlet 的 hello 範圍限制一次。 這是慣用方法其中 hello 完成分區會保持離線狀態及其所有 shardlet hello 課程分割或合併作業的期間。 批次，一次定義為 hello 數目相異的 shardlet toomove hello 大小是設定參數。 它可以定義每個分割及合併作業視 hello 應用程式的可用性和效能需求而定。 請注意，正在鎖定 hello 分區對應中的 hello 範圍可能大於指定的 hello 批次大小。 這是因為 hello 服務會挑選 hello 範圍的大小，使得 hello 的分區化索引鍵值 hello 資料中的實際數目大約符合 hello 批次大小。 這是重要的 tooremember 特別沒有嚴密填入的分區化索引鍵。 

**中繼資料儲存體**

hello 分割合併服務會使用其狀態和 tookeep 要求處理期間會記錄資料庫 toomaintain。 hello 使用者在其訂用帳戶中建立此資料庫，並提供它 hello 連接字串 hello hello 服務部署的組態檔中。 從 hello 使用者的組織的系統管理員也可以連接 toothis 資料庫 tooreview 要求進度和 tooinvestigate 詳細潛在的失敗有關的資訊。

**分區化感知**

hello 分割合併服務區別 （1） 分區化資料表、 （2） 的參考資料表，以及 （3） 標準的資料表。 hello 語意分割/合併/移動作業使用的 hello 資料表 hello 類型而定，以及定義如下： 

* **分區化資料表**： 分割、 合併和移動作業從來源 tootarget 分區中移動 shardlet。 Hello 順利完成之後整體要求，這些 shardlet 不再存在 hello 來源。 請注意，需要在 hello 目標分區 tooexist hello 目標資料表，而且不能包含的 hello 作業的 hello 目標範圍先前 tooprocessing 中的資料。 
* **參考資料表**： 參考資料表，hello 分割合併，並移動作業的 hello 資料複製 hello 來源 toohello 目標分區。 不過請注意，是否任何資料列已存在於此資料表上 hello 目標 hello 目標分區給定資料表上會發生任何變更。 hello 資料表具有空的未處理任何參考資料表複製作業 tooget toobe。
* **其他資料表**： 其他資料表可以在 hello 來源或分割及合併作業的 hello 目標存在。 hello 分割合併服務會忽略這些資料表的任何資料移動或複製作業。 但是請注意，在有條件約束時，它們會干擾這些作業。

hello 與分區化資料表的參考資訊係由 hello **SchemaInfo** hello 分區對應上的應用程式開發介面。 hello 下列範例會說明這些 Api 上指定的分區對應管理員物件 smm hello 用法： 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

hello 資料表的 'region' 及 '民族' 定義為參考資料表，並將複製的分割/合併/移動作業。 ‘customer’ 和 ‘orders’ 接著定義為分區化資料表。 C_CUSTKEY 和 O_CUSTKEY 做為 hello 分區化索引鍵。 

**參考完整性**

hello 分割合併服務會分析資料表之間的相依性，並使用外部索引鍵主索引鍵關聯性 toostage hello 作業來移動參考資料表和 shardlet。 一般而言會先根據相依性順序複製參考資料表，然後在每個批次中再根據相依性順序複製 Shardlet。 這是必要的如此 hello 新資料到達時，系統會接受 FK PK hello 目標分區的條件約束。 

**分區對應一致性與最終完成**

失敗 hello 存在，請在 hello 分割合併服務任何中斷之後繼續作業，以外的工具 toocomplete 任何要求正在進行中。 不過，可能無法復原的情況下，例如遺失或無法修復危害 hello 目標分區時。 在這些情況下，某些原本 toobe 移動的 shardlet 可能繼續 tooreside hello 來源分區上。 hello 服務會確保 hello 必要的資料已順利複製的 toohello 目標後，才會更新 shardlet 對應。 當所有其資料已複製 toohello 目標，而且已成功更新 hello 對應的對應，Shardlet 只會刪除 hello 來源。 在開啟時 hello 範圍已經線上 hello 目標分區 hello 刪除作業就會發生在 hello 背景。 hello 分割合併服務一律可以確保儲存在 hello 分區對應中的 hello 對應的正確性。

## <a name="hello-split-merge-user-interface"></a>hello 分割合併使用者介面
hello 分割合併服務封裝包含背景工作角色和 web 角色。 hello web 角色是使用的 toosubmit 分割合併要求，以互動方式。 如下所示為 hello hello 使用者介面的主要元件：

* 作業類型： hello 作業類型是作業的控制 hello 種類的 hello 服務此要求所執行的選項按鈕。 您可以選擇 hello 分割、 合併和移動案例。 您也可以取消先前提交的作業。 您可以在範圍分區對應中使用分割、合併和移動等要求。 清單分區對應僅支援移動作業。
* 分區對應： hello 的下一節有關 hello 分區對應和 hello database 主控分區對應的要求參數封面資訊。 特別是，則需要 hello Azure SQL Database 伺服器和資料庫裝載 hello shardmap tooprovide hello 名稱、 認證 tooconnect toohello 分區對應資料庫，而且最後 hello hello 分區對應的名稱。 目前，hello 作業只會接受一組認證。 這些認證需要 toohave 足夠的權限 tooperform 變更 toohello 分區對應，以及在 hello 分區 toohello 使用者資料。
* 來源範圍 (分割和合併)：分割及合併作業會採用其低和高索引鍵處理該範圍。 toospecify unbounded 高索引鍵值，核取的操作 hello 「 高索引鍵是最大 」 核取方塊，並將 hello 高索引鍵欄位保留空白。 對應和其分區對應中的界限，hello 範圍索引鍵指定值，會執行不需要 tooprecisely 相符。 如果您未指定任何範圍界限完全 hello 服務將 hello 最接近的範圍為您自動推斷。 您可以指定的分區對應中使用 hello GetMappings.ps1 PowerShell 指令碼 tooretrieve hello 目前的對應。
* 分割來源行為 （分割）： 分割作業定義 hello 點 toosplit hello 來源範圍。 您藉由提供您要執行 hello 分割 toooccur hello 分區化索引鍵。 使用 [hello] 選項按鈕指定您是否要 hello 下半部的 hello （不含 hello 分割索引鍵） 的範圍 toomove，或是要 hello 上半部 toomove （包括 hello 分割索引鍵）。
* 來源 Shardlet （移動）： 移動作業會與不同分割或合併作業，因為它們不需要範圍 toodescribe hello 來源。 移動來源只需識別 hello 分區化索引鍵值您計劃 toomove。
* 目標分區 （分割）： 一旦您已經提供 hello 資訊 hello split 作業來源，您需要的 toodefine 您要執行 hello 資料 toobe 複製 tooby 提供 hello Azure SQL Db 伺服器及 hello 目標的資料庫名稱。
* 在目標範圍 （合併）： 合併作業移動 shardlet tooan 現有分區。 您可以識別 hello 現有分區藉由提供您想要使用 toomerge hello 現有範圍的 hello 範圍界限。
* 批次大小： hello 批次大小控制 hello 將離線期間 hello 資料移動一次的 shardlet 數目。 這是整數值都區分 toolong 週期的 shardlet 的停機時間時，可使用較小的值。 較大的值會增加所給定的 shardlet 是 hello 時間離線，但可能會改善效能。
* 作業識別碼 （取消）： 如果您不再需要的進行中作業，您可以取消 hello 作業提供其在此欄位中的作業識別碼。 您可以從 hello 要求狀態資料表擷取 hello 作業 ID （請參閱 > 一節 8.1） 或從您送出 hello 要求 hello 網頁瀏覽器中的 hello 輸出。

## <a name="requirements-and-limitations"></a>需求和限制
hello 目前的實作中的 hello 分割合併服務是主體 toohello 下列需求和限制： 

* hello 分區需要 tooexist 和 hello 分區對應中註冊，才能執行這些分區分割 merge 作業。 
* hello 服務不會建立資料表或其他任何資料庫物件會自動做為其作業的一部分。 這表示 hello 所有分區化資料表的結構描述和參考資料表需要 tooexist hello 目標分區先前 tooany 分割/合併/移動作業。 分區化資料表尤其是需要的 toobe 空 hello 範圍新 shardlet 的 toobe 分割/合併/移動作業所加入的位置中。 否則，hello 作業將會失敗 hello 目標分區執行 hello 初始一致性的檢查。 也請注意，如果 hello 參考資料表是空的只會複製參考資料，而且沒有任何一致性保證與 hello 參考資料表上的考慮 tooother 並行寫入作業。 我們建議您這樣做： 當執行分割/合併作業，任何寫入作業變更 toohello 參考資料表。
* hello 服務會依賴唯一索引或索引鍵包含 hello 分區化索引鍵 tooimprove 效能和可靠性，大型的 shardlet 所建立的資料列識別。 如此 hello 服務 toomove 資料即使細微比只 hello 分區化索引鍵值。 這有助於 tooreduce hello 最大記錄檔空間量以及 hello 作業期間所需的鎖定。 請考慮建立唯一索引或主索引鍵包括 hello 給定資料表上的分區化索引鍵，如果您想 toouse 該資料表具有分割/合併/移動要求。 基於效能考量，hello 分區化索引鍵應該是 hello hello 索引鍵或 hello 索引中的前置資料行。
* 在 hello 要求處理期間，某些 shardlet 資料可能會出現 hello 來源和 hello 目標分區。 這是必要 tooprotect 故障期間 hello shardlet 移動。 hello 與 hello 分區對應的分割-合併的整合可確保透過 hello 資料依存路由應用程式開發介面使用的連線 hello **OpenConnectionForKey**方法 hello 分區對應上的看不到任何不一致的中繼狀態。 不過，當連接 toohello 來源或 hello 目標分區不使用 hello **OpenConnectionForKey**方法，不一致的中繼狀態可能會看到當分割/合併/移動要求所進行的作業。 這些連線可能會顯示部分或重複的結果，根據 hello 計時或 hello 分區基礎 hello 連接。 這項限制目前包含彈性延展多-Shard-查詢所進行的 hello 連線。
* hello hello 分割合併服務的中繼資料資料庫必須不同的角色之間共用。 例如，角色執行臨時比 hello 生產角色需要 toopoint tooa 不同的中繼資料資料庫中的 hello 分割合併服務。

## <a name="billing"></a>計費
hello 分割合併服務會執行您的 Microsoft Azure 訂用帳戶中的雲端服務。 因此雲端服務的費用 tooyour hello 服務執行個體。 除非您經常執行分割/合併/移動作業，否則建議您刪除分割合併雲端服務。 這可以節省執行中或已部署的雲端服務執行個體的成本。 您可以重新部署並啟動您隨時可執行的設定，每當您需要 tooperform 分割或合併作業。 

## <a name="monitoring"></a>監視
### <a name="status-tables"></a>狀態資料表
hello 分割合併服務提供 hello **RequestStatus**監視的要求已完成與進行中的 hello 中繼資料存放區資料庫中的資料表。 hello 資料表會列出每個分割合併要求已送出的 toothis hello 分割合併服務執行個體的資料列。 它提供下列資訊為每個要求的 hello:

* **時間戳記**: hello hello 要求啟動時的日期和時間。
* **OperationId**： 唯一識別 hello 要求的 GUID。 這項要求也可以使用的 toocancel hello 作業仍在進行中時。
* **狀態**: hello hello 要求的目前狀態。 對於進行中的要求，它也會列出 hello 在哪一個 hello 是要求的目前階段。
* **CancelRequest**: 旗標，指出是否 hello 要求已取消。
* **進度**: hello 作業完成的百分比估計。 一個 50 的值會指出 hello 作業已完成大約 50%。
* **Details**：XML 值，提供更詳細的進度報表。 hello 進度 報表會隨著個資料列集都會從來源 tootarget 複製定期更新。 如果發生失敗或例外狀況，此資料行也包含 hello 失敗的詳細的資訊。

### <a name="azure-diagnostics"></a>Azure 診斷
hello 分割合併服務會使用 Azure 診斷以 Azure SDK 2.5 監視和診斷。 您控制 hello 診斷組態，如這裡所說明：[在 Azure 雲端服務和虛擬機器中啟用診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)。 hello 下載封裝包含兩個診斷組態-一個用於 hello web 角色，一個 hello 背景工作角色。 請遵循從 hello 指引，這些 hello 服務的診斷組態[Microsoft Azure 中雲端服務基本概念](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649)。 其中包括 hello 定義 toolog 效能計數器、 IIS 記錄檔、 Windows 事件記錄檔，以及分割合併應用程式事件記錄檔。 

## <a name="deploy-diagnostics"></a>部署診斷
tooenable 監視和診斷使用 hello hello NuGet 封裝，執行下列命令，使用 Azure PowerShell 的 hello 所提供的 hello web 和背景工作角色的診斷組態： 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

您可以找到更多有關如何 tooconfigure 和部署以下的診斷設定：[在 Azure 雲端服務和虛擬機器中啟用診斷](../cloud-services/cloud-services-dotnet-diagnostics.md)。 

## <a name="retrieve-diagnostics"></a>擷取診斷
您可以從 hello Azure hello 伺服器總管 樹狀目錄的組件中的 hello Visual Studio 伺服器總管，輕鬆存取您的診斷。 開啟 Visual Studio 執行個體，並在 hello 功能表列中按一下 [檢視] 和 [伺服器總管]。 按一下 hello Azure 圖示 tooconnect tooyour Azure 訂用帳戶。 然後瀏覽 tooAzure]-> [儲存體]-> [ <your storage account> ]-> [資料表]-> [WADLogsTable。 如需詳細資訊，請參閱 [使用伺服器總管瀏覽儲存體資源](http://msdn.microsoft.com/library/azure/ff683677.aspx)。 

![WADLogsTable][2]

hello WADLogsTable hello 上圖中反白顯示包含 hello hello 分割合併服務的應用程式記錄檔的事件詳細資訊。 請注意該 hello 的預設組態 hello 下載封裝導向到生產環境部署。 因此，記錄檔和計數器取自 hello 服務執行個體的 hello 間隔是大型 （5 分鐘）。 針對測試和開發，需要較低的 hello 間隔，藉由調整 hello web 或 hello 背景工作角色 tooyour hello 診斷設定。 Hello Visual Studio 伺服器總管 （請參閱上面說明） 中的 hello 角色上按一下滑鼠右鍵，然後調整 [hello 傳輸期間在 hello] 對話方塊中的 hello 診斷組態設定： 

![組態][3]

## <a name="performance"></a>效能
一般情況下，較佳的效能是 toobe 預期來自 hello 更高版本，Azure SQL Database 中的多個高效能服務層。 Hello 更高的服務層的高 IO、 CPU 和記憶體配置獲益 hello 大量複製和刪除 hello 分割合併服務所使用的作業。 因此，只針對這些資料庫用於已定義的增加 hello 服務層限制一段時間。

hello 服務也會執行驗證查詢做為其正常作業的一部分。 這些驗證查詢檢查 hello 目標範圍中的資料的非預期出現，並確保一致的狀態從會啟動任何分割/合併/移動作業。 這些查詢所有工作透過 hello 操作與 hello 批次大小為 hello 要求定義的一部分提供的 hello 範圍所定義的分區化索引鍵範圍。 這些查詢會具有最佳的索引時有 hello 分區化索引鍵如下 hello 開頭的資料行，以便於出現。 

此外，hello 分區化索引鍵為 hello 前置資料行的唯一性屬性將可讓 hello 服務 toouse，限制資源耗用量，以記錄檔空間和記憶體最佳化的方法。 這個唯一性屬性是必要的 toomove 大型的資料大小 （通常超過 1 GB)。 

## <a name="how-tooupgrade"></a>如何 tooupgrade
1. 中的 hello 步驟[部署分割合併服務](sql-database-elastic-scale-configure-deploy-split-and-merge.md)。
2. 變更雲端服務組態檔的分割合併部署 tooreflect hello 新組態參數。 新的必要的參數是 hello hello 用於加密的憑證資訊。 輕鬆 toodo 這是 toocompare hello 新設定的範本檔從 hello 下載針對現有的組態。 請確認您新增 hello"DataEncryptionPrimaryCertificateThumbprint"和"DataEncryptionPrimary"hello web 和設定 hello 背景工作角色。
3. 在部署之前 hello 更新 tooAzure，確定所有目前執行分割合併作業已完成。 您可以輕鬆地執行這項操作藉由查詢要求進行中的 hello 分割合併中繼資料資料庫中的 hello RequestStatus 和 PendingWorkflows 資料表。
4. 更新現有的雲端服務部署，您的 Azure 訂閱 hello 新的套件和更新的服務組態檔中的分割合併。

您不需要分割合併 tooupgrade tooprovision 新的中繼資料資料庫。 hello 新版本，將會自動升級現有的中繼資料資料庫 toohello 新版本。 

## <a name="best-practices--troubleshooting"></a>最佳作法和疑難排解
* 定義的測試租用戶並執行您最重要的分割/合併/移動作業與 hello 測試租用戶跨數個分區。 確定分區對應中定義的所有中繼資料是正確的 hello 作業不會違反條件約束或外部索引鍵。
* 保留 hello 測試租用戶的資料大小超過 hello 最大的資料大小的最大的租用戶 tooensure 未遇到資料大小相關問題。 這可協助您評估 hello 花的時間 toomove 周圍的單一租用戶上的上限。 
* 請確定您的結構描述允許刪除動作。 hello 分割合併服務需要來自 hello 來源分區 hello 能力 tooremove 資料 hello 資料已順利複製的 toohello 目標後。 例如，**刪除觸發程序**可以避免 hello 服務刪除 hello hello 來源資料，而導致作業 toofail。
* hello 分區化索引鍵應該是主索引鍵或唯一索引定義中的 hello 前端資料行。 這可確保 hello hello 最佳效能分割或合併驗證查詢和 hello 實際的資料移動和刪除作業一律在分區化索引鍵範圍上運作。
* 共置分割合併服務在您的資料庫所在的 hello 區域及資料中心。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png

