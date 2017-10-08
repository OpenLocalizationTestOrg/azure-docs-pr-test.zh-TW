---
title: "aaaRun Apache Sqoop 作業與 Azure HDInsight (Hadoop) |Microsoft 文件"
description: "了解如何從工作站 toorun Sqoop toouse Azure PowerShell 匯入和匯出的 Hadoop 叢集和 Azure SQL database 之間。"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 2fdcc6b7-6ad5-4397-a30b-e7e389b66c7a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bdac507704937d77921c9c13d70aa2434c7e3be4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-sqoop-with-hadoop-in-hdinsight"></a><span data-ttu-id="ce68c-103">在 HDInsight 上將 Sqoop 與 Hadoop 搭配使用</span><span class="sxs-lookup"><span data-stu-id="ce68c-103">Use Sqoop with Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="ce68c-104">深入了解如何 toouse Sqoop 在 HDInsight tooimport 與 HDInsight 叢集和 Azure SQL database 或 SQL Server 資料庫之間的匯出。</span><span class="sxs-lookup"><span data-stu-id="ce68c-104">Learn how toouse Sqoop in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

<span data-ttu-id="ce68c-105">雖然 Hadoop 是合理的選擇來處理非結構化和半結構化資料，例如記錄檔和檔案，也可能需要 tooprocess 結構化資料儲存在關聯式資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ce68c-105">Although Hadoop is a natural choice for processing unstructured and semistructured data, such as logs and files, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="ce68c-106">[Sqoop] [ sqoop-user-guide-1.4.4]是設計工具 tootransfer Hadoop 叢集和關聯式資料庫之間的資料。</span><span class="sxs-lookup"><span data-stu-id="ce68c-106">[Sqoop][sqoop-user-guide-1.4.4] is a tool designed tootransfer data between Hadoop clusters and relational databases.</span></span> <span data-ttu-id="ce68c-107">您可以使用它 tooimport 資料從關聯式資料庫管理系統 (RDBMS) 例如 SQL Server、 MySQL 或 Oracle hello Hadoop 分散式檔案系統 (HDFS)，到 Hadoop MapReduce 或登錄區，使用中的 hello 資料轉換，然後匯出成的 hello 資料RDBMS。</span><span class="sxs-lookup"><span data-stu-id="ce68c-107">You can use it tooimport data from a relational database management system (RDBMS) such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="ce68c-108">在本教學課程中，您將使用 SQL Server Database 做為關聯式資料庫。</span><span class="sxs-lookup"><span data-stu-id="ce68c-108">In this tutorial, you are using a SQL Server database for your relational database.</span></span>

<span data-ttu-id="ce68c-109">Sqoop HDInsight 叢集支援的版本，請參閱[HDInsight 所提供的 hello 叢集版本中最新消息？][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="ce68c-109">For Sqoop versions that are supported on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions]</span></span>

## <a name="understand-hello-scenario"></a><span data-ttu-id="ce68c-110">了解 hello 案例</span><span class="sxs-lookup"><span data-stu-id="ce68c-110">Understand hello scenario</span></span>

<span data-ttu-id="ce68c-111">HDInsight 叢集附有某些範例資料。</span><span class="sxs-lookup"><span data-stu-id="ce68c-111">HDInsight cluster comes with some sample data.</span></span> <span data-ttu-id="ce68c-112">您使用下列兩個樣本的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce68c-112">You use hello following two samples:</span></span>

