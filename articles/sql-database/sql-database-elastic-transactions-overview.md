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
# <a name="distributed-transactions-across-cloud-databases"></a><span data-ttu-id="66ca8-103">跨雲端資料庫的分散式交易</span><span class="sxs-lookup"><span data-stu-id="66ca8-103">Distributed transactions across cloud databases</span></span>
<span data-ttu-id="66ca8-104">Azure SQL Database (SQL DB) 的彈性資料庫交易可讓您跨越多個資料庫中的 SQL DB toorun 交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-104">Elastic database transactions for Azure SQL Database (SQL DB) allow you toorun transactions that span several databases in SQL DB.</span></span> <span data-ttu-id="66ca8-105">SQL 資料庫的彈性資料庫交易適用於使用 ADO.NET 的.NET 應用程式，並與 hello 熟悉的程式設計體驗使用 hello 整合[System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="66ca8-105">Elastic database transactions for SQL DB are available for .NET applications using ADO .NET and integrate with hello familiar programming experience using hello [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) classes.</span></span> <span data-ttu-id="66ca8-106">tooget hello 程式庫，請參閱[.NET Framework 4.6.1 （Web 安裝程式）](https://www.microsoft.com/download/details.aspx?id=49981)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-106">tooget hello library, see [.NET Framework 4.6.1 (Web Installer)](https://www.microsoft.com/download/details.aspx?id=49981).</span></span>

<span data-ttu-id="66ca8-107">在內部部署，這種案例通常需要執行 Microsoft Distributed Transaction Coordinator (MSDTC)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-107">On premises, such a scenario usually required running Microsoft Distributed Transaction Coordinator (MSDTC).</span></span> <span data-ttu-id="66ca8-108">MSDTC 不適用於 Azure 中的平台做為服務應用程式，因為 hello 能力 toocoordinate 分散式交易已現在直接整合至 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="66ca8-108">Since MSDTC is not available for Platform-as-a-Service application in Azure, hello ability toocoordinate distributed transactions has now been directly integrated into SQL DB.</span></span> <span data-ttu-id="66ca8-109">應用程式可以連接 tooany SQL Database toolaunch 分散式交易，並 hello 遵循圖所示，其中一個 hello 資料庫將以透明的方式協調 hello 分散式交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-109">Applications can connect tooany SQL Database toolaunch distributed transactions, and one of hello databases will transparently coordinate hello distributed transaction, as shown in hello following figure.</span></span> 

  ![<span data-ttu-id="66ca8-110">Azure SQL Database 的分散式交易 - 使用彈性資料庫交易</span><span class="sxs-lookup"><span data-stu-id="66ca8-110">Distributed transactions with Azure SQL Database using elastic database transactions</span></span> ][1]

## <a name="common-scenarios"></a><span data-ttu-id="66ca8-111">常見案例</span><span class="sxs-lookup"><span data-stu-id="66ca8-111">Common scenarios</span></span>
<span data-ttu-id="66ca8-112">SQL 資料庫的彈性資料庫交易可讓應用程式 toomake 不可部分完成的變更 toodata 儲存在數個不同的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="66ca8-112">Elastic database transactions for SQL DB enable applications toomake atomic changes toodata stored in several different SQL Databases.</span></span> <span data-ttu-id="66ca8-113">hello 預覽著重於 C# 和.NET 用戶端開發經驗。</span><span class="sxs-lookup"><span data-stu-id="66ca8-113">hello preview focuses on client-side development experiences in C# and .NET.</span></span> <span data-ttu-id="66ca8-114">未來預計加入使用 T-SQL 的伺服器端經驗。</span><span class="sxs-lookup"><span data-stu-id="66ca8-114">A server-side experience using T-SQL is planned for a later time.</span></span>  
<span data-ttu-id="66ca8-115">彈性資料庫交易的目標 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="66ca8-115">Elastic database transactions targets hello following scenarios:</span></span>

* <span data-ttu-id="66ca8-116">Azure 中的多資料庫應用程式：在此案例中，資料垂直分割到 SQL DB 中的多個資料庫，使得不同種類的資料位於不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="66ca8-116">Multi-database applications in Azure: With this scenario, data is vertically partitioned across several databases in SQL DB such that different kinds of data reside on different databases.</span></span> <span data-ttu-id="66ca8-117">某些作業需要變更 toodata 保存兩個或多個資料庫中。</span><span class="sxs-lookup"><span data-stu-id="66ca8-117">Some operations require changes toodata which is kept in two or more databases.</span></span> <span data-ttu-id="66ca8-118">hello 應用程式會使用跨資料庫的彈性資料庫交易 toocoordinate hello 變更，並確認不可部分完成性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-118">hello application uses elastic database transactions toocoordinate hello changes across databases and ensure atomicity.</span></span>
* <span data-ttu-id="66ca8-119">Azure 中的分區化資料庫應用程式： hello 資料層會與此案例中，使用 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)或自行區分化 toohorizontally 分割 hello 資料跨多個資料庫中的 SQL DB。</span><span class="sxs-lookup"><span data-stu-id="66ca8-119">Sharded database applications in Azure: With this scenario, hello data tier uses hello [Elastic Database client library](sql-database-elastic-database-client-library.md) or self-sharding toohorizontally partition hello data across many databases in SQL DB.</span></span> <span data-ttu-id="66ca8-120">一個顯著的使用案例時變更跨越租用戶的分區化的多租用戶應用程式的 hello 需要 tooperform 不可部分完成變更。</span><span class="sxs-lookup"><span data-stu-id="66ca8-120">One prominent use case is hello need tooperform atomic changes for a sharded multi-tenant application when changes span tenants.</span></span> <span data-ttu-id="66ca8-121">將執行個體從一個租用戶 tooanother，這兩個位於不同的資料庫傳輸。</span><span class="sxs-lookup"><span data-stu-id="66ca8-121">Think for instance of a transfer from one tenant tooanother, both residing on different databases.</span></span> <span data-ttu-id="66ca8-122">第二個案例是大型依次通常意味著，跨多個資料庫用於 hello 某些不可部分完成的作業需要 toostretch 相同租用戶的租用戶的更細緻的分區化 tooaccommodate 容量需求。</span><span class="sxs-lookup"><span data-stu-id="66ca8-122">A second case is fine-grained sharding tooaccommodate capacity needs for a large tenant which in turn typically implies that some atomic operations needs toostretch across several databases used for hello same tenant.</span></span> <span data-ttu-id="66ca8-123">第三個案例是不可部分完成的更新 tooreference 資料，會在資料庫之間複寫。</span><span class="sxs-lookup"><span data-stu-id="66ca8-123">A third case is atomic updates tooreference data that are replicated across databases.</span></span> <span data-ttu-id="66ca8-124">沿著這些的不可部分完成的交易，作業現在可以協調跨越多個資料庫使用 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="66ca8-124">Atomic, transacted, operations along these lines can now be coordinated across several databases using hello preview.</span></span>
  <span data-ttu-id="66ca8-125">彈性資料庫交易的資料庫，使用兩階段認可 tooensure 交易不可部分完成性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-125">Elastic database transactions use two-phase commit tooensure transaction atomicity across databases.</span></span> <span data-ttu-id="66ca8-126">如果交易涉及的資料庫少於 100，則適合併入單一交易內。</span><span class="sxs-lookup"><span data-stu-id="66ca8-126">It is a good fit for transactions that involve less than 100 databases at a time within a single transaction.</span></span> <span data-ttu-id="66ca8-127">這些限制不會強制執行，但其中一個超出這些限制時應預期效能和彈性資料庫交易 toosuffer 的成功率。</span><span class="sxs-lookup"><span data-stu-id="66ca8-127">These limits are not enforced, but one should expect performance and success rates for elastic database transactions toosuffer when exceeding these limits.</span></span>

