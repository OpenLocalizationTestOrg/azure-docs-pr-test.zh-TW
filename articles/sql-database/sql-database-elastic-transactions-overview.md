---
title: "跨雲端資料庫 aaaDistributed 交易"
description: "Azure SQL Database 的彈性資料庫交易概觀"
services: sql-database
documentationcenter: 
author: torsteng
manager: jhubbard
editor: torsteng
ms.assetid: e14df7a3-7788-4cfb-bcd1-7ad6433ef1f9
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: sql-database
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 9a18f2749108d337bf115b3dc21dd0c7828dd9c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a>跨雲端資料庫的分散式交易
Azure SQL Database (SQL DB) 的彈性資料庫交易可讓您跨越多個資料庫中的 SQL DB toorun 交易。 SQL 資料庫的彈性資料庫交易適用於使用 ADO.NET 的.NET 應用程式，並與 hello 熟悉的程式設計體驗使用 hello 整合[System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx)類別。 tooget hello 程式庫，請參閱[.NET Framework 4.6.1 （Web 安裝程式）](https://www.microsoft.com/download/details.aspx?id=49981)。

在內部部署，這種案例通常需要執行 Microsoft Distributed Transaction Coordinator (MSDTC)。 MSDTC 不適用於 Azure 中的平台做為服務應用程式，因為 hello 能力 toocoordinate 分散式交易已現在直接整合至 SQL 資料庫。 應用程式可以連接 tooany SQL Database toolaunch 分散式交易，並 hello 遵循圖所示，其中一個 hello 資料庫將以透明的方式協調 hello 分散式交易。 

  ![Azure SQL Database 的分散式交易 - 使用彈性資料庫交易 ][1]

## <a name="common-scenarios"></a>常見案例
SQL 資料庫的彈性資料庫交易可讓應用程式 toomake 不可部分完成的變更 toodata 儲存在數個不同的 SQL Database。 hello 預覽著重於 C# 和.NET 用戶端開發經驗。 未來預計加入使用 T-SQL 的伺服器端經驗。  
彈性資料庫交易的目標 hello 下列案例：

* Azure 中的多資料庫應用程式：在此案例中，資料垂直分割到 SQL DB 中的多個資料庫，使得不同種類的資料位於不同的資料庫。 某些作業需要變更 toodata 保存兩個或多個資料庫中。 hello 應用程式會使用跨資料庫的彈性資料庫交易 toocoordinate hello 變更，並確認不可部分完成性。
* Azure 中的分區化資料庫應用程式： hello 資料層會與此案例中，使用 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)或自行區分化 toohorizontally 分割 hello 資料跨多個資料庫中的 SQL DB。 一個顯著的使用案例時變更跨越租用戶的分區化的多租用戶應用程式的 hello 需要 tooperform 不可部分完成變更。 將執行個體從一個租用戶 tooanother，這兩個位於不同的資料庫傳輸。 第二個案例是大型依次通常意味著，跨多個資料庫用於 hello 某些不可部分完成的作業需要 toostretch 相同租用戶的租用戶的更細緻的分區化 tooaccommodate 容量需求。 第三個案例是不可部分完成的更新 tooreference 資料，會在資料庫之間複寫。 沿著這些的不可部分完成的交易，作業現在可以協調跨越多個資料庫使用 hello 預覽。
  彈性資料庫交易的資料庫，使用兩階段認可 tooensure 交易不可部分完成性。 如果交易涉及的資料庫少於 100，則適合併入單一交易內。 這些限制不會強制執行，但其中一個超出這些限制時應預期效能和彈性資料庫交易 toosuffer 的成功率。

## <a name="installation-and-migration"></a>安裝和移轉
更新 toohello.NET 程式庫 System.Data.dll 和 System.Transactions.dll 提供 hello 功能的 SQL DB 彈性資料庫交易。 hello Dll 確保在需要時，會使用該兩階段認可 tooensure 不可部份完成性。 使用彈性資料庫交易 toostart 開發應用程式安裝[.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981)或更新版本。 舊版的 hello.NET framework 上執行時，交易將會失敗 toopromote tooa 分散式交易，而且會引發例外狀況。