* <span data-ttu-id="ce68c-113">位於 */example/data/sample.log*的 log4j 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ce68c-113">A log4j log file, which is located at */example/data/sample.log*.</span></span> <span data-ttu-id="ce68c-114">從 hello 檔案中擷取下列記錄檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce68c-114">hello following logs are extracted from hello file:</span></span>
  
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
* <span data-ttu-id="ce68c-115">名為的 Hive 資料表*hivesampletable*，其參考 hello 資料檔案位於*/hive/warehouse/hivesampletable*。</span><span class="sxs-lookup"><span data-stu-id="ce68c-115">A Hive table named *hivesampletable*, which references hello data file located at */hive/warehouse/hivesampletable*.</span></span> <span data-ttu-id="ce68c-116">hello 資料表包含某些行動裝置資料。</span><span class="sxs-lookup"><span data-stu-id="ce68c-116">hello table contains some mobile device data.</span></span> 
  
  | <span data-ttu-id="ce68c-117">欄位</span><span class="sxs-lookup"><span data-stu-id="ce68c-117">Field</span></span> | <span data-ttu-id="ce68c-118">資料類型</span><span class="sxs-lookup"><span data-stu-id="ce68c-118">Data type</span></span> |
  | --- | --- |
  | <span data-ttu-id="ce68c-119">clientid</span><span class="sxs-lookup"><span data-stu-id="ce68c-119">clientid</span></span> |<span data-ttu-id="ce68c-120">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-120">string</span></span> |
  | <span data-ttu-id="ce68c-121">querytime</span><span class="sxs-lookup"><span data-stu-id="ce68c-121">querytime</span></span> |<span data-ttu-id="ce68c-122">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-122">string</span></span> |
  | <span data-ttu-id="ce68c-123">market</span><span class="sxs-lookup"><span data-stu-id="ce68c-123">market</span></span> |<span data-ttu-id="ce68c-124">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-124">string</span></span> |
  | <span data-ttu-id="ce68c-125">deviceplatform</span><span class="sxs-lookup"><span data-stu-id="ce68c-125">deviceplatform</span></span> |<span data-ttu-id="ce68c-126">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-126">string</span></span> |
  | <span data-ttu-id="ce68c-127">devicemake</span><span class="sxs-lookup"><span data-stu-id="ce68c-127">devicemake</span></span> |<span data-ttu-id="ce68c-128">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-128">string</span></span> |
  | <span data-ttu-id="ce68c-129">devicemodel</span><span class="sxs-lookup"><span data-stu-id="ce68c-129">devicemodel</span></span> |<span data-ttu-id="ce68c-130">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-130">string</span></span> |
  | <span data-ttu-id="ce68c-131">state</span><span class="sxs-lookup"><span data-stu-id="ce68c-131">state</span></span> |<span data-ttu-id="ce68c-132">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-132">string</span></span> |
  | <span data-ttu-id="ce68c-133">country</span><span class="sxs-lookup"><span data-stu-id="ce68c-133">country</span></span> |<span data-ttu-id="ce68c-134">string</span><span class="sxs-lookup"><span data-stu-id="ce68c-134">string</span></span> |
  | <span data-ttu-id="ce68c-135">querydwelltime</span><span class="sxs-lookup"><span data-stu-id="ce68c-135">querydwelltime</span></span> |<span data-ttu-id="ce68c-136">double</span><span class="sxs-lookup"><span data-stu-id="ce68c-136">double</span></span> |
  | <span data-ttu-id="ce68c-137">sessionid</span><span class="sxs-lookup"><span data-stu-id="ce68c-137">sessionid</span></span> |<span data-ttu-id="ce68c-138">bigint</span><span class="sxs-lookup"><span data-stu-id="ce68c-138">bigint</span></span> |
  | <span data-ttu-id="ce68c-139">sessionpagevieworder</span><span class="sxs-lookup"><span data-stu-id="ce68c-139">sessionpagevieworder</span></span> |<span data-ttu-id="ce68c-140">bigint</span><span class="sxs-lookup"><span data-stu-id="ce68c-140">bigint</span></span> |

<span data-ttu-id="ce68c-141">首先，匯出*sample.log*和*hivesampletable* toohello Azure SQL database 或 tooSQL 伺服器，然後匯入 hello 資料表，其中包含 hello 行動裝置資料回 tooHDInsight 使用 hello下列路徑：</span><span class="sxs-lookup"><span data-stu-id="ce68c-141">First, you export *sample.log* and *hivesampletable* toohello Azure SQL database or tooSQL Server, and then import hello table that contains hello mobile device data back tooHDInsight by using hello following path:</span></span>

    /tutorials/usesqoop/importeddata

## <a name="create-cluster-and-sql-database"></a><span data-ttu-id="ce68c-142">建立叢集與 SQL Database</span><span class="sxs-lookup"><span data-stu-id="ce68c-142">Create cluster and SQL database</span></span>
<span data-ttu-id="ce68c-143">本節說明如何 toocreate 叢集、 SQL 資料庫和 hello 執行 hello 教學課程使用的 SQL 資料庫結構描述 hello Azure 入口網站和 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="ce68c-143">This section shows you how toocreate a cluster, a SQL Database, and hello SQL database schemas for running hello tutorial using hello Azure portal and an Azure Resource Manager template.</span></span> <span data-ttu-id="ce68c-144">可以在中找到 hello 範本[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/)。</span><span class="sxs-lookup"><span data-stu-id="ce68c-144">hello template can be found in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-sql-database/).</span></span> <span data-ttu-id="ce68c-145">hello Resource Manager 範本呼叫 bacpac 封裝 toodeploy hello 資料表結構描述 tooSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ce68c-145">hello Resource Manager template calls a bacpac package toodeploy hello table schemas tooSQL database.</span></span>  <span data-ttu-id="ce68c-146">hello bacpac 封裝位於公用 blob 容器，https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac。</span><span class="sxs-lookup"><span data-stu-id="ce68c-146">hello bacpac package is located in a public blob container, https://hditutorialdata.blob.core.windows.net/usesqoop/SqoopTutorial-2016-2-23-11-2.bacpac.</span></span> <span data-ttu-id="ce68c-147">如果您想要私用容器 toouse hello bacpac 檔案，使用 hello 遵循 hello 範本中的值：</span><span class="sxs-lookup"><span data-stu-id="ce68c-147">If you want toouse a private container for hello bacpac files, use hello following values in hello template:</span></span>
   
        "storageKeyType": "Primary",
        "storageKey": "<TheAzureStorageAccountKey>",