## <a name="installation-and-migration"></a><span data-ttu-id="66ca8-128">安裝和移轉</span><span class="sxs-lookup"><span data-stu-id="66ca8-128">Installation and migration</span></span>
<span data-ttu-id="66ca8-129">更新 toohello.NET 程式庫 System.Data.dll 和 System.Transactions.dll 提供 hello 功能的 SQL DB 彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-129">hello capabilities for elastic database transactions in SQL DB are provided through updates toohello .NET libraries System.Data.dll and System.Transactions.dll.</span></span> <span data-ttu-id="66ca8-130">hello Dll 確保在需要時，會使用該兩階段認可 tooensure 不可部份完成性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-130">hello DLLs ensure that two-phase commit is used where necessary tooensure atomicity.</span></span> <span data-ttu-id="66ca8-131">使用彈性資料庫交易 toostart 開發應用程式安裝[.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981)或更新版本。</span><span class="sxs-lookup"><span data-stu-id="66ca8-131">toostart developing applications using elastic database transactions, install [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) or a later version.</span></span> <span data-ttu-id="66ca8-132">舊版的 hello.NET framework 上執行時，交易將會失敗 toopromote tooa 分散式交易，而且會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="66ca8-132">When running on an earlier version of hello .NET framework, transactions will fail toopromote tooa distributed transaction and an exception will be raised.</span></span>