安裝之後，您可以使用 hello 分散式交易應用程式開發介面中 System.Transactions 連線 tooSQL DB。 如果您有使用這些 Api 的現有 MSDTC 應用程式時，重建現有的應用程式的.NET 4.6 安裝 hello 4.6.1 之後架構。 如果您的專案目標.NET 4.6，它們會自動使用更新 hello hello 新的 Framework 版本與分散式的交易的 API 呼叫的 Dll 結合連接 tooSQL DB 現在將會成功。

請記住，彈性資料庫交易不需要安裝 MSDTC。 彈性資料庫交易直接由 SQL DB 管理。 這會大幅簡化雲端案例，因為 MSDTC 的部署不是以 SQL DB 必要 toouse 分散式交易。 第 4 節更詳細地說明 toodeploy 彈性資料庫交易和 hello 需要.NET framework，以及您的雲端應用程式 tooAzure。

## <a name="development-experience"></a>開發經驗
### <a name="multi-database-applications"></a>多重資料庫應用程式
hello 下列範例程式碼會使用熟悉的程式設計體驗 hello.NET System.Transactions。 hello TransactionScope 類別會建立在.NET 環境交易。 （「 環境交易 」 是一個存在於 hello 目前執行緒中）。Hello TransactionScope 內開啟的所有連線都參與 hello 交易。 如果加入不同的資料庫，就會自動提高的 tooa 分散式交易 hello 交易。 認可設定 hello 範圍 toocomplete tooindicate 受到 hello hello 交易結果。

    using (var scope = new TransactionScope())
    {
        using (var conn1 = new SqlConnection(connStrDb1))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = new SqlConnection(connStrDb2))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T2 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }

### <a name="sharded-database-applications"></a>分區化資料庫應用程式
SQL 資料庫的彈性資料庫交易也支援協調分散式的交易中您使用的 hello 彈性資料庫用戶端程式庫 tooopen 連線 hello OpenConnectionForKey 方法向外延展的資料層。 請考慮您需要的情況 tooguarantee 交易一致性變更跨數個不同的分區化索引鍵值。 使用 OpenConnectionForKey，被代理連線 toohello 分區裝載 hello 不同分區化索引鍵值。 在一般情況下 hello，hello 連線可以是 toodifferent 分區，使得確保異動保證需要分散式的交易。 hello，下列程式碼範例將示範這個方法。 它會假設名為 shardmap 位於使用的 toorepresent 分區對應 hello 彈性資料庫用戶端程式庫：

    using (var scope = new TransactionScope())
    {
        using (var conn1 = shardmap.OpenConnectionForKey(tenantId1, credentialsStr))
        {
            conn1.Open();
            SqlCommand cmd1 = conn1.CreateCommand();
            cmd1.CommandText = string.Format("insert into T1 values(1)");
            cmd1.ExecuteNonQuery();
        }

        using (var conn2 = shardmap.OpenConnectionForKey(tenantId2, credentialsStr))
        {
            conn2.Open();
            var cmd2 = conn2.CreateCommand();
            cmd2.CommandText = string.Format("insert into T1 values(2)");
            cmd2.ExecuteNonQuery();
        }

        scope.Complete();
    }


## <a name="net-installation-for-azure-cloud-services"></a>Azure 雲端服務的 .NET 安裝
Azure 提供數個供應項目 toohost.NET 應用程式。 Hello 不同供應項目的比較位於[Azure App Service、 雲端服務和虛擬機器的比較](../app-service-web/choose-web-site-cloud-service-vm.md)。 Hello 客體作業系統的 hello 供應項目小於.NET 4.6.1 彈性的交易所需的如果您需要 tooupgrade hello 客體 OS too4.6.1。 

針對 Azure 應用程式服務，會升級 toohello 客體 OS 目前不支援。 適用於 Azure 虛擬機器中，只需登入 hello VM，並執行 hello hello 最新的.NET framework 的安裝程式。 Azure 雲端服務，您需要 tooinclude hello 安裝較新版的.NET 到部署的 hello 啟動工作。 hello 概念和步驟會記載於[雲端服務角色上安裝的.NET](../cloud-services/cloud-services-dotnet-install-dotnet.md)。  

