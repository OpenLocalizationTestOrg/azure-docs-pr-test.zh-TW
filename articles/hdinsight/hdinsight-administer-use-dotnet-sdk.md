---
title: "在使用.NET SDK-Azure HDInsight 中的 aaaManage Hadoop 叢集 |Microsoft 文件"
description: "了解如何 tooperform 系統管理工作 hello HDInsight 使用 HDInsight.NET SDK 中的 Hadoop 叢集。"
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="00baf-103">使用 .NET SDK 管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="00baf-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="00baf-104">了解如何 toomanage HDInsight 叢集使用[HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="00baf-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="00baf-105">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="00baf-105">**Prerequisites**</span></span>

<span data-ttu-id="00baf-106">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="00baf-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="00baf-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="00baf-107">**An Azure subscription**.</span></span> <span data-ttu-id="00baf-108">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="00baf-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="00baf-109">連接 tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="00baf-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="00baf-110">您需要下列 Nuget 套件 hello:</span><span class="sxs-lookup"><span data-stu-id="00baf-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="00baf-111">hello 下列程式碼範例會示範如何 tooconnect tooAzure 之前您可以管理 HDInsight 叢集在您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="00baf-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
            {
                var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
                var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                    ClientId, 
                    new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                    PromptBehavior.Always, 
                    UserIdentifier.AnyUser);
                return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
            }
            /// <summary>
            /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
            /// </summary>
            /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
            /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
            /// <param name="authToken">An authentication token for your Azure subscription</param>
            static void EnableHDInsight(TokenCloudCredentials authToken)
            {
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="00baf-112">當您執行此程式時，應該會看到提示。</span><span class="sxs-lookup"><span data-stu-id="00baf-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="00baf-113">如果您不想 toosee hello 提示字元，請參閱[建立.NET HDInsight 應用程式的非互動式驗證](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="00baf-114">建立叢集</span><span class="sxs-lookup"><span data-stu-id="00baf-114">Create clusters</span></span>
<span data-ttu-id="00baf-115">請參閱[建立 linux 叢集使用 HDInsight 中的 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="00baf-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="00baf-116">列出叢集</span><span class="sxs-lookup"><span data-stu-id="00baf-116">List clusters</span></span>
<span data-ttu-id="00baf-117">hello 下列程式碼片段會列出叢集，某些屬性：</span><span class="sxs-lookup"><span data-stu-id="00baf-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="00baf-118">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="00baf-118">Delete clusters</span></span>
<span data-ttu-id="00baf-119">使用下列程式碼片段 toodelete 叢集，以同步或非同步的 hello:</span><span class="sxs-lookup"><span data-stu-id="00baf-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="00baf-120">調整叢集</span><span class="sxs-lookup"><span data-stu-id="00baf-120">Scale clusters</span></span>
<span data-ttu-id="00baf-121">hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="00baf-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="00baf-122">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="00baf-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="00baf-123">如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="00baf-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="00baf-124">請參閱[列出和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="00baf-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="00baf-125">hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：</span><span class="sxs-lookup"><span data-stu-id="00baf-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="00baf-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="00baf-126">Hadoop</span></span>
  
    <span data-ttu-id="00baf-127">您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="00baf-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="00baf-128">Hello 作業正在進行時，也可以提交新的作業。</span><span class="sxs-lookup"><span data-stu-id="00baf-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="00baf-129">使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。</span><span class="sxs-lookup"><span data-stu-id="00baf-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="00baf-130">當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="00baf-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="00baf-131">這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。</span><span class="sxs-lookup"><span data-stu-id="00baf-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="00baf-132">您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="00baf-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="00baf-133">HBase</span><span class="sxs-lookup"><span data-stu-id="00baf-133">HBase</span></span>
  
    <span data-ttu-id="00baf-134">順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。</span><span class="sxs-lookup"><span data-stu-id="00baf-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="00baf-135">完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="00baf-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="00baf-136">不過，您就可以手動平衡 hello 地區的伺服器登入 hello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="00baf-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="00baf-137">Storm</span><span class="sxs-lookup"><span data-stu-id="00baf-137">Storm</span></span>
  
    <span data-ttu-id="00baf-138">順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="00baf-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="00baf-139">但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="00baf-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="00baf-140">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="00baf-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="00baf-141">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="00baf-141">Storm web UI</span></span>
  * <span data-ttu-id="00baf-142">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="00baf-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="00baf-143">請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="00baf-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="00baf-144">hello Storm web UI 是在 hello HDInsight 叢集上使用：</span><span class="sxs-lookup"><span data-stu-id="00baf-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="00baf-146">以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：</span><span class="sxs-lookup"><span data-stu-id="00baf-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="00baf-147">hello 下列程式碼片段會示範如何 tooresize 叢集中同步或非同步方式：</span><span class="sxs-lookup"><span data-stu-id="00baf-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="00baf-148">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="00baf-148">Grant/revoke access</span></span>
<span data-ttu-id="00baf-149">HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="00baf-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="00baf-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="00baf-150">ODBC</span></span>
* <span data-ttu-id="00baf-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="00baf-151">JDBC</span></span>
* <span data-ttu-id="00baf-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="00baf-152">Ambari</span></span>
* <span data-ttu-id="00baf-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="00baf-153">Oozie</span></span>
* <span data-ttu-id="00baf-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="00baf-154">Templeton</span></span>

<span data-ttu-id="00baf-155">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="00baf-155">By default, these services are granted for access.</span></span> <span data-ttu-id="00baf-156">您可以撤銷/授與 hello 存取。</span><span class="sxs-lookup"><span data-stu-id="00baf-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="00baf-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="00baf-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="00baf-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="00baf-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="00baf-159">授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="00baf-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="00baf-160">這也可以透過 hello 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="00baf-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="00baf-161">請參閱[管理 HDInsight 使用 hello Azure 入口網站][hdinsight-admin-portal]。</span><span class="sxs-lookup"><span data-stu-id="00baf-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="00baf-162">更新 HTTP 使用者認證</span><span class="sxs-lookup"><span data-stu-id="00baf-162">Update HTTP user credentials</span></span>
<span data-ttu-id="00baf-163">它是相同的 hello 與程序[Grant/revoke HTTP 存取](#grant/revoke-access)。如果已授與 hello 叢集 hello HTTP 存取，您必須先撤銷。</span><span class="sxs-lookup"><span data-stu-id="00baf-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="00baf-164">然後授與 hello 存取以新的 HTTP 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="00baf-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="00baf-165">找不到 hello 預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="00baf-165">Find hello default storage account</span></span>
<span data-ttu-id="00baf-166">hello，下列程式碼片段示範如何 tooget hello 預設儲存體帳戶名稱和 hello 叢集的預設儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="00baf-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="00baf-167">提交工作</span><span class="sxs-lookup"><span data-stu-id="00baf-167">Submit jobs</span></span>
<span data-ttu-id="00baf-168">**toosubmit MapReduce 工作**</span><span class="sxs-lookup"><span data-stu-id="00baf-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="00baf-169">請參閱 [在 HDInsight 中執行 Hadoop MapReduce 範例](hdinsight-hadoop-run-samples-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="00baf-170">**toosubmit Hive 工作**</span><span class="sxs-lookup"><span data-stu-id="00baf-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="00baf-171">請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="00baf-172">**toosubmit Pig 工作**</span><span class="sxs-lookup"><span data-stu-id="00baf-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="00baf-173">請參閱 [使用 .NET SDK 執行 Pig 作業](hdinsight-hadoop-use-pig-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="00baf-174">**toosubmit Sqoop 作業**</span><span class="sxs-lookup"><span data-stu-id="00baf-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="00baf-175">請參閱 [在 HDInsight 上使用 Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="00baf-176">**toosubmit Oozie 工作**</span><span class="sxs-lookup"><span data-stu-id="00baf-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="00baf-177">請參閱[Hadoop toodefine 與執行 HDInsight 中的工作流程使用 Oozie](hdinsight-use-oozie-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="00baf-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="00baf-178">上傳資料 tooAzure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="00baf-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="00baf-179">請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="00baf-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="00baf-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="00baf-180">See Also</span></span>
* [<span data-ttu-id="00baf-181">HDInsight .NET SDK 參考文件</span><span class="sxs-lookup"><span data-stu-id="00baf-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="00baf-182">[使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="00baf-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="00baf-183">[使用命令列介面管理 HDInsight][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="00baf-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="00baf-184">[建立 HDInsight 叢集][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="00baf-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="00baf-185">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="00baf-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="00baf-186">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="00baf-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