<span data-ttu-id="66ca8-133">安裝之後，您可以使用 hello 分散式交易應用程式開發介面中 System.Transactions 連線 tooSQL DB。</span><span class="sxs-lookup"><span data-stu-id="66ca8-133">After installation, you can use hello distributed transaction APIs in System.Transactions with connections tooSQL DB.</span></span> <span data-ttu-id="66ca8-134">如果您有使用這些 Api 的現有 MSDTC 應用程式時，重建現有的應用程式的.NET 4.6 安裝 hello 4.6.1 之後架構。</span><span class="sxs-lookup"><span data-stu-id="66ca8-134">If you have existing MSDTC applications using these APIs, simply rebuild your existing applications for .NET 4.6 after installing hello 4.6.1 Framework.</span></span> <span data-ttu-id="66ca8-135">如果您的專案目標.NET 4.6，它們會自動使用更新 hello hello 新的 Framework 版本與分散式的交易的 API 呼叫的 Dll 結合連接 tooSQL DB 現在將會成功。</span><span class="sxs-lookup"><span data-stu-id="66ca8-135">If your projects target .NET 4.6, they will automatically use hello updated DLLs from hello new Framework version and distributed transaction API calls in combination with connections tooSQL DB will now succeed.</span></span>

<span data-ttu-id="66ca8-136">請記住，彈性資料庫交易不需要安裝 MSDTC。</span><span class="sxs-lookup"><span data-stu-id="66ca8-136">Remember that elastic database transactions do not require installing MSDTC.</span></span> <span data-ttu-id="66ca8-137">彈性資料庫交易直接由 SQL DB 管理。</span><span class="sxs-lookup"><span data-stu-id="66ca8-137">Instead, elastic database transactions are directly managed by and within SQL DB.</span></span> <span data-ttu-id="66ca8-138">這會大幅簡化雲端案例，因為 MSDTC 的部署不是以 SQL DB 必要 toouse 分散式交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-138">This significantly simplifies cloud scenarios since a deployment of MSDTC is not necessary toouse distributed transactions with SQL DB.</span></span> <span data-ttu-id="66ca8-139">第 4 節更詳細地說明 toodeploy 彈性資料庫交易和 hello 需要.NET framework，以及您的雲端應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="66ca8-139">Section 4 explains in more detail how toodeploy elastic database transactions and hello required .NET framework together with your cloud applications tooAzure.</span></span>

