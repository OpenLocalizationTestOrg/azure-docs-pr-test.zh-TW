---
title: "升級至最新的彈性資料庫用戶端程式庫 | Microsoft Docs"
description: "使用 Nuget 升級應用程式和程式庫"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 0a546510-76e7-465e-9271-f15ff0cfa959
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: ddove
ms.openlocfilehash: 7e28d128645e856c0efa6e4f78d8f9f36982a76c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-an-app-to-use-the-latest-elastic-database-client-library"></a><span data-ttu-id="9b11e-103">將應用程式升級以使用最新的彈性資料庫用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="9b11e-103">Upgrade an app to use the latest elastic database client library</span></span>
<span data-ttu-id="9b11e-104">新版本的[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)是透過 Visual Studio 中的 NuGet 和 NuGetPackage Manager 介面提供。</span><span class="sxs-lookup"><span data-stu-id="9b11e-104">New versions of the [Elastic Database client library](sql-database-elastic-database-client-library.md) are  available through NuGetand the NuGetPackage Manager interface in Visual Studio.</span></span> <span data-ttu-id="9b11e-105">升級包含用戶端程式庫的錯誤修正以及對新功能的支援。</span><span class="sxs-lookup"><span data-stu-id="9b11e-105">Upgrades contain bug fixes and support for new capabilities of the client library.</span></span>

<span data-ttu-id="9b11e-106">**如需最新版本** ：請瀏覽 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="9b11e-106">**For the latest version:** Go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span>

<span data-ttu-id="9b11e-107">使用新的程式庫重新建置您的應用程式，以及變更您 Azure SQL Databases 中儲存的現有分區對應管理員中繼資料以支援新功能。</span><span class="sxs-lookup"><span data-stu-id="9b11e-107">Rebuild your application with the new library, as well as change your existing Shard Map Manager metadata stored in your Azure SQL Databases to support new features.</span></span>

<span data-ttu-id="9b11e-108">依照順序執行步驟可確保在更新中繼資料物件時，舊版用戶端程式庫不會再於您的環境中出現，這表示升級之後將不會再建立舊版中繼資料物件。</span><span class="sxs-lookup"><span data-stu-id="9b11e-108">Performing these steps in order ensures that old versions of the client library are no longer present in your environment when metadata objects are updated, which means that old-version metadata objects won’t be created after upgrade.</span></span>   

## <a name="upgrade-steps"></a><span data-ttu-id="9b11e-109">升級步驟</span><span class="sxs-lookup"><span data-stu-id="9b11e-109">Upgrade steps</span></span>
<span data-ttu-id="9b11e-110">**1.升級您的應用程式。**</span><span class="sxs-lookup"><span data-stu-id="9b11e-110">**1. Upgrade your applications.**</span></span> <span data-ttu-id="9b11e-111">在 Visual Studio 中，將最新的用戶端程式庫版本下載到您所有使用程式庫的開發專案中，並加以參照；然後重新建置及部署。</span><span class="sxs-lookup"><span data-stu-id="9b11e-111">In Visual Studio, download and reference the latest client library version into all of your development projects that use the library; then rebuild and deploy.</span></span> 

* <span data-ttu-id="9b11e-112">在您的 Visual Studio 解決方案中，依序選取 [工具] -->  [NuGet 套件管理員]  -->  [管理解決方案的 NuGet 套件]。</span><span class="sxs-lookup"><span data-stu-id="9b11e-112">In your Visual Studio solution, select **Tools** --> **NuGet Package Manager** -->  **Manage NuGet Packages for Solution**.</span></span> 
* <span data-ttu-id="9b11e-113">(Visual Studio 2013) 在左邊面板中，選取 [更新]，然後在視窗中顯示的 [Azure SQL Database Elastic Scale 用戶端程式庫]套件上選取 [更新]按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b11e-113">(Visual Studio 2013) In the left panel, select **Updates**, and then select the **Update** button on the package **Azure SQL Database Elastic Scale Client Library** that appears in the window.</span></span>
* <span data-ttu-id="9b11e-114">(Visual Studio 2015) 設定篩選方塊為 [可升級] 。</span><span class="sxs-lookup"><span data-stu-id="9b11e-114">(Visual Studio 2015) Set the Filter box to **Upgrade available**.</span></span> <span data-ttu-id="9b11e-115">選取要更新的套件，然後按一下 [更新]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b11e-115">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="9b11e-116">(Visual Studio 2017) 在對話方塊頂端，選取 [更新]。</span><span class="sxs-lookup"><span data-stu-id="9b11e-116">(Visual Studio 2017) At the top of the dialog, select **Updates**.</span></span> <span data-ttu-id="9b11e-117">選取要更新的套件，然後按一下 [更新]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9b11e-117">Select the package to update, and click the **Update** button.</span></span>
* <span data-ttu-id="9b11e-118">建置並部署。</span><span class="sxs-lookup"><span data-stu-id="9b11e-118">Build and Deploy.</span></span> 

