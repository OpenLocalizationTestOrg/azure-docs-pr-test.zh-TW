---
title: "aaaDeploy 分割合併服務 |Microsoft 文件"
description: "使用彈性資料庫工具來分割及合併"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>部署分割合併服務
hello 分割合併工具可讓您在分區化資料庫之間移動資料。 請參閱 [在相應放大的雲端資料庫之間移動資料](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>下載 hello 分割合併封裝
1. 下載 hello 最新的 NuGet 版本從[NuGet](http://docs.nuget.org/docs/start-here/installing-nuget)。
2. 開啟命令提示字元並瀏覽 toohello nuget.exe 的下載位置的目錄。 hello 下載包含 PowerShell commmands。
3. 下載 hello 最新的分割合併封裝到 hello 目前目錄中以 hello 下列命令：
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

hello 檔案會放置於名為**Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x**其中*x.x.xxx.x*反映 hello 版本號碼。 尋找 hello 的分割合併服務檔案 hello **content\splitmerge\service**子目錄，hello 分割合併 PowerShell 指令碼 （和必要的用戶端.dll 檔） 中 hello **content\splitmerge\powershell**子目錄。

## <a name="prerequisites"></a>必要條件
1. 建立 Azure SQL DB 資料庫，將用作 hello 分割合併狀態資料庫。 移 toohello [Azure 入口網站](https://portal.azure.com)。 建立新的 **SQL Database**。 提供 hello 資料庫的名稱，並建立新的系統管理員和密碼。 是確定 toorecord hello 名稱和密碼，供日後使用。
2. 請確定您的 Azure SQL DB 伺服器允許 Azure 服務 tooconnect tooit。 在 hello 入口網站中 hello**防火牆設定**，確保該 hello **tooAzure 服務允許存取**設定為太**上**。 按一下 [儲存] 圖示的 hello。
   
   ![允許的服務][1]
3. 建立要用於診斷輸出的 Azure 儲存體帳戶。 移 toohello Azure 入口網站。 Hello 左列中，按一下**新增**，按一下 **資料 + 儲存體**，然後**儲存體**。
4. 建立將包含分割合併服務的 Azure 雲端服務。  移 toohello Azure 入口網站。 Hello 左列中，按一下**新增**，然後**計算**，**雲端服務**，和**建立**。 

## <a name="configure-your-split-merge-service"></a>設定分割合併服務
### <a name="split-merge-service-configuration"></a>分割合併服務組態
1. 在您下載 hello 分割合併組件的 hello 資料夾中建立 的副本 hello **ServiceConfiguration.Template.cscfg**檔案一起出貨**SplitMergeService.cspkg**並將它重新命名**ServiceConfiguration.cscfg**。
2. 開啟**ServiceConfiguration.cscfg**驗證的輸入，例如 hello 格式的憑證指紋的 Visual Studio 這類文字編輯器中。
3. 建立新的資料庫或選擇現有的資料庫 tooserve 做為分割合併作業的 hello 狀態資料庫並擷取 hello 該資料庫的連接字串。 
   
   > [!IMPORTANT]
   > 此時，hello 狀態資料庫必須使用 hello 拉丁文定序 (SQL\_Latin1\_一般\_CP1\_CI\_AS)。 如需詳細資訊，請參閱 [Windows 定序名稱 (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx)。
   >

   使用 Azure SQL DB、 hello 連接字串通常是 hello 表單的：
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. 輸入此連接字串 hello cscfg 檔案中這兩個 hello **SplitMergeWeb**和**SplitMergeWorker** hello ElasticScaleMetadata 設定中的角色區段。
5. Hello **SplitMergeWorker**角色中，輸入有效的連接字串 tooAzure 儲存體 hello **WorkerRoleSynchronizationStorageAccountConnectionString**設定。

### <a name="configure-security"></a>設定安全性
Hello 服務的 tooconfigure hello 安全性的詳細的指示，請參閱 toohello[分割合併安全性組態](sql-database-elastic-scale-split-merge-security-configuration.md)。

本教學課程的簡單的測試部署的 hello 用途，最基本的組態步驟將會執行 tooget hello 服務啟動並執行。 這些步驟會啟用只 hello 一個機器/帳戶執行它們 toocommunicate 與 hello 服務。

### <a name="create-a-self-signed-certificate"></a>建立自我簽署憑證
建立新的目錄，下列命令會使用這個目錄執行 hello 從[Visual Studio 的開發人員命令提示字元](http://msdn.microsoft.com/library/ms229859.aspx)視窗：

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

會要求您輸入的密碼 tooprotect hello 私用金鑰。 輸入強式密碼並加以確認。 您接著會提示輸入 hello 密碼 toobe 之後，一次使用。 按一下**是**在 hello 結束 tooimport 它 toohello 受信任憑證授權單位的根存放區。

### <a name="create-a-pfx-file"></a>建立 PFX 檔案
執行下列命令從 hello hello 執行 makecert 所在; 相同的視窗使用 hello 相同的密碼，您使用的 toocreate hello 憑證：

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Hello 用戶端憑證匯入到個人存放區 hello
1. 在 Windows 檔案總管中，按兩下 [MyCert.pfx] 。
2. 在 [hello**憑證匯入精靈**選取**目前使用者**按一下**下一步]**。
3. 確認 hello 檔案路徑，然後按一下**下一步**。
4. 輸入 hello 密碼保持**包含所有延伸的屬性**檢查，然後按一下**下一步**。
5. 保留**hello 自動選取憑證存放區 […]**檢查，然後按一下**下一步**。
6. 按一下 [完成] 和 [確定]。

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>上傳 hello PFX 檔案 toohello 雲端服務
1. 移 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選取 [雲端服務] 。
3. 選取先前建立的 hello 分割/合併服務的 hello 雲端服務。
4. 按一下**憑證**hello 上方功能表上。
5. 按一下**上傳**hello 下方列中。
6. 選取 hello PFX 檔案，然後輸入 hello 與上面相同的密碼。
7. 完成後，複製 hello hello 清單中的新項目中的 hello 憑證指紋。

### <a name="update-hello-service-configuration-file"></a>更新 hello 服務組態檔
貼上上述複製 hello 指紋/value 屬性，這些設定的 hello 憑證指紋。
Hello 背景工作角色：
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Hello web 角色：

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

請注意，不同的憑證應該用於 hello CA，來加密，生產環境部署的 hello 伺服器憑證和用戶端憑證。 如需詳細指示，請參閱 [安全性設定](sql-database-elastic-scale-split-merge-security-configuration.md)。

## <a name="deploy-your-service"></a>部署您的服務
1. 移 toohello [Azure 入口網站](https://manage.windowsazure.com)。
2. 按一下 hello**雲端服務**hello 左側索引標籤，選取您稍早建立的 hello 雲端服務。
3. 按一下 [儀表板] 。
4. 選擇 hello 預備環境，然後按一下**上傳新的預備環境部署**。
   
   ![預備][3]
5. 在 [hello] 對話方塊中，輸入部署標籤。 「 封裝 」 和 「 設定 」 中，按一下 ' 從 Local'，然後選擇 hello **SplitMergeService.cspkg**檔案與您先前設定的.cscfg 檔案。
6. 請確定該 hello 核取方塊標示為**即使一個或多個角色包含單一執行個體部署**已核取。
7. 叫用 hello 底部右 toobegin hello 部署中的 hello 刻度按鈕。 預期 tootake 幾分鐘的時間 toocomplete。

   ![上傳][4]

## <a name="troubleshoot-hello-deployment"></a>疑難排解 hello 部署
如果您的 web 角色失敗 toocome 線上，可能是 hello 安全性組態有問題。 請檢查該 hello 上面所述，設定 SSL。

如果背景工作角色失敗 toocome 線上，但您的 web 角色會成功，則最有可能連接您稍早建立的 toohello 狀態資料庫時發生問題。

* 請確定您的.cscfg 中的 hello 連接字串正確無誤。
* 請檢查確定 hello 伺服器和資料庫存在，而且 hello 使用者識別碼和密碼正確無誤。
* Azure SQL db，hello 格式應該是 hello 連接字串：

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* 請確定該 hello 伺服器名稱開頭不是**https://**。
* 請確定您的 Azure SQL DB 伺服器允許 Azure 服務 tooconnect tooit。 toodo，開啟 https://manage.windowsazure.com、 向左 hello 按一下 「 SQL 資料庫 」，在 hello 頂端，按一下 [伺服器] 然後選取您的伺服器。 按一下**設定**在 hello 排名最前面，並確保該 hello **Azure 服務**設定為太"Yes"。 (請參閱 hello 必要條件 > 一節的這篇文章 hello 頂端)。

## <a name="test-hello-service-deployment"></a>測試 hello 服務部署
### <a name="connect-with-a-web-browser"></a>使用網頁瀏覽器連接
判斷您的分割合併服務的 hello web 端點。 您可以依移 toohello hello Azure 傳統入口網站中找到這**儀表板**您的雲端服務和下方**網站 URL** hello 右側。 取代**http://**與**https://**因為 hello 預設安全性設定停用 hello HTTP 端點。 此 url hello 頁面載入瀏覽器。

### <a name="test-with-powershell-scripts"></a>使用 PowerShell 指令碼進行測試
hello 部署和您的環境，可以透過執行包含的 hello 範例 PowerShell 指令碼測試。

包含的 hello 指令碼檔案會：

1. **SetupSampleSplitMergeEnvironment.ps1** - 設定分割/合併的測試資料層 (請參閱下表中的詳細說明)
2. **ExecuteSampleSplitMerge.ps1** -hello 測試的測試作業會執行資料層 （請參閱下的表詳細說明）
3. **GetMappings.ps1** -最上層的範例指令碼會列印出 hello 的 hello 分區對應的目前狀態。
4. **ShardManagement.psm1** -包裝的協助程式指令碼 hello ShardManagement 應用程式開發介面
5. **SqlDatabaseHelpers.psm1** - 用來建立及管理 SQL 資料庫的協助程式指令碼
   
   <table style="width:100%">
     <tr>
       <th>PowerShell 檔案</th>
       <th>步驟</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    建立分區對應管理員資料庫</td>
     </tr>
     <tr>
       <td>2.    建立 2 個分區資料庫。
     </tr>
     <tr>
       <td>3.    建立這些資料庫的分區對應 (刪除這些資料庫上的任何現有分區對應)。 </td>
     </tr>
     <tr>
       <td>4.    在這兩個 hello 分區中, 建立小型範例資料表，並填入其中一種 hello 分區 hello 資料表。</td>
     </tr>
     <tr>
       <td>5.    宣告 hello SchemaInfo hello 分區化資料表。</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>PowerShell 檔案</th>
       <th>步驟</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    傳送的分割要求 toohello 分割合併服務 web 前端，可將來自 hello 第一個分區 toohello 第二個分區的一半 hello 資料分割。</td>
     </tr>
     <tr>
       <td>2.    輪詢 hello hello 分割要求的狀態並等待，直到完成 hello 要求的 web 前端。</td>
     </tr>
     <tr>
       <td>3.    傳送的合併要求 toohello 分割合併服務 web 前端，將 hello 資料移從 hello 第二個分區後 toohello 第一個分區。</td>
     </tr>
     <tr>
       <td>4.    輪詢 hello web 前端的 hello 合併要求的狀態並等待直到 hello 要求完成為止。</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>使用 PowerShell tooverify 部署
1. 開啟新的 PowerShell 視窗並瀏覽 toohello 下載的目錄，hello 分割合併封裝，，然後瀏覽到 hello"powershell"目錄。
2. 建立 Azure SQL database 伺服器 （或選擇現有的伺服器），將建立 hello 分區對應管理員和分區。
   
   > [!NOTE]
   > hello SetupSampleSplitMergeEnvironment.ps1 指令碼會建立這些資料庫上 hello 預設 tookeep hello 指令碼簡單的同一部伺服器。 這不是限制的 hello 分割合併服務本身。
   >
   
   具有讀取/寫入存取 toohello hello 分割合併服務 toomove 資料和更新 hello 分區對應時需要資料庫的 SQL 驗證登入。 Hello 分割合併服務是在 hello 雲端執行，因為它目前不支援整合式驗證。
   
   請確定已 hello Azure SQL server tooallow hello IP 位址執行下列指令碼的 hello 機器的存取權。 您可以找到此設定下 hello Azure SQL server / 設定 / 允許的 IP 位址。
3. 執行 hello SetupSampleSplitMergeEnvironment.ps1 指令碼 toocreate hello 範例環境。
   
   執行這個指令碼將會清除任何現有的分區對應管理資料結構上 hello 分區對應管理員資料庫與 hello 分區。 如果您希望 toore 初始化 hello 分區對應或分區，它可能會有用 toorerun hello 指令碼。
   
   範例命令列：

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Hello 範例環境中執行 hello Getmappings.ps1 指令碼 tooview hello 對應目前存在。
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Split 作業 （hello 第一個分區 toohello 第二個分區上移動半 hello 資料），然後合併作業 （hello 將資料移回至 hello 第一個分區），請執行 hello ExecuteSampleSplitMerge.ps1 指令碼 tooexecute。 如果您已設定 SSL 和左的 hello http 端點停用，請確定您改為使用 hello https:// 端點。
   
   範例命令列：

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   如果您收到錯誤的下方 hello，很可能是 Web 端點的憑證有問題。 請嘗試 toohello Web 端點連接與您最愛的網頁瀏覽器，並檢查是否有憑證錯誤。
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   如果成功，hello 輸出看起來應該像下面的 hello:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. 試驗其他資料類型！ 所有這些指令碼採用選擇性-ShardKeyType 參數，可讓您 toospecify hello 索引鍵類型。 hello 預設是 Int32，但您也可以指定 Int64、 Guid 或二進位檔。

## <a name="create-requests"></a>建立要求
hello 服務可使用 hello web UI，或藉由匯入及使用 hello SplitMerge.psm1 PowerShell 模組會送出您的要求，透過 hello web 角色。

hello 服務可以移動分區化資料表和參考資料表中的資料。 分區資料表具有分區化索引鍵資料行，且在每個分區上有不同的資料列資料。 參考資料表不是分區化使其包含 hello 相同資料上每個分區列資料。 參考資料表適合用於不常變更，是使用的 tooJOIN 與查詢中的分區化資料表的資料。

在訂單 tooperform 分割合併作業，您必須宣告 hello 分區化資料表和您想要移動的 toohave 的參考資料表。 這是以 hello **SchemaInfo**應用程式開發介面。 這個 API 已在 hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema**命名空間。

1. 針對每個分區化資料表建立**ShardedTableInfo**物件，描述 hello 資料表的父結構描述名稱 (選擇性，預設值太"dbo")、 hello 資料表名稱和 hello 包含 hello 分區化索引鍵的該資料表中的資料行名稱。
2. 每個參考資料表中，建立**ReferenceTableInfo**物件，描述 hello 資料表的父結構描述名稱 (選擇性，預設值太"dbo") 和 hello 資料表名稱。
3. 新增上述 TableInfo 物件 tooa 新 hello **SchemaInfo**物件。
4. 取得參考 tooa **ShardMapManager**物件，並呼叫**GetSchemaInfoCollection**。
5. 新增 hello **SchemaInfo** toohello **SchemaInfoCollection**，提供 hello 分區對應名稱。

Hello SetupSampleSplitMergeEnvironment.ps1 指令碼中可以看到此動作的範例。

hello 分割合併服務不會建立 hello 目標資料庫 （或 hello 資料庫中任何資料表的結構描述） 為您。 您必須預先建立傳送要求 toohello 服務之前。

## <a name="troubleshooting"></a>疑難排解
執行 hello 範例 powershell 指令碼時，您可能會看到下列訊息的 hello:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

此錯誤表示您的 SSL 憑證未正確設定。 請依照 '連接的網頁瀏覽器' hello 一節中的指示。

若無法提交要求，您可能會看到：

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

在此情況下，請檢查您的組態檔，在特定的 hello 設定**WorkerRoleSynchronizationStorageAccountConnectionString**。 此錯誤通常表示該 hello 背景工作角色無法順利初始化 hello 第一次使用的中繼資料資料庫。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