<span data-ttu-id="ce68c-148">如果您偏好 toouse Azure PowerShell toocreate hello 叢集和 hello SQL 資料庫，請參閱[附錄 A](#appendix-a---a-powershell-sample)。</span><span class="sxs-lookup"><span data-stu-id="ce68c-148">If you prefer toouse Azure PowerShell toocreate hello cluster and hello SQL Database, see [Appendix A](#appendix-a---a-powershell-sample).</span></span>

1. <span data-ttu-id="ce68c-149">按一下下列映像 tooopen Resource Manager 範本使用 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="ce68c-149">Click hello following image tooopen a Resource Manager template in hello Azure portal.</span></span>         
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-sql-database%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-use-sqoop/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   

2. <span data-ttu-id="ce68c-150">輸入下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce68c-150">Enter hello following properties:</span></span>

    - <span data-ttu-id="ce68c-151">**訂用帳戶**：輸入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ce68c-151">**Subscription**: Enter your Azure subscription.</span></span>
    - <span data-ttu-id="ce68c-152">**資源群組**：建立新的 Azure 資源群組，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ce68c-152">**Resource Group**: Create a new Azure Resource Group, or select an existing Resource Group.</span></span>  <span data-ttu-id="ce68c-153">資源群組是為了管理之用。</span><span class="sxs-lookup"><span data-stu-id="ce68c-153">A Resource Group is for management purpose.</span></span>  <span data-ttu-id="ce68c-154">它是物件的容器。</span><span class="sxs-lookup"><span data-stu-id="ce68c-154">It is a container for objects.</span></span>
    - <span data-ttu-id="ce68c-155">**位置**：選取區域。</span><span class="sxs-lookup"><span data-stu-id="ce68c-155">**Location**: Select a region.</span></span>
    - <span data-ttu-id="ce68c-156">**ClusterName**： 輸入 hello Hadoop 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ce68c-156">**ClusterName**: Enter a name for hello Hadoop cluster.</span></span>
    - <span data-ttu-id="ce68c-157">**叢集登入名稱和密碼**: hello 預設登入名稱是系統管理員。</span><span class="sxs-lookup"><span data-stu-id="ce68c-157">**Cluster login name and password**: hello default login name is admin.</span></span>
    - <span data-ttu-id="ce68c-158">SSH 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ce68c-158">**SSH user name and password**.</span></span>
    - <span data-ttu-id="ce68c-159">**SQL Database 伺服器登入名稱和密碼**。</span><span class="sxs-lookup"><span data-stu-id="ce68c-159">**SQL database server login name and password**.</span></span>
    - <span data-ttu-id="ce68c-160">**_artifacts 位置**： 使用 hello 預設值，除非您希望 toouse backpac 檔案在不同的位置。</span><span class="sxs-lookup"><span data-stu-id="ce68c-160">**_artifacts Location**: Use hello default value unless you want toouse your own backpac file in a different location.</span></span>
    - <span data-ttu-id="ce68c-161">**_artifacts 位置 SAS 權杖**︰保留為空白。</span><span class="sxs-lookup"><span data-stu-id="ce68c-161">**_artifacts Location Sas Token**: Leave it blank.</span></span>
    - <span data-ttu-id="ce68c-162">**Bacpac 檔案名稱**： 使用 hello 的預設值，除非您想 toouse backpac 檔案。</span><span class="sxs-lookup"><span data-stu-id="ce68c-162">**Bacpac File Name**: Use hello default value unless you want toouse your own backpac file.</span></span>
     
     <span data-ttu-id="ce68c-163">下列值的 hello 是硬式編碼 hello 變數區段中：</span><span class="sxs-lookup"><span data-stu-id="ce68c-163">hello following values are hardcoded in hello variables section:</span></span>
     
     | <span data-ttu-id="ce68c-164">預設儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="ce68c-164">Default storage account name</span></span> | <span data-ttu-id="ce68c-165"><CluterName>store</span><span class="sxs-lookup"><span data-stu-id="ce68c-165"><CluterName>store</span></span> |
     | --- | --- |
     | <span data-ttu-id="ce68c-166">Azure SQL Database 伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="ce68c-166">Azure SQL database server name</span></span> |<span data-ttu-id="ce68c-167"><ClusterName>dbserver</span><span class="sxs-lookup"><span data-stu-id="ce68c-167"><ClusterName>dbserver</span></span> |
     | <span data-ttu-id="ce68c-168">Azure SQL Database 名稱</span><span class="sxs-lookup"><span data-stu-id="ce68c-168">Azure SQL database name</span></span> |<span data-ttu-id="ce68c-169"><ClusterName>db</span><span class="sxs-lookup"><span data-stu-id="ce68c-169"><ClusterName>db</span></span> |
     
     <span data-ttu-id="ce68c-170">請記下這些值。</span><span class="sxs-lookup"><span data-stu-id="ce68c-170">Please write down these values.</span></span>  <span data-ttu-id="ce68c-171">您稍後在 hello 教學課程需要它們。</span><span class="sxs-lookup"><span data-stu-id="ce68c-171">You need them later in hello tutorial.</span></span>

<span data-ttu-id="ce68c-172">3.按一下**確定**toosave hello 參數。</span><span class="sxs-lookup"><span data-stu-id="ce68c-172">3.Click **OK** toosave hello parameters.</span></span>

<span data-ttu-id="ce68c-173">4.從 hello**自訂部署**刀鋒視窗中，按一下 **資源群組**下拉式清單方塊，然後再按一下**新增**toocreate 新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="ce68c-173">4.From hello **Custom deployment** blade, click **Resource group** dropdown box, and then click **New** toocreate a new resource group.</span></span> <span data-ttu-id="ce68c-174">hello 資源群組是群組 hello 叢集、 hello 相依的儲存體帳戶和其他已連結之資源的容器。</span><span class="sxs-lookup"><span data-stu-id="ce68c-174">hello resource group is a container that groups hello cluster, hello dependent storage account and other linked resource.</span></span>

<span data-ttu-id="ce68c-175">5. 按一下 法律條款，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="ce68c-175">5.Click **Legal terms**, and then click **Create**.</span></span>

<span data-ttu-id="ce68c-176">6. 按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ce68c-176">6.Click **Create**.</span></span> <span data-ttu-id="ce68c-177">您會看到新的圖格，標題為「提交範本部署的部署」。</span><span class="sxs-lookup"><span data-stu-id="ce68c-177">You see a new tile titled Submitting deployment for Template deployment.</span></span> <span data-ttu-id="ce68c-178">可能需要約 20 分鐘 toocreate hello 叢集和 SQL database。</span><span class="sxs-lookup"><span data-stu-id="ce68c-178">It takes about around 20 minutes toocreate hello cluster and SQL database.</span></span>

<span data-ttu-id="ce68c-179">如果您選擇 toouse 現有的 Azure SQL 資料庫或 Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="ce68c-179">If you choose toouse existing Azure SQL database or Microsoft SQL Server</span></span>

* <span data-ttu-id="ce68c-180">**Azure SQL database**： 您必須從您的工作站設定 hello Azure SQL database 伺服器 tooallow 存取的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ce68c-180">**Azure SQL database**: You must configure a firewall rule for hello Azure SQL database server tooallow access from your workstation.</span></span> <span data-ttu-id="ce68c-181">如需有關建立 Azure SQL database 和 hello 防火牆設定的指示，請參閱[開始使用 Azure SQL database][sqldatabase-get-started]。</span><span class="sxs-lookup"><span data-stu-id="ce68c-181">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="ce68c-182">根據預設，Azure SQL Database 接受來自 Azure 服務 (例如 Azure HDInsight) 的連線。</span><span class="sxs-lookup"><span data-stu-id="ce68c-182">By default an Azure SQL database allows connections from Azure services, such as Azure HDInsight.</span></span> <span data-ttu-id="ce68c-183">如果防火牆已停用此設定，您需要 tooenable 從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ce68c-183">If this firewall setting is disabled, you need tooenable it from hello Azure portal.</span></span> <span data-ttu-id="ce68c-184">如需關於建立 Azure SQL Database 和設定防火牆規則的指示，請參閱[建立和設定 SQL Database][sqldatabase-create-configue]。</span><span class="sxs-lookup"><span data-stu-id="ce68c-184">For instruction about creating an Azure SQL database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-create-configue].</span></span>
  > 
  > 