## <a name="development-experience"></a><span data-ttu-id="66ca8-140">開發經驗</span><span class="sxs-lookup"><span data-stu-id="66ca8-140">Development experience</span></span>
### <a name="multi-database-applications"></a><span data-ttu-id="66ca8-141">多重資料庫應用程式</span><span class="sxs-lookup"><span data-stu-id="66ca8-141">Multi-database applications</span></span>
<span data-ttu-id="66ca8-142">hello 下列範例程式碼會使用熟悉的程式設計體驗 hello.NET System.Transactions。</span><span class="sxs-lookup"><span data-stu-id="66ca8-142">hello following sample code uses hello familiar programming experience with .NET System.Transactions.</span></span> <span data-ttu-id="66ca8-143">hello TransactionScope 類別會建立在.NET 環境交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-143">hello TransactionScope class establishes an ambient transaction in .NET.</span></span> <span data-ttu-id="66ca8-144">（「 環境交易 」 是一個存在於 hello 目前執行緒中）。Hello TransactionScope 內開啟的所有連線都參與 hello 交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-144">(An “ambient transaction” is one that lives in hello current thread.) All connections opened within hello TransactionScope participate in hello transaction.</span></span> <span data-ttu-id="66ca8-145">如果加入不同的資料庫，就會自動提高的 tooa 分散式交易 hello 交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-145">If different databases participate, hello transaction is automatically elevated tooa distributed transaction.</span></span> <span data-ttu-id="66ca8-146">認可設定 hello 範圍 toocomplete tooindicate 受到 hello hello 交易結果。</span><span class="sxs-lookup"><span data-stu-id="66ca8-146">hello outcome of hello transaction is controlled by setting hello scope toocomplete tooindicate a commit.</span></span>

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

### <a name="sharded-database-applications"></a><span data-ttu-id="66ca8-147">分區化資料庫應用程式</span><span class="sxs-lookup"><span data-stu-id="66ca8-147">Sharded database applications</span></span>
<span data-ttu-id="66ca8-148">SQL 資料庫的彈性資料庫交易也支援協調分散式的交易中您使用的 hello 彈性資料庫用戶端程式庫 tooopen 連線 hello OpenConnectionForKey 方法向外延展的資料層。</span><span class="sxs-lookup"><span data-stu-id="66ca8-148">Elastic database transactions for SQL DB also support coordinating distributed transactions where you use hello OpenConnectionForKey method of hello elastic database client library tooopen connections for a scaled out data tier.</span></span> <span data-ttu-id="66ca8-149">請考慮您需要的情況 tooguarantee 交易一致性變更跨數個不同的分區化索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="66ca8-149">Consider cases where you need tooguarantee transactional consistency for changes across several different sharding key values.</span></span> <span data-ttu-id="66ca8-150">使用 OpenConnectionForKey，被代理連線 toohello 分區裝載 hello 不同分區化索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="66ca8-150">Connections toohello shards hosting hello different sharding key values are brokered using OpenConnectionForKey.</span></span> <span data-ttu-id="66ca8-151">在一般情況下 hello，hello 連線可以是 toodifferent 分區，使得確保異動保證需要分散式的交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-151">In hello general case, hello connections can be toodifferent shards such that ensuring transactional guarantees requires a distributed transaction.</span></span> <span data-ttu-id="66ca8-152">hello，下列程式碼範例將示範這個方法。</span><span class="sxs-lookup"><span data-stu-id="66ca8-152">hello following code sample illustrates this approach.</span></span> <span data-ttu-id="66ca8-153">它會假設名為 shardmap 位於使用的 toorepresent 分區對應 hello 彈性資料庫用戶端程式庫：</span><span class="sxs-lookup"><span data-stu-id="66ca8-153">It assumes that a variable called shardmap is used toorepresent a shard map from hello elastic database client library:</span></span>

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


