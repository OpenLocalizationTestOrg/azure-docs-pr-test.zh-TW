---
title: "使用 .NET SDK 管理 HDInsight 中的 Hadoop 叢集 - Azure | Microsoft Docs"
description: "了解如何使用 HDInsight .NET SDK 對 HDInsight 中的 Hadoop 叢集執行管理工作。"
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
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="cc508-103">使用 .NET SDK 管理 HDInsight 中的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="cc508-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="cc508-104">了解如何使用 [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)管理 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cc508-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="cc508-105">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="cc508-105">**Prerequisites**</span></span>

<span data-ttu-id="cc508-106">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="cc508-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="cc508-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cc508-107">**An Azure subscription**.</span></span> <span data-ttu-id="cc508-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="cc508-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="cc508-109">連接至 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc508-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="cc508-110">您需要下列 Nuget 套件：</span><span class="sxs-lookup"><span data-stu-id="cc508-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="cc508-111">下列程式碼範例示範如何先連接至 Azure，然後才透過 Azure 訂用帳戶管理 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="cc508-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
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
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="cc508-112">當您執行此程式時，應該會看到提示。</span><span class="sxs-lookup"><span data-stu-id="cc508-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="cc508-113">如果您不想要看到提示，請參閱 [建立非互動式驗證 .NET HDInsight 應用程式](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="cc508-114">建立叢集</span><span class="sxs-lookup"><span data-stu-id="cc508-114">Create clusters</span></span>
<span data-ttu-id="cc508-115">請參閱 [使用 .NET SDK 在 HDInsight 中建立 Linux 型叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="cc508-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="cc508-116">列出叢集</span><span class="sxs-lookup"><span data-stu-id="cc508-116">List clusters</span></span>
<span data-ttu-id="cc508-117">下列程式碼片段列出叢集和一些屬性︰</span><span class="sxs-lookup"><span data-stu-id="cc508-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="cc508-118">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="cc508-118">Delete clusters</span></span>
<span data-ttu-id="cc508-119">使用下列程式碼片段，同步或非同步地刪除叢集︰</span><span class="sxs-lookup"><span data-stu-id="cc508-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="cc508-120">調整叢集</span><span class="sxs-lookup"><span data-stu-id="cc508-120">Scale clusters</span></span>
<span data-ttu-id="cc508-121">叢集調整功能可讓您變更在 Azure HDInsight 中執行的叢集所用的背景工作節點數目，而不需要重新建立叢集。</span><span class="sxs-lookup"><span data-stu-id="cc508-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cc508-122">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="cc508-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="cc508-123">如果不確定您的叢集版本，您可以檢查 [屬性] 頁面。</span><span class="sxs-lookup"><span data-stu-id="cc508-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="cc508-124">請參閱[列出和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="cc508-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="cc508-125">變更 HDInsight 支援的每一種叢集所用的資料節點數目會有何影響：</span><span class="sxs-lookup"><span data-stu-id="cc508-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="cc508-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="cc508-126">Hadoop</span></span>
  
    <span data-ttu-id="cc508-127">您可以順暢地增加正在執行的 Hadoop 叢集中背景工作節點數目，而不會影響任何擱置或執行中的工作。</span><span class="sxs-lookup"><span data-stu-id="cc508-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="cc508-128">您也可以在作業進行當中提交新工作。</span><span class="sxs-lookup"><span data-stu-id="cc508-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="cc508-129">系統會順暢處理失敗的調整作業，讓叢集永保正常運作狀態。</span><span class="sxs-lookup"><span data-stu-id="cc508-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="cc508-130">減少資料節點數目以縮減 Hadoop 叢集時，系統會重新啟動叢集中的部分服務。</span><span class="sxs-lookup"><span data-stu-id="cc508-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="cc508-131">這會導致所有執行中和擱置的工作在調整作業完成時失敗。</span><span class="sxs-lookup"><span data-stu-id="cc508-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="cc508-132">但您可以在作業完成後重新提交這些工作。</span><span class="sxs-lookup"><span data-stu-id="cc508-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="cc508-133">HBase</span><span class="sxs-lookup"><span data-stu-id="cc508-133">HBase</span></span>
  
    <span data-ttu-id="cc508-134">您可以順暢地在 HBase 叢集運作時對其新增或移除資料節點。</span><span class="sxs-lookup"><span data-stu-id="cc508-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="cc508-135">區域伺服器會在完成調整作業的數分鐘之內自動取得平衡。</span><span class="sxs-lookup"><span data-stu-id="cc508-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="cc508-136">但是，您也可以手動平衡區域伺服器，方法是登入叢集的前端節點，然後從命令提示字元視窗執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cc508-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="cc508-137">Storm</span><span class="sxs-lookup"><span data-stu-id="cc508-137">Storm</span></span>
  
    <span data-ttu-id="cc508-138">您可以順暢地在 Storm 叢集運作時對其新增或移除資料節點。</span><span class="sxs-lookup"><span data-stu-id="cc508-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="cc508-139">但在調整作業順利完成後，您需要重新平衡拓撲。</span><span class="sxs-lookup"><span data-stu-id="cc508-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="cc508-140">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="cc508-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="cc508-141">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="cc508-141">Storm web UI</span></span>
  * <span data-ttu-id="cc508-142">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="cc508-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="cc508-143">如需詳細資訊，請參閱 [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 。</span><span class="sxs-lookup"><span data-stu-id="cc508-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="cc508-144">HDInsight 叢集上有提供 Storm Web UI：</span><span class="sxs-lookup"><span data-stu-id="cc508-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="cc508-146">以下是如何使用 CLI 命令重新平衡 Storm 拓撲的範例：</span><span class="sxs-lookup"><span data-stu-id="cc508-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="cc508-147">下列程式碼片段示範如何同步或非同步地調整叢集大小︰</span><span class="sxs-lookup"><span data-stu-id="cc508-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="cc508-148">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="cc508-148">Grant/revoke access</span></span>
<span data-ttu-id="cc508-149">HDInsight 叢集具有下列 HTTP Web 服務 (所有這些服務都有 RESTful 端點)：</span><span class="sxs-lookup"><span data-stu-id="cc508-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="cc508-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="cc508-150">ODBC</span></span>
* <span data-ttu-id="cc508-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="cc508-151">JDBC</span></span>
* <span data-ttu-id="cc508-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="cc508-152">Ambari</span></span>
* <span data-ttu-id="cc508-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="cc508-153">Oozie</span></span>
* <span data-ttu-id="cc508-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="cc508-154">Templeton</span></span>

<span data-ttu-id="cc508-155">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="cc508-155">By default, these services are granted for access.</span></span> <span data-ttu-id="cc508-156">您可以撤銷/授與存取權。</span><span class="sxs-lookup"><span data-stu-id="cc508-156">You can revoke/grant the access.</span></span> <span data-ttu-id="cc508-157">撤銷：</span><span class="sxs-lookup"><span data-stu-id="cc508-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="cc508-158">授與：</span><span class="sxs-lookup"><span data-stu-id="cc508-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="cc508-159">透過授與/撤銷存取權，您將重設叢的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="cc508-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="cc508-160">這也可以透過入口網站完成。</span><span class="sxs-lookup"><span data-stu-id="cc508-160">This can also be done via the Portal.</span></span> <span data-ttu-id="cc508-161">請參閱[使用 Azure 入口網站管理 HDInsight][hdinsight-admin-portal]。</span><span class="sxs-lookup"><span data-stu-id="cc508-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="cc508-162">更新 HTTP 使用者認證</span><span class="sxs-lookup"><span data-stu-id="cc508-162">Update HTTP user credentials</span></span>
<span data-ttu-id="cc508-163">與[授與/撤銷 HTTP 存取權](#grant/revoke-access)程序一樣。若已授與叢集 HTTP 存取權，則必須先將其撤銷。</span><span class="sxs-lookup"><span data-stu-id="cc508-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="cc508-164">然後再使用新的 HTTP 使用者認證授與存取權。</span><span class="sxs-lookup"><span data-stu-id="cc508-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="cc508-165">尋找預設的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="cc508-165">Find the default storage account</span></span>
<span data-ttu-id="cc508-166">下列程式碼片段示範如何取得叢集的預設儲存體帳戶名稱和預設儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="cc508-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="cc508-167">提交工作</span><span class="sxs-lookup"><span data-stu-id="cc508-167">Submit jobs</span></span>
<span data-ttu-id="cc508-168">**提交 MapReduce 作業**</span><span class="sxs-lookup"><span data-stu-id="cc508-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="cc508-169">請參閱 [在 HDInsight 中執行 Hadoop MapReduce 範例](hdinsight-hadoop-run-samples-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="cc508-170">**提交 Hive 作業**</span><span class="sxs-lookup"><span data-stu-id="cc508-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="cc508-171">請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="cc508-172">**提交 Pig 作業**</span><span class="sxs-lookup"><span data-stu-id="cc508-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="cc508-173">請參閱 [使用 .NET SDK 執行 Pig 作業](hdinsight-hadoop-use-pig-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="cc508-174">**提交 Sqoop 作業**</span><span class="sxs-lookup"><span data-stu-id="cc508-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="cc508-175">請參閱 [在 HDInsight 上使用 Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="cc508-176">**提交 Oozie 作業**</span><span class="sxs-lookup"><span data-stu-id="cc508-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="cc508-177">請參閱 [在 HDInsight 上搭配 Hadoop 使用 Oozie 來定義並執行工作流程](hdinsight-use-oozie-linux-mac.md)。</span><span class="sxs-lookup"><span data-stu-id="cc508-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="cc508-178">將資料上傳至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="cc508-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="cc508-179">請參閱[將資料上傳至 HDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="cc508-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="cc508-180">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cc508-180">See Also</span></span>
* [<span data-ttu-id="cc508-181">HDInsight .NET SDK 參考文件</span><span class="sxs-lookup"><span data-stu-id="cc508-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="cc508-182">[使用 Azure 入口網站管理 HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="cc508-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="cc508-183">[使用命令列介面管理 HDInsight][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="cc508-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="cc508-184">[建立 HDInsight 叢集][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="cc508-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="cc508-185">[將資料上傳至 HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="cc508-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="cc508-186">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="cc508-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