<span data-ttu-id="9b11e-119">**2.升級您的指令碼。**</span><span class="sxs-lookup"><span data-stu-id="9b11e-119">**2. Upgrade your scripts.**</span></span> <span data-ttu-id="9b11e-120">如果您是使用 **PowerShell** 指令碼來管理分區，請[下載新的程式庫版本](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)並將它複製到您從中執行指令碼的目錄。</span><span class="sxs-lookup"><span data-stu-id="9b11e-120">If you are using **PowerShell** scripts to manage shards, [download the new library version](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) and copy it into the directory from which you execute scripts.</span></span> 

<span data-ttu-id="9b11e-121">**3.升級您的分割合併服務。**</span><span class="sxs-lookup"><span data-stu-id="9b11e-121">**3. Upgrade your split-merge service.**</span></span> <span data-ttu-id="9b11e-122">如果您使用彈性資料庫分割合併工具來重新安排分區資料，請[下載並部署最新版本的工具](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)。</span><span class="sxs-lookup"><span data-stu-id="9b11e-122">If you use the elastic database split-merge tool to reorganize sharded data, [download and deploy the latest version of the tool](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/).</span></span> <span data-ttu-id="9b11e-123">服務的詳細升級步驟可以在[這裡](sql-database-elastic-scale-overview-split-and-merge.md)找到。</span><span class="sxs-lookup"><span data-stu-id="9b11e-123">Detailed upgrade steps for the Service can be found [here](sql-database-elastic-scale-overview-split-and-merge.md).</span></span> 

<span data-ttu-id="9b11e-124">**4.升級您的分區對應管理員資料庫**。</span><span class="sxs-lookup"><span data-stu-id="9b11e-124">**4. Upgrade your Shard Map Manager databases**.</span></span> <span data-ttu-id="9b11e-125">升級支援您 Azure SQL Database 中之分區對應的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9b11e-125">Upgrade the metadata supporting your Shard Maps in Azure SQL Database.</span></span>  <span data-ttu-id="9b11e-126">您可以使用 PowerShell 或 C# 來完成此作業。</span><span class="sxs-lookup"><span data-stu-id="9b11e-126">There are two ways you can accomplish this, using PowerShell or C#.</span></span> <span data-ttu-id="9b11e-127">下面會說明這兩個選項。</span><span class="sxs-lookup"><span data-stu-id="9b11e-127">Both options are shown below.</span></span>

<span data-ttu-id="9b11e-128">***選項 1：使用 PowerShell 升級中繼資料***</span><span class="sxs-lookup"><span data-stu-id="9b11e-128">***Option 1: Upgrade metadata using PowerShell***</span></span>

