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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>使用 .NET SDK 管理 HDInsight 中的 Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

了解如何 toomanage HDInsight 叢集使用[HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)。

**必要條件**

在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

## <a name="connect-tooazure-hdinsight"></a>連接 tooAzure HDInsight

您需要下列 Nuget 套件 hello:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

hello 下列程式碼範例會示範如何 tooconnect tooAzure 之前您可以管理 HDInsight 叢集在您的 Azure 訂用帳戶。

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

當您執行此程式時，應該會看到提示。  如果您不想 toosee hello 提示字元，請參閱[建立.NET HDInsight 應用程式的非互動式驗證](hdinsight-create-non-interactive-authentication-dotnet-applications.md)。

## <a name="create-clusters"></a>建立叢集
請參閱[建立 linux 叢集使用 HDInsight 中的 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>列出叢集
hello 下列程式碼片段會列出叢集，某些屬性：

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>刪除叢集
使用下列程式碼片段 toodelete 叢集，以同步或非同步的 hello: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>調整叢集
hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。

> [!NOTE]
> 只支援使用 HDInsight 3.1.3 版或更高版本的叢集。 如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。  請參閱[列出和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)。
> 
> 

hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：

* Hadoop
  
    您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。 Hello 作業正在進行時，也可以提交新的作業。 使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。
  
    當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。 這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。 您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。
* HBase
  
    順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。 完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。 不過，您就可以手動平衡 hello 地區的伺服器登入 hello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。 但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。
  
    您可以使用兩種方式來完成重新平衡作業：
  
  * Storm Web UI
  * 命令列介面 (CLI) 工具
    
    請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。
    
    hello Storm web UI 是在 hello HDInsight 叢集上使用：
    
    ![HDInsight Storm 調整重新平衡](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

hello 下列程式碼片段會示範如何 tooresize 叢集中同步或非同步方式：

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>授與/撤銷存取權
HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

預設會授與這些服務的存取權。 您可以撤銷/授與 hello 存取。 toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> 授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。
> 
> 

這也可以透過 hello 入口網站來完成。 請參閱[管理 HDInsight 使用 hello Azure 入口網站][hdinsight-admin-portal]。

## <a name="update-http-user-credentials"></a>更新 HTTP 使用者認證
它是相同的 hello 與程序[Grant/revoke HTTP 存取](#grant/revoke-access)。如果已授與 hello 叢集 hello HTTP 存取，您必須先撤銷。  然後授與 hello 存取以新的 HTTP 使用者認證。

## <a name="find-hello-default-storage-account"></a>找不到 hello 預設儲存體帳戶
hello，下列程式碼片段示範如何 tooget hello 預設儲存體帳戶名稱和 hello 叢集的預設儲存體帳戶金鑰。

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>提交工作
**toosubmit MapReduce 工作**

請參閱 [在 HDInsight 中執行 Hadoop MapReduce 範例](hdinsight-hadoop-run-samples-linux.md)。

**toosubmit Hive 工作** 

請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。

**toosubmit Pig 工作**

請參閱 [使用 .NET SDK 執行 Pig 作業](hdinsight-hadoop-use-pig-dotnet-sdk.md)。

**toosubmit Sqoop 作業**

請參閱 [在 HDInsight 上使用 Sqoop](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)。

**toosubmit Oozie 工作**

請參閱[Hadoop toodefine 與執行 HDInsight 中的工作流程使用 Oozie](hdinsight-use-oozie-linux-mac.md)。

## <a name="upload-data-tooazure-blob-storage"></a>上傳資料 tooAzure Blob 儲存體
請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。

## <a name="see-also"></a>另請參閱
* [HDInsight .NET SDK 參考文件](https://msdn.microsoft.com/library/mt271028.aspx)
* [使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]
* [使用命令列介面管理 HDInsight][hdinsight-admin-cli]
* [建立 HDInsight 叢集][hdinsight-provision]
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [開始使用 Azure HDInsight][hdinsight-get-started]

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