請注意，.NET 4.6.1 可能需要更多的暫存儲存空間 hello 比 hello.NET 4.6 的安裝程式啟動載入 Azure 雲端服務的程序期間 hello 安裝程式。 tooensure 安裝成功，您需要 tooincrease 暫存儲存體 Azure 雲端服務在 ServiceDefinition.csdef 檔案中的 hello LocalResources 區段和 hello 環境設定的啟動工作，hello 下列所示範例：

    <LocalResources>
    ...
        <LocalStorage name="TEMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
        <LocalStorage name="TMP" sizeInMB="5000" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
        <Task commandLine="install.cmd" executionContext="elevated" taskType="simple">
            <Environment>
        ...
                <Variable name="TEMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TEMP']/@path" />
                </Variable>
                <Variable name="TMP">
                    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='TMP']/@path" />
                </Variable>
            </Environment>
        </Task>
    </Startup>

## <a name="transactions-across-multiple-servers"></a>跨多部伺服器的交易
在 Azure SQL Database 中，支援跨不同邏輯伺服器的彈性資料庫交易。 當交易跨越邏輯伺服器界限時，hello 參與伺服器第一次需要 toobe 輸入相互通訊關聯性。 一旦建立 hello 通訊關聯性，任何資料庫中任何兩部伺服器可以參與具有來自資料庫的彈性交易 hello hello 另一部伺服器。 跨越兩個以上的邏輯伺服器的交易，使用的通訊關聯性會需要就地 toobe 邏輯伺服器的任何一組。

使用下列 PowerShell cmdlet toomanage 跨伺服器的通訊關聯性的彈性資料庫交易的 hello:

* **新 AzureRmSqlServerCommunicationLink**： 使用這個指令程式 toocreate 新 Azure SQL DB 中的兩部邏輯伺服器的通訊關聯性。 hello 關聯性為對稱，表示這兩部伺服器可以起始交易 hello 與另一部伺服器。
* **Get AzureRmSqlServerCommunicationLink**： 使用這個指令程式 tooretrieve 現有通訊關聯性和其屬性。
* **移除 AzureRmSqlServerCommunicationLink**： 使用這個指令程式 tooremove 現有通訊關聯性。 

## <a name="monitoring-transaction-status"></a>監視交易狀態
使用動態管理檢視 (Dmv) 中進行中的彈性資料庫交易的 SQL DB toomonitor 狀態與進度。 所有的 Dmv 相關的 tootransactions 是相關的 SQL DB 分散式交易。 您可以找到 hello 對應清單的 Dmv:[交易相關動態管理檢視和函數 (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms178621.aspx)。

這些 DMV 特別有用：

* **sys.dm\_tran\_active\_transactions**：列出目前使用中的交易及其狀態。 hello UOW （工作單位） 欄可以識別 hello 不同的子交易 toohello 屬於相同的分散式交易。 所有的交易內執行相同的分散式的交易的 hello hello UOW 值相同。 請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms174302.aspx)如需詳細資訊。
* **sys.dm\_tran\_資料庫\_交易**： 提供有關交易，例如放置 hello 記錄檔中的 hello 交易的額外資訊。 請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms186957.aspx)如需詳細資訊。
* **sys.dm\_tran\_鎖定**： 提供目前進行中的交易所持有的 hello 鎖定的相關資訊。 請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms190345.aspx)如需詳細資訊。

## <a name="limitations"></a>限制
hello 下列限制目前適用於 tooelastic 資料庫交易的 SQL 資料庫：

* 僅支援 SQL DB 中跨資料庫的交易。 其他 [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) 資源提供者和 SQL DB 以外的資料庫無法參與彈性資料庫交易。 這表示彈性資料庫交易無法延伸到內部部署 SQL Server 和 Azure SQL Database。 在內部部署的分散式交易，請繼續 toouse MSDTC。 
* 僅支援來自 .NET 應用程式的用戶端協調交易。 目前已規劃 T-SQL 的伺服器端支援，例如 BEGIN DISTRIBUTED TRANSACTION，但尚未推出。 
* 不支援跨 WCF 服務的交易。 例如，您有執行交易的 WCF 服務方法。 封入 hello 呼叫交易範圍內將會失敗，因為[System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception)。

## <a name="next-steps"></a>後續步驟
如有問題，請聯繫 toous 上 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)和功能的要求，請將它們加入 toohello [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