* <span data-ttu-id="ce68c-185">**SQL Server**： 如果您的 HDInsight 叢集位於 hello 相同虛擬網路在 Azure 與 SQL Server 中，您可以使用 hello 步驟，此文章 tooimport 和匯出資料 tooa SQL Server 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="ce68c-185">**SQL Server**: If your HDInsight cluster is on hello same virtual network in Azure as SQL Server, you can use hello steps in this article tooimport and export data tooa SQL Server database.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ce68c-186">HDInsight 僅支援以位置為基礎的虛擬網路，目前無法使用以同質群組為基礎的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ce68c-186">HDInsight supports only location-based virtual networks, and it does not currently work with affinity group-based virtual networks.</span></span>
  > 
  > 
  
  * <span data-ttu-id="ce68c-187">toocreate 和設定虛擬網路，請參閱[建立虛擬網路使用 Azure 入口網站 hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="ce68c-187">toocreate and configure a virtual network, see [Create a virtual network using hello Azure portal](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>
    
    * <span data-ttu-id="ce68c-188">當您使用 SQL Server 資料中心中時，您必須設定 hello 與虛擬網路*站對站*或*點對站台*。</span><span class="sxs-lookup"><span data-stu-id="ce68c-188">When you are using SQL Server in your datacenter, you must configure hello virtual network as *site-to-site* or *point-to-site*.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ce68c-189">如**點對站台**虛擬網路時，SQL Server 必須執行 hello VPN 用戶端設定應用程式，可從 hello**儀表板**的 Azure 虛擬網路組態。</span><span class="sxs-lookup"><span data-stu-id="ce68c-189">For **point-to-site** virtual networks, SQL Server must be running hello VPN client configuration application, which is available from hello **Dashboard** of your Azure virtual network configuration.</span></span>
      > 
      > 
    * <span data-ttu-id="ce68c-190">如果 hello 主控 SQL Server 的虛擬機器隸屬的 hello，當您在 Azure 虛擬機器上使用 SQL Server 時，可以使用任何虛擬網路設定與 HDInsight 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ce68c-190">When you are using SQL Server on an Azure virtual machine, any virtual network configuration can be used if hello virtual machine hosting SQL Server is a member of hello same virtual network as HDInsight.</span></span>
  * <span data-ttu-id="ce68c-191">toocreate HDInsight 叢集上虛擬網路，請參閱[建立 Hadoop 叢集使用的自訂選項的 HDInsight 中](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="ce68c-191">toocreate an HDInsight cluster on a virtual network, see [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ce68c-192">SQL Server 也必須允許驗證。</span><span class="sxs-lookup"><span data-stu-id="ce68c-192">SQL Server must also allow authentication.</span></span> <span data-ttu-id="ce68c-193">您必須使用 SQL Server 登入 toocomplete hello 本文章中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ce68c-193">You must use a SQL Server login toocomplete hello steps in this article.</span></span>
    > 
    > 

## <a name="run-sqoop-jobs"></a><span data-ttu-id="ce68c-194">執行 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="ce68c-194">Run Sqoop jobs</span></span>
<span data-ttu-id="ce68c-195">HDInsight 可以使用各種方法執行 Sqoop 工作。</span><span class="sxs-lookup"><span data-stu-id="ce68c-195">HDInsight can run Sqoop jobs by using a variety of methods.</span></span> <span data-ttu-id="ce68c-196">使用下列資料表 toodecide 哪一種方法是最適合您，hello，然後遵循逐步解說中的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="ce68c-196">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="ce68c-197">**使用此方法** </span><span class="sxs-lookup"><span data-stu-id="ce68c-197">**Use this** if you want...</span></span> | <span data-ttu-id="ce68c-198">...一個 **互動式** 殼層</span><span class="sxs-lookup"><span data-stu-id="ce68c-198">...an **interactive** shell</span></span> | <span data-ttu-id="ce68c-199">...**批次** 處理</span><span class="sxs-lookup"><span data-stu-id="ce68c-199">...**batch** processing</span></span> | <span data-ttu-id="ce68c-200">...搭配此 **叢集作業系統**</span><span class="sxs-lookup"><span data-stu-id="ce68c-200">...with this **cluster operating system**</span></span> | <span data-ttu-id="ce68c-201">...從此 **用戶端作業系統**</span><span class="sxs-lookup"><span data-stu-id="ce68c-201">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ce68c-202">SSH</span><span class="sxs-lookup"><span data-stu-id="ce68c-202">SSH</span></span>](hdinsight-use-sqoop-mac-linux.md) |<span data-ttu-id="ce68c-203">✔</span><span class="sxs-lookup"><span data-stu-id="ce68c-203">✔</span></span> |<span data-ttu-id="ce68c-204">✔</span><span class="sxs-lookup"><span data-stu-id="ce68c-204">✔</span></span> |<span data-ttu-id="ce68c-205">Linux</span><span class="sxs-lookup"><span data-stu-id="ce68c-205">Linux</span></span> |<span data-ttu-id="ce68c-206">Linux、Unix、Mac OS X 或 Windows</span><span class="sxs-lookup"><span data-stu-id="ce68c-206">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ce68c-207">.NET SDK for Hadoop</span><span class="sxs-lookup"><span data-stu-id="ce68c-207">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="ce68c-208">✔</span><span class="sxs-lookup"><span data-stu-id="ce68c-208">✔</span></span> |<span data-ttu-id="ce68c-209">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="ce68c-209">Linux or Windows</span></span> |<span data-ttu-id="ce68c-210">Windows (目前)</span><span class="sxs-lookup"><span data-stu-id="ce68c-210">Windows (for now)</span></span> |
| [<span data-ttu-id="ce68c-211">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce68c-211">Azure PowerShell</span></span>](hdinsight-hadoop-use-sqoop-powershell.md) |&nbsp; |<span data-ttu-id="ce68c-212">✔</span><span class="sxs-lookup"><span data-stu-id="ce68c-212">✔</span></span> |<span data-ttu-id="ce68c-213">Linux 或 Windows</span><span class="sxs-lookup"><span data-stu-id="ce68c-213">Linux or Windows</span></span> |<span data-ttu-id="ce68c-214">Windows</span><span class="sxs-lookup"><span data-stu-id="ce68c-214">Windows</span></span> |

## <a name="limitations"></a><span data-ttu-id="ce68c-215">限制</span><span class="sxs-lookup"><span data-stu-id="ce68c-215">Limitations</span></span>
* <span data-ttu-id="ce68c-216">大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。</span><span class="sxs-lookup"><span data-stu-id="ce68c-216">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="ce68c-217">批次處理-與 linux 的 HDInsight，當使用 hello`-batch`參數執行插入時，Sqoop 執行而不是批次處理 hello 插入作業的多個插入。</span><span class="sxs-lookup"><span data-stu-id="ce68c-217">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce68c-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce68c-218">Next steps</span></span>
<span data-ttu-id="ce68c-219">現在您已經學會如何 toouse Sqoop。</span><span class="sxs-lookup"><span data-stu-id="ce68c-219">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="ce68c-220">toolearn 詳細資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ce68c-220">toolearn more, see:</span></span>

* [<span data-ttu-id="ce68c-221">搭配 HDInsight 使用 Hivet</span><span class="sxs-lookup"><span data-stu-id="ce68c-221">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ce68c-222">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="ce68c-222">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* <span data-ttu-id="ce68c-223">[搭配 HDInsight 使用 Oozie][hdinsight-use-oozie]：在 Oozie 工作流程中使用 Sqoop 動作。</span><span class="sxs-lookup"><span data-stu-id="ce68c-223">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="ce68c-224">[飛行延遲使用分析資料 HDInsight][hdinsight-analyze-flight-data]： 使用 Hive tooanalyze 飛行延遲的資料，然後再使用 Sqoop tooexport 資料 tooan Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="ce68c-224">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="ce68c-225">[上傳資料 tooHDInsight][hdinsight-upload-data]： 尋找其他方法上, 傳資料 tooHDInsight/Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ce68c-225">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

## <a name="appendix-a---a-powershell-sample"></a><span data-ttu-id="ce68c-226">附錄 A - PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="ce68c-226">Appendix A - a PowerShell sample</span></span>
<span data-ttu-id="ce68c-227">hello PowerShell 範例會執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ce68c-227">hello PowerShell sample performs hello following steps:</span></span>

1. <span data-ttu-id="ce68c-228">連接 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ce68c-228">Connect tooAzure.</span></span>
2. <span data-ttu-id="ce68c-229">建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="ce68c-229">Create an Azure resource group.</span></span> <span data-ttu-id="ce68c-230">如需詳細資訊，請參閱 [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="ce68c-230">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)</span></span>
3. <span data-ttu-id="ce68c-231">建立 Azure SQL Database 伺服器、Azure SQL Database 和兩個資料表。</span><span class="sxs-lookup"><span data-stu-id="ce68c-231">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> 
   
    <span data-ttu-id="ce68c-232">如果您改為使用 SQL Server，請使用下列陳述式 toocreate hello 資料表 hello:</span><span class="sxs-lookup"><span data-stu-id="ce68c-232">If you use SQL Server instead, use hello following statements toocreate hello tables:</span></span>
   
        CREATE TABLE [dbo].[log4jlogs](
         [t1] [nvarchar](50),
         [t2] [nvarchar](50),
         [t3] [nvarchar](50),
         [t4] [nvarchar](50),
         [t5] [nvarchar](50),
         [t6] [nvarchar](50),
         [t7] [nvarchar](50))
   
        CREATE TABLE [dbo].[mobiledata](
         [clientid] [nvarchar](50),
         [querytime] [nvarchar](50),
         [market] [nvarchar](50),
         [deviceplatform] [nvarchar](50),
         [devicemake] [nvarchar](50),
         [devicemodel] [nvarchar](50),
         [state] [nvarchar](50),
         [country] [nvarchar](50),
         [querydwelltime] [float],
         [sessionid] [bigint],
         [sessionpagevieworder][bigint])
   
    <span data-ttu-id="ce68c-233">hello 最簡單方式 tooexamine hello 資料庫和資料表是 toouse Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ce68c-233">hello easiest way tooexamine hello database and tables is toouse Visual Studio.</span></span> <span data-ttu-id="ce68c-234">檢查 hello 資料庫伺服器和 hello 資料庫，可以使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ce68c-234">hello database server and hello database can be examined using hello Azure portal.</span></span>
4. <span data-ttu-id="ce68c-235">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce68c-235">Create an HDInsight cluster.</span></span>
   
    <span data-ttu-id="ce68c-236">tooexamine hello 叢集中，您可以使用 hello Azure 入口網站或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ce68c-236">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="ce68c-237">前置處理 hello 來源資料檔。</span><span class="sxs-lookup"><span data-stu-id="ce68c-237">Pre-process hello source data file.</span></span>
   
    <span data-ttu-id="ce68c-238">在本教學課程中，您可以匯出 log4j 記錄檔 （分隔檔） 和 Hive 資料表 tooan Azure SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ce68c-238">In this tutorial, you export a log4j log file (a delimited file) and a Hive table tooan Azure SQL database.</span></span> <span data-ttu-id="ce68c-239">hello 分隔的檔案稱為*/example/data/sample.log*。</span><span class="sxs-lookup"><span data-stu-id="ce68c-239">hello delimited file is called */example/data/sample.log*.</span></span> <span data-ttu-id="ce68c-240">稍早在 hello 教學課程中，您會看到 log4j 記錄檔的一些範例。</span><span class="sxs-lookup"><span data-stu-id="ce68c-240">Earlier in hello tutorial, you saw a few samples of log4j logs.</span></span> <span data-ttu-id="ce68c-241">在 hello 記錄檔中，有一些空白行及某些線條類似 toothese:</span><span class="sxs-lookup"><span data-stu-id="ce68c-241">In hello log file, there are some empty lines and some lines similar toothese:</span></span>
   
        java.lang.Exception: 2012-02-03 20:11:35 SampleClass2 [FATAL] unrecoverable system problem at id 609774657
            at com.osa.mocklogger.MockLogger$2.run(MockLogger.java:83)
   
    <span data-ttu-id="ce68c-242">這是正常的其他範例，使用此資料，但我們可以匯入 hello Azure SQL database 或 SQL Server 之前，我們必須移除這些例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ce68c-242">This is fine for other examples that use this data, but we must remove these exceptions before we can import into hello Azure SQL database or SQL Server.</span></span> <span data-ttu-id="ce68c-243">Sqoop 匯出失敗，則為空字串或較少的線條比 hello hello Azure SQL 資料庫資料表中定義的欄位數目的項目。</span><span class="sxs-lookup"><span data-stu-id="ce68c-243">Sqoop export  fails if there is an empty string or a line with a fewer elements than hello number of fields defined in hello Azure SQL database table.</span></span> <span data-ttu-id="ce68c-244">hello log4jlogs 資料表有 7 的字串類型欄位。</span><span class="sxs-lookup"><span data-stu-id="ce68c-244">hello log4jlogs table has 7 string-type fields.</span></span>
   
    <span data-ttu-id="ce68c-245">此程序會建立新 hello 叢集上的檔案： tutorials/usesqoop/data/sample.log。</span><span class="sxs-lookup"><span data-stu-id="ce68c-245">This procedure creates a new file on hello cluster: tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ce68c-246">tooexamine hello 已修改的資料檔案，您可以使用 hello Azure 入口網站、 Azure 儲存體總管工具或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ce68c-246">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span> <span data-ttu-id="ce68c-247">[開始使用 HDInsight] [ hdinsight-get-started]有程式碼範例使用 Azure PowerShell toodownload 檔案，並顯示 hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="ce68c-247">[Get started with HDInsight][hdinsight-get-started] has a code sample for using Azure PowerShell toodownload a file and display hello file content.</span></span>
6. <span data-ttu-id="ce68c-248">匯出資料檔案 toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="ce68c-248">Export a data file toohello Azure SQL database.</span></span>
   
    <span data-ttu-id="ce68c-249">tutorials/usesqoop/data/sample.log hello 來源檔案。</span><span class="sxs-lookup"><span data-stu-id="ce68c-249">hello source file is tutorials/usesqoop/data/sample.log.</span></span> <span data-ttu-id="ce68c-250">hello 資料表 hello 資料匯出的 toois 呼叫 log4jlogs。</span><span class="sxs-lookup"><span data-stu-id="ce68c-250">hello table where hello data is exported toois called log4jlogs.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ce68c-251">以外的連接字串資訊，本節中的 hello 步驟應該適用 Azure SQL database 或 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ce68c-251">Other than connection string information, hello steps in this section should work for an Azure SQL database or for SQL Server.</span></span> <span data-ttu-id="ce68c-252">使用下列組態的 hello 測試步驟執行：</span><span class="sxs-lookup"><span data-stu-id="ce68c-252">These steps were tested by using hello following configuration:</span></span>
   > 
   > * <span data-ttu-id="ce68c-253">**Azure 虛擬網路的點對站組態**： 連接 hello HDInsight 叢集 tooa 私人資料中心中的 SQL Server 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ce68c-253">**Azure virtual network point-to-site configuration**: A virtual network connected hello HDInsight cluster tooa SQL Server in a private datacenter.</span></span> <span data-ttu-id="ce68c-254">請參閱[hello 管理入口網站中設定點對站 VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="ce68c-254">See [Configure a Point-to-Site VPN in hello Management Portal](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>
   > * <span data-ttu-id="ce68c-255">**Azure HDInsight 3.1**：如需有關在虛擬網路上建立叢集的資訊，請參閱 [使用自訂選項在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md) 。</span><span class="sxs-lookup"><span data-stu-id="ce68c-255">**Azure HDInsight 3.1**: See [Create Hadoop clusters in HDInsight using custom options](hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster on a virtual network.</span></span>
   > * <span data-ttu-id="ce68c-256">**SQL Server 2014**： 安全地設定 tooallow 驗證和執行 hello VPN 用戶端組態封裝 tooconnect toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ce68c-256">**SQL Server 2014**: Configured tooallow authentication and running hello VPN client configuration package tooconnect securely toohello virtual network.</span></span>
   > 
   > 
7. <span data-ttu-id="ce68c-257">匯出 Hive 資料表 toohello Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="ce68c-257">Export a Hive table toohello Azure SQL database.</span></span>
8. <span data-ttu-id="ce68c-258">匯入 hello mobiledata 資料表 toohello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="ce68c-258">Import hello mobiledata table toohello HDInsight cluster.</span></span>
   
    <span data-ttu-id="ce68c-259">tooexamine hello 已修改的資料檔案，您可以使用 hello Azure 入口網站、 Azure 儲存體總管工具或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ce68c-259">tooexamine hello modified data file, you can use hello Azure portal, an Azure Storage explorer tool, or Azure PowerShell.</span></span>  <span data-ttu-id="ce68c-260">[開始使用 HDInsight] [ hdinsight-get-started]具有使用 Azure PowerShell toodownload 檔案的相關範例，並顯示 hello 檔案內容的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ce68c-260">[Get started with HDInsight][hdinsight-get-started] has a code sample about using Azure PowerShell toodownload a file and display hello file content.</span></span>

### <a name="hello-powershell-sample"></a><span data-ttu-id="ce68c-261">hello PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="ce68c-261">hello PowerShell sample</span></span>
    # Prepare an Azure SQL database toobe used by hello Sqoop tutorial

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure Subscription ID>"

    $sqlDatabaseLogin = "<Enter a SQL Database Login name>" #SQL Database server login
    $sqlDatabasePassword = "<Enter a Password>"

    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<Enter a Password>"

    # used for creating Azure service names
    $nameToken = "<Enter an alias>" 
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # Used for creating tables and clustered indexes
    $cmdCreateLog4jTable = "CREATE TABLE [dbo].[log4jlogs](
        [t1] [nvarchar](50),
        [t2] [nvarchar](50),
        [t3] [nvarchar](50),
        [t4] [nvarchar](50),
        [t5] [nvarchar](50),
        [t6] [nvarchar](50),
        [t7] [nvarchar](50))"

    $cmdCreateLog4jClusteredIndex = "CREATE CLUSTERED INDEX log4jlogs_clustered_index on log4jlogs(t1)"

    $cmdCreateMobileTable = " CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder][bigint])"

    $cmdCreateMobileDataClusteredIndex = "CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $credential `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating an Azure SQL database ..." -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region - Create tables
    Write-Host "Creating hello log4jlogs table and hello mobiledata table ..." -ForegroundColor Green

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jTable
    $ret = $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateLog4jClusteredIndex
    $cmd.ExecuteNonQuery()

    # Create hello mobiledata table and index
    $cmd.CommandText = $cmdCreateMobileTable
    $cmd.ExecuteNonQuery()
    $cmd.CommandText = $cmdCreateMobileDataClusteredIndex
    $cmd.ExecuteNonQuery()

    $conn.close()

    #endregion


    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - pre-process hello source file

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    # This procedure creates a new file with $destBlobName
    $sourceBlobName = "example/data/sample.log"
    $destBlobName = "tutorials/usesqoop/data/sample.log"

    # Define hello connection string
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    # Create block blob objects referencing hello source and destination blob.
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $sourceBlob = $storageContainer.GetBlockBlobReference($sourceBlobName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)

    # Define a MemoryStream and a StreamReader for reading from hello source file
    $stream = New-Object System.IO.MemoryStream
    $stream = $sourceBlob.OpenRead()
    $sReader = New-Object System.IO.StreamReader($stream)

    # Define a MemoryStream and a StreamWriter for writing into hello destination file
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    # Pre-process hello source blob
    $exString = "java.lang.Exception:"
    while(-Not $sReader.EndOfStream){
        $line = $sReader.ReadLine()
        $split = $line.Split(" ")

        # remove hello "java.lang.Exception" from hello first element of hello array
        # for example: java.lang.Exception: 2012-02-03 19:11:02 SampleClass8 [WARN] problem finding id 153454612
        if ($split[0] -eq $exString){
            #create a new ArrayList tooremove $split[0]
            $newArray = [System.Collections.ArrayList] $split
            $newArray.Remove($exString)

            # update $split and $line
            $split = $newArray
            $line = $newArray -join(" ")
        }

        # remove hello lines that has less than 7 elements
        if ($split.count -ge 7){
            write-host $line
            $writeStream.WriteLine($line)
        }
    }

    # Write toohello destination blob
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    #endregion

    #region - export a log file from hello cluster toohello SQL database

    Write-Host "Preprocessing hello source file ..." -ForegroundColor Green

    $tableName_log4j = "log4jlogs"

    # Connection string for Azure SQL Database.
    # Comment if using SQL Server
    $connectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"
    # Connection string for SQL Server.
    # Uncomment if using SQL Server.
    #$connectionString = "jdbc:sqlserver://$sqlDatabaseServerName;user=$sqlDatabaseLogin;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $exportDir_log4j = "/tutorials/usesqoop/data"

    # Submit a Sqoop job
    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_log4j --export-dir $exportDir_log4j --input-fields-terminated-by \0x20 -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose
    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardError
    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -HttpCredential $httpCredential -JobId $sqoopJob.JobId -DisplayOutputType StandardOutput

    #endregion

    #region - export a Hive table

    $tableName_mobile = "mobiledata"
    $exportDir_mobile = "/hive/warehouse/hivesampletable"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "export --connect $connectionString --table $tableName_mobile --export-dir $exportDir_mobile --fields-terminated-by \t -m 1"
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion

    #region - import a database

    $targetDir_mobile = "/tutorials/usesqoop/importeddata/"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
        -Command "import --connect $connectionString --table $tableName_mobile --target-dir $targetDir_mobile --fields-terminated-by \t --lines-terminated-by \n -m 1"

    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId

    Write-Host "Standard Error" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    Write-Host "Standard Output" -BackgroundColor Green
    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultBlobContainerName `
        -HttpCredential $httpCredential `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardOutput

    #endregion



[azure-management-portal]: https://portal.azure.com/

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database/sql-database-get-started.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
