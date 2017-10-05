---
title: "跨雲端資料庫的分散式交易"
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
ms.openlocfilehash: f7f1ad3f1933b39a0030a784cae40521254037d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="distributed-transactions-across-cloud-databases"></a><span data-ttu-id="8c13b-103">跨雲端資料庫的分散式交易</span><span class="sxs-lookup"><span data-stu-id="8c13b-103">Distributed transactions across cloud databases</span></span>
<span data-ttu-id="8c13b-104">Azure SQL Database (SQL DB) 的彈性資料庫交易可讓您在 SQL DB 中跨多個資料庫執行交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-104">Elastic database transactions for Azure SQL Database (SQL DB) allow you to run transactions that span several databases in SQL DB.</span></span> <span data-ttu-id="8c13b-105">SQL DB 的彈性資料庫交易適用於使用 ADO .NET 的 .NET 應用程式，而且與以往熟悉使用 [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) 類別的程式設計經驗整合。</span><span class="sxs-lookup"><span data-stu-id="8c13b-105">Elastic database transactions for SQL DB are available for .NET applications using ADO .NET and integrate with the familiar programming experience using the [System.Transaction](https://msdn.microsoft.com/library/system.transactions.aspx) classes.</span></span> <span data-ttu-id="8c13b-106">如要取得程式庫，請參閱 [.NET Framework 4.6.1 (Web 安裝程式)](https://www.microsoft.com/download/details.aspx?id=49981)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-106">To get the library, see [.NET Framework 4.6.1 (Web Installer)](https://www.microsoft.com/download/details.aspx?id=49981).</span></span>

<span data-ttu-id="8c13b-107">在內部部署，這種案例通常需要執行 Microsoft Distributed Transaction Coordinator (MSDTC)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-107">On premises, such a scenario usually required running Microsoft Distributed Transaction Coordinator (MSDTC).</span></span> <span data-ttu-id="8c13b-108">因為 MSDTC 不適用於 Azure 中的平台即服務應用程式，協調分散式交易的功能現在已直接整合至 SQL DB。</span><span class="sxs-lookup"><span data-stu-id="8c13b-108">Since MSDTC is not available for Platform-as-a-Service application in Azure, the ability to coordinate distributed transactions has now been directly integrated into SQL DB.</span></span> <span data-ttu-id="8c13b-109">應用程式可以連接到任何 SQL Database 來啟動分散式交易，而其中一個資料庫會明確協調分散式交易，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="8c13b-109">Applications can connect to any SQL Database to launch distributed transactions, and one of the databases will transparently coordinate the distributed transaction, as shown in the following figure.</span></span> 

  ![<span data-ttu-id="8c13b-110">Azure SQL Database 的分散式交易 - 使用彈性資料庫交易</span><span class="sxs-lookup"><span data-stu-id="8c13b-110">Distributed transactions with Azure SQL Database using elastic database transactions</span></span> ][1]

## <a name="common-scenarios"></a><span data-ttu-id="8c13b-111">常見案例</span><span class="sxs-lookup"><span data-stu-id="8c13b-111">Common scenarios</span></span>
<span data-ttu-id="8c13b-112">SQL DB 的彈性資料庫交易可讓應用程式對數個不同 SQL Database 中儲存的資料進行不可部分完成的變更。</span><span class="sxs-lookup"><span data-stu-id="8c13b-112">Elastic database transactions for SQL DB enable applications to make atomic changes to data stored in several different SQL Databases.</span></span> <span data-ttu-id="8c13b-113">預覽版著重於 C# 和 .NET 的用戶端開發經驗。</span><span class="sxs-lookup"><span data-stu-id="8c13b-113">The preview focuses on client-side development experiences in C# and .NET.</span></span> <span data-ttu-id="8c13b-114">未來預計加入使用 T-SQL 的伺服器端經驗。</span><span class="sxs-lookup"><span data-stu-id="8c13b-114">A server-side experience using T-SQL is planned for a later time.</span></span>  
<span data-ttu-id="8c13b-115">彈性資料庫交易以下列案例為目標：</span><span class="sxs-lookup"><span data-stu-id="8c13b-115">Elastic database transactions targets the following scenarios:</span></span>

* <span data-ttu-id="8c13b-116">Azure 中的多資料庫應用程式：在此案例中，資料垂直分割到 SQL DB 中的多個資料庫，使得不同種類的資料位於不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c13b-116">Multi-database applications in Azure: With this scenario, data is vertically partitioned across several databases in SQL DB such that different kinds of data reside on different databases.</span></span> <span data-ttu-id="8c13b-117">某些作業需要變更兩個以上的資料庫中保存的資料。</span><span class="sxs-lookup"><span data-stu-id="8c13b-117">Some operations require changes to data which is kept in two or more databases.</span></span> <span data-ttu-id="8c13b-118">應用程式使用彈性資料庫交易來協調資料庫之間的變更，確保不可部分完成性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-118">The application uses elastic database transactions to coordinate the changes across databases and ensure atomicity.</span></span>
* <span data-ttu-id="8c13b-119">Azure 中的分區化資料庫應用程式：在此案例中，資料層使用 [彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md) 或自我分區化功能，在 SQL DB 中橫跨許多資料庫來水平分割資料。</span><span class="sxs-lookup"><span data-stu-id="8c13b-119">Sharded database applications in Azure: With this scenario, the data tier uses the [Elastic Database client library](sql-database-elastic-database-client-library.md) or self-sharding to horizontally partition the data across many databases in SQL DB.</span></span> <span data-ttu-id="8c13b-120">一個顯著的使用案例是在分區化多租用戶應用程式中，當變更牽涉多個租用戶時，需要執行不可部分完成的變更。</span><span class="sxs-lookup"><span data-stu-id="8c13b-120">One prominent use case is the need to perform atomic changes for a sharded multi-tenant application when changes span tenants.</span></span> <span data-ttu-id="8c13b-121">例如，從一個租用戶轉移到另一個租用戶，而兩者位於不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c13b-121">Think for instance of a transfer from one tenant to another, both residing on different databases.</span></span> <span data-ttu-id="8c13b-122">第二個案例是以細緻分區化來因應大型租用戶的容量需求，這又通常表示某些不可部分完成的作業需要延伸至用於相同租用戶的多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="8c13b-122">A second case is fine-grained sharding to accommodate capacity needs for a large tenant which in turn typically implies that some atomic operations needs to stretch across several databases used for the same tenant.</span></span> <span data-ttu-id="8c13b-123">第三種案例是以不可部分完成的更新來參考資料庫之間複寫的資料。</span><span class="sxs-lookup"><span data-stu-id="8c13b-123">A third case is atomic updates to reference data that are replicated across databases.</span></span> <span data-ttu-id="8c13b-124">現在可以利用預覽版，跨多個資料庫協調這幾方面不可部分完成的交易式作業。</span><span class="sxs-lookup"><span data-stu-id="8c13b-124">Atomic, transacted, operations along these lines can now be coordinated across several databases using the preview.</span></span>
  <span data-ttu-id="8c13b-125">彈性資料庫交易使用兩階段認可，確保跨資料庫的交易不可部分完成性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-125">Elastic database transactions use two-phase commit to ensure transaction atomicity across databases.</span></span> <span data-ttu-id="8c13b-126">如果交易涉及的資料庫少於 100，則適合併入單一交易內。</span><span class="sxs-lookup"><span data-stu-id="8c13b-126">It is a good fit for transactions that involve less than 100 databases at a time within a single transaction.</span></span> <span data-ttu-id="8c13b-127">不強制規定這些限制，但超出這些限制時，彈性資料庫交易的效能和成功率必然下降。</span><span class="sxs-lookup"><span data-stu-id="8c13b-127">These limits are not enforced, but one should expect performance and success rates for elastic database transactions to suffer when exceeding these limits.</span></span>

## <a name="installation-and-migration"></a><span data-ttu-id="8c13b-128">安裝和移轉</span><span class="sxs-lookup"><span data-stu-id="8c13b-128">Installation and migration</span></span>
<span data-ttu-id="8c13b-129">我們更新 .NET 程式庫 System.Data.dll 和 System.Transactions.dll，以支援在 SQL DB 中執行彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-129">The capabilities for elastic database transactions in SQL DB are provided through updates to the .NET libraries System.Data.dll and System.Transactions.dll.</span></span> <span data-ttu-id="8c13b-130">DLL 確保必要時使用兩階段交易認可，以確保不可部分完成性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-130">The DLLs ensure that two-phase commit is used where necessary to ensure atomicity.</span></span> <span data-ttu-id="8c13b-131">若要使用彈性資料庫交易來開始開發應用程式，請安裝 [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8c13b-131">To start developing applications using elastic database transactions, install [.NET Framework 4.6.1](https://www.microsoft.com/download/details.aspx?id=49981) or a later version.</span></span> <span data-ttu-id="8c13b-132">在舊版 .NET Framework 上執行時，交易無法升級為分散式交易，將會引發例外狀況。</span><span class="sxs-lookup"><span data-stu-id="8c13b-132">When running on an earlier version of the .NET framework, transactions will fail to promote to a distributed transaction and an exception will be raised.</span></span>

<span data-ttu-id="8c13b-133">安裝之後，您就可以使用 System.Transactions 中的分散式交易 API 和 SQL DB 連接。</span><span class="sxs-lookup"><span data-stu-id="8c13b-133">After installation, you can use the distributed transaction APIs in System.Transactions with connections to SQL DB.</span></span> <span data-ttu-id="8c13b-134">如果您有使用這些 API 的現有 MSDTC 應用程式，只要在安裝 4.6.1 Framework 之後，為 .NET 4.6 重建現有的應用程式即可。</span><span class="sxs-lookup"><span data-stu-id="8c13b-134">If you have existing MSDTC applications using these APIs, simply rebuild your existing applications for .NET 4.6 after installing the 4.6.1 Framework.</span></span> <span data-ttu-id="8c13b-135">如果專案以 .NET 4.6 為目標，它們會自動使用新 Framework 版本中更新的 DLL，而結合 SQL DB 連接的分散式交易 API 呼叫現在會成功。</span><span class="sxs-lookup"><span data-stu-id="8c13b-135">If your projects target .NET 4.6, they will automatically use the updated DLLs from the new Framework version and distributed transaction API calls in combination with connections to SQL DB will now succeed.</span></span>

<span data-ttu-id="8c13b-136">請記住，彈性資料庫交易不需要安裝 MSDTC。</span><span class="sxs-lookup"><span data-stu-id="8c13b-136">Remember that elastic database transactions do not require installing MSDTC.</span></span> <span data-ttu-id="8c13b-137">彈性資料庫交易直接由 SQL DB 管理。</span><span class="sxs-lookup"><span data-stu-id="8c13b-137">Instead, elastic database transactions are directly managed by and within SQL DB.</span></span> <span data-ttu-id="8c13b-138">這可大幅簡化雲端案例，因為 MSDTC 的部署不需要使用分散式交易和 SQL DB。</span><span class="sxs-lookup"><span data-stu-id="8c13b-138">This significantly simplifies cloud scenarios since a deployment of MSDTC is not necessary to use distributed transactions with SQL DB.</span></span> <span data-ttu-id="8c13b-139">第 4 節更詳細地說明如何將彈性資料庫交易和必要的 .NET Framework 連同您的雲端應用程式一起部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="8c13b-139">Section 4 explains in more detail how to deploy elastic database transactions and the required .NET framework together with your cloud applications to Azure.</span></span>

## <a name="development-experience"></a><span data-ttu-id="8c13b-140">開發經驗</span><span class="sxs-lookup"><span data-stu-id="8c13b-140">Development experience</span></span>
### <a name="multi-database-applications"></a><span data-ttu-id="8c13b-141">多重資料庫應用程式</span><span class="sxs-lookup"><span data-stu-id="8c13b-141">Multi-database applications</span></span>
<span data-ttu-id="8c13b-142">下列範例程式碼使用熟悉的 .NET System.Transactions 程式設計經驗。</span><span class="sxs-lookup"><span data-stu-id="8c13b-142">The following sample code uses the familiar programming experience with .NET System.Transactions.</span></span> <span data-ttu-id="8c13b-143">TransactionScope 類別會在 .NET 中建立環境交易</span><span class="sxs-lookup"><span data-stu-id="8c13b-143">The TransactionScope class establishes an ambient transaction in .NET.</span></span> <span data-ttu-id="8c13b-144">(「環境交易」是位於目前執行緒中的交易)。TransactionScope 內開啟的所有連接都參與交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-144">(An “ambient transaction” is one that lives in the current thread.) All connections opened within the TransactionScope participate in the transaction.</span></span> <span data-ttu-id="8c13b-145">如果有不同的資料庫參與，交易會自動提升為分散式交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-145">If different databases participate, the transaction is automatically elevated to a distributed transaction.</span></span> <span data-ttu-id="8c13b-146">設定完成範圍來指出認可，即可控制交易的結果。</span><span class="sxs-lookup"><span data-stu-id="8c13b-146">The outcome of the transaction is controlled by setting the scope to complete to indicate a commit.</span></span>

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

### <a name="sharded-database-applications"></a><span data-ttu-id="8c13b-147">分區化資料庫應用程式</span><span class="sxs-lookup"><span data-stu-id="8c13b-147">Sharded database applications</span></span>
<span data-ttu-id="8c13b-148">SQL DB 的彈性資料庫交易也支援協調分散式交易，您需要使用彈性資料庫用戶端程式庫的 OpenConnectionForKey 方法，開啟相應放大資料層的連接。</span><span class="sxs-lookup"><span data-stu-id="8c13b-148">Elastic database transactions for SQL DB also support coordinating distributed transactions where you use the OpenConnectionForKey method of the elastic database client library to open connections for a scaled out data tier.</span></span> <span data-ttu-id="8c13b-149">假設變更跨數個不同分區化索引鍵值，而您需要保證交易一致性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-149">Consider cases where you need to guarantee transactional consistency for changes across several different sharding key values.</span></span> <span data-ttu-id="8c13b-150">連接到裝載不同分區化索引鍵值的分區時，由 OpenConnectionForKey 代理連接。</span><span class="sxs-lookup"><span data-stu-id="8c13b-150">Connections to the shards hosting the different sharding key values are brokered using OpenConnectionForKey.</span></span> <span data-ttu-id="8c13b-151">在一般情況下可連接到不同分區，以確保交易保證需要分散式交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-151">In the general case, the connections can be to different shards such that ensuring transactional guarantees requires a distributed transaction.</span></span> <span data-ttu-id="8c13b-152">下列程式碼範例說明此方法。</span><span class="sxs-lookup"><span data-stu-id="8c13b-152">The following code sample illustrates this approach.</span></span> <span data-ttu-id="8c13b-153">其中假設使用一個稱為 shardmap 的變數，代表來自彈性資料庫用戶端程式庫的分區對應：</span><span class="sxs-lookup"><span data-stu-id="8c13b-153">It assumes that a variable called shardmap is used to represent a shard map from the elastic database client library:</span></span>

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


## <a name="net-installation-for-azure-cloud-services"></a><span data-ttu-id="8c13b-154">Azure 雲端服務的 .NET 安裝</span><span class="sxs-lookup"><span data-stu-id="8c13b-154">.NET installation for Azure Cloud Services</span></span>
<span data-ttu-id="8c13b-155">Azure 會提供數個供應項目，以裝載 .NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c13b-155">Azure provides several offerings to host .NET applications.</span></span> <span data-ttu-id="8c13b-156">如需不同供應項目的比較，請參閱 [Azure App Service、雲端服務與虛擬機器之比較](../app-service-web/choose-web-site-cloud-service-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-156">A comparison of the different offerings is available in [Azure App Service, Cloud Services, and Virtual Machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span> <span data-ttu-id="8c13b-157">如果供應項目的客體 OS 小於彈性交易所需的 .NET 4.6.1，則您必須將客體 OS 升級至 4.6.1。</span><span class="sxs-lookup"><span data-stu-id="8c13b-157">If the guest OS of the offering is smaller than .NET 4.6.1 required for elastic transactions, you need to upgrade the guest OS to 4.6.1.</span></span> 

<span data-ttu-id="8c13b-158">對於 Azure App Service，目前將不支援升級至客體 OS。</span><span class="sxs-lookup"><span data-stu-id="8c13b-158">For Azure App Services, upgrades to the guest OS are currently not supported.</span></span> <span data-ttu-id="8c13b-159">對於 Azure 虛擬機器，只要登入 VM，並執行最新的 .NET Framework 的安裝程式即可。</span><span class="sxs-lookup"><span data-stu-id="8c13b-159">For Azure Virtual Machines, simply log into the VM and run the installer for the latest .NET framework.</span></span> <span data-ttu-id="8c13b-160">對於 Azure 雲端服務，您需要將新版 .NET 的安裝包含在您部署的啟動工作中。</span><span class="sxs-lookup"><span data-stu-id="8c13b-160">For Azure Cloud Services, you need to include the installation of a newer .NET version into the startup tasks of your deployment.</span></span> <span data-ttu-id="8c13b-161">[在雲端服務角色上安裝 .NET](../cloud-services/cloud-services-dotnet-install-dotnet.md)中說明概念和步驟。</span><span class="sxs-lookup"><span data-stu-id="8c13b-161">The concepts and steps are documented in [Install .NET on a Cloud Service Role](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>  

<span data-ttu-id="8c13b-162">請注意，相較於 .NET 4.6 的安裝程式，.NET 4.6.1 的安裝程式在 Azure 雲端服務上進行啟動程序期間，可能需要更多的暫存儲存空間。</span><span class="sxs-lookup"><span data-stu-id="8c13b-162">Note that the installer for .NET 4.6.1 may require more temporary storage during the bootstrapping process on Azure cloud services than the installer for .NET 4.6.</span></span> <span data-ttu-id="8c13b-163">為了確保能夠順利安裝，您必須在 ServiceDefinition.csdef 檔案中，於啟動工作的 LocalResources 區段和環境設定中，增加 Azure 雲端服務的暫存儲存體，如以下範例所示：</span><span class="sxs-lookup"><span data-stu-id="8c13b-163">To ensure a successful installation, you need to increase temporary storage for your Azure cloud service in your ServiceDefinition.csdef file in the LocalResources section and the environment settings of your startup task, as shown in the following sample:</span></span>

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

## <a name="transactions-across-multiple-servers"></a><span data-ttu-id="8c13b-164">跨多部伺服器的交易</span><span class="sxs-lookup"><span data-stu-id="8c13b-164">Transactions across multiple servers</span></span>
<span data-ttu-id="8c13b-165">在 Azure SQL Database 中，支援跨不同邏輯伺服器的彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-165">Elastic database transactions are supported across different logical servers in Azure SQL Database.</span></span> <span data-ttu-id="8c13b-166">當交易跨越邏輯伺服器的界限時，參與的伺服器首先必須進入一個相互通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-166">When transactions cross logical server boundaries, the participating servers first need to be entered into a mutual communication relationship.</span></span> <span data-ttu-id="8c13b-167">一旦建立通訊關聯性之後，任一部伺服器中的任何資料庫都可以和另一部伺服器中的資料庫一起參與彈性交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-167">Once the communication relationship has been established, any database in any of the two servers can participate in elastic transactions with databases from the other server.</span></span> <span data-ttu-id="8c13b-168">對於跨越兩個以上的邏輯伺服器的交易，任何一組邏輯伺服器都必須先具備通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-168">With transactions spanning more than two logical servers, a communication relationship needs to be in place for any pair of logical servers.</span></span>

<span data-ttu-id="8c13b-169">使用下列 PowerShell Cmdlet 管理跨伺服器的通訊關聯性，以進行彈性資料庫交易：</span><span class="sxs-lookup"><span data-stu-id="8c13b-169">Use the following PowerShell cmdlets to manage cross-server communication relationships for elastic database transactions:</span></span>

* <span data-ttu-id="8c13b-170">**New-AzureRmSqlServerCommunicationLink**：使用這個 Cmdlet 建立 Azure SQL DB 中兩部邏輯伺服器之間的新通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-170">**New-AzureRmSqlServerCommunicationLink**: Use this cmdlet to create a new communication relationship between two logical servers in Azure SQL DB.</span></span> <span data-ttu-id="8c13b-171">此關聯性是對稱的，也就是說，這兩部伺服器彼此都可以起始交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-171">The relationship is symmetric which means both servers can initiate transactions with the other server.</span></span>
* <span data-ttu-id="8c13b-172">**Get-AzureRmSqlServerCommunicationLink**：使用這個 Cmdlet 擷取現有的通訊關聯性及其屬性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-172">**Get-AzureRmSqlServerCommunicationLink**: Use this cmdlet to retrieve existing communication relationships and their properties.</span></span>
* <span data-ttu-id="8c13b-173">**Remove-AzureRmSqlServerCommunicationLink**：使用這個 Cmdlet 移除現有的通訊關聯性。</span><span class="sxs-lookup"><span data-stu-id="8c13b-173">**Remove-AzureRmSqlServerCommunicationLink**: Use this cmdlet to remove an existing communication relationship.</span></span> 

## <a name="monitoring-transaction-status"></a><span data-ttu-id="8c13b-174">監視交易狀態</span><span class="sxs-lookup"><span data-stu-id="8c13b-174">Monitoring transaction status</span></span>
<span data-ttu-id="8c13b-175">使用 SQL DB 中的動態管理檢視 (DMV) 來監視進行中彈性資料庫交易的狀態和進度。</span><span class="sxs-lookup"><span data-stu-id="8c13b-175">Use Dynamic Management Views (DMVs) in SQL DB to monitor status and progress of your ongoing elastic database transactions.</span></span> <span data-ttu-id="8c13b-176">所有與交易相關的 DMV 都與 SQL DB 中的分散式交易有關聯。</span><span class="sxs-lookup"><span data-stu-id="8c13b-176">All DMVs related to transactions are relevant for distributed transactions in SQL DB.</span></span> <span data-ttu-id="8c13b-177">您可以在這裡找到對應的 DMV 清單： [交易相關的動態管理檢視和函數 (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-177">You can find the corresponding list of DMVs here: [Transaction Related Dynamic Management Views and Functions (Transact-SQL)](https://msdn.microsoft.com/library/ms178621.aspx).</span></span>

<span data-ttu-id="8c13b-178">這些 DMV 特別有用：</span><span class="sxs-lookup"><span data-stu-id="8c13b-178">These DMVs are particularly useful:</span></span>

* <span data-ttu-id="8c13b-179">**sys.dm\_tran\_active\_transactions**：列出目前使用中的交易及其狀態。</span><span class="sxs-lookup"><span data-stu-id="8c13b-179">**sys.dm\_tran\_active\_transactions**: Lists currently active transactions and their status.</span></span> <span data-ttu-id="8c13b-180">UOW (工作單位) 資料行可以識別屬於相同分散式交易的不同子交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-180">The UOW (Unit Of Work) column can identify the different child transactions that belong to the same distributed transaction.</span></span> <span data-ttu-id="8c13b-181">相同分散式交易內的所有交易具有相同的 UOW 值。</span><span class="sxs-lookup"><span data-stu-id="8c13b-181">All transactions within the same distributed transaction carry the same UOW value.</span></span> <span data-ttu-id="8c13b-182">如需詳細資訊，請參閱 [DMV 文件](https://msdn.microsoft.com/library/ms174302.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8c13b-182">See the [DMV documentation](https://msdn.microsoft.com/library/ms174302.aspx) for more details.</span></span>
* <span data-ttu-id="8c13b-183">**sys.dm\_tran\_database\_transactions**：提供交易的其他相關資訊，例如交易在記錄檔中的位置。</span><span class="sxs-lookup"><span data-stu-id="8c13b-183">**sys.dm\_tran\_database\_transactions**: Provides additional information about transactions, such as placement of the transaction in the log.</span></span> <span data-ttu-id="8c13b-184">如需詳細資訊，請參閱 [DMV 文件](https://msdn.microsoft.com/library/ms186957.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8c13b-184">See the [DMV documentation](https://msdn.microsoft.com/library/ms186957.aspx) for more details.</span></span>
* <span data-ttu-id="8c13b-185">**sys.dm\_tran\_locks**：提供目前進行中交易所持有的鎖定相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8c13b-185">**sys.dm\_tran\_locks**: Provides information about the locks that are currently held by ongoing transactions.</span></span> <span data-ttu-id="8c13b-186">如需詳細資訊，請參閱 [DMV 文件](https://msdn.microsoft.com/library/ms190345.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="8c13b-186">See the [DMV documentation](https://msdn.microsoft.com/library/ms190345.aspx) for more details.</span></span>

## <a name="limitations"></a><span data-ttu-id="8c13b-187">限制</span><span class="sxs-lookup"><span data-stu-id="8c13b-187">Limitations</span></span>
<span data-ttu-id="8c13b-188">SQL DB 中的彈性資料庫交易目前有下列限制：</span><span class="sxs-lookup"><span data-stu-id="8c13b-188">The following limitations currently apply to elastic database transactions in SQL DB:</span></span>

* <span data-ttu-id="8c13b-189">僅支援 SQL DB 中跨資料庫的交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-189">Only transactions across databases in SQL DB are supported.</span></span> <span data-ttu-id="8c13b-190">其他 [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) 資源提供者和 SQL DB 以外的資料庫無法參與彈性資料庫交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-190">Other [X/Open XA](https://en.wikipedia.org/wiki/X/Open_XA) resource providers and databases outside of SQL DB cannot participate in elastic database transactions.</span></span> <span data-ttu-id="8c13b-191">這表示彈性資料庫交易無法延伸到內部部署 SQL Server 和 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8c13b-191">That means that elastic database transactions cannot stretch across on premises SQL Server and Azure SQL Databases.</span></span> <span data-ttu-id="8c13b-192">對於內部部署的分散式交易，請繼續使用 MSDTC。</span><span class="sxs-lookup"><span data-stu-id="8c13b-192">For distributed transactions on premises, continue to use MSDTC.</span></span> 
* <span data-ttu-id="8c13b-193">僅支援來自 .NET 應用程式的用戶端協調交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-193">Only client-coordinated transactions from a .NET application are supported.</span></span> <span data-ttu-id="8c13b-194">目前已規劃 T-SQL 的伺服器端支援，例如 BEGIN DISTRIBUTED TRANSACTION，但尚未推出。</span><span class="sxs-lookup"><span data-stu-id="8c13b-194">Server-side support for T-SQL such as BEGIN DISTRIBUTED TRANSACTION is planned, but not yet available.</span></span> 
* <span data-ttu-id="8c13b-195">不支援跨 WCF 服務的交易。</span><span class="sxs-lookup"><span data-stu-id="8c13b-195">Transactions across WCF services are not supported.</span></span> <span data-ttu-id="8c13b-196">例如，您有執行交易的 WCF 服務方法。</span><span class="sxs-lookup"><span data-stu-id="8c13b-196">For example, you have a WCF service method that executes a transaction.</span></span> <span data-ttu-id="8c13b-197">納入交易範圍內的呼叫將會失敗，因為 [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-197">Enclosing the call within a transaction scope will fail as a [System.ServiceModel.ProtocolException](https://msdn.microsoft.com/library/system.servicemodel.protocolexception).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c13b-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c13b-198">Next steps</span></span>
<span data-ttu-id="8c13b-199">如有問題，請透過 [SQL Database 論壇](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted)與我們連絡，如需要求增加功能，請將這些功能新增至 [SQL Database 意見反應論壇](https://feedback.azure.com/forums/217321-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="8c13b-199">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-transactions-overview/distributed-transactions.png