## <a name="net-installation-for-azure-cloud-services"></a><span data-ttu-id="66ca8-154">Azure 雲端服務的 .NET 安裝</span><span class="sxs-lookup"><span data-stu-id="66ca8-154">.NET installation for Azure Cloud Services</span></span>
<span data-ttu-id="66ca8-155">Azure 提供數個供應項目 toohost.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66ca8-155">Azure provides several offerings toohost .NET applications.</span></span> <span data-ttu-id="66ca8-156">Hello 不同供應項目的比較位於[Azure App Service、 雲端服務和虛擬機器的比較](../app-service-web/choose-web-site-cloud-service-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-156">A comparison of hello different offerings is available in [Azure App Service, Cloud Services, and Virtual Machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span> <span data-ttu-id="66ca8-157">Hello 客體作業系統的 hello 供應項目小於.NET 4.6.1 彈性的交易所需的如果您需要 tooupgrade hello 客體 OS too4.6.1。</span><span class="sxs-lookup"><span data-stu-id="66ca8-157">If hello guest OS of hello offering is smaller than .NET 4.6.1 required for elastic transactions, you need tooupgrade hello guest OS too4.6.1.</span></span> 

<span data-ttu-id="66ca8-158">針對 Azure 應用程式服務，會升級 toohello 客體 OS 目前不支援。</span><span class="sxs-lookup"><span data-stu-id="66ca8-158">For Azure App Services, upgrades toohello guest OS are currently not supported.</span></span> <span data-ttu-id="66ca8-159">適用於 Azure 虛擬機器中，只需登入 hello VM，並執行 hello hello 最新的.NET framework 的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="66ca8-159">For Azure Virtual Machines, simply log into hello VM and run hello installer for hello latest .NET framework.</span></span> <span data-ttu-id="66ca8-160">Azure 雲端服務，您需要 tooinclude hello 安裝較新版的.NET 到部署的 hello 啟動工作。</span><span class="sxs-lookup"><span data-stu-id="66ca8-160">For Azure Cloud Services, you need tooinclude hello installation of a newer .NET version into hello startup tasks of your deployment.</span></span> <span data-ttu-id="66ca8-161">hello 概念和步驟會記載於[雲端服務角色上安裝的.NET](../cloud-services/cloud-services-dotnet-install-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-161">hello concepts and steps are documented in [Install .NET on a Cloud Service Role](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>  

<span data-ttu-id="66ca8-162">請注意，.NET 4.6.1 可能需要更多的暫存儲存空間 hello 比 hello.NET 4.6 的安裝程式啟動載入 Azure 雲端服務的程序期間 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="66ca8-162">Note that hello installer for .NET 4.6.1 may require more temporary storage during hello bootstrapping process on Azure cloud services than hello installer for .NET 4.6.</span></span> <span data-ttu-id="66ca8-163">tooensure 安裝成功，您需要 tooincrease 暫存儲存體 Azure 雲端服務在 ServiceDefinition.csdef 檔案中的 hello LocalResources 區段和 hello 環境設定的啟動工作，hello 下列所示範例：</span><span class="sxs-lookup"><span data-stu-id="66ca8-163">tooensure a successful installation, you need tooincrease temporary storage for your Azure cloud service in your ServiceDefinition.csdef file in hello LocalResources section and hello environment settings of your startup task, as shown in hello following sample:</span></span>

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

## <a name="transactions-across-multiple-servers"></a><span data-ttu-id="66ca8-164">跨多部伺服器的交易</span><span class="sxs-lookup"><span data-stu-id="66ca8-164">Transactions across multiple servers</span></span>
<span data-ttu-id="66ca8-165">在 Azure SQL Database 中，支援跨不同邏輯伺服器的彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-165">Elastic database transactions are supported across different logical servers in Azure SQL Database.</span></span> <span data-ttu-id="66ca8-166">當交易跨越邏輯伺服器界限時，hello 參與伺服器第一次需要 toobe 輸入相互通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-166">When transactions cross logical server boundaries, hello participating servers first need toobe entered into a mutual communication relationship.</span></span> <span data-ttu-id="66ca8-167">一旦建立 hello 通訊關聯性，任何資料庫中任何兩部伺服器可以參與具有來自資料庫的彈性交易 hello hello 另一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="66ca8-167">Once hello communication relationship has been established, any database in any of hello two servers can participate in elastic transactions with databases from hello other server.</span></span> <span data-ttu-id="66ca8-168">跨越兩個以上的邏輯伺服器的交易，使用的通訊關聯性會需要就地 toobe 邏輯伺服器的任何一組。</span><span class="sxs-lookup"><span data-stu-id="66ca8-168">With transactions spanning more than two logical servers, a communication relationship needs toobe in place for any pair of logical servers.</span></span>

<span data-ttu-id="66ca8-169">使用下列 PowerShell cmdlet toomanage 跨伺服器的通訊關聯性的彈性資料庫交易的 hello:</span><span class="sxs-lookup"><span data-stu-id="66ca8-169">Use hello following PowerShell cmdlets toomanage cross-server communication relationships for elastic database transactions:</span></span>

* <span data-ttu-id="66ca8-170">**新 AzureRmSqlServerCommunicationLink**： 使用這個指令程式 toocreate 新 Azure SQL DB 中的兩部邏輯伺服器的通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-170">**New-AzureRmSqlServerCommunicationLink**: Use this cmdlet toocreate a new communication relationship between two logical servers in Azure SQL DB.</span></span> <span data-ttu-id="66ca8-171">hello 關聯性為對稱，表示這兩部伺服器可以起始交易 hello 與另一部伺服器。</span><span class="sxs-lookup"><span data-stu-id="66ca8-171">hello relationship is symmetric which means both servers can initiate transactions with hello other server.</span></span>
* <span data-ttu-id="66ca8-172">**Get AzureRmSqlServerCommunicationLink**： 使用這個指令程式 tooretrieve 現有通訊關聯性和其屬性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-172">**Get-AzureRmSqlServerCommunicationLink**: Use this cmdlet tooretrieve existing communication relationships and their properties.</span></span>
* <span data-ttu-id="66ca8-173">**移除 AzureRmSqlServerCommunicationLink**： 使用這個指令程式 tooremove 現有通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="66ca8-173">**Remove-AzureRmSqlServerCommunicationLink**: Use this cmdlet tooremove an existing communication relationship.</span></span> 

## <a name="monitoring-transaction-status"></a><span data-ttu-id="66ca8-174">監視交易狀態</span><span class="sxs-lookup"><span data-stu-id="66ca8-174">Monitoring transaction status</span></span>
<span data-ttu-id="66ca8-175">使用動態管理檢視 (Dmv) 中進行中的彈性資料庫交易的 SQL DB toomonitor 狀態與進度。</span><span class="sxs-lookup"><span data-stu-id="66ca8-175">Use Dynamic Management Views (DMVs) in SQL DB toomonitor status and progress of your ongoing elastic database transactions.</span></span> <span data-ttu-id="66ca8-176">所有的 Dmv 相關的 tootransactions 是相關的 SQL DB 分散式交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-176">All DMVs related tootransactions are relevant for distributed transactions in SQL DB.</span></span> <span data-ttu-id="66ca8-177">您可以找到 hello 對應清單的 Dmv:[交易相關動態管理檢視和函數 (TRANSACT-SQL)](https://msdn.microsoft.com/library/ms178621.aspx)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-177">You can find hello corresponding list of DMVs here: [Transaction Related Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).</span></span>

<span data-ttu-id="66ca8-178">這些 DMV 特別有用：</span><span class="sxs-lookup"><span data-stu-id="66ca8-178">These DMVs are particularly useful:</span></span>

* <span data-ttu-id="66ca8-179">**sys.dm\_tran\_active\_transactions**：列出目前使用中的交易及其狀態。</span><span class="sxs-lookup"><span data-stu-id="66ca8-179">**sys.dm\_tran\_active\_transactions**: Lists currently active transactions and their status.</span></span> <span data-ttu-id="66ca8-180">hello UOW （工作單位） 欄可以識別 hello 不同的子交易 toohello 屬於相同的分散式交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-180">hello UOW (Unit Of Work) column can identify hello different child transactions that belong toohello same distributed transaction.</span></span> <span data-ttu-id="66ca8-181">所有的交易內執行相同的分散式的交易的 hello hello UOW 值相同。</span><span class="sxs-lookup"><span data-stu-id="66ca8-181">All transactions within hello same distributed transaction carry hello same UOW value.</span></span> <span data-ttu-id="66ca8-182">請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms174302.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66ca8-182">See hello [DMV documentation](https://msdn.microsoft.com/library/ms174302.aspx) for more details.</span></span>
* <span data-ttu-id="66ca8-183">**sys.dm\_tran\_資料庫\_交易**： 提供有關交易，例如放置 hello 記錄檔中的 hello 交易的額外資訊。</span><span class="sxs-lookup"><span data-stu-id="66ca8-183">**sys.dm\_tran\_database\_transactions**: Provides additional information about transactions, such as placement of hello transaction in hello log.</span></span> <span data-ttu-id="66ca8-184">請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms186957.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66ca8-184">See hello [DMV documentation](https://msdn.microsoft.com/library/ms186957.aspx) for more details.</span></span>
* <span data-ttu-id="66ca8-185">**sys.dm\_tran\_鎖定**： 提供目前進行中的交易所持有的 hello 鎖定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="66ca8-185">**sys.dm\_tran\_locks**: Provides information about hello locks that are currently held by ongoing transactions.</span></span> <span data-ttu-id="66ca8-186">請參閱 hello [DMV 文件](https://msdn.microsoft.com/library/ms190345.aspx)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="66ca8-186">See hello [DMV documentation](https://msdn.microsoft.com/library/ms190345.aspx) for more details.</span></span>

## <a name="limitations"></a><span data-ttu-id="66ca8-187">限制</span><span class="sxs-lookup"><span data-stu-id="66ca8-187">Limitations</span></span>
<span data-ttu-id="66ca8-188">hello 下列限制目前適用於 tooelastic 資料庫交易的 SQL 資料庫：</span><span class="sxs-lookup"><span data-stu-id="66ca8-188">hello following limitations currently apply tooelastic database transactions in SQL DB:</span></span>

* <span data-ttu-id="66ca8-189">僅支援 SQL DB 中跨資料庫的交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-189">Only transactions across databases in SQL DB are supported.</span></span> <span data-ttu-id="66ca8-190">其他 [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) 資源提供者和 SQL DB 以外的資料庫無法參與彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-190">Other [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) resource providers and databases outside of SQL DB cannot participate in elastic database transactions.</span></span> <span data-ttu-id="66ca8-191">這表示彈性資料庫交易無法延伸到內部部署 SQL Server 和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="66ca8-191">That means that elastic database transactions cannot stretch across on premises SQL Server and Azure SQL Databases.</span></span> <span data-ttu-id="66ca8-192">在內部部署的分散式交易，請繼續 toouse MSDTC。</span><span class="sxs-lookup"><span data-stu-id="66ca8-192">For distributed transactions on premises, continue toouse MSDTC.</span></span> 
* <span data-ttu-id="66ca8-193">僅支援來自 .NET 應用程式的用戶端協調交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-193">Only client-coordinated transactions from a .NET application are supported.</span></span> <span data-ttu-id="66ca8-194">目前已規劃 T-SQL 的伺服器端支援，例如 BEGIN DISTRIBUTED TRANSACTION，但尚未推出。</span><span class="sxs-lookup"><span data-stu-id="66ca8-194">Server-side support for T-SQL such as BEGIN DISTRIBUTED TRANSACTION is planned, but not yet available.</span></span> 
* <span data-ttu-id="66ca8-195">不支援跨 WCF 服務的交易。</span><span class="sxs-lookup"><span data-stu-id="66ca8-195">Transactions across WCF services are not supported.</span></span> <span data-ttu-id="66ca8-196">例如，您有執行交易的 WCF 服務方法。</span><span class="sxs-lookup"><span data-stu-id="66ca8-196">For example, you have a WCF service method that executes a transaction.</span></span> <span data-ttu-id="66ca8-197">封入 hello 呼叫交易範圍內將會失敗，因為[System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-197">Enclosing hello call within a transaction scope will fail as a [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).</span></span>

## <a name="next-steps"></a><span data-ttu-id="66ca8-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66ca8-198">Next steps</span></span>
<span data-ttu-id="66ca8-199">如有問題，請聯繫 toous 上 hello [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)和功能的要求，請將它們加入 toohello [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="66ca8-199">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