1. <span data-ttu-id="9b11e-129">請從 [這裡](http://nuget.org/nuget.exe) 下載 NuGet 的最新命令列公用程式並儲存至資料夾。</span><span class="sxs-lookup"><span data-stu-id="9b11e-129">Download the latest command-line utility for NuGet from [here](http://nuget.org/nuget.exe) and save to a folder.</span></span> 
2. <span data-ttu-id="9b11e-130">開啟命令提示字元，瀏覽至相同的資料夾，然後下達命令： `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span><span class="sxs-lookup"><span data-stu-id="9b11e-130">Open a Command Prompt, navigate to the same folder, and issue the command: `nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Client`</span></span>
3. <span data-ttu-id="9b11e-131">瀏覽至包含您剛剛下載的新用戶端 DLL 版本的子資料夾，例如： `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span><span class="sxs-lookup"><span data-stu-id="9b11e-131">Navigate to the subfolder containing the new client DLL version you have just downloaded, for example: `cd .\Microsoft.Azure.SqlDatabase.ElasticScale.Client.1.0.0\lib\net45`</span></span>
4. <span data-ttu-id="9b11e-132">從 [指令碼中心](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9)下載彈性資料庫用戶端升級程式碼片段，然後將它儲存到包含 DLL 的相同資料夾。</span><span class="sxs-lookup"><span data-stu-id="9b11e-132">Download the elastic database client upgrade scriptlet from the [Script Center](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-Elastic-6442e6a9), and save it into the same folder containing the DLL.</span></span>
5. <span data-ttu-id="9b11e-133">從該資料夾中，從命令提示字元執行 “PowerShell .\upgrade.ps1”，然後依照提示完成作業。</span><span class="sxs-lookup"><span data-stu-id="9b11e-133">From that folder, run “PowerShell .\upgrade.ps1” from the command prompt and follow the prompts.</span></span>

<span data-ttu-id="9b11e-134">***選項 2：使用 C# 升級中繼資料***</span><span class="sxs-lookup"><span data-stu-id="9b11e-134">***Option 2: Upgrade metadata using C#***</span></span>

<span data-ttu-id="9b11e-135">或者，建立一個可以開啟您的 ShardMapManager 的 Visual Studio 應用程式，複製到所有分區，然後透過呼叫 [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) 和 [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) 方法來執行中繼資料升級，如此範例中所示：</span><span class="sxs-lookup"><span data-stu-id="9b11e-135">Alternatively, create a Visual Studio application that opens your ShardMapManager, iterates over all shards, and performs the metadata upgrade by calling the methods [UpgradeLocalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradelocalstore.aspx) and [UpgradeGlobalStore](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.upgradeglobalstore.aspx) as in this example:</span></span> 

    ShardMapManager smm =
       ShardMapManagerFactory.GetSqlShardMapManager
       (connStr, ShardMapManagerLoadPolicy.Lazy); 
    smm.UpgradeGlobalStore(); 

    foreach (ShardLocation loc in
     smm.GetDistinctShardLocations()) 
    {   
       smm.UpgradeLocalStore(loc); 
    } 

<span data-ttu-id="9b11e-136">這些中繼資料升級技巧可以套用多次且不會造成損害。</span><span class="sxs-lookup"><span data-stu-id="9b11e-136">These techniques for metadata upgrades can be applied multiple times without harm.</span></span> <span data-ttu-id="9b11e-137">例如，如果較舊的用戶端版本在您已經更新之後意外建立分區，您可以在所有分區上再次執行升級，以確保您的整個基礎結構都擁有最新的中繼資料版本。</span><span class="sxs-lookup"><span data-stu-id="9b11e-137">For example, if an older client version inadvertently creates a shard after you have already updated, you can run upgrade again across all shards to ensure that the latest metadata version is present throughout your infrastructure.</span></span> 

<span data-ttu-id="9b11e-138">**注意：**至今發佈的新版本用戶端程式庫可以繼續和 Azure SQL DB 上的舊版分區對應管理員中繼資料搭配使用，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="9b11e-138">**Note:**  New versions of the client library published to-date continue to work with prior versions of the Shard Map Manager metadata on Azure SQL DB, and vice-versa.</span></span>   <span data-ttu-id="9b11e-139">但是，若要使用最新用戶端中的部分新功能，則必須升級中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9b11e-139">However to take advantage of some of the new features in the latest client, metadata needs to be upgraded.</span></span>   <span data-ttu-id="9b11e-140">請注意，中繼資料升級將不會影響任何使用者資料或應用程式特定資料，只會影響分區對應管理員所建立及使用的物件。</span><span class="sxs-lookup"><span data-stu-id="9b11e-140">Note that metadata upgrades will not affect any user-data or application-specific data, only objects created and used by the Shard Map Manager.</span></span>  <span data-ttu-id="9b11e-141">而且應用程式會繼續透過上述的升級順序運作。</span><span class="sxs-lookup"><span data-stu-id="9b11e-141">And applications continue to operate through the upgrade sequence described above.</span></span> 

## <a name="elastic-database-client-version-history"></a><span data-ttu-id="9b11e-142">彈性資料庫用戶端版本歷程記錄</span><span class="sxs-lookup"><span data-stu-id="9b11e-142">Elastic database client version history</span></span>
<span data-ttu-id="9b11e-143">如需版本歷程記錄，請瀏覽 [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span><span class="sxs-lookup"><span data-stu-id="9b11e-143">For version history, go to [Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]:./media/sql-database-elastic-scale-upgrade-client-library/nuget-upgrade.png

